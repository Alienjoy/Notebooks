# 1.overfitting

在training set上得到好的结果，但是在testing set上得不到好的结果就是overfitting

在testing set上假如56层的隐含层的结果比30层的结果要差，则不一定是overfitting，因为在training set上56层的结果就是比30层的差，如果是overfitting的话，training set上56层的要比30层的差才对。

# 2.问题的解决

不同的方法解不同的问题，主要分为两个问题，一是training data上的performance不好，一个是testing data上的performance不好。

### 

### 应用的情况1：training data的performance不好的时候。

- new activation function，换新的激活函数
- Adaptive Learning Rate

### 应用的情况2：testing data的performance不好的时候。

- Early Stopping
- dropout方法
- Regularization



### 应用的情况1：new activation function

### 情况：随着隐含层的增加，performance却下降。这个问题叫做vanishing gradient 的问题

sigmoid激励函数的缺点，就是当层数比较多的时候，前面层w巨大的变化，对后面输出几乎不产生影响。

解决方法，激活函数换为ReLU

下面是ReLU的变种：



<img src="https://i.loli.net/2021/03/22/axNruvMhz64JdlD.png" alt="ML Lecture 9-1_ Tips for Training DNN 00-24-44 .png" style="zoom: 50%;" />

下面方法叫做Maxout：它会在多个输出之间选择大的那个，这样可以自动调整激活函数的形状。

<img src="https://i.loli.net/2021/03/22/ZB4YlesxgzpwGy3.png" alt="ML Lecture 9-1_ Tips for Training DNN 00-27-43 .png" style="zoom:50%;" />





### Adaptive Learning Rate

下面是Adagrad方法的进化版，可以由a的值来调节现在和过去梯度所占的权重。

<img src="https://i.loli.net/2021/03/22/noCfHJ9DtbmGih3.png" alt="ML Lecture 9-1_ Tips for Training DNN 00-41-13 .png" style="zoom:50%;" />

<img src="https://i.loli.net/2021/03/22/dRw3J7VrUHPpyxB.png" alt="ML Lecture 9-1_ Tips for Training DNN 00-54-47 .png" style="zoom:50%;" />

-------



### 应用的情况2：Early stopping

<img src="https://i.loli.net/2021/03/23/qeIO83lxSvNfz52.png" alt="截屏2021-03-23 上午11.03.21.png" style="zoom:50%;" />

early stopping的意思就是在total loss 最小的时候就停止训练

[early stopping的keras使用方法](https://keras.io/getting_started/faq/#how-can-i-interrupt-training-when-the-validation-loss-isnt-decreasing-anymore)

### regulation正则化

作用：为了消除过拟合，让曲线更加的平滑一点，相当于减少了model的层数复杂程度。

实现方法：找一个新的loss function去minimize，在原来的loss function上加上一个二分之一$\lambda$乘w的二范数，实现过程中就是让w每次都小一点小一点，weight乘上一个小于1的数，会一次一次的变小。

<img src="https://i.loli.net/2021/03/23/4MbdnChQxAtwkZ8.png" alt="ML Lecture 9-1_ Tips for Training DNN 01-02-42 .png" style="zoom:50%;" />



### Dropout丢弃法

每一个neural有p%的概率被丢掉，然后这个model的structure也会产生变化。dropout就是不用所有的参数进行训练，使model变得更加强壮。

在training的时候做dropout，在testing的时候不做dropout，即所有的neural都要用。

如果在training的时候dropout的概率为p%，则在testing的时候要在weight上乘(1-p)%







