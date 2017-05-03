# compile

$ sudo apt install subversion
$ sudo apt install cmake

$ cd where-you-want-llvm-to-live/
$ svn co http://llvm.org/svn/llvm-project/llvm/trunk llvm
$ cd llvm/tools
$ svn co http://llvm.org/svn/llvm-project/cfe/trunk clang
$ cd ../projects
$ svn co http://llvm.org/svn/llvm-project/compiler-rt/trunk compiler-rt
$ svn co http://llvm.org/svn/llvm-project/libcxx/trunk libcxx
$ svn co http://llvm.org/svn/llvm-project/libcxxabi/trunk libcxxabi


$ cd ..
$ mkdir build
$ cd build
$ cmake -DCMAKE_BUILD_TYPE:String=Release -DCMAKE_INSTALL_PREFIX=$HOME/bin/llvm ../
$ make install


$ rm -rf build/*
$ export CC=clang CXX=clang++
$ cmake -DLLVM_PATH=../ \
	-DCMAKE_INSTALL_PREFIX=$HOME/bin/llvm \
        -DLIBCXX_CXX_ABI=libcxxabi \
        -DLIBCXX_CXX_ABI_INCLUDE_PATHS=../projects/libcxxabi/include \
	../projects/libcxx
$ make install 











$ cmake -DCMAKE_BUILD_TYPE=Release -DCMAKE_INSTALL_PREFIX=$HOME/bin/llvm -DCMAKE_C_COMPILER=clang -DCMAKE_CXX_COMPILER=clang++ ..
$ make install

cmake -DCMAKE_BUILD_TYPE=Release -DCMAKE_INSTALL_PREFIX=$HOME/bin/llvm -DCMAKE_C_COMPILER=clang -DCMAKE_CXX_COMPILER=clang++ -DLIBCXX_CXX_ABI=libcxxabi -DLIBCXX_CXX_ABI_INCLUDE_PATHS=../../libcxxabi/include ..




$ ls
bin                    CPackConfig.cmake        lib              test
cmake                  CPackSourceConfig.cmake  LLVMBuild.cmake  tools
CMakeCache.txt         docs                     llvm.spec        unittests
CMakeFiles             DummyConfigureOutput     Makefile         utils
cmake_install.cmake    examples                 projects
compile_commands.json  include                  runtimes
$ ls bin/

$ cd where-you-want-llvm-to-live/
$ svn co http://llvm.org/svn/llvm-project/libcxx/trunk libcxx
$ cd libcxx/lib
$ ./buildit




sudo cp ./libc++.so.1.0 /usr/lib
cd /usr/lib
sudo ln -sf /usr/lib/libc++.so.1.0 libc++.so
sudo ln -sf /usr/lib/libc++.so.1.0 libc++.so.1


