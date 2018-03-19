# back prop

Hadamard product(按位相乘)

$$ (s\odot t)_{j}=s_{j}t_{j} $$

前向传播

$$C=\frac{1}{2}||y-a^{L}||^{2}= \frac{1}{2}\sum_{j}(y_{j}-a_{j}^{L})^{2}$$
$$ a^{l}=\sigma(z^{l}) $$
$$z^{l}=w^{l}a^{l-1}+b^{l}$$

后向传播


$$\delta^{L}=\frac{\partial C}{\partial z^{L}}=\nabla_{a}C\odot\sigma'(z^{L})$$
$$\delta^{l}=\frac{\partial C}{\partial z^{l}}=((w^{l+1})^{T}\delta^{l+1})\odot\sigma'(z^{l})$$
$$\frac{\partial C}{\partial b_{j}^{l}}=\delta_{j}^{l} $$
$$\frac{\partial C}{\partial w_{jk}^{l}}=a_{k}^{l-1}\delta_{j}^{l} $$


# MLP

1. 前馈神经网络（包括全连接层、卷积层等）可以表示为 

$$F = f_{3} (f_{2} (f_{1} (xW_{1})W_{2})W_{3})$$

网络输出对$W_{1}$求偏导

$$ \frac{\partial F}{\partial W_{1}}= x*f'_{1}*W_{2}*f'_{2}*W_{3}*f'_{3} $$

这里$W_{1}W_{2}W_{3}$ 是相互独立的，一般不会有数值问题；主要问题在于激活函数的导数$f'$在饱和区接近于零，导致梯度消失。


# CNN

## 池化层

- max pooling: 梯度直接传给前一层最大的那个点，而其他点梯度为0
- mean pooling: 梯度等分为n份分配给前一层

已知池化层$\delta^{l}$，推导上一层$\delta^{l-1}$(卷积层)

$$\delta^{l-1}=upsample(\delta^{l})\odot\sigma'(z^{l-1}) $$

## [卷积层](http://www.cnblogs.com/pinard/p/6494810.html)

### 已知卷积层$\delta^{l}$，推导上一层$\delta^{l-1}$

1. 卷积前向传播

$$a^{l}=\sigma(z^{l})=\sigma(a^{l-1}*W^{l}+b^{l})$$

2. $\delta^{l-1}$和$\delta^{l}$递推关系

$$\delta^{l}=\frac{\partial C}{\partial z^{l}}=\frac{\partial C}{\partial z^{l+1}}\frac{\partial z^{l+1}}{\partial z^{l}}=\delta^{l+1}\frac{\partial z^{l+1}}{\partial z^{l}}$$

3. $z^{l-1}$和$z^{l}$前向关系

$$z^{l}=a^{l-1}*W^{l}+b^{l}=\sigma(z^{l-1})*W^{l}+b^{l}$$

4. 因此

$$\delta^{l-1}=\delta^{l}\frac{\partial z^{l}}{\partial z^{l-1}}=\delta^{l}*rot180(W^{l})\odot\sigma'(z^{l-1})$$

### 已知卷积层$\delta^{l}$，推导$W$和$b$的梯度

1. 卷积层$z$和$W,b$的前向关系

$$ z^{l}=a^{l-1}*W^{l}+b $$

2. 因此

$$\frac{\partial C}{\partial W^{l}}=\frac{\partial C}{\partial z^{l}}\frac{\partial z^{l}}{\partial W^{l}}=\delta^{l}*rot180(a^{l-1})$$

3. 将$\delta^{l}$(三维张量)的各个子矩阵的项分别求和，得到一个误差向量，即为$b$的梯度

$$\frac{\partial C}{\partial b^{l}}=\sum_{u,v}\delta_{u,v}^{l}  $$


# RNN

## 前向传播

$$h^{t}=\sigma(z^t)=\sigma(Ux^{t}+Wh^{t-1}+b)$$
$$o^{t}=Vh^{t}+c$$
$$\hat{y}^t=\sigma(o^t)$$
$$L=\sum_{t=1}L^t$$

## 反向传播

V,c的梯度计算比较简单

$$\frac{\partial L}{\partial c}=\sum_{t=1}\frac{\partial L^t}{\partial c}=\sum_{t=1}\frac{\partial L^t}{\partial o^t}\frac{\partial o^t}{\partial c}=\sum_{t=1}(\nabla L^t)\sigma'(o^t)$$
$$\frac{\partial L}{\partial V}=\sum_{t=1}\frac{\partial L^t}{\partial V}=\sum_{t=1}\frac{\partial L^t}{\partial o^t}\frac{\partial o^t}{\partial V}=\sum_{t=1}(\nabla L^t) (h^t)^T$$


U,W,b在t位置的梯度由t位置的输出和t+1位置的隐藏节点两部分决定

1. 定义隐藏节点的梯度为

$$\delta^t =\frac{\partial L}{\partial h^t}=\frac{\partial L}{\partial o^t}\frac{\partial o^t}{\partial h^t}+\frac{\partial L}{\partial h^{t+1}}\frac{\partial h^{t+1}}{\partial h^t}$$

$$\delta^T =\frac{\partial L}{\partial o^T}\frac{\partial o^T}{\partial h^T}$$

2. W,U,b的梯度计算表达式

$$\frac{\partial L}{\partial W}=\sum_{t=1}\frac{\partial L}{\partial h^t}\frac{\partial h^t}{\partial W} $$
$$\frac{\partial L}{\partial U}=\sum_{t=1}\frac{\partial L}{\partial h^t}\frac{\partial h^t}{\partial U} $$
$$\frac{\partial L}{\partial b}=\sum_{t=1}\frac{\partial L}{\partial h^t}\frac{\partial h^t}{\partial b} $$