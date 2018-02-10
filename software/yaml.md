# install

```bash
$ git clone https://github.com/jbeder/yaml-cpp.git
$ cd yaml-cpp
$ mkdir build
$ cd build
$ cmake -DBUILD_SHARED_LIBS=1 -DCMAKE_INSTALL_PREFIX=$HOME/bin/yaml-cpp  ..
$ make all install
```

# compile

Try setting `C_INCLUDE_PATH` (for C header files) or `CPLUS_INCLUDE_PATH` (for C++ header files).

```bash
$ export YAML_CPP_HOME=$HOME/bin/yaml-cpp
$ export CPLUS_INCLUDE_PATH=$CPLUS_INCLUDE_PATH:$YAML_CPP_HOME/include
$ export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:$YAML_CPP_HOME/lib
```

```c++
#include <iostream>
#include "yaml-cpp/yaml.h"

int main()
{
   YAML::Emitter out;
   out << "Hello, World!";
   
   std::cout << "Here's the output YAML:\n" << out.c_str(); // prints "Hello, World!"
   return 0;
}
```

```c++
$ g++ -std=c++11 example.cpp -lyaml-cpp -o example -L$YAML_CPP_HOME/lib
$ ./example
```

# cmake



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

