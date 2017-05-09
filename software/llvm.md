# compile llvm 

```
$ sudo apt install subversion
$ sudo apt install cmake

$ cd where-you-want-llvm-to-live/
$ svn co http://llvm.org/svn/llvm-project/llvm/trunk llvm
$ cd llvm/tools
$ svn co http://llvm.org/svn/llvm-project/cfe/trunk clang
$ cd ../projects
$ svn co http://llvm.org/svn/llvm-project/compiler-rt/trunk compiler-rt
 #$ svn co http://llvm.org/svn/llvm-project/libcxx/trunk libcxx
 #$ svn co http://llvm.org/svn/llvm-project/libcxxabi/trunk libcxxabi


$ cd ..
$ mkdir build
$ cd build
$ cmake -DCMAKE_BUILD_TYPE:String=Release -DCMAKE_INSTALL_PREFIX=$HOME/bin/llvm ../
$ make install
```


# compile gcc

bzip2 -d gcc-5.4.0.tar.bz2
tar xvf gcc-5.4.0.tar
cd gcc-5.4.0
./contrib/download_prerequisites
cd ..
mkdir objdir
cd objdir
$PWD/../gcc-5.4.0/configure --prefix=$HOME/bin/gcc-5.4.0 --disable-multilib --enable-languages=c,c++,go # 64-bit only
make
make install

# compile glibc
sudo apt install gawk

git clone git://sourceware.org/git/glibc.git
cd glibc
git checkout --track -b local_glibc-2.25 origin/release/2.25/master
mkdir build
cd build
../configure --prefix=$HOME/bin/glibc-2.25
make
make install



# lib

export LD_LIBRARY_PATH="$HOME/bin/gcc-5.4.0/lib64:$LD_LIBRARY_PATH"
export LD_LIBRARY_PATH="$HOME/bin/glibc-2.25/lib:$LD_LIBRARY_PATH" 段错误

ln -sf lib64 ~/bin/lib
