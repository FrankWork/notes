http://www.cnblogs.com/witcxc/archive/2011/12/28/2304704.html
https://blog.csdn.net/tietao/article/details/6862341

字体大小：xshell客户端 菜单栏->文件->属性->外观

## vim安装与配置

```bash
$ yum install vim-enhanced
$ vim /etc/bashrc
	alias vi='vim'

$ yum install gcc-c++ ncurses-devel python-devel
$ git clone https://github.com/vim/vim.git
$ cd vim/src
$ ./configure --enable-multibyte --enable-pythoninterp=yes
$ make && make install 
$ vim --version # log out and log in to refresh
```
用户自定义配置文件：~/.vimrc
配置文件
	~/.vimrc
	/etc/vimrc

帮助
	:help

设置 :set

:set nu 			" 显示行号
" :set nonu			" 取消显示行号
:set tabstop=4		" tab空格数
:set shiftwidth=4	" 自动缩进时，缩进的空格数
:set smartindent   	" 开启新行时智能缩进
:set wrap			" 折叠过长文本
" :set nowrap			" 取消折叠
" :set invlist		" 显示特殊字符
" :set list			" 显示特殊字符
:set nolist			" 取消显示特殊字符
:set hlsearch   	" 搜索时高亮显示被找到的文本
:set sm				" 显示匹配的括号
:set cursorline		" 高亮显示当前行
:set textwidth=79	" 自动折叠的文本最大长度
:set nobackup		" 不自动备份
:set ruler			" 显示当前位置
":set paste			" 防止起始行为注释时，自动注释到后面几行；原本意思为粘贴时保持原样，和自动缩进冲突
:set fenc"文件编码 
:set fileencoding"文件编码
syntax on

语法折叠
:set foldmethod=syntax " 语法折叠"
	zc 关闭折叠； 
	zo 打开折叠； 
	za 打开/关闭折叠互相切换

## 跳转

^或0		行首	
$		 行尾

## 编辑

复制
　　yy  复制当前整行
　　yw  复制一个字
　　#yy 复制#行
　　#yw 复制#个单词
粘贴
	vim有12个粘贴板，分别是0、1、2、...、9、a、"、+；
	:reg "N 命令可以查看各个粘贴板里的内容。
	
	y     p    粘贴板为 "
	"Ny   "Np  粘贴板为 N, 0<=N<=9
	"+y   "+p   系统粘贴板"

删除(剪切)
	dd	删除整行
	d$	删除到行尾
回退
	u   	撤销上一步的操作
	ctrl+r	恢复被撤销的操作
缩进
	>> 缩进 >表示shift+>
	<< 回缩
	:10,100>	第10行至第100行缩进
	:20,80<		第20行至第80行反缩进
多行缩进
	1 //在这里按下'v'进入选择模式
	1
	1
	1//光标移动到这里，再按一次大于号'>'缩进一次，按'6>'缩进六次，按'<'回缩。以下同理	
多行编辑
	选定区域：将光标移到要编辑的开始位置，按CTRL+V进入visual block模式，将光标移到编辑块的最后位置
	编辑：   按i或I编辑一行，按esc退出编辑模式，vi自动扩展到多行
多行复制
	: 6,9 co 12  "第6行到第9行复制到第12行"
多行剪切
	: 6,9 m 12
多行删除
	: 6,9 de
多文件编辑
    vim file1 file2 ... filen
    :open file
    :bn—下一个文件
    :bp—上一个文件

正则表达式
	\/ 	匹配 / 字符。
	\\ 	匹配 \ 字符。
	
    \m: magic			除了`^.*$`之外所有的字符都需要加反斜杠
    \M: nomagic			除了`^$`之外所有的字符都需要加反斜杠
    \v: very magic		任何字符都不需要加反斜杠
    \V: very nomagic	任何字体都需要加反斜杠

	\v[\u4e00-\u9fa5]+ " 查找中文"
	[\u4e00-\u9fa5]\+  " 默认为magic, `+`需要加反斜杠"

特殊字符
    ^M windows下换行符, 替换 :%s/^M//g
    按Ctrl+V+M输入^M
    空格替换为换行 :%s/ /\r/g

查找
	/patern  向后找 n N
	?pattern 向前找 n N 查找下一个

替换
	:%s/old_text/new_text/g
    :%s/  /\t/g   "两个空格替换为一个tab"
跳转
	:1 跳到文件头
	:$ 跳到文件尾

历史记录
	输入`:`，然后用上下箭头
	:history

二进制编辑
	vim -b file

## 插件管理 Vundle

https://juejin.im/post/5a38c37f6fb9a0450909a151

```bash
$ git clone https://github.com/gmarik/Vundle.vim.git ~/.vim/bundle/Vundle.vim
$ vi ~/.vimrc
```
```vimscript
set nocompatible               " be iMproved, required
filetype off                   " required
set rtp+=~/.vim/bundle/Vundle.vim
call vundle#begin()

Plugin 'gmarik/Vundle.vim'		" 插件管理
Plugin 'scrooloose/nerdtree' 	" 目录树
Plugin 'majutsushi/tagbar'		" 代码导航
Plugin 'terryma/vim-multiple-cursors' "多光标编辑

call vundle#end()              " required
filetype plugin indent on      " required

"打开文件夹时，自动打开NERDTree窗口"
autocmd StdinReadPre * let s:std_in=1
autocmd VimEnter * if argc() == 1 && isdirectory(argv()[0]) && !exists("s:std_in") | exe 'NERDTree' argv()[0] | wincmd p | ene | endif
map <F2> :NERDTreeToggle<CR>	" F2打开NERDTree窗口

let g:tagbar_left = 1
nmap <F3> :TagbarToggle<CR>		"F3打开TagBar窗口，依赖ctags程序

```
打开vim运行:PluginInstall，就可以安装好配置文件中的插件

## 插件管理 vim-plug

```vimscript
if empty(glob('~/.vim/autoload/plug.vim'))
  silent !curl -fLo ~/.vim/autoload/plug.vim --create-dirs
    \ https://raw.githubusercontent.com/junegunn/vim-plug/master/plug.vim
  autocmd VimEnter * PlugInstall --sync | source ~/.vimrc
endif

call plug#begin('~/.vim/plugged')

Plug 'junegunn/vim-easy-align'
Plug 'scrooloose/nerdtree'		" 目录树
Plug 'majutsushi/tagbar'		" 代码导航
Plug 'terryma/vim-multiple-cursors'	"多光标编辑

" Initialize plugin system
call plug#end()

"打开文件夹时，自动打开NERDTree窗口"
autocmd StdinReadPre * let s:std_in=1
autocmd VimEnter * if argc() == 1 && isdirectory(argv()[0]) && !exists("s:std_in") | exe 'NERDTree' argv()[0] | wincmd p | ene | endif
map <F2> :NERDTreeToggle<CR>	" F2打开NERDTree窗口

let g:tagbar_left = 1
nmap <F3> :TagbarToggle<CR>	"F3打开TagBar窗口，依赖ctags程序

" Start interactive EasyAlign in visual mode (e.g. vipga)
xmap ga <Plug>(EasyAlign)
" Start interactive EasyAlign for a motion/text object (e.g. gaip)
nmap ga <Plug>(EasyAlign)

```
打开vim运行:PlugInstall，就可以安装好配置文件中的插件

## 自动对齐 vim-easy-align

用=对齐文本，有以下两种方法
- vipga=
- gaip=

https://github.com/junegunn/vim-easy-align

## 目录管理 NERDTree

`CTRL+WW`在左右两侧窗口跳转，<C+W><C+h/j/k/l>来执行左下上右的跳转
在目录上按回车，可以打开目录树，再按一下可以关闭目录树
在文件上按回车，可以进入文件编辑

t	在标签页中打开, 按ctrl+pageup, ctrl+pagedown在标签页中切换
r	刷新窗口
m	文件系统菜单(添加、删除、移动）

:bn		下一个文件
:bp		上一个文件

## 多窗口编辑

:split 水平分割
:vsplit 垂直分割


## 代码补全 

- 原生补全：
	<C-x><C-o>触发。<C-n> 和 <C-p> 选择
	<C-p> 自动补全文件中能找到的字符串

- YouCompleteMe
	不好用，容易卡死
	$ yum install cmake
	$ cd ~/.vim/bundle/YouCompleteMe && python ./install.py

## 多光标编辑 vim-multiple-cursors

a, b, c,

 v 进入visual mode
 <C-n> 选择
 <C-n> 选择下一个 。。。
 I或A编辑
 <Esc> 退出编辑



## 代码导航 CTags + TagList + TagBar

https://blog.csdn.net/leopard21/article/details/40402515

```bash
$ yum install ctags
$ ctags --list-languages
$ ctags --list-maps
$ ctags --list-kinds=c++
$ ctags -R --c++-kinds=+px # 增加分析c++的p和x语法元素
$ ctags -R # 默认当前目录，递归处理子目录
```
在当前目录生成`tags`文件后，用vi打开源代码，
通过快捷键"CTRL+]"，即可快速跳转到函数定义，
通过快捷键"CTRL+T"，回到跳转之前的位置
通过快捷键"CTRL+O"，回到最初的位置

安装TagList （弃用）
```
$ curl -o taglist_46.zip https://www.vim.org/scripts/download_script.php?src_id=19574
$ mkdir -p ~/.vim
$ unzip taglist_46.zip -d ~/.vim
$ vi ~/.vimrc
" Tlist                             "
let Tlist_Auto_Open=0 				" don't auto open
"let Tlist_Use_Left_Window=1		"set taglist window in left
let Tlist_Auto_Update=1
let Tlist_File_Fold_Auto_Close=1 	"auto close Tlist when exiting file.
let Tlist_Exit_OnlyWindow = 1
nmap <F7> :copen<CR>
nmap <F6> :cclose<CR>
nnoremap <silent> <F8> :TlistToggle<CR>
```
按F8打开TagList左侧窗口，`CTRL+WW`在左右两侧窗口跳转

# neovim

```bash
$ yum -y install epel-release
$ curl -o /etc/yum.repos.d/dperson-neovim-epel-7.repo https://copr.fedorainfracloud.org/coprs/dperson/neovim/repo/epel-7/dperson-neovim-epel-7.repo 
$ yum -y install neovim
$ vim /etc/bashrc
	alias vi='vim'
$ mkdir -p .config/nvim
$ vi .config/nvim/init.vim
set nu 			" 显示行号
set tabstop=4	" tab空格数
set shiftwidth=4	" 自动缩进时，缩进的空格数
set softtabstop=4
set wrap			" 折叠过长文本
set cursorline		" 高亮显示当前行
set textwidth=79	" 自动折叠的文本最大长度
set nobackup		" 不自动备份
set ruler			" 显示当前位置
```
