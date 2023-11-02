# 1.CNN

CNN=Convolution Neural Network 卷积神经网络

应用场景：图像识别

对于一个图像识别，它的第一层做的就是一个基本的分类器，例如分出绿色和蓝色的区别，第二层分出更复杂的元素，然后依此往下进行。

<img src="https://i.loli.net/2021/03/24/O7iyavNSjdXkn1R.png" alt="ML Lecture 10_ Convolutional Neural Network 00-02-06 .png" style="zoom:50%;" />

问题：假如第一层有1000个neural，图像是100*100的彩色 的则输入feature有100\*100\*3个，则第一层有1000\*30000个parameter了，参数太多了。

解决方法：CNN。

实现：利用先验知识prior knowledge把fully connected层的参数拿掉，简化model

这样操作可以实现的可能性分析：举例分析实现一个在图片中detector（检测器）鸟嘴的model

三个Property（特性）：

- 这个model不需要对图片的全部进行侦测，只需要对有鸟嘴的那部分进行detector就可以
- 鸟嘴在图片中出现的位置不一致。但是我们不需要进行设置两个detector，可以共用一个detector就可以了
- 可以对一张图片进行subsampling二次抽样，就是压缩图片，但是并不会对我们理解图片的内容产生影响，可以把奇数行偶数列的像素拿掉。

CNN架构：

- 首先进行convolution卷积，然后进行Max pooling最大池化，可以循环进行多次这两种操作，次数是自己设定
- 然后进行flatten展平，
- 然后送入一个全链接层的分类器（fully connected 前馈网络），全连接的分类器的作用是看整张图

<img src="https://i.loli.net/2021/03/24/jywoEi3ar8IH6Ke.png" alt="ML Lecture 10_ Convolutional Neural Network 00-08-54 .png" style="zoom:50%;" />



Convolution可以解决Property的一二个问题，Max pooling可以解决Subsampling的问题

# 2.Convolution

<img src="https://i.loli.net/2021/03/24/mIGbTQ56OWKvHEn.png" alt="ML Lecture 10_ Convolutional Neural Network 00-13-48 .png" style="zoom:50%;" />



卷积其实就是设置一个filter （过滤器，卷积核，特征提取器）对图片进行内积，（其实就是对应位置的元素相乘然后相加）其实一个filter就等价于一个neural的效果，然后根据stride步幅的大小依次从图片的左上角检测到右下角，相当于上面的Property 1中说的检测有没有鸟嘴图案（pattern）的出现，对不同位置都于filter卷积，相当于上面的Property 2中说的鸟嘴出现图片的不同位置共用一个detector

说明：filter就是一个特征提取器，其中元素为1的部分相当于想要检测到的部分，等于-1的部分相当于不想要检测到（想要减少对输出的结果的影响就写成负的）的部分，根据卷积后的结果我们可以看到左上角和左下角的卷积结果都为3，表示图片中相应位置有我们需要检测的图案。



> 一个卷积核就是一个特征提取器，多个卷积核就是多个特征提取器。对于以上的例子来说多个特征提取器可以提取鸟的嘴，鸟的羽毛，鸟的脚，颜色等等，然后再进行进行特征的进一步提取，例如红色的鸟羽毛，黑色的鸟嘴。这样就能进行分类了
>
> 例如一个图像大小是5*5。
>
> 有一个3\*3的卷积核对着图像进行卷积，卷积结束后生成一个3*3的矩阵。
>
> 如果有2个卷积核对着图像卷积，就会生成两个3*3的矩阵。
>
> 同理有多少个卷积核对图像卷积就有多少个矩阵。
>
> 这个叫做通道。
>
> 4个3\*3的卷积核对5*5的图像卷积就会生成4\*3\*3，即4个3\*3的矩阵。
>
> 有4个通道。
>
> 4个通道互相独立，代表着不同卷积核提取的不同特征，没必要把他们加起来变成一个矩阵。



# 3.Max pooling

Max pooling的意思就是经过convolution后得到的结果，在一个池中选最大的那个

<img src="https://i.loli.net/2021/03/24/RcGi5hCJxou6WTB.png" alt="ML Lecture 10_ Convolutional Neural Network 00-24-15 .png" style="zoom:50%;" />

假如第一个convolution有25个filter，则会产生25个feature map，就是25个通道，然后第二个convolution有15个filter，则这15个filter会对25维的feature map同时考虑，这15个filter也是三维的，则会产生15个三维的feature map，每一个feature map的高度是25。

<img src="https://i.loli.net/2021/03/24/QbrsLeihHpIlDgv.png" alt="" style="zoom:50%;" />

# 4.使用keras来实做

步骤：

- 添加卷积层
- 添加池化层
- 重复以上两个步骤n次
- 添加flatten
- 添加一个全连接层

<img src="https://i.loli.net/2021/03/24/JqN867PRgijYGTI.png" alt="ML Lecture 10_ Convolutional Neural Network 00-08-24 .png" style="zoom:50%;" />



```python
#keras实做
from keras.models import Sequential
model = Sequential()

#添加convolution
model.add(Convolution2D(25,3,3,input_shape(1,28,28)))
#有25个filter，每个filter的尺寸是3x3，输入数据为1代表黑白，假如写3代表RGB，shape为28x28pixel
#对于每个filter有3x3=9个参数
#添加max pooling
model.add(MaxPooling2D((2,2)))#添加一个2x2的Max Pooling的池化层

#添加convolution
model.add(Convolution2D(50,3,3))
#有50个filter，每个filter的尺寸是3x3，输入就是上一个池化层的输出。
#对于每个filter有3x3x25=255个parameter，因为这一层的filter是三维的，长宽为3x3，高为上一层的输出的个数
#添加max pooling
model.add(MaxPooling2D((2,2)))#添加一个2x2的Max Pooling的池化层

#添加flatten展平
model.add(Flatten())

#添加全连接层
from keras.layers import Dense#Dense就是全连接层的意思

model.add(Dense(units=64, activation='relu'))#不需要添加输入的维数，keras会自动将上层的输出当这层的输入
model.add(Dense(units=10, activation='softmax'))
```

<img src="https://i.loli.net/2021/03/24/U1ia5CNqjKtYEDP.png" alt="ML Lecture 10_ Convolutional Neural Network 00-30-03 .png" style="zoom:50%;" />

<img src="https://i.loli.net/2021/03/24/ZKM6v1gurdU4aW5.png" alt="ML Lecture 10_ Convolutional Neural Network 00-32-42 .png" style="zoom:50%;" />

<img src="/Users/zhangshuheng/Desktop/Notebooks/机器学习ML/李宏毅Tutorial/10CNN.assets/image-20211020214125869.png" alt="image-20211020214125869" style="zoom:50%;" />

<img src="https://i.loli.net/2021/03/24/Wl6UBtQ7pyemcAh.png" alt="ML Lecture 10_ Convolutional Neural Network 00-33-18 .png" style="zoom:50%;" />



# 5.Deep style

把一张图片改成另外一张图片风格的形式

<img src="https://i.loli.net/2021/03/25/5nPfhLpwHKeoZiI.png" alt="ML Lecture 10_ Convolutional Neural Network 00-59-07 .png" style="zoom:50%;" />

# 计算CNN的参数个数

[计算卷积层中对应参数个数](https://zhuanlan.zhihu.com/p/35333316)

