http://www.cnblogs.com/witcxc/archive/2011/12/28/2304704.html
https://blog.csdn.net/tietao/article/details/6862341

字体大小：xshell客户端 菜单栏->文件->属性->外观

用户自定义配置文件：~/.vimrc
配置文件
	~/.vimrc
	/etc/vimrc

帮助
	:help

设置 :set

:set nu 			" 显示行号
:set nonu			" 取消显示行号
:set tabstop=4		" tab空格数
:set shiftwidth=4	" 自动缩进时，缩进的空格数
:set smartindent   	" 开启新行时智能缩进
:set wrap			" 折叠过长文本
:set nowrap			" 取消折叠
:set invlist		" 显示特殊字符
:set list			" 显示特殊字符
:set nolist			" 取消显示特殊字符
:set hlsearch   	" 搜索时高亮显示被找到的文本
:set sm				" 显示匹配的括号
:set cursorline		" 高亮显示当前行
:set textwidth=79	" 自动折叠的文本最大长度
:set nobackup		" 不自动备份

语法折叠
:set foldmethod=syntax " 语法折叠
	zc 关闭折叠； 
	zo 打开折叠； 
	za 打开/关闭折叠互相切换

函数跳转
	sudo apt-get install exuberant-ctags
	ctags -R .
	将光标移到想要跳转的函数或变量上，通过快捷键 " CTRL + ] "即可快速跳转，
	通过快捷键“ CTRL + T ”，回到跳转之前的位置



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

删除
	d$	删除到行尾

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