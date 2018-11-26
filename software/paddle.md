python 2.7, python 3.5

```bash
pip2 install paddlepaddle # linux cpu
```



conda create -n paddle paddlepaddle
source activate paddle
pip install paddlepaddle

source deactivate 

## paddle C++ 预测库

编译需要外网，还特别慢

```bash
git clone https://github.com/PaddlePaddle/Paddle.git
cd Paddle
mkdir -p build && cd build
cmake -DFLUID_INFERENCE_INSTALL_DIR=${HOME}/local \
      -DCMAKE_BUILD_TYPE=Release \
      -DWITH_FLUID_ONLY=ON \
      -DWITH_SWIG_PY=OFF \
      -DWITH_PYTHON=OFF \
      -DWITH_MKL=OFF \
      -DWITH_GPU=OFF  \
      -DON_INFER=ON \
      ..

make -j16
make inference_lib_dist


PaddleRoot/
├── CMakeCache.txt
├── paddle
│   ├── include
│   │   └── paddle_inference_api.h
│   └── lib
│       ├── libpaddle_fluid.a
│       └── libpaddle_fluid.so
├── third_party
│   ├── boost
│   │   └── boost
│   ├── eigen3
│   │   ├── Eigen
│   │   └── unsupported
│   └── install
│       ├── gflags
│       ├── glog
│       ├── mklml
│       ├── protobuf
│       ├── snappy
│       ├── snappystream
│       └── zlib
└── version.txt
```



## lac分词

```bash
git clone https://github.com/baidu/lac.git
cd lac
mkdir build
cd build
# /path/to/fluid_inference_lib是上节第五步的对应的Fluid预测库编译产出路径
# LAC的demo程序，以及依赖LAC静态库的程序，都要依赖这个路径作为动态库的搜索路径
# 如果这个路径在编译完成之后有变动，需要手工设置LD_LIBRARY_PATH环境变量
cmake -DPADDLE_ROOT=/path/to/fluid_inference_lib ..
make
make install # 编译产出在 ../output 下
```

