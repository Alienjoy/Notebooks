

# 1、Numpy

[Numpy教程](https://www.runoob.com/numpy/numpy-linear-algebra.html)

```python
dot(a,b)#a向量与b向量的点积
```

1. power(x1, x2)

    对x1中的每个元素求x2次方。不会改变x1的shape。

2. sum(a, axis=None, dtype=None, out=None, keepdims=False)

 对a求和，如果axis=None，将矩阵中的每一个数加起来，如果axis=0，矩阵按列相加，如果axis大于0,矩阵按行相加。

 dtype定义输出的类型。

 out：自定义存放输出结果的矩阵，shape必须和输出一致。

3. tile(A, reps)

 以A为元素，构造一个reps为shap的矩阵。

 例tile([1 2],[3,4])

  输出为

[1 2 1 2 1 2 1 2

1 2 1 2 1 2 1 2

 1 2 1 2 1 2 1 2]

4. transpose(A)

  做矩阵A的转置。

5.shape(A)

 返回A的每一维的度数。

6. mat(A)

 将A转换成matrix，matrix和array的区别是，matrix必须是2维的，而array可以是多维的。

7.dot(A,B)

 对矩阵A和B做矩阵乘法。

```
a = np.array([[1, 2], [3, 4]])
mean(a,0)函数功能：求取均值 
经常操作的参数为axis，以m * n矩阵举例：
axis 不设置值，对 m*n 个数求均值，返回一个实数
axis = 0：压缩行，对各列求均值，返回 1* n 矩阵
axis =1 ：压缩列，对各行求均值，返回 m *1 矩阵
```

8.[Numpy.random.seed()的用法](https://blog.csdn.net/weixin_41571493/article/details/80549833)

通俗的来说就是用seed里面的值一样的话每次取的随机数都是一样的。