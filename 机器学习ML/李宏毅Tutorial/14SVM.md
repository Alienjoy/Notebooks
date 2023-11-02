# 1.SVM

support vector machine支持向量机=Hinge Loss合叶loss+Kernel Trick核心

# 2.Hinge Loss

在二分类问题中的步骤为

<img src="https://i.loli.net/2021/04/06/FK7eLRDZPuEJmXp.png" alt="ML Lecture 20_ Support Vector Machine (SVM) 00-03-44 .png" style="zoom:50%;" />

Loss Function比较：

<img src="https://i.loli.net/2021/04/06/F4OfCMLKdvsuNnI.png" alt="ML Lecture 20_ Support Vector Machine (SVM) 00-12-58 .png" style="zoom:50%;" />

Hinge Loss:

<img src="https://i.loli.net/2021/04/06/1DHlauLQvAgGFtO.png" alt="ML Lecture 20_ Support Vector Machine (SVM) 00-17-56 .png" style="zoom:50%;" />



# 3.SVM的loss采用hinge loss

SVM用gradient descent来进行training，以下是对w进行求导，就是对hinge loss 进行求导

hinge loss的形式：

<img src="https://i.loli.net/2021/04/06/dj8FNYlQf7yUZH9.png" alt="ML Lecture 20_ Support Vector Machine (SVM) 00-28-42 .png" style="zoom:50%;" />

<img src="https://i.loli.net/2021/04/06/WHysSXwQJD25BnA.png" alt="ML Lecture 20_ Support Vector Machine (SVM) 00-28-13 .png" style="zoom:50%;" />

<img src="https://i.loli.net/2021/04/06/tCfUYOjMeG6KXy9.png" alt="ML Lecture 20_ Support Vector Machine (SVM) 00-34-40 .png" style="zoom:50%;" />

# 4.Kernel Trick

<img src="https://i.loli.net/2021/04/06/X6ztT3J5Qk2gDaN.png" alt="ML Lecture 20_ Support Vector Machine (SVM) 00-38-28 .png" style="zoom:50%;" />

SVM相较于logistic regression来说不是每一笔data都会对最后的结果造成影响。

对W*来做化简得：其中$K(x^n,x)=x^n.x$

<img src="https://i.loli.net/2021/04/06/mY2qUoyHev6z9ZX.png" alt="ML Lecture 20_ Support Vector Machine (SVM) 00-44-16 .png" style="zoom:50%;" />