用户自定义配置文件：~/.vimrc
http://www.cnblogs.com/witcxc/archive/2011/12/28/2304704.html

帮助
	:help

配置高亮颜色：
	 ls /usr/share/vim/vim74/syntax
显示行号
    :set nu 	显示行号，设定之后，会在每一行的前缀显示该行的行号
    :set nonu
wrap
	:set wrap
	:set nowrap
show tab list
	:set invlist 或 :set list
	:set nolist
复制操作
　　yy  复制当前整行
　　yw  复制一个字
　　#yy 复制#行
　　#yw 复制#个单词
查找
	/patern  向后找 n N
	?pattern 向前找 n N 查找下一个

粘贴
	vim有12个粘贴板，分别是0、1、2、...、9、a、"、+；
	:reg "N 命令可以查看各个粘贴板里的内容。
	
	y     p    粘贴板为 "
	"Ny   "Np  粘贴板为 N, 0<=N<=9
	"+y   "+p   系统粘贴板
	 
回退
	u   撤销上一步的操作

正则表达式
	\/ 	匹配 / 字符。
	\\ 	匹配 \ 字符。
	
    \m: magic			除了`^.*$`之外所有的字符都需要加反斜杠
    \M: nomagic			除了`^$`之外所有的字符都需要加反斜杠
    \v: very magic		任何字符都不需要加反斜杠
    \V: very nomagic	任何字体都需要加反斜杠

	\v[\u4e00-\u9fa5]+ " 查找中文
	[\u4e00-\u9fa5]\+  " 默认为magic, `+`需要加反斜杠

替换
	:%s/old_text/new_text/g

跳转
	:1 跳到文件头
	:$ 跳到文件尾


二进制编辑
	vim -b file