# VGG(Visual Geometry Group)网络

[学习率](https://blog.csdn.net/u012526436/article/details/90486021):在梯度下降的过程中更新权重时的超参数

## 1、[VGG](https://zhuanlan.zhihu.com/p/41423739)原理

VGG16相比AlexNet的一个改进是**采用连续的几个3x3的卷积核代替AlexNet中的较大卷积核（11x11，7x7，5x5）**。对于给定的感受野（与输出有关的输入图片的局部大小），采用堆积的小卷积核是优于采用大的卷积核，因为多层非线性层可以增加网络深度来保证学习更复杂的模式，而且代价还比较小（参数更少）。

简单来说，在VGG中，使用了3个3x3卷积核来代替7x7卷积核，使用了2个3x3卷积核来代替5*5卷积核，这样做的主要目的是在保证具有相同感知野的条件下，提升了网络的深度，在一定程度上提升了神经网络的效果。

比如，3个步长为1的3x3卷积核的一层层叠加作用可看成一个大小为7的感受野（其实就表示3个3x3连续卷积相当于一个7x7卷积），其参数总量为 3x(9xC^2) ，如果直接使用7x7卷积核，其参数总量为 49xC^2 ，这里 C 指的是输入和输出的通道数。很明显，27xC^2小于49xC^2，即减少了参数；而且3x3卷积核有利于更好地保持图像性质。

**这里解释一下为什么使用2个3x3卷积核可以来代替5\*5卷积核：**

5x5卷积看做一个小的全连接网络在5x5区域滑动，我们可以先用一个3x3的卷积滤波器卷积，然后再用一个全连接层连接这个3x3卷积输出，这个全连接层我们也可以看做一个3x3卷积层。这样我们就可以用两个3x3卷积级联（叠加）起来代替一个 5x5卷积。

具体如下图所示：

![](https://pic2.zhimg.com/80/v2-d3bdfd338d8999d2ce1dde2082fa95e1_1440w.jpg)

2个3x3和5x5

至于为什么使用3个3x3卷积核可以来代替7*7卷积核，推导过程与上述类似，大家可以自行绘图理解。

如果你想看到更加形象化的VGG网络，可以使用[经典卷积神经网络（CNN）结构可视化工具](https://link.zhihu.com/?target=https%3A//mp.weixin.qq.com/s/gktWxh1p2rR2Jz-A7rs_UQ)来查看高清无码的[VGG网络](https://link.zhihu.com/?target=https%3A//dgschwend.github.io/netscope/%23/preset/vgg-16)。

## 2、VGG优缺点

**VGG优点**

VGGNet的结构非常简洁，整个网络都使用了同样大小的卷积核尺寸（3x3）和最大池化尺寸（2x2）。

- 几个小滤波器（3x3）卷积层的组合比一个大滤波器（5x5或7x7）卷积层好：
- 验证了通过不断加深网络结构可以提升性能。

- 验证了通过不断加深网络结构可以提升性能


**VGG缺点**

- VGG耗费更多计算资源，并且使用了更多的参数（这里不是3x3卷积的锅），导致更多的内存占用（140M）。其中绝大多数的参数都是来自于第一个全连接层。VGG可是有3个全连接层啊！

## 3、代码和测试

这里推荐两个开源库，训练请参考[tensorflow-vgg](https://link.zhihu.com/?target=https%3A//github.com/machrisaa/tensorflow-vgg)，快速测试请参考[VGG-in TensorFlow](https://link.zhihu.com/?target=https%3A//www.cs.toronto.edu/~frossard/post/vgg16/)。

代码我就不介绍了，其实跟上述内容一致，跟着原理看code应该会很快。我快速跑了一下，[VGG-in TensorFlow](https://link.zhihu.com/?target=https%3A//www.cs.toronto.edu/~frossard/post/vgg16/)，代码亲测可用，效果很nice，就是model下载比较烦。

贴心的Amusi已经为你准备好了[VGG-in TensorFlow]([VGG in TensorFlow](https://link.zhihu.com/?target=https%3A//www.cs.toronto.edu/~frossard/post/vgg16/))的测试代码、model和图像。需要的同学可以关注CVer微信公众号，后台回复：VGG。