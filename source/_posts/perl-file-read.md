---
title: perl文件读取
date: 2017-09-07 16:56:57
tags:
- Perl
categories:
- Perl
comments:
---

Perl程序读取文件有两种方式，一是用计算机内存来读取整个文件，然后在内存中操作文件，将其读出；另外一种方式就是使用seek()来在文件中移动文件读写指针(文件句柄)来读取文件的内容。

# 从内存中读取文件
使用计算机内存读取整个文件的内容，然后有两种方法来处理内存中的文件内容；

第一种方法是每次从文件中读取一行数据并存储到一个简单变量$Line中，然后把文件读写指针向后移动一行；如：
```buildoutcfg
$Line = <FILEHANDLE>；   # 从文件句柄FILEHANDLE中读取一行数据并存储到简单变量$Line中
```

第二种方法是把文件中的全部内容以行为单位读取到数组@Array中，文件中的每一行(含回车符)作为数组@Array的一个元素，使用数组的下标来访问文件中的不同行；如：
```buildoutcfg
@Array = <FILEHANDLE>；  # 把文件句柄FILEHANDLE中的所有行以行为单位读取到数组@Array中
```

由此可见，读取文件的操作符<>是根据上下文来决定每次是读取一行还是读取文件中的所有内容的：如果等号左边是一个简单的标量变量，则读取文件操作符<>每次只读取一行，并存储到这个简单变量中；如果等号左边是一个数组，那么读取文件操作符<>就把整个文件中的内容以行(包含回车符)为单位读取到数组中，每一行作为数组中的一个元素；如果读取文件操作符<>不带任何参数(即：“<”和“>”之间不带任何文件句柄)，则默认是从标准输入文件句柄STDIN中读取数据，即：通过键盘从命令行读取数据；
每次读取新行时，文件输入运算符<>返回1；读取完最后一行再读取时，文件输入运算符返回空值，这个条件就可以作为判断文件读写位置指针是否已经到达文件尾部的条件；
这种方式使用起来比较简单，适用于小文件中，但是如果文件的体积比较大的话，就不合适了，这个时候可以适用seek()函数；

# 使用seek()函数读取文件
seek()函数是通过文件句柄来移动文件读写指针的方式来读取或写入文件的，以字节为单位进行读取和写入；使用seek()函数可以定位程序需要读取或写入的下一个位置；在打开一个文件进行读取时，文件读写位置指针停在文件的开头，每次读写文件中的数据时，文件读写指针就会自动向前移动，其位置是读写停止的位置；在打开一个文件进行追加时，文件的读写位置指针停在文件尾部；当需要在文件开头和结尾之间进行转移时，就需要使用seek()函数进行文件读写位置定位；
seek()函数可以在文件中随意地移动文件句柄(文件读写指针)的位置；seek()函数有三个基本的位置：文件开头(0)、当前位置(1)和文件末尾(2)，可以从这些位置处指定偏移量，来指定文件句柄(文件读写指针)在文件中所要移动到的位置；
seek()函数的语法如下：
seek(FILEHANDLE，BytesToSkip，StartLocation)；
BytesToSkip：表示文件句柄(读写位置指针)要移动的字节数；如果尾为正数，则表示向文件尾的方向移动；如果为负数，则表示向文件头的方向移动；需要注意的是，文件句柄(读写位置指针)不能移动到文件头和文件尾之外的地方，即：文件句柄(读写位置指针)只能在文件头和文件尾之间进行移动；每个英文字母和标点符号各占用一个字节，而每个汉字和中文标点符号则各需要占用两个字节；
StartLocaltion：表示文件句柄(读写位置指针)开始移动时的起始位置，可以取的值为0、1、2；分别表示文件开头、当前位置和文件尾；
FILEHANDLE：需要被操作的文件句柄；
函数调用成功时返回非零值(真)，失败时返回零值(假)；常与tell()函数合用；
在两个seek()调用之间不必关闭文件再重新打开，这样就提高了文件的读取速度；

# tell()函数
使用seek()函数定位文件读写位置指针时的一个最大的缺点就是，它以字节为单位来定位文件读写位置指针，在不同的计算机上的可移植性较差，程序不一定能在其它计算机上运行；
解决这个问题的方法就是使用tell()函数来提取文件读写位置指针所指向的位置；语法如下：
$Position = tell(FILEHANDLE)；
seek(FILEHANDLE，$Position，0) ；
这个函数用于返回从文件开头位置处到当前读写位置处的距离(字节数)；
**注意：** seek()函数和tell()函数不能用于指向管道的文件变量；

# seek(), tell()实例
```buildoutcfg
#!/usr/bin/env perl
use strict;
use warnings;
use Cwd 'abs_path';
use File::Basename;
use Getopt::Long;
use Data::Dumper;

# Global variable
my ($help, $outDir, $bedFile, $bam_region);

# Get Parameter
GetOptions(
	"h|help" => \$help,	
	"outDir=s" => \$outDir,
	"bedFile=s" => \$bedFile,
	"bam_region=s" => \$bam_region,
);

my $tmpDir = `pwd`;
chomp $tmpDir;
$outDir ||= "$tmpDir";
$bedFile ||= "/datapool/home/xuxiangyang/pipeline/levicare/example/uniq_reads_count/hg19_k24.uniq.sort.merge24.5k.bed";
$bam_region ||= "";

# Guide for program
my $guide_separator = "#" x 80;
my $program = basename(abs_path($0));
$program =~ s/\.pl//;
my $guide=<<INFO;
VER
	AUTHOR: xuxiangyang(xy_xu\@foxmail.com)
	NAME: $program
	PATH: $0
        VERSION: v0.1	2017-09-05
NOTE
	1. bam and bed must be sorted by coordinate
	2. you must be count reads by chr
	3. you must set bam_region parameter

USAGE
	$program <options> *.bam
	$guide_separator Basic $guide_separator
	--help			print help information
	--outDir <s>		script out Dir, default "$outDir"
	--bedFile <s>		region file for count reads number, default "$bedFile"
	--bam_region <s>	count reads number for which chr, format like: chr1, chr1:10000, chr1:10000-20000, default "$bam_region"

INFO

die $guide if (@ARGV == 0 || defined $help);

# Main
my $grep_opt;
my $chr_id;
if ($bam_region) {
	my @arr = split ":", $bam_region;
	$chr_id = $arr[0];
	$grep_opt = "-w " . $arr[0];
} else {
	$grep_opt = ".";	
}
my $position=0;
my (%region_count, $start, $end, @jump);

open BAM, "/datapool/home/xuxiangyang/pipeline/exome/bin/samtools_v0.1.18/samtools view -X $ARGV[0] $bam_region |" or die $!;
#open BAM, $ARGV[0] or die $!;
open BED, "grep $grep_opt $bedFile |" or die $!;

while (<BED>) {
	chomp;
	next if(/^#/);
	my @arr = split /\s+/;
	$start = $arr[1];
	$end = $arr[2];
	$region_count{$arr[0]}{$start}{$end} = 0;
	# 校验BAM跳出所在行是否在新的bed区间，没有区分染色体
	if (@jump) {
		if($jump[3] >= $start && $jump[3] <= $end) {
			$region_count{$jump[2]}{$start}{$end}++;
			@jump = ();
		}
	}
	# 渐进读取BAM文件，BAM文件与BED文件必须排序，且以染色体为单元进行统计	
	seek(BAM, $position, 0);	# 绑定文件句柄BAM至新的position
	while (<BAM>) {
		my @arr2 = split /\s+/;
		next if ($arr2[1] =~ m/u/);
		if ($arr2[3] > $end) {
			$position = tell(BAM);
			@jump = @arr2;
			last;
		}
		if($arr2[3] >= $start && $arr2[3] <= $end) {
			$region_count{$arr2[2]}{$start}{$end}++;
		}
	}	

}
close BAM;
close BED;

#print Dumper \%region_count;

my $prefix = basename $ARGV[0]; 
$prefix =~ s/\.bam//;

open OUTPUT, ">$outDir/$prefix.$chr_id.count" or die $!; 
foreach my $chr (sort {$a cmp $b} keys %region_count) {
	foreach my $s (sort {$a <=> $b} keys %{$region_count{$chr}}) {
		foreach my $e (sort {$a <=> $b}keys %{$region_count{$chr}{$s}}) {
			print OUTPUT "$chr\t$s\t$e\t$region_count{$chr}{$s}{$e}\n";
		}
	}
}
close OUTPUT;
```