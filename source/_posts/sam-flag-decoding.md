---
title: SAM FLAG 解析
date: 2020-02-11 10:32:43
tags:
- flag
categories:
- BI
comments:
---

## 简介
FLAG记录了许多有关reads比对情况的信息（共含12项内容）。
* 这条read是read1 (forward-read) 还是read2 (reverse-read)？
* 这条read比对上了吗？与它对应的另一头read比对上了吗？
* ……

而每一项又只有两种情况，是或否，那么我们可以用一个12位的二进制数来记录所有的信息（一般会用16位的整数代表），每一位表示某一项的情况，这就是原始FLAG信息的由来，但是二进制数适合给计算机看，不适合人看，需要转换成对应的十进制数，也就有了我们在SAM文件中看到的FLAG值。

|二进制|十六进制|十进制|英文描述|中文描述|
|---|---|---|---|---|
|000000000001|0X1|1|read paired|1代表PE，0代表SE|
|000000000010|0X2|2|read mapped in proper pair|正常比对，如果是PE测序，还代表两条reads之间的比对距离没有明显偏离插入片段长度|
|000000000100|0X4|4|read unmapped|该read没有比对上参考序列|
|000000001000|0X8|8|mate unmapped|PE测序中的另一条read没有比对上参考序列|
|000000010000|0X10|16|read reverse strand|反向互补后比对上参考序列，意即比对上负链|
|000000100000|0X20|32|mate reverse strand|PE测序中的另一条read反向互补后比对上参考序列|
|000001000000|0X40|64|first in pair|PE测序中read1|
|000010000000|0X80|128|second in pair|PE测序中read2|
|000100000000|0X100|256|not primary alignment|非初级比对，意即该read在基因组上比对了多个位置，当前的比对位置是次佳比对位置，通常需要过滤掉，但在有些分析场景中是很有用的信息|
|001000000000|0X200|512|read fails platform/vendor quality checks|低于（测序平台等）过滤阈值|
|010000000000|0X400|1024|read is PCR or optical duplicate|PCR重复（来自测序文库构建过程）或者光学重复（来自测序过程），这些都可以通过picard标记或过滤，对于光学重复不需要比对也能发现|
|100000000000|0X800|2048|supplementary alignment|意即这条read可能存在嵌合，这个比对部分只是来自其中的一部分序列|

通过上表信息，我们就可以清楚地知道每一个FLAG中都包含了什么内容。比如看到FLAG = 77时，我们第一步要做的就是将其分解为二进制序列（也可以理解为分解成若干个2的n次方之和）：77 = 000001001101 = 1 + 4 + 8 +64，这样就得到了这个FLAG包含的意思：PE read，read比对不上参考序列，它的配对read也同样比不上参考序列，它是read1。

当然，如果你希望自己在程序中写一段处理FLAG的代码，那么显然是不会像我们这个例子那样去分解这个整数的，多麻烦啊！那么该如何做呢？其实也很简单，比如我们要获得其中某个位（假设第N位）的值——只需要将这个FLAG值和2的（N-1）次方做与的运算即可。在与运算时，FLAG值首先会被转换成一串二进制序列（如77=000001001101），而2的（N-1）次方除了第N位是1之外，其它的都是0，“与”了之后其它信息就会被屏蔽掉。比如，我们想知道该read是否比对上了参考序列，那么只需要计算FLAG & 4 的值就行了，如果结果是1那么就是比对上了，如果是0则代表没有比上。

## 解析
下面是perl对BAM文件FLAG实战解析的代码。
```buildoutcfg
#!/usr/bin/env perl
use strict;
use warnings;
use Cwd 'abs_path';
use File::Basename;
use Getopt::Long;
use Data::Dumper;
use FindBin qw($Bin);

# Global variable
my ($help, $outDir);

# Get Parameter
GetOptions(
	"h|help" => \$help, 
	"outDir=s" => \$outDir,
);

my $tmpDir = `pwd`;
chomp $tmpDir;
$outDir ||= "$tmpDir";

# Guide for program
my $guide_separator = "#" x 80;
my $program = basename(abs_path($0));
$program =~ s/\.pl//;
my $guide=<<INFO;
VER
	AUTHOR: xuxiangyang(xy_xu\@foxmail.com)
	NAME: $program
	PATH: $0
	VERSION: v1.0   2020-01-21
NOTE

USAGE
	$program <options> *.bam|*.sam 
	$guide_separator Basic $guide_separator
	--help				print help information
	--outDir <s>		script out Dir, default "$outDir"

INFO

die $guide if (@ARGV == 0 || defined $help);

# Main

my $total_read;
my $unmapped_read;
my $dup_read;
my $lowq_read;
my $effect_read;
my %result;

if ($ARGV[0] =~ m/bam$/i) {
	open IN, "samtools view $ARGV[0] | " or die $!; 
} else {
	open IN, $ARGV[0] or die $!;
}
while (<IN>) {
	$total_read++;
	chomp;
	my @arr = split /\t/;
	# 过滤未必对上的reads
	if ($arr[1] & 4) {
		$unmapped_read++;
		next;
	}
	# 过滤非初级比对的reads
	next if ($arr[1] & 256);
	# 过滤dup reads
	if ($arr[1] & 1024) {
		$dup_read++;
		next;
	}
	# 过滤supplementary alignment
	next if ($arr[1] & 2048);
	# 过滤低质量的reads
	if ($arr[4] < 30) {
		$lowq_read++;
		next;
	}
	if ($arr[5] =~ m/36M/) {
		$effect_read++;
		my $pos = $arr[3];
		#print "$arr[9]\n";
		while ($arr[9] =~ /(\w*?)((?:cg){2,})/gi) {
			#print "$1\n";
			#print "$2\n";
			my $s = $pos + length($1);
			my $e = $pos + length($1) + length($2) - 1;
			$pos += length($1) + length($2);
			#print "$arr[2]\t$s\t$e\t$2\t$2\n"; 
			$result{$arr[2]}{$s}{$e}{$2}++;
		}
	}
}
close IN;

my $unmapped_ratio = sprintf("%.2f", $unmapped_read/$total_read*100);
my $dup_ratio = sprintf("%.2f", $dup_read/$total_read*100);
my $lowq_ratio = sprintf("%.2f", $lowq_read/$total_read*100);
my $effect_ratio = sprintf("%.2f", $effect_read/$total_read*100);

print STDERR "unmapped_ratio: $unmapped_ratio%\n";
print STDERR "dup_ratio: $dup_ratio%\n";
print STDERR "lowq_ratio: $lowq_ratio%\n";
print STDERR "effect_ratio: $effect_ratio%\n";

foreach my $chr (sort {$a cmp $b} keys %result) {
	foreach my $start (sort {$a <=> $b} keys %{$result{$chr}}) {
		foreach my $end (sort {$a <=> $b} keys %{$result{$chr}{$start}}) {
			foreach my $genotype (sort {$a cmp $b} keys %{$result{$chr}{$start}{$end}}) {
				my $count = $result{$chr}{$start}{$end}{$genotype};
				print "$chr\t$start\t$end\t$genotype\t$genotype\t$count\n";
			}
		}
	}
}
```

## 其它
对于解析结果，可以参考<https://broadinstitute.github.io/picard/explain-flags.html>网站，进行验证。