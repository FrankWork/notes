# install on centos 

## 编译

PREFIX=$HOME/bin
mkdir -p PREFIX

tar xvfJ Python-3.6.0.tar.xz # tar > 1.22, on centos 7.2 tar 1.26
cd Python-3.6.0/

./configure --prefix=$PREFIX # run ./configure --help to find out the options
make
make test
make install


## yum

yum install https://centos7.iuscommunity.org/ius-release.rpm
yum install python36u
ln -s /bin/python3.6 /bin/python3
yum install python36u-pip
ln -s /bin/pip3.6 /bin/pip3




# install Pip
wget https://bootstrap.pypa.io/get-pip.py
python3.4 get-pip.py



python注释,模块结构和布局

＃/usr/bin/env python		起始行
# -*- encoding:utf-8 -*-	文本编码

"this is a test module"		模块文档

import sys					模块导入
import os

debug = True				全局变量

class FooClass(object):		类定义
	"Foo Class"				类注释
	pass

def test():					函数定义
	"test function"			函数注释
	foo = FooClass()

	if debug:
		print 'ran test()'
	
if __name__ == '__main__':	主程序
	test()


# pdb debug





