# 卷积公式

深度学习中的卷积在数学上叫做“互相关”

$$X*W(i,j)=\sum_{m}\sum_{n}X(i+m,j+n)W(m,n)$$

# 卷积复杂度

$$ Time \sim O(M^{2} \cdot K^{2} \cdot C_{in} \cdot C_{out}) $$
$$ Space \sim O(K^{2} \cdot C_{in} \cdot C_{out}) $$

- $M$:卷积核输出特征图(Feature Map)的边长
- $K$:每个卷积核 (kernel) 的边长
- $C_{in}$:每个卷积核的通道数，也即输入通道数，也即上一层的输出通道数。
- $C_{out}$:本卷积层具有的卷积核个数，也即输出通道数
- $$ M= \frac{(X-K+2*Padding)}{Stride}+1 $$

```Python
# Stride = 1, Padding = 0
def conv2d(img, kernel):
    height, width, in_channels = img.shape
    kernel_height, kernel_width, in_channels, out_channels = kernel.shape
    out_height = height - kernel_height + 1
    out_width = width - kernel_width + 1
    feature_maps = np.zeros(shape=(out_height, out_width, out_channels))
    for oc in range(out_channels):              # Iterate out_channels (# of kernels)
        for h in range(out_height):             # Iterate out_height
            for w in range(out_width):          # Iterate out_width
                for ic in range(in_channels):   # Iterate in_channels
                    patch = img[h: h + Two-dimensional correlation is equivalent to two-dimensional convolution with the filter matrix rotated 180 degrees.kernel_height, w: w + kernel_width, ic]
                    feature_maps[h, w, oc] += np.sum(patch * kernel[:, :, ic, oc])

    return feature_maps
```

# QA

## CNN为什么可以在CV/NLP/Speech等领域都可以使用？

1. 卷积是因为输入数据的局部相关性；
2. 权值共享是因为输入数据的局部特征具有平移不变性，即在不同位置具有共性的局部特征。
   低层局部特征可以组合成高层全局特征。
3. 权值共享能够降低参数量，而且降低了网络的训练难度。
   
   note: 如果权值不共享，那就是局部连接层了。在某些应用，如人脸在不同的区域存在不同的特征（眼睛／鼻子／嘴的分布位置相对固定），当不存在全局的局部特征分布时，局部连接层更适合特征的提取。
   
4. CNN抓住此共性的手段主要有四个：局部连接／权值共享／池化操作／多层次结构。
5. 局部连接使网络可以提取数据的局部特征；权值共享大大降低了网络的训练难度
   池化操作与多层次结构一起，实现了数据的降维，将低层次的局部特征组合成为较高层次的特征

## 池化层

1. 提高平移伸缩不变性
2. 降低维度，减少参数，防止过拟合
3. 减少无关信息