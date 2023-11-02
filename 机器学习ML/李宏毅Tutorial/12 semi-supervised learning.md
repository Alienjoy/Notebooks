# 1.semi-supervised learning半监督学习

监督学习是有数据特征和标签。监督学习是少部分同时有特征和标签，大部分只有特征但是没有标签的。半监督学习也分为**transductive learning**和**inductive learning**，前者是训练时利用**testing data**的 **feature**也就是说**unlabeled data**是**testing data**，而后者是不使用**testing set**，训练好后，再去**classify**它。

<img src="https://i.loli.net/2021/03/31/Pv3JRQ5Zo2NF1yH.png" alt="ML Lecture 12_ Semi-supervised 00-04-05 .png" style="zoom:50%;" />

# 2.Generative model

### 对比supervised generative model

有监督的生成模型，是根据图中的公式来计算，根据$P(C_1),P(C_2),\mu^1,\mu^2,\sum$的值就可以计算出x属于$C_1$的概率

<img src="https://i.loli.net/2021/03/31/J6rBUEIiNeKojYb.png" alt="ML Lecture 12_ Semi-supervised 00-08-45 .png" style="zoom:50%;" />



### semi-supervised learning的Generative model

- 先初始化一组参数$\theta=\{P(C_1),P(C_2),\mu^1,\mu^2,\sum\} $，可以随机产生，也可以用有label的data来先计算出一组参数
- 根据现在有的参数$\theta$，来计算无label的data $x^u$属于class 1的概率
- 然后根据计算的概率来update你的model，就是更新先验概率$P(C_1),P(C_2)$，公式为

<img src="https://i.loli.net/2021/03/31/W62h3QEMDaALeRx.png" alt="ML Lecture 12_ Semi-supervised 00-14-16 .png" style="zoom:50%;" />



N为data的总数，N1为属于Class 1的data数，然后加上所有的unlabeled 的data属于class1的posterior probability后验概率的和。

supervised learning的$\mu^1$是等于$\frac{1}{N_1}\sum_{x^r\in C_1}^{}x^r$，semi-supervised learning的$\mu^1$需要加上unlabeled的data $x^u$属于class 1的概率乘上$x^u$，然后再除以所有unlabeled的data $x^u$属于class 1的概率，即做了个加权平均。

利用的方法是EM演算法

# 3.self-training

步骤：

- 给定labeled data 和unlabeled data
- 根据labeled data训练model
- 根据训练的model来计算unlabeled data的虚假的label，就是计算出来的label
- 把加了label 的unlabeled data的一部分加入labeled data ，然后回到第二步

<img src="https://i.loli.net/2021/03/31/38SCabojdX6RriD.png" alt="ML Lecture 12_ Semi-supervised 00-20-29 .png" style="zoom:50%;" />

但是self-training不可以用在regression线性回归上，因为你算出来的就是你线性model的产生的数字，所以你加进去还是不改变平均值和偏差

hard label就是一个data，就是属于class 1或则是class 2，soft label的意思是一个data属于class 1的概率为p，属于calss 2 的概率为1-p

<img src="https://i.loli.net/2021/03/31/cNnU5JSBO2D6ZYG.png" alt="ML Lecture 12_ Semi-supervised 00-24-38 .png" style="zoom:50%;" />

如果是用neural network的话，用soft label是不work的，原理它生成的就是[0.7,0.3]你又用[0.7,0.3]来训练它，相当于没有对它造成激励。

根据low-density separation考虑，我们希望同类分布比较密集，所以我们就引入熵的公式xln(x)，前两个熵是0，第三个是ln5，熵一般是越小越好。

<img src="https://i.loli.net/2021/03/31/xCzoHMI1jbl9ELc.jpg" alt="hhh.jpg" style="zoom:50%;" />

损失函数按照labeled data实际label和预测label的cross entropy加上unlabeled data 的entropy

<img src="https://i.loli.net/2021/03/31/UGq4pm3oT5PdHl9.png" alt="ML Lecture 12_ Semi-supervised 00-29-53 .png" style="zoom:50%;" />

**svm**：找一个边界，可以提供最大的空白margin和最小的error

# 4.Smoothness Assumption

<img src="https://i.loli.net/2021/03/31/ETlLMSfcC6F4XvN.png" alt="ML Lecture 12_ Semi-supervised 00-35-37 .png" style="zoom:50%;" />

举例说明：

<img src="https://i.loli.net/2021/03/31/uiUTKRmWeQZ29Sy.png" alt="ML Lecture 12_ Semi-supervised 00-38-46 .png" style="zoom:50%;" />

# 5.Graph-based Approach

首先建立data和data之间的连接，例如做网页的分类，网页之间的连接会表明这两个网页属于同一类，还有例如论文之间的引用也表明这两个论文表示同一类。所以我们可以根据其他的一些方法，例如距离等等来对data建立Graph-based Approach图

<img src="https://i.loli.net/2021/03/31/CbZ9lz6xdiVSPf3.png" alt="ML Lecture 12_ Semi-supervised 00-46-15 .png" style="zoom:50%;" />

这表明下图中虽然A点和B点相聚很远，但是根据链路可以知道，A和B属于同一个class

<img src="https://i.loli.net/2021/03/31/dufo1nkeCjaHDy5.png" alt="ML Lecture 12_ Semi-supervised 00-50-01 .png" style="zoom:50%;" />

**定量**的分析在图片上label的平滑程度：

计算公式：

<img src="https://i.loli.net/2021/03/31/SFYCIqm9nEx5dui.png" alt="ML Lecture 12_ Semi-supervised 00-56-02 .png" style="zoom:50%;" />

