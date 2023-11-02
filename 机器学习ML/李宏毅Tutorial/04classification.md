# 1.Generative model

**手动去算，没人会这样做，我们采用logistic regression**

classification的Loss：
$$
L(f)=\sum_{n}^{}\delta (f(x^n)\neq \hat{y}^n)
$$
即，如果期望输出不等于实际应该的则$\delta$为1，否则为0，则目的要让分类错误的次数最少。

<img src="https://i.loli.net/2021/03/16/X7m1fa5vo4sTHLC.png" alt="ML Lecture 4_ Classification 00-18-46 .png" style="zoom: 50%;" />

给定一个x，求出x属于class 1的概率$P(C_1|x)$，叫做posterior probability后验概率

$P(C_1|x)$叫做一个data x属于$C_1$的概率，$P(C_1)$叫做prior probability先验概率，$P(x|C_1)$叫做从$C_1$中sample出x的概率，事先可以知道的：例如语音辨识的时候提前知道每一句话被说出来的概率。

说明：从第一个盒子中抽取球的概率为1/3，从第二个盒子抽取球的概率为2/3，第一个盒子中蓝球的概率为4/5，第二个盒子中蓝球的概率为2/5

则假如抽取的一个为蓝球，则它属于第一个盒子的概率为
$$
P(C_1|x)=\frac{\frac{1}{3}\times \frac{4}{5}}{\frac{1}{3}\times \frac{4}{5}+\frac{2}{3}\times \frac{2}{5}}
$$
**一元高斯分布**：

最中间为平均值，一个格为一个标准差，假如平均值为5，标准差为1，则[4，6]的概率为68%

<img src="https://i.loli.net/2021/03/16/ho6mc5AMsxWVgrS.png" alt="截屏2021-03-16 下午8.29.35.png" style="zoom:25%;" />

**多元高斯分布**：

<img src="https://pic2.zhimg.com/v2-e2690ca9a9c7ee17203aa1842aee844b_1440w.jpg?source=172ae18b" style="zoom:25%;" />

**Gaussian distribution**高斯分布：

假设class 1和class 2的sample分布符合高斯分布。则求出class 1和class 2的高斯函数。

exp=exponential指数的缩写$exp(x)=e^x$

<img src="https://i.loli.net/2021/03/16/JQeKLU873sVc5xY.png" alt="ML Lecture 4_ Classification 00-27-48 .png" style="zoom: 50%;" />

上图probability可能性，其实是probability的density密度

mean平均值=$\mu$，代表的是分布的最高点，如果输入向量x有7个feature则它是7维向量

[协方差](https://www.cnblogs.com/leezx/p/9929340.html)

variance方差=covariance协方差， matrix矩阵，$\sum$读作sigma，小写的为$\sigma$，代表的是发散的程度，如果输入向量有7个feature则$\sum$是7维矩阵。

$|\sum|$表示矩阵sigma的行列式，determinant行列式

<img src="https://i.loli.net/2021/03/16/5sCNW1bjwa6qKQL.png" alt="ML Lecture 4_ Classification 00-33-42 .png" style="zoom:50%;" />

某个高斯函数sample出这79个点的概率（Likelihood可能性）为79个点代入Gaussian distribution高斯分布公式中的乘积

结下来就是找出使likelihood最大的$\mu$和$\sum$，记为$\mu^*$和$\sum^*$

根据推论有如下公式可以找出$\mu^*$和$\sum^*$，使likelyhood最大

$\mu^*=\frac{1}{79}\sum_{n=1}^{79}x_n$,其中$x_n$为feature向量，也可记为$x^n$，就是对所有向量求平均值
$$
\sum^*=\frac{1}{79}\sum_{n=1}^{79}(x^n-\mu ^*)(x^n-\mu ^*)^T
$$


则接下来可以预测新的sample的属于class 1和class 2的概率了，如果x在class 1中的几率大于0.5则属于class 1，如果x在class 2中的几率大于0.5则属于class 2

<img src="https://i.loli.net/2021/03/16/oS4Mj7UCHyA1gqY.png" alt="ML Lecture 4_ Classification 00-38-39 .png" style="zoom:50%;" />

# 2.改进

- 以上是不同的class具有不同的高斯分布函数，就是不同的$\mu^*$和$\sum^*$

实际使用中则不同的class可以共用同一个$\sum^*$

则此时的likelyhood变为了如下图所示，$\mu^*$不变，$\sum^*$变成了加权平均值也如下图所示

<img src="https://i.loli.net/2021/03/16/vzkHxGET72aWOoq.png" alt="ML Lecture 4_ Classification 00-48-44 .png" style="zoom:50%;" />

# 3.概率模型的三个步骤

- 1、function set就是建立model

  模型就是P(C1|x)，表示x在class 1中的概率，如果大于0.5则表示属于class 1

  <img src="https://i.loli.net/2021/03/16/oS4Mj7UCHyA1gqY.png" alt="ML Lecture 4_ Classification 00-38-39 .png" style="zoom: 25%;" />

- 2、最优化model

  找出可以最大化likelyhood的可能性分布（probability distribution就是找出$\mu^*$和$\sum^*$），likelyhood的大小定义了一组参数（或者说model，或者说function）的好坏

- 3、找出最优的model

# 4.分类器的概率模型可以表示为

sigmoid函数 叫做s型函数$\sigma(z)=\frac{1}{1+e^{-z}}$，z大于0会变成[0.5,1)，z小于0会变成(0,0.5]

分类概率模型推导：

<img src="https://i.loli.net/2021/03/17/aJNDuYZreOAgyWk.png" alt="ML Lecture 4_ Classification 01-00-38 .png" style="zoom:50%;" />

<img src="https://i.loli.net/2021/03/17/vAGfXyd57zCpZqj.png" alt="ML Lecture 4_ Classification 01-09-24 .png" style="zoom: 50%;" />



把z展开化简可以得到$z=\vec{w}^T\vec{x}+b$，则$P(C_1|x)=\sigma(z)=\sigma(\vec{w}.\vec{x}+b)$，其中$P(C_1|x)$表示x属于class 1的概率，$\vec{w}.\vec{x}$表示w向量和x向量的内积 inner product

