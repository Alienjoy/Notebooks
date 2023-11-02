# 1.逻辑回归 (Logistic regression)

### step 1：function set

我们要找出的判定x属于class 1的概率函数就是这样：

我们假设的函数就是给定一个data x，它属于class 1（也就是out=1）的概率
$$
P(C_1|x)=\sigma(z)=\frac{1}{1+e^{-z}}
\\
z=\vec{w}.\vec{x}+b=\sum_{i}^{}w_ix_i+b
$$
概率函数图解：

<img src="https://i.loli.net/2021/03/17/7DWbJS3OzmuEFi8.png" alt="ML Lecture 5_ Logistic Regression 00-03-00 .png" style="zoom:50%;" />

**目标**：找出w和b

**对比**

与linear regression相对比就是在函数输出上串了一个sigmoid函数。使可以是任何值的输出，压缩到了(0.1)上

<img src="https://i.loli.net/2021/03/17/yXqwCU87vVOfxMm.png" alt="ML Lecture 5_ Logistic Regression 00-03-41 .png" style="zoom:50%;" />

### step 2：Goodness of a Function

目标：最大化likelyhood，likelyhood为下图所示，找出能最大化likelyhood的w和b

<img src="https://i.loli.net/2021/03/17/H3rYmeRK6swEuWJ.png" alt="ML Lecture 5_ Logistic Regression 00-05-27 .png" style="zoom:50%;" />

则训练集的Likelyhood=x_1属于c1的几率乘以x_2属于c1的几率乘以x_3属于c2的几率等等，其中x_3属于c2的几率为（1-x_3属于c1的几率，因为是二元分类）

进行一个变换：就是找出一个w,b使-lnL(w,b)

<img src="https://i.loli.net/2021/03/17/TH56shYufg2antk.png" alt="ML Lecture 5_ Logistic Regression 00-09-08 .png" style="zoom:50%;" />

<img src="https://i.loli.net/2021/03/17/8YkvtBSGc9UpVwl.png" alt="截屏2021-03-17 下午5.17.43.png" style="zoom: 25%;" />

说明：$arg\ \underset{x}{max}\ f(x)$: 当f(x)取最大值时，x的取值

Cross entropy 交叉熵，就是相当于两个向量进行内积，只不过对一个向量进行了ln处理，代表的含义是这两个向量有多接近，因为同方向的两个向量内积最大

**对比**  ：logistic regression是最小化预测向量，与实际向量的交叉熵最小，即把n个sample的预测值，与实际值$\hat{y}$同方向。

<img src="https://i.loli.net/2021/03/17/Ztlec4Ny1WUIXQh.png" alt="ML Lecture 5_ Logistic Regression 00-13-58 .png" style="zoom:50%;" />

### step3:find the best function

就是找一个最小的w和b，minimum这个likelyhood。

方法：用梯度下降法，gradient descent，就是对likelyhood进行wi微分，更新谁的参数就对谁微分。

对likelyhood微分推导过程：

<img src="https://i.loli.net/2021/03/17/GaVBulsJ8Ngdk6x.png" alt="ML Lecture 5_ Logistic Regression 00-18-16 .png" style="zoom: 50%;" />

<img src="https://i.loli.net/2021/03/17/zmGjYyOXL8ZJRq9.png" alt="ML Lecture 5_ Logistic Regression 00-20-25 .png" style="zoom:50%;" />

对比：

<img src="https://i.loli.net/2021/03/17/IJfvK2t4TcN1kCV.png" alt="ML Lecture 5_ Logistic Regression 00-22-22 .png" style="zoom:50%;" />

# 2.为什么逻辑回归loss不能用square error

因为对square error求导后可以得到，如果w距离目标点很远和很近的时候，gradient都是接近0，就会导致如果w落在了离目标很远的点的时候更新很慢

推导过程：

<img src="https://i.loli.net/2021/03/17/EWRLOZoudN8eBJb.png" alt="ML Lecture 5_ Logistic Regression 00-27-16 .png" style="zoom:50%;" />



用最小化likelyhood（是Cross entropy 交叉熵）VS 最小化Loss（用square error）

<img src="https://i.loli.net/2021/03/17/zYCiHEqWwXkgucZ.png" alt="ML Lecture 5_ Logistic Regression 00-30-21 .png" style="zoom:50%;" />



# 3.discriminative model（有识别力的）和generative modle

用logistic计算出来的w和b是discriminative，用高斯函数计算出来的(前一个markdown的方法)叫generative

<img src="https://i.loli.net/2021/03/17/ULXWzMSwbs3INQD.png" alt="ML Lecture 5_ Logistic Regression 00-35-00 .png" style="zoom:50%;" />

相同的model，但是用相同的traning tata却得到两个不同的function参数。

在data量少的时候，generative model其实有可能比得过discriminative，generative model受data量影响不大

例如语音辨识的时候要首先利用generative来设定每句话出现的概率，然后再用discriminative

# 4.多分类系统

softmax的意思就是它会强化输入的差距，多分类系统不接sigmoid接softmax

softmax：先对每个输入做Exponential（取e为底的指数），然后再求加权平均和，

<img src="https://i.loli.net/2021/03/17/GDtqQkbVTP7zpO8.png" alt="" style="zoom:50%;" />



<img src="https://i.loli.net/2021/03/17/fT6MjFY4KSNDWXo.png" alt="ML Lecture 5_ Logistic Regression 00-55-19 .png" style="zoom:50%;" />

# 5.Logistic Regression的限制

单层的logistic regression，两个class 之间的boundary是一条直线，不能区分下列的输入的四个data

<img src="https://i.loli.net/2021/03/17/PR4nYrv3K6DIaGq.png" alt="image.png" style="zoom:50%;" />

办法：就是对feature进行一个转换，feature transformation

出现问题：怎么找到一个合适的transformation呢，就在classfication之前再加一个logistic regression做feature transformation

下图中classfication应该也是两个logistic regression，logistic regression又叫neuron 神经元

<img src="https://i.loli.net/2021/03/17/1Q3walSp5DPvyLW.png" alt="image.png" style="zoom:50%;" />

<img src="https://i.loli.net/2021/03/17/eb58oxHqcT1FGAW.png" alt="image.png" style="zoom:50%;" />











