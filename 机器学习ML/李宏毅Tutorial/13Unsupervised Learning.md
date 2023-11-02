<img src="/Users/zhangshuheng/Desktop/Notebooks/机器学习ML/李宏毅Tutorial/13Unsupervised Learning.assets/image-20211021203648311.png" alt="image-20211021203648311" style="zoom:50%;" />

# 1.Clustering，聚类

clustering分类，cluster是群的意思

### 方法1:K-means

- 首先初始化k个cluster的中心向量$c^i$
- 计算每一个x是否属于X，如果$x^n$**足够靠近**$c^i$则参数$b_i^n=1$，否则为0
- 根据公式更新$c^i$

![640](/Users/zhangshuheng/Desktop/Notebooks/机器学习ML/李宏毅Tutorial/13Unsupervised Learning.assets/640.gif)

![IMG_0141.PNG](https://i.loli.net/2021/04/01/kBNt7MZ94HG16Xh.png)

### 方法2.HAC

- 第一步首先根据data计算两两的相似度，最像的分为一个cluster，循环
- 找一个阈值，来决定分为多少类。

distributed representation分布式表达，就是属于这一类的概率为几十%，属于另一类的概率为几十%。

# 2.dimension reduction纬度缩减 （线性降维）重点

是找出一个function使输入是高纬的向量，输出的是低维的向量。

方法1: feature selection

方法2:principle component analysis (PCA)**主成分分析**，就是进行线性变换z=Wx，将高纬的数据压缩成低纬度的数据

假如要把高纬空间中的向量变成一维空间（对于高纬来说其实就是对W的每一个行向量做内积），相当于z=w.x，就是x和一个w做内积，w的长度为1，则x在w上的投影就等于w.x，找w的标准是要尽可能的使原始数据经过线性变换后分的很开。就等价于找出是变换后的z的方差最大的w。原理省略，可以直接使用toolkit

### PCA的另外一种解释

一个向量等于另外几个向量的线性组合，**我们要做的是要找出一组基向量**使得x约等于号尽可能的接近于等于。之间的误差叫做Reconstruction error重建误差。就是一个data是由几种基本的元素组成的，基本元素就是基向量。



<img src="https://i.loli.net/2021/04/05/QJauZWNRUcYHI68.png" alt="ML Lecture 13_ Unsupervised Learning - Linear Methods 00-43-40 .png" style="zoom:50%;" />

<img src="https://i.loli.net/2021/04/05/4lCzAdeo25rZKhG.png" alt="ML Lecture 13_ Unsupervised Learning - Linear Methods 00-49-32 .png" style="zoom:50%;" />

因为pca是考虑整体的一个向量，不是只有叠加，也可以减去一部分，所以手写数字辨识的basic component不是局部的拼接，是类似下图的样子，如果只考虑相加的话，有一种方法叫做Non-negative matrix factorization（NMF）方法，非负矩阵分解

<img src="https://i.loli.net/2021/04/05/aSrgJ58ZWXxDKFq.png" alt="ML Lecture 13_ Unsupervised Learning - Linear Methods 01-11-48 .png" style="zoom:50%;" />

# 3.PCA和神经网络的关系

自动编码器Autoencoder，但是有要求，w之间是相互正交的，即W是正交矩阵，即$w^1$和$w^2$和$w^n$是垂直的，注意是下图中的上标，即c1和c2的权重向量是垂直的。

就是输入一个向量，希望输出的向量与输入向量越接近越好，就是下图中的$x-\bar{x}\approx \hat{x}$使约等于尽可能为等于

<img src="https://i.loli.net/2021/04/05/3HZltsPoGvKw2h6.png" alt="ML Lecture 13_ Unsupervised Learning - Linear Methods 00-57-31 .png" style="zoom:50%;" />

# 4.word embedding

word embedding是dimension reduction的应用，就是把每一个词汇分布在多维坐标系中。

怎么说明两个词汇具有某种关系呢，假如他们的上下文一样，则机器认为他们是一种有关联的东西，例如我喜欢吃米饭，我喜欢吃面条，则米饭和面条这两个东西就有一定的关联。

# 5.neighbor embedding（非线性降纬）

就是把高维空间的data分布，展开到低维空间上，来计算两个data之间的联系程度

 把高维空间的数据经过乘上权重后会输出一个data（输入的data是输出data的邻居），在进行data transform后转换到低维空间上后，乘上相同的weight也会得到对应的out data（也是经过data transform后的）

<img src="https://i.loli.net/2021/04/05/oO8DPQhjqi2KlSR.png" alt="ML Lecture 15_ Unsupervised Learning - Neighbor Embedding 00-07-34 .png" style="zoom:50%;" />

<img src="https://i.loli.net/2021/04/05/PiVqrTNKDIhHCeo.png" alt="ML Lecture 15_ Unsupervised Learning - Neighbor Embedding 00-16-43 .png" style="zoom:50%;" />

# 6.t-SNE t分布的随机邻居embedding

t-distribution 

<img src="/Users/zhangshuheng/Desktop/Notebooks/机器学习ML/李宏毅Tutorial/13Unsupervised Learning.assets/v2-5e124a2c8139681afec706799ebabcec_1440w.jpg.png" alt="v2-5e124a2c8139681afec706799ebabcec_1440w.jpg" style="zoom:75%;" />

解决了虽然相同的data的分布比较近，但是不同的data却没有分的很开的问题

先用PCA从50维到20维，然后用t-SNE从20维降到5维，

t-SNE一般用来可视化很多高纬x在二位平面的分布

# 7.Deep Auto-encoder

encode和decode编码和解码，编码就是把输入的data向量进行降维，decode就是把编码的数据重新升维到原来的纬度

<img src="https://i.loli.net/2021/04/05/KOh7tlERuwSkVcU.png" alt="ML Lecture 16_ Unsupervised Learning - Auto-encoder 00-04-56 .png" style="zoom:50%;" />

auto-encoder就是自动做encode和decode，目标就是对输入进行编码后再解码后与输入尽可能像。

auto-encoder for cnn

<img src="https://i.loli.net/2021/04/05/EXko8v5yhaD6Mxn.png" alt="ML Lecture 16_ Unsupervised Learning - Auto-encoder 00-28-59 .png" style="zoom:50%;" />

<img src="https://i.loli.net/2021/04/05/pVFO1qQvJgAMksI.png" alt="ML Lecture 16_ Unsupervised Learning - Auto-encoder 00-31-56 .png" style="zoom:50%;" />

用途：用在以图搜图上。

# 8.深度生成模型deep generative model





