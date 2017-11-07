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

# 递归删除子文件夹

```
$ find ./ -name __pycache__ | xargs rm -rf
```

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
