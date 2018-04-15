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
	:set invlist
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
