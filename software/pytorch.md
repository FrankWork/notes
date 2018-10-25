# python

pip3 install http://download.pytorch.org/whl/cpu/torch-0.4.1-cp36-cp36m-linux_x86_64.whl

# c++

https://pytorch.org/cppdocs

https://pytorch.org/cppdocs/installing.html


```bash
wget https://download.pytorch.org/libtorch/nightly/cpu/libtorch-shared-with-deps-latest.zip
unzip libtorch-shared-with-deps-latest.zip

example-app/
  CMakeLists.txt # 源码在下面
  example-app.cc

mkdir build
cd build
cmake -DCMAKE_PREFIX_PATH=/full/path/to/libtorch .. 
make -j4

./example-app
```

CMakeLists.txt
```cmake
cmake_minimum_required(VERSION 3.0 FATAL_ERROR)
project(example-app)

find_package(Torch REQUIRED)

add_executable(example-app example-app.cc)
target_link_libraries(example-app "${TORCH_LIBRARIES}")
set_property(TARGET example-app PROPERTY CXX_STANDARD 11)
```

example-app.cc
```c++
#include <torch/torch.h>
#include <iostream>

int main() {
  at::Tensor tensor = torch::rand({2, 3});
  std::cout << tensor << std::endl;
}
```