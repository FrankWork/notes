# whereis <程序名称>
    查找软件的安装路径
    Locate the binary, source, and manual-page files for a command.

    选项：
     -b         search only for binaries
     -B <dirs>  define binaries lookup path
     -m         search only for manuals and infos
     -M <dirs>  define man and info lookup path
     -s         search only for sources
     -S <dirs>  define sources lookup path
     -f         terminate <dirs> argument list
     -u         search for unusual entries
     -l         output effective lookup paths

# find [路径] <表达式>
    查找文件
    用法: find [-H] [-L] [-P] [-Olevel] [-D help|tree|search|stat|rates|opt|exec|time] [path...] [expression]

    默认路径为当前目录；默认表达式为 -print
    表达式可能由下列成份组成：操作符、选项、测试表达式以及动作：

    操作符 (优先级递减；未做任何指定时默认使用 -and):
          ( EXPR )   ! EXPR   -not EXPR   EXPR1 -a EXPR2   EXPR1 -and EXPR2
          EXPR1 -o EXPR2   EXPR1 -or EXPR2   EXPR1 , EXPR2

    位置选项 (总是真): -daystart -follow -regextype

    普通选项 (总是真，在其它表达式前指定):
          -depth --help -maxdepth LEVELS -mindepth LEVELS -mount -noleaf
          --version -xdev -ignore_readdir_race -noignore_readdir_race

    测试(N可以是 +N 或-N 或 N):-amin N -anewer FILE -atime N -cmin  
          -cnewer 文件 -ctime N -empty -false -fstype 类型 -gid N -group 名称
          -ilname 匹配模式 -iname 匹配模式 -inum N -ipath 匹配模式 -iregex 匹配模式
          -links N -lname 匹配模式 -mmin N -mtime N -name 匹配模式 -newer 文件
          -nouser -nogroup -path PATTERN -perm [-/]MODE -regex PATTERN
          -readable -writable -executable
          -wholename PATTERN -size N[bcwkMG] -true -type [bcdpflsD] -uid N
          -used N -user NAME -xtype [bcdpfls]
          -context 文本


    操作: -delete -print0 -printf 格式 -fprintf 文件 格式 -print
          -fprint0 文件 -fprint 文件 -ls -fls 文件 -prune -quit
          -exec 命令 ; -exec 命令 {} + -ok 命令 ;
          -execdir 命令 ; -execdir 命令 {} + -okdir 命令 ;

# 从文件内容查找匹配指定字符串的行：

$ grep "被查找的字符串" 文件名
$ grep -e "正则表达式" 文件名

# 从根目录查找所有扩展名为.log的文本文件， 并找出包含“ERROR”的行
$ find / -type f -name "*.log" | xargs grep "ERROR"

# 查找到httpd.conf文件后即在屏幕上显示文件信息
$ find / -name "httpd.conf" -ls

# 查找某个文件
$ find . -name "test"

# 查找包含某个字符串的文件
$ grep -r "zh_CN" ./
