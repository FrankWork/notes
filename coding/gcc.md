```bash
strings /usr/lib64/libstdc++.so.6 | grep GLIBCXX

```

## version `GLIBC_2.23` not found

rpm2cpio glibc-2.26-21.fc27.i686.rpm | cpio -idv

ldd anaconda3/lib/python3.6/site-packages/tensorflow/python/_pywrap_tensorflow_internal.so

##

/usr/lib64/libstdc++.so.6: version `CXXABI_1.3.5' not found

strings /usr/lib64/libstdc++.so.6 | grep 'CXXABI'

CXXABI_1.3
CXXABI_1.3.1
CXXABI_1.3.2
CXXABI_1.3.3

strings /opt/compiler/gcc-4.8.2/lib64/libstdc++.so.6 | grep 'CXXABI'
CXXABI_1.3
CXXABI_1.3.1
CXXABI_1.3.2
CXXABI_1.3.3
CXXABI_1.3.4
CXXABI_1.3.5
CXXABI_1.3.6
CXXABI_1.3.7
CXXABI_TM_1

指定动态库
1. 
/opt/compiler/gcc-4.8.2/lib/ld-linux-x86-64.so.2 --library-path /opt/compiler/gcc-4.8.2/lib Python-3.6.5-horovod-torch1.4/bin/python3
2. 
export LD_LIBRARY_PATH="$LD_LIBRARY_PATH:${HOME}/local/lib64"
3. 
gcc 编译时指定
gcc中的rpath参数可以用编译时指定动态库的搜索路径，这样运行时就不需要export LD_LIBRARY_PATH了。


# compile gcc

```bash
export GCC_HOME=$HOME/bin/gcc-5.5.0
unset LIBRARY_PATH

tar zxvf gcc-5.5.0.tar.gz
cd gcc-5.5.0
./contrib/download_prerequisites
cd ..
mkdir objdir
cd objdir
$PWD/../gcc-5.5.0/configure --prefix=$GCC_HOME --disable-multilib --enable-languages=c,c++,go # 64-bit only
make
make install

export PATH=$GCC_HOME/bin:$PATH
export LD_LIBRARY_PATH=$GCC_HOME/lib:$LD_LIBRARY_PATH
export LD_LIBRARY_PATH=$GCC_HOME/lib64:$LD_LIBRARY_PATH
```



