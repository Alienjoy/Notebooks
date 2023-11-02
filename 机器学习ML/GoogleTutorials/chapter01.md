

# 1、Framing框架

Lables标签：the `y ` variable in simple linear regression

Feature特征：the `x` variable in simple linear regression

Regression回归：a regression model predicts continues values

Classification分类：a classification model predicts discreat values

[专业术语Glossary](https://developers.google.com/machine-learning/glossary#l)

[Pandas简介教程](https://colab.research.google.com/notebooks/mlcc/intro_to_pandas.ipynb?utm_source=mlcc&utm_campaign=colab-external&utm_medium=referral&utm_content=pandas-colab&hl=zh-cn)

[Pandas官方教程](https://pandas.pydata.org/docs/reference/index.html)

# 2、Descending into ML深入了解机器学习

b=bias偏见，偏斜

Loss损失函数，L2 Loss也称平方误差squared error，L2 loss=(预测值-标签值)^2

**均方误差** (**MSE**) 指的是每个样本的平均平方损失，MSE=L2 loss/N（N为样本数量）

最小二乘法又叫最小平方法least square

### 线性回归

输入和输出呈现线性的关系，回归就是整体上呈现线性的意思，可以解释为整体线性

# 3、Reducing Loss降低损失

梯度步长=学习速率*倒数（即loss函数的对x的斜率，也就是计算参数对L的偏微分），然后计算loss看是否变小，对于函数`y=b+wx`损失函数为`L(w,b)`，首先随机选择w和b，然后分别计算w和b的梯度步长，来确定最好的w和b，由于线性回归是凸函数，所以局部最小点就是全局最小点，神经网络只适应于凸函数

**批量梯度下降法**（Batch Gradient Descent，BGD)              //一般说的梯度下降法就是指BGD。 

**随机梯度下降法**（Stochastic Gradient Descent, SGD）    

[**小批量梯度下降法**](https://blog.csdn.net/pengchengliu/article/details/89215659)（Mini-batch Gradient Descent, MBGD）

# 4、回归与分类

**回归**模型可预测连续值。例如，回归模型做出的预测可回答如下问题：

- 由前9个小时来预测第10小时的PM2.5值
- 用户点击此广告的概率是多少？

**分类**模型可预测离散值。例如，分类模型做出的预测可回答如下问题：

- 某个指定电子邮件是垃圾邮件还是非垃圾邮件？
- 这是一张狗、猫还是仓鼠图片？
- 指定一张图片是衬衫还是裤子。