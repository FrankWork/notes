All our prebuilt binaries have been built with CUDA 8 and cuDNN 6.
We anticipate releasing TensorFlow 1.5 with CUDA 9 and cuDNN 7.

# cuda 8.0 cudnn 6.0

```bash
export CUDA_HOME="$HOME/cuda-8.0"
export PATH="$CUDA_HOME/bin:$PATH"
export LD_LIBRARY_PATH="$CUDA_HOME/lib64:$LD_LIBRARY_PATH"

cd $CUDA_HOME/nvvm/libdevice
ln -s libdevice.compute_50.10.bc libdevice.10.bc

cp cuda/include/cudnn.h  $CUDA_HOME/include/

chmod a+r $CUDA_HOME/include/cudnn.h
chmod a+r $CUDA_HOME/lib64/libcudnn*
```


# cuda 9.0 cudnn 7.0

