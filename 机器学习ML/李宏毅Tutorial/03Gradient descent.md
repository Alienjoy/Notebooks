# 1. Adagrad

__自适应梯度下降法__:Adaptive Gradient descent

例如：$learning\ rate=\frac{\eta }{\sqrt{1+t}}$ 意思就是随着每一次iteration learning rate要下降，下面的式子是对于每一个参数w而言，即是对某一个w的梯度g之和。
$$
均方根rms=root\ mean\ square=\sqrt{\frac{x_{1}^2+s_{2}^2+s_{3}^2+.....+s_{n}^2}{n}}
$$

$$
w^{t+1}=w^{t}-\frac{\eta}{\sqrt{\sum_{i-0}^{t}}(g^i)^2}g^t
\\
g=gradient梯度
$$

原理：

就是在梯度比较大的部分（比较陡，分母部分大），需要设置步伐比较小步（权重更新慢一点），防止参数更新太大跳过最小值点

在梯度比较小的部分，比较平缓，则可以设置权重更新的快一点，加快Loss的变化，可以加快training的速度。

**想法**💡：

可以只计算离这个点比较近的梯度的平方，不需要计算全部的梯度的平方

<img src="https://i.loli.net/2021/03/15/oXZ2pmRJuE4vPd1.png" alt="image.png" style="zoom: 25%;" />



# 2. SGD

**SGD随机梯度下降法**Stochastic Gradient descent

原理：

就是用随机一个sample来计算Loss，而不是用全部的sample计算Loss=sum(y-Y)^2

<img src="https://i.loli.net/2021/03/16/adR1YsMFm5uzSTl.png" style="zoom:25%;" />

优点：

假设有20个sample，假如用gradient descent，要20个sample的Loss都计算完后才更新一次权重，而SGD则每一个sample都更新一次权重，则更新20次参数，更新的更快

<img src="https://i.loli.net/2021/03/16/ok2rR3sUnlp4ujZ.png" alt="image.png" style="zoom:25%;" />

# 3.feature scaling 、Standardization



[**方差**](https://zhuanlan.zhihu.com/p/83410946)（差的平方，variance）：
$$
D(x)=\sum [x-\overline{x}\ ]^2
$$


**标准差**（standard deviation）又叫**均方差**：
$$
\sigma =\sqrt{\frac{1}{n}\sum_{i=1}^{n} [x_i-\overline{x}\ ]^2}
$$
班级平均成绩是70分，标准差是9，则（61，79）分的人的概率为68%,(52,88)分人的概率为95%

![](https://pic4.zhimg.com/80/v2-5a369710775af7bfd07139ec5a7eb06b_1440w.jpg)

**均方误差**（mean squared error）
$$
mse=\sum_{i=1}^{n}\frac{(x_{i}-\overline{x}\ )^2}{n}
$$
**feature scaling，Standardization**就是把多个feature的分布归一化，缩放成一样的范围，方法
$$
x_i=\frac{x_i-\overline{x}}{\sigma_i}
$$
就是对`每一个sample` 用`第i个feature`减去`第i个feature`的平均值再除以`第i个feature的标准差`进行处理

对每个feature做完feature scaling后，平均值为0，均方误差为1

### Normalization Standardization

<img src="/Users/zhangshuheng/Desktop/Notebooks/机器学习ML/李宏毅Tutorial/03Gradient descent.assets/image-20220223205121234.png" alt="image-20220223205121234" style="zoom:50%;" />

# 4. 梯度下降法的原理

1. 在Loss平面随便找一个点L0，然后以这个点为圆心画圆，找出圆上Loss最小的点L1
2. 然后以L1为中心画圆，找出圆上Loss最小的点，循环一直找到minima

找圆上Loss最小点的方法：（假设圆点为$(\theta_1=a,\theta_2=b)$有两个权重w分别为$\theta_1,\theta_2$）

根据泰勒展开式：
$$
L(\theta)\approx L(a,b)+\frac{\partial L(a,b)}{\partial\theta_1}(\theta_1-a)+\frac{\partial L(a,b)}{\partial\theta_2}(\theta_2-b)
\\
u=\frac{\partial L(a,b)}{\partial\theta_1},\upsilon =\frac{\partial L(a,b)}{\partial\theta_2}
$$


<img src="https://i.loli.net/2021/03/15/xkLcNMgf9U1RDHt.png" alt="截屏2021-03-15 下午9.46.09.png" style="zoom:25%;" />

如果要$L(\theta)$最小的话，则$u\Delta \theta _1+\upsilon \Delta \theta _2$最小，$\overrightarrow{a}=（u,v）,\overrightarrow{b}=（\Delta \theta _1,\Delta \theta _2）$,则$u\Delta \theta _1+\upsilon \Delta \theta _2=\overrightarrow{a}\textbf{.}\overrightarrow{b}$最小，内积最小的话则a,b向量方向相反，b向量长度最长，即$\vec{a}=-\eta \vec{b}$

<img src="https://i.loli.net/2021/03/15/mKafgrRDtuhvWo7.png" alt="image.png" style="zoom:25%;" />

<img src="https://i.loli.net/2021/03/16/ciQps2oqkl7vRDj.png" alt="image.png" style="zoom:25%;" />

# 5. Optimization for Deep Learning

off-line就是所有sample样本的x向量和所有样本的y向量进行一次运算

on-line就是一次运算一个sample的x向量和一个sample的y向量

<img src="https://i.loli.net/2021/03/15/xtPinTlIeDbKzYL.png" alt="image.png" style="zoom:25%;" />

# 6.SGDM方法

**带有momentum动量的SGD随机梯度下降法**

原理：

就是在SGD的基础上，加上前几次iter迭代的累加和，目的是防止某一次的$\bigtriangledown L(\theta ^{0})$很小（接近0），则权重参数w便卡在某一处，不会进行更新了。

<img src="https://i.loli.net/2021/03/16/a7Ly51lcDzoZkXm.jpg" alt="截屏2021-03-16 上午9.20.57.jpeg" style="zoom: 25%;" />
$$
v^0=0
\\
v^1=-\eta \triangledown L(\theta ^0)
\\
v^2=-\eta (\  \triangledown  L(\theta ^1)+\lambda \triangledown  L(\theta ^0))
\\
v^3=-\eta (\  \triangledown  L(\theta ^2)+\lambda \triangledown  L(\theta ^1)+\lambda^2 \triangledown  L(\theta ^0))
$$

其中$\lambda$决定了惯性对下一次方向更新的权重，



图解：

在走到第三步的时候，原来的SGD方法会计算梯度为0，则权重参数w便不进行更新，会卡在局部最小点的位置，但是加了Momentum动量的话，它还会继续往前更新权重参数w，

补充：saddle point鞍点，就是倒数为0的点，但是又不是minimum

<img src="https://i.loli.net/2021/03/16/ADCFVmOcdKraEj8.png" alt="截屏2021-03-16 上午10.30.38.png" style="zoom:25%;" />

# 7. RMSProp

原理：

就是把Adagrad分母部分替换为下图所示，为了防止如果刚开始梯度比较大的话Adagrad方法会权重参数更新的过慢。因为Adagrad的分母是一直累加的，不会减少，而RMSProp会减少分母。他的分母是借鉴了SGDM方法的momentum动量

<img src="https://i.loli.net/2021/03/16/QbFMvxDWwKymTuj.png" alt="image.png" style="zoom:25%;" />



# 8. Adam

adaptive moment estimation

Adam=SGDM+RMSProp

<img src="https://i.loli.net/2021/03/16/R1pH8GoQh7r3Isg.png" alt="image.png" style="zoom:100%;" />

# 9. 应用

### computer version的算法：

- YOLO用SGDM训练出来的
- Mask R-CNN用SGDM训练出来的
- ResNet 也是用SGDM训练出来的

### ADAM训练出来的东西

- BERT用来做文意理解，做QA，生成文章的model
- Transformer 用来做翻译的model
- Tacotron用neural network做语音生成的model
- Big-GAN做生成影像的model
- MEMO演算法，这个model可以很容易学会新的task

### ADAM和SGDM

- Adam优点：
  - 快速的traning，因为Adam是在平缓的地方走大步，sharp的地方走小步，所以比较快
- 缺点：
  - 大的泛化差距，不稳定
- SGDM优点：
  - 稳定，小的泛化差距，better convergence熟练到小的值
- 缺点：
  - 慢

泛化差距generalization gap：就是指训练的参数和实际测试的参数有个offset，就是下图中的training和testing两个最低点的差距，对于比较平缓的loss function来说gap不是很大，但是对比较sharp的Loss function来说gap影响就比较大

<img src="https://i.loli.net/2021/03/16/F3TNzA85pHIJRBa.png" alt="截屏2021-03-16 下午2.45.48.png" style="zoom:25%;" />

# 10. 优化

## 10.1 结合法

前期用Adam，后面用SGDM，叫做SWATS   [keskar,et al.,arXiv'17]

## 10.2 优化Adam

[变的又稳又好 ](https://www.youtube.com/watch?v=4pUmZ8hXlHM)





