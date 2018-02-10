```bash
$ ldd example
	linux-vdso.so.1 =>  (0x00007fff05dfe000)
	libyaml-cpp.so.0.6 => /home/liuzhihui/bin/yaml-cpp/lib/libyaml-cpp.so.0.6 (0x00007f84f16bb000)
	libstdc++.so.6 => /lib64/libstdc++.so.6 (0x00007f84f1389000)
	libm.so.6 => /lib64/libm.so.6 (0x00007f84f1087000)
	libgcc_s.so.1 => /lib64/libgcc_s.so.1 (0x00007f84f0e71000)
	libc.so.6 => /lib64/libc.so.6 (0x00007f84f0aaf000)
	/lib64/ld-linux-x86-64.so.2 (0x00007f84f1941000)

$ cat /etc/ld.so.conf
include ld.so.conf.d/*.conf
/usr/local/lib

$ ls /etc/ld.so.conf.d
atlas-x86_64.conf                  libiscsi-x86_64.conf  xulrunner-64.conf
dyninst-x86_64.conf                mariadb-x86_64.conf
kernel-3.10.0-327.el7.x86_64.conf  qt-x86_64.conf
```


#在PATH中找到可执行文件程序的路径。
export PATH =$PATH:$HOME/bin

#gcc找到头文件的路径
C_INCLUDE_PATH=/usr/include/libxml2:/MyLib
export C_INCLUDE_PATH

#g++找到头文件的路径
CPLUS_INCLUDE_PATH=$CPLUS_INCLUDE_PATH:/usr/include/libxml2:/MyLib
export CPLUS_INCLUDE_PATH

#运行时找到动态链接库的路径
LD_LIBRARY_PATH=$LD_LIBRARY_PATH:/MyLib
export LD_LIBRARY_PATH

#运行时找到静态库的路径
LIBRARY_PATH=$LIBRARY_PATH:/MyLib
export LIBRARY_PATH