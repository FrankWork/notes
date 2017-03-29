# install

$ sudo -H pip3 install numpy

On Ubuntu >= 13.10, one can install the dependencies by

$ sudo apt-get update
$ sudo apt-get install -y build-essential git libatlas-base-dev libopencv-dev (这个要下载好多东西)

Then build mxnet

$ git clone --recursive https://github.com/dmlc/mxnet
$ cd mxnet; make -j$(nproc)


Install system-widely, which requires root permission
$ cd python; sudo python3 setup.py install
$ export PYTHONPATH=~/git/mxnet/python




time:

real	4m23.864s
user	16m13.776s
sys	0m24.164s


