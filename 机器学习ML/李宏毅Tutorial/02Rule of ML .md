# 1、Error的来源

- 来自bias（偏差）：整体偏移，不发散
- 来自variance（方差）：发散，但是平均值是在期望值附近


$$
方差\sigma^{2}=\frac{\sum(X-\mu)^{2}}{N}
$$
Bias和Variance的解释：

<img src="https://i.loli.net/2021/03/11/96U4O1ZKyBSEwaP.png" alt="截屏2021-03-11 下午1.54.19.png" style="zoom: 25%;" />

简单的model是bias比较大，variance比较小

比较复杂的model是bias比较小，然而variance比较大



<img src="https://i.loli.net/2021/03/11/OcVTftUuRYCyrah.png" alt="截屏2021-03-11 下午2.35.15.png" style="zoom:25%;" />

简单的model会产生underfitting（欠拟合），复杂的model会产生overfitting（过拟合）



- underfitting表现为：model不能很好的fit这training data

- overfitting表现为：在training data中误差较小，但是在testing data中有large error

解决方法：

- underfitting的时候：需要重新设计model，增加model的阶数或者是增加feature（特征），如高度，年龄
- overfitting的时候：增加更多的data，或则是改造data。或则是regularization（正则化）

drade-off（权衡）between bias and variance

### 训练model的时候需要注意的问题：

- 把trainning set分为trainning set 和validation set（确认数据集），用来选择哪个model好
- 把training set分为三分，其中一份作为validation set，求出每一次的error，然后根据三次的error求出average error，根据最小的average error来选择model，然后用所有的training set来training 选出来的model，（tips：不要过分看重testing set集上的error）

### 泛化能力

避免模型的过拟合，可以兼顾准确率和泛化能力的模型。泛化能力（generalization ability）是指机器学习算法对新鲜样本的适应能力