*    $0 ： ./test.sh,即命令本身，相当于c/c++中的argv[0]
*    $1 ： -f,第一个参数.
*    $2 ： config.conf
*    $3, $4 ... ：类推。
*    $#  参数的个数，不包括命令本身，上例中$#为4.
*    $@ ：参数本身的列表，也不包括命令本身，如上例为 -f config.conf -v --prefix=/home
*    $* ：和$@相同，但"$*" 和 "$@"(加引号)并不同，"$*"将所有的参数解释成一个字符串，而"$@"是一个参数数组。

# 颜色设置

black='\[\033[0;30m\]' 
darkgray='\[\033[1;30m\]'
blue='\[\033[0;34m\]' 
lightBlue='\[\033[1;34m\]'
green='\[\033[0;32m\]' 
lightgreen='\[\033[0;32m\]'
cyan='\[\033[0;36m\]' 
lightcyan='\[\033[1;36m\]'
red='\[\033[0;31m\]' 
lightred='\[\033[1;31m\]'
purple='\[\033[0;35m\]' 
lightpurple='\[\033[0;35m\]'
brown='\[\033[0;33m\]' 
yellow='\[\033[1;33m\]'
lightgray='\[\033[0;37m\]' 
white='\[\033[1;37m\]'
nocolor='\[\033[0m\]'

PS1="${lightgreen}\u@\h${nocolor}:${lightpurple}\w ${nocolor}\$ "
