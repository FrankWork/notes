# Install Anaconda

```
$ wget https://repo.continuum.io/archive/Anaconda3-5.0.0.1-Linux-x86_64.sh
$ bash Anaconda3-5.0.0.1-Linux-x86_64.sh
$ conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/free/
$ conda config --set show_channel_urls yes
```

## update

$ conda --version
$ conda update conda

## channels

$ conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/free/
$ conda config --set show_channel_urls yes
$ conda config --show

## envs

$ conda create --name bunnies python=3.5 astroid babel #  creates a new environment in /envs named “bunnies”, with Python, Astroid and Babel installed.
$ conda info --envs

$ source activate bunnies # Switch to another environment
$ source deactivate # Change your path from the current environment back to the root

$ conda remove -n ENV_NAME --all

## install packages

conda search tensorflow-gpu
conda install package=version

# PyTorch

$ conda create -n pytorch
$ source activate pytorch

$ pip install http://download.pytorch.org/whl/cu75/torch-0.2.0.post3-cp36-cp36m-manylinux1_x86_64.whl
$ pip install torchvision


# Tensorflow

$ conda create -n tensorflow
$ source activate tensorflow

(tensorflow)$ pip install --ignore-installed --upgrade tensorflow # CPU support
(tensorflow)$ pip install --ignore-installed --upgrade tensorflow-gpu # GPU support


