# basic

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

# add lib

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