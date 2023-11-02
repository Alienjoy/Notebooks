# 1、Linear Regression线性回归

step1: model

y=wx+b，就叫做线性model

step2:loss用来表示这个model的好坏

$Loss= \frac{\left ( \hat{y}-y\right )^{2}}{n}$

### Gradient descent

[梯度下降法](https://www.youtube.com/watch?v=fegAeph9UaA)

### Overfitting&Regularization

[regularization正则化](https://www.cnblogs.com/jianxinzhou/p/4083921.html)：是用来消除过拟合的，让曲线变得更加smooth，不至于参数变化一点结果有大幅度的变化

<img src="https://i.loli.net/2021/03/11/Z45JLHxVmOnbisQ.png" alt="截屏2021-03-11 下午3.16.35.png" style="zoom:25%;" />



# 2、python各个工具

pyenv：python的运行环境，用来切换python的版本号

virtualenv：python的虚拟环境

anaconda：包和python环境管理工具

Conda :是一个开源的软件包管理系统和环境管理系统

conda list:列出当前 conda 环境所链接的软件包

conda create: 创建一个 conda 环境，名称为 tf

```
#安装homebrew
/bin/zsh -c "$(curl -fsSL https://gitee.com/cunkai/HomebrewCN/raw/master/Homebrew.sh)"
```

