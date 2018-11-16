```bash
strings /usr/lib64/libstdc++.so.6 | grep GLIBCXX

```

## version `GLIBC_2.23` not found

rpm2cpio glibc-2.26-21.fc27.i686.rpm | cpio -idv

ldd anaconda3/lib/python3.6/site-packages/tensorflow/python/_pywrap_tensorflow_internal.so


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
