## install

wget https://cmake.org/files/v3.11/cmake-3.11.4.tar.gz
tar zxvf cmake-3.11.4.tar.gz
cd cmake-3.11.4

./bootstrap --prefix=$HOME

gmake  
gmake install

## basic

main.cpp

```c++
#include<iostream>
 
int main()
{
    std::cout<<"Hello word!"<<std::endl;
    return 0;
}
```

CMakeLists.txt
```cmake
PROJECT(main)
CMAKE_MINIMUM_REQUIRED(VERSION 2.6)
AUX_SOURCE_DIRECTORY(. DIR_SRCS)
ADD_EXECUTABLE(main ${DIR_SRCS})
```

```bash
$ cmake .
$ make
```

## add lib

CMakeLists.txt
```cmake
PROJECT(main)
CMAKE_MINIMUM_REQUIRED(VERSION 2.6)

# set cxx flags
set(CMAKE_CXX_FLAGS "-Wall -O2 -std=c++11 -g")

# set include path
include_directories($ENV{HOME}/bin/yaml-cpp/include)

# set the path to the library folder
link_directories($ENV{HOME}/bin/yaml-cpp/lib)

AUX_SOURCE_DIRECTORY(. DIR_SRCS)
ADD_EXECUTABLE(main ${DIR_SRCS})

# link the libraries to the executable
target_link_libraries (main yaml-cpp)
```

## 编译安装json-cpp

```bash
wget https://github.com/open-source-parsers/jsoncpp/archive/1.8.4.tar.gz
tar zxvf 1.8.4.tar.gz
cd jsoncpp-1.8.4
mkdir -p build/release
cd build/release
cmake -DCMAKE_BUILD_TYPE=release \
	-DBUILD_STATIC_LIBS=OFF \
	-DBUILD_SHARED_LIBS=ON \
	-DCMAKE_INSTALL_PREFIX=${HOME}/local \
	-G "Unix Makefiles" \
	../..
make
make install
#
```
