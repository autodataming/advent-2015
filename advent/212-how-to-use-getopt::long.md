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
···Perl


···

##Getopt::Long::Descriptive
这是一个新型模块，作者是RJBS
corelist Getopt::Long::Descriptive
