
```bash
$ yum install ctags

$ wget http://prdownloads.sourceforge.net/ctags/ctags-5.8.tar.gz
$ tar zxvf ctags-5.8.tar.gz
$ cd ctags-5.8 && ./configure --prefix=$HOME/local/ctags
$ make && make install





$ ctags --list-languages
$ ctags --list-maps
$ ctags --list-kinds=c++
$ ctags -R --c++-kinds=+px # 增加分析c++的p和x语法元素
$ ctags -R # 默认当前目录，递归处理子目录
```
