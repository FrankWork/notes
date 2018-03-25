
# svm

## 基本型
- 法向量：垂直与平面的直线所在的向量
- 特征向量：缩放后方向不变，缩放比例叫特征值

分类面目标，$\mathbf{w}$为超平面法向量

$$
\begin{cases}
w^Tx_i+b\ge+1 \qquad y_i=+1 \\
w^Tx_i+b\le-1 \qquad y_i=-1 \\

\end{cases}
$$

点到超平面距离

$$r=\frac{|w^Tx+b|}{||w||}$$

间隔：异类支持向量到超平面的距离之和

$$\gamma=\frac{2}{||w||}$$

目标函数

$$min\frac{1}{2}||w||^2$$

## SVM　拉格朗日乘子法

SVM使用拉格朗日乘子法更为高效地求解了优化问题。

SVM将寻找具有最大几何间隔划分超平面的任务转化成一个凸优化问题,我们当然可以直接使用现成工具求解，但还有更为高效的方法，那就是使用拉格朗日乘子法将原问题转化为对偶问题求解。

1. 将约束融入目标函数中，得到拉格朗日函数；
2. 然后对模型参数w和b求偏导，并令之为零；
3. 得到w后，将其带入拉格朗日函数中，消去模型参数w和b；
4. 这样就得到了原问题的对偶问题，对偶问题和原问题等价，同时对偶问题也是一个凸优化问题，使用SMO算法求解拉格朗日乘子；
5. 得到拉格朗日乘子后，进一步可以得到模型参数w和b，也就得到了我们想要的划分超平面。

## smo算法

固定$a_i$之外的所有参数，求$a_i$上的极值
- 选取需更新的$a_i$和$a_j$
- 

## SVM在哪个地方引入的核函数,

如果原始空间线性不可分，可以将原始空间映射到高维空间，映射函数为f，在高维空间求解svm要算高维空间的內积，计算量比较大。若高维空间的內积可以表示为原始空间的通过某个函数计算出来的结果，这个函数叫做核函数。

线性核，多项式核，高斯核，sigmoid核，拉普拉斯核

## 如果用高斯核可以升到多少维。

高斯核 $exp(-||x-y||^2)$的泰勒展开是无穷的，可以映射到无穷维

## 软间隔
允许在一些样本上出错,但不满足约束的点应该尽量少

## SVM怎么防止过拟合

过拟合的办法是为SVM引入了松弛变量, 能够容忍异常点的存在

## 支持向量

距离超平面最近的几个训练样本点,两个异类支持向量到超平面的距离为间隔