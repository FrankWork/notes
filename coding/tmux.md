

## install by release tarball

- libevent 2.x

- ncurses

wget https://github.com/tmux/tmux/releases/download/2.8/tmux-2.8.tar.gz -O tmux-2.8.tar.gz
cd tmux-2.8
./configure --prefix=${HOME}/local
make -j8 && make install




install by git

$ git clone https://github.com/tmux/tmux.git
$ cd tmux
$ sh autogen.sh
$ ./configure --prefix=$HOME && make -j 16 && make install




apt install tmux

 tmux所有自带命令都默认需要先按Ctrl + b，然后再键入对应的命令

Ctrl+b " - split pane horizontally"
Ctrl+b % - 将当前窗格垂直划分
Ctrl+b 方向键 - 在各窗格间切换
Ctrl+b，并且不要松开Ctrl，方向键 - 调整窗格大小
Ctrl+b c - (c)reate 生成一个新的窗口
Ctrl+b n - (n)ext 移动到下一个窗口
Ctrl+b p - (p)revious 移动到前一个窗口.
Ctrl+b 空格键 - 采用下一个内置布局 
Ctrl+b q - 显示分隔窗口的编号 
Ctrl+b o - 跳到下一个分隔窗口 
Ctrl+b & - 确认后退出 tmux 

这几个命令都试几遍，这个工具基本上也就算上手了，简单才是最重要的。

再顺便提一个“高级”点的用法：

我经常进了tmux后会习惯地再生成几个窗格，好比上面那个图中的布局，左边一个，右边上下各一个。而每次进了tmux都这样输命令，是不是很麻烦？有没有办法一进tmux，就自动生成如上的布局，答案是有的，方法应该不止一种。下面提供一个作者选用的方法：

首先写一个脚本，来创建各个窗格

~/.tmux/mylayout

selectp -t 0    #选中第0个窗格
splitw -h -p 50  #将其分成左右两个
selectp -t 1     #选中第一个，也就是右边那个
splitw -v -p 50  #将其分成上下两个，这样就变成了图中的布局了
selectp -t 0     #选回第一个

在.tmux.conf 后面加上一句

bind D source-file ~/.tmux/mylayout  

结束，这样每次进入tmux后，键入 Ctrl + b D (D是大写，要按shrift，你也可以按成其他字符，只要跟tmux已经用的不冲突即可)，即会自动执行mylayout脚本，生成图示布局。如果 .tmux.conf 文件不存在的话，请自己生成。注意前面有个.(点)


另外还有一些小功能，通过在.tmux.conf中添加相应的命令打开对应的功能即可：

鼠标可以选中窗格  set-option -g mouse-select-pane on

鼠标滚轮可以用    set-window-option -g mode-mouse on
