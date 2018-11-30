## 编译安装 json-cpp

```bash
wget https://github.com/open-source-parsers/jsoncpp/archive/1.8.4.tar.gz -O jsoncpp-1.8.4.tar.gz
tar zxvf jsoncpp-1.8.4.tar.gz
cd jsoncpp-1.8.4 && mkdir -p build && cd build
cmake -DCMAKE_BUILD_TYPE=release \
	-DBUILD_SHARED_LIBS=ON \
	-DCMAKE_INSTALL_PREFIX=${HOME}/local \
	-G "Unix Makefiles" \
	..

make -j10
make install
#
#程序运行时的动态库加载路径
export LD_LIBRARY_PATH="$LD_LIBRARY_PATH:${HOME}/local/lib64"
```




## 编译安装 gflags

```bash
wget https://github.com/gflags/gflags/archive/v2.2.2.tar.gz -O gflags-2.2.2.tar.gz
tar zxvf gflags-2.2.2.tar.gz
cd gflags-2.2.2 && mkdir build && cd build
cmake -DBUILD_SHARED_LIBS=ON \
    -DCMAKE_INSTALL_PREFIX=${HOME}/local \
    ..  
            
make -j10
make install

export LD_LIBRARY_PATH="$LD_LIBRARY_PATH:${HOME}/local/lib"
```



## 编译安装 protobuf

```bash
sudo apt-get install autoconf automake libtool curl make g++ unzip

wget https://github.com/protocolbuffers/protobuf/releases/download/v3.5.1/protobuf-cpp-3.5.1.tar.gz
wget https://github.com/protocolbuffers/protobuf/releases/download/v3.6.1/protobuf-cpp-3.6.1.tar.gz
tar zxvf protobuf-cpp-3.6.1.tar.gz && cd protobuf-3.6.1/
./configure --prefix=${HOME}/local
make -j10
make install

export LD_LIBRARY_PATH="$LD_LIBRARY_PATH:${HOME}/local/lib"
#sudo ldconfig # refresh shared library cache.
export LIBRARY_PATH=${LIBRARY_PATH}:${HOME}/local/lib

export C_INCLUDE_PATH=${C_INCLUDE_PATH}:${HOME}/local/include
export CPLUS_INCLUDE_PATH=${CPLUS_INCLUDE_PATH}:${HOME}/local/include
```

c++ my_program.cc my_proto.pb.cc `pkg-config --cflags --libs protobuf`

or configure CXXFLAGS="$(pkg-config --cflags protobuf)" \
          LIBS="$(pkg-config --libs protobuf)"


## 编译安装 SentencePiece

```bash
git clone https://github.com/google/sentencepiece.git
cd sentencepiece
mkdir -p build && cd build
cmake .. -DCMAKE_INSTALL_PREFIX=${HOME}/local
make -j10
make install
#ldconfig -v
export PATH=${PATH}:${HOME}/local/bin
```


## OpenCC

```bash
wget https://github.com/BYVoid/OpenCC/archive/ver.1.0.5.tar.gz -O opencc-1.0.5.tar.gz
tar zxvf opencc-1.0.5.tar.gz
cd OpenCC-ver.1.0.5/
mkdir -p build/ && cd build 
cmake \
	-DENABLE_GTEST:BOOL=OFF \
	-DCMAKE_BUILD_TYPE=Release \
	-DCMAKE_INSTALL_PREFIX=${HOME}/local \
	..
make -j10
make install

```
opencc -i input.txt -o output.txt -c ~/local/share/opencc/t2s.json

