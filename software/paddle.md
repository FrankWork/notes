# Linux CPU
pip install paddlepaddle
# Linux GPU cuda9cudnn7
pip install paddlepaddle-gpu
# Linux GPU cuda8cudnn7
pip install paddlepaddle-gpu==0.14.0.post87
# Linux GPU cuda8cudnn5
pip install paddlepaddle-gpu==0.14.0.post85

# For installation on other platform, refer to http://paddlepaddle.org/



conda create -n paddle paddlepaddle
source activate paddle
pip install paddlepaddle

source deactivate 
