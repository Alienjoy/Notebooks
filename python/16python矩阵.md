# 1.矩阵的叉乘，点乘

tf.matmul(A,C)=np.dot(A,C)= A@C都属于叉乘，而tf.multiply(A,C)= A*C=A∙C属于点乘(内积)，但是如果是一个数`*`矩阵，那就表示乘，一个数乘矩阵

![](https://img-blog.csdnimg.cn/20190925135103300.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2hhaXppY2Nj,size_16,color_FFFFFF,t_70)

# 2.矩阵中的axis轴

[矩阵中的轴](https://zhuanlan.zhihu.com/p/25761406)axis = 0的轴表示行那个轴，axis=1轴表示列那个轴

# 3.python中的一个n维向量

```python
import numpy as np
x =np.array([1,2,3,4])
print(x.shape)
#输出为(4,)
y=np.array([[1,2,3,4],[2,4,6,8]])
print(x)
#输出的为[1 2 3 4]，这表示的是一个4维的向量，python中向量为横着的，因为只有一个axis，所以不是输出
[[1]
 [2]
 [3]
 [4]]
#当一个axis的向量和有两个axis的矩阵运算时，如
print(np.matmul(y,x))#把x的纬度大小当成一个(4,1)
#输出
[30 60]
#输出的还是一个(2,)这样只有一个axis的数组矩阵


x =np.array([1,2,3,4]).reshape(-1,1)
print(x.shape)
y=np.array([[1,2,3,4],[2,4,6,8]])
print(np.matmul(y,x))
#输出：
(4, 1)
[[30]
 [60]]
#也就是说最后的结果变成了(2,1)维的具有两个axis的数组矩阵

a=[1,2,3,4]
print(a)
#输出的为[1, 2, 3, 4]

```

# 4.python中[-1]、[:-1]、[::-1]、[2::-1]的使用方法

import numpy as np
a=[1,2,3,4,5]
print(a)
[ 1 2 3 4 5 ]

print(a[-1]) ###取最后一个元素
[5]

print(a[:-1])  ### 除了最后一个取全部
[ 1 2 3 4 ]

print(a[::-1]) ### 取从后向前（相反）的元素，倒叙，见02python列表
[ 5 4 3 2 1 ]

print(a[2::-1]) ### 取从下标为2的元素翻转读取
[ 3 2 1 ]

直观来说，对于一个二维数组X，X[:,0]就是取所有行的第0个数据, X[:,1] 就是取所有行的第1个数据。