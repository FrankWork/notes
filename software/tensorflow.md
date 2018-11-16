资料：
https://github.com/tensorflow/tensorflow/blob/master/tensorflow/g3doc/get_started/os_setup.md
https://www.tensorflow.org/

# install tensorflow 1.12 from src

## java && jdk

$ mkdir -p ~/local
$ tar zxvf jdk-8u191-linux-x64.tar.gz
$ vi ~/.bashrc
export JAVA_HOME="${HOME}/local/jdk1.8.0_191"
export PATH="$JAVA_HOME/bin:$PATH"
$ source ~/.bashrc && java -version

## bazel

$ wget https://github.com/bazelbuild/bazel/releases/download/0.19.1/bazel-0.19.1-dist.zip
$ unzip bazel-<VERSION>-dist.zip -d bazel-<Version> # 解压到文件夹中
$ cd bazel-<Version> &&  bash ./compile.sh # 需要JDK
$ export PATH="${HOME}/local/bazel-0.19.1/output:$PATH"

## cuda 9 + cudnn 7

$ sh cuda_9.0.176_384.81_linux.run # 只安装编译时需要的动态链接库，可以不安装驱动
$ cp cudnn7/include/cudnn.h cuda-9.0/include
$ cp cudnn7/lib64/* cuda-9.0/lib64/
$ chmod a+r cuda-9.0/lib64/libcudnn*
$ chmod a+r cuda-9.0/include/cudnn.h 

## fetch libs


$ wget https://github.com/tensorflow/tensorflow/archive/v1.12.0.tar.gz
$ tar zxvf v1.12.0.tar.gz
$ cd tensorflow-1.12.0/
$ ./configure

online 
$ mkdir /tmp/tf_deps
$ bazel --output_user_root=/tmp/tf_deps fetch --config=opt --config=cuda //tensorflow/tools/pip_package:build_pip_package


$ bazel build --config=opt --config=cuda //tensorflow/tools/pip_package:build_pip_package



# pip install 

$ **pip install -i https://pypi.tuna.tsinghua.edu.cn/simple tensorflow**
$ pip install tensorflow      # CPU support (no GPU support)
$ pip install tensorflow-gpu  # GPU support

$ pip install dm-sonnet
$ pip install dm-sonnet-gpu

## install cuda

- CUDA 9 and cuDNN 7 for tensorflow-1.5.0rc0
- CUDA® Toolkit 8.0. `LD_LIBRARY_PATH` environment variable
    /usr/local/cuda-8.0/lib64
    http://developer.download.nvidia.com/compute/cuda/repos/
- The NVIDIA drivers associated with CUDA Toolkit 8.0.
- cuDNN v6.0. `CUDA_HOME` environment variable
- libcupti-dev on ubuntu

```
import tensorflow as tf

# Creates a graph.
a = tf.constant([1.0, 2.0, 3.0, 4.0, 5.0, 6.0], shape=[2, 3], name='a')
b = tf.constant([1.0, 2.0, 3.0, 4.0, 5.0, 6.0], shape=[3, 2], name='b')
c = tf.matmul(a, b)
# Creates a session with log_device_placement set to True.
sess = tf.Session(config=tf.ConfigProto(log_device_placement=True))
# Runs the op.
print(sess.run(c))

```

## compile tensorflow

sudo apt-get install openjdk-8-jdk

wget https://github.com/bazelbuild/bazel/releases/download/0.12.0/bazel-0.12.0-dist.zip
mkdir bazel
cp bazel-<VERSION>-dist.zip bazel/
unzip bazel-<VERSION>-dist.zip -d bazel
bash ./compile.sh 
mv output/bazel ~/bin/bazel

git clone https://github.com/tensorflow/tensorflow
cd tensorflow  # cd to the top-level directory created
git branch -r
git checkout r1.10 

git fetch origin r1.8:r1.8
git checkout r1.8

bazel clean
./configure

bazel build --config=opt //tensorflow/tools/pip_package:build_pip_package # cpu
bazel build --config=opt --config=cuda //tensorflow/tools/pip_package:build_pip_package   # gpu

bazel-bin/tensorflow/tools/pip_package/build_pip_package /tmp/tensorflow_pkg
pip install /tmp/tensorflow_pkg/tensorflow-1.1.0rc1-cp35-cp35m-linux_x86_64.whl

cd ~ # to fix ImportError: No module named pywrap_tensorflow_internal

export CUDA_VISIBLE_DEVICES=3

```python
import tensorflow as tf
import tensorflow.contrib.eager as tfe
tfe.enable_eager_execution()
```

## compile tensorflow lib

git branch -r
git checkout r1.10 

bazel clean
./configure
bazel build --config=opt //tensorflow:libtensorflow_cc.so # cpu
ls bazel-bin/tensorflow/
    libtensorflow_cc.so     libtensorflow_framework.so

https://github.com/FrankWork/tf-tutorials/tree/master/cc_tensor


## compile sonnet
$ git clone --recursive https://github.com/deepmind/sonnet
$ cd sonnet/tensorflow
$ ./configure
$ cd $(bazel info output_base)
$ tar zcvf external.tar.gz external/
$ cd ../

tar zcvf sonnet.tar.gz sonnet

$ mkdir /tmp/sonnet
$ bazel build --config=opt :install
$ ./bazel-bin/install /tmp/sonnet

$ pip install /tmp/sonnet/*.whl

$ cd ~/
$ python
>>> import sonnet as snt
>>> import tensorflow as tf
>>> snt.resampler(tf.constant([0.]), tf.constant([0.]))



# test

$ python3
...
>>> import tensorflow as tf
>>> hello = tf.constant('Hello, TensorFlow!')
>>> sess = tf.Session()
>>> print(sess.run(hello))
Hello, TensorFlow!
>>> a = tf.constant(10)
>>> b = tf.constant(32)
>>> print(sess.run(a + b))
42
>>>









