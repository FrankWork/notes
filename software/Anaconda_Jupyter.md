# Install Anaconda

$ bash Anaconda3-4.2.0-Linux-x86_64.sh

# Install tensorflow on Anaconda

$ conda config --add channels conda-forge
$ conda install -c conda-forge tensorflow

=>

$ conda config --add channels conda-forge
$ conda install tensorflow

或
	$ export TF_BINARY_URL=https://storage.googleapis.com/tensorflow/linux/cpu/tensorflow-0.10.0-cp35-cp35m-linux_x86_64.whl
	$ sudo -H pip3 install --upgrade $TF_BINARY_URL
	
$ jupyter notebook
