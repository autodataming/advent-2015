#巧妙使用getopt

##getopt::Long

这是一个核心模块,作者是JV

corelist  Getopt::Long

###功能
让脚本使用起来更简单，通过增加选项，来传递参数，这样就有意义，方便记忆。 比单纯通过@ARGV来传递参数好。

一个有素质的程序员，一定是为用户考虑的。强烈推荐大家使用Getopt::Long 来传递参数。

比如linux下有各种命令

ls -rtlh  这里的可选项是开关作用

比如分子格式转换的程序

antechamber -fi gout -i 1.log -fo prepi -o 1.prep

这里的选项的作用就不是开关而是传递参数。由于和书写先后顺序无关，所以比@ARGV更好记忆。

###例子

框架如下。

首先确定需要的可选项。

各种可选项的定义：

ls -rtlh 这几个参数（rtlh），这里称他们为开关选项，属于非强制选项

-fi  gout -i 1.log 这些选项称为强制选项，需要引入die 机制

--help 比较特殊，随意在代码中的布局，要放到最前面

比如默认是定位到屏幕中，有时候我们想把它定位到文件中

--out  out.txt 非强制选项

```Perl
use Getopt::Long;  #核心模块，非常好用，功能强悍
#申明各种选项变量
my ($errfile, $forcefile,$outfile,$gjffile); #非开关选项

#开关选项，0代表默认是关
my $help=0;
my $debug=0;
my $warning=0;

#建议大家定义一个usage函数，用来报错的
#返回出错信息以及用法
sub usage {
   my $message = $_[0];
   my $command = $0;
   print STDERR (
      $message,
      "usage: perl $command --errfile file.err --igjf file.gjf --forcefile gaff.dat [--out out.txt] \n" .
      "file.err: Include all MM classes(start)... MM function not complete(end)       ...\n" .
      "forcefile: some forefield files like gaff.dat\n" .
      "gjffile:  to increare accuracy,you should special gjf file\n"
   );

   die("\n")
}


#引入getopt机制传递命令行到变量
#define all the options (force or not force)
#if some new options come across ,error will be report
#default all the option is not force
GetOptions
(
'errfile=s'=>\$errfile,
'igjf=s'=>\$gjffile,
'forcefile=s'=>\$forcefile,
'help!'=>\$help,
'debug!'=>\$debug,
'warning!'=>\$warning,
)
or usage( "Error in command line arguments");
 
#对help选项进行定义
#help should before the force option
if($help)
{
   usage("usage:
   ");	
}
 
#对强制选项进行检查
#set some options is force 

usage("The errorfile  must be specified.")
   unless defined $errfile;
   
usage("The forcefile  must be specified.")
   unless defined $forcefile;

usage("The gjffile  must be specified.")
   unless defined $gjffile;
   

```

##Getopt::Long::Descriptive

这是一个新型模块，作者是RJBS

corelist Getopt::Long::Descriptive

非核心模块。把usage函数封装了而已。

建议大家使用Getopt::Long
