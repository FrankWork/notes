资料：
https://github.com/tensorflow/tensorflow/blob/master/tensorflow/g3doc/get_started/os_setup.md
https://www.tensorflow.org/



# install


$ pip install tensorflow      # CPU support (no GPU support)
$ pip install tensorflow-gpu  # GPU support

$ pip install dm-sonnet
$ pip install dm-sonnet-gpu

## compile

sudo apt-get install openjdk-8-jdk
wget bazel-<VERSION>-dist.zip from https://github.com/bazelbuild/bazel/releases
unzip bazel-<VERSION>-dist.zip
bash ./compile.sh
mv output/bazel ~/bin/bazel

git clone https://github.com/tensorflow/tensorflow
cd tensorflow  # cd to the top-level directory created
./configure

bazel build --config=opt //tensorflow/tools/pip_package:build_pip_package # cpu
bazel build --config=opt --config=cuda //tensorflow/tools/pip_package:build_pip_package   # gpu

bazel-bin/tensorflow/tools/pip_package/build_pip_package /tmp/tensorflow_pkg
pip install /tmp/tensorflow_pkg/tensorflow-1.1.0rc1-cp35-cp35m-linux_x86_64.whl

cd ~ # to fix ImportError: No module named pywrap_tensorflow_internal
python
>>> import tensorflow as tf

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

## pip install
$ export TF_BINARY_URL=https://storage.googleapis.com/tensorflow/linux/cpu/tensorflow-0.10.0-cp35-cp35m-linux_x86_64.whl
$ sudo -H pip3 install --upgrade $TF_BINARY_URL

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

# Run a TensorFlow demo model
NOTE: it takes times!

$ python3 -c 'import os; import inspect; import tensorflow; print(os.path.dirname(inspect.getfile(tensorflow)))'
/usr/local/lib/python3.5/dist-packages/tensorflow

$ python3 -m tensorflow.models.image.mnist.convolutional
or 
$ python3 /usr/local/lib/python3.5/dist-packages/tensorflow/models/image/mnist/convolutional.py
Successfully downloaded train-images-idx3-ubyte.gz 9912422 bytes.
Successfully downloaded train-labels-idx1-ubyte.gz 28881 bytes.
Successfully downloaded t10k-images-idx3-ubyte.gz 1648877 bytes.
Successfully downloaded t10k-labels-idx1-ubyte.gz 4542 bytes.
Extracting data/train-images-idx3-ubyte.gz
Extracting data/train-labels-idx1-ubyte.gz
Extracting data/t10k-images-idx3-ubyte.gz
Extracting data/t10k-labels-idx1-ubyte.gz
Initialized!
Step 0 (epoch 0.00), 5.6 ms
Minibatch loss: 12.054, learning rate: 0.010000
Minibatch error: 90.6%
Validation error: 84.6%
Step 100 (epoch 0.12), 312.0 ms
Minibatch loss: 3.287, learning rate: 0.010000
Minibatch error: 6.2%
Validation error: 7.0%
Step 200 (epoch 0.23), 307.8 ms
Minibatch loss: 3.491, learning rate: 0.010000
Minibatch error: 12.5%
Validation error: 3.6%
Step 300 (epoch 0.35), 314.2 ms
Minibatch loss: 3.265, learning rate: 0.010000
Minibatch error: 10.9%
Validation error: 3.2%
Step 400 (epoch 0.47), 308.3 ms
Minibatch loss: 3.221, learning rate: 0.010000
Minibatch error: 7.8%
Validation error: 2.7%
Step 500 (epoch 0.58), 309.2 ms
Minibatch loss: 3.292, learning rate: 0.010000
Minibatch error: 7.8%
Validation error: 2.7%
.....
.....
Step 8400 (epoch 9.77), 337.1 ms
Minibatch loss: 1.596, learning rate: 0.006302
Minibatch error: 0.0%
Validation error: 0.7%
Step 8500 (epoch 9.89), 334.9 ms
Minibatch loss: 1.604, learning rate: 0.006302
Minibatch error: 0.0%
Validation error: 0.9%
Test error: 0.7%










