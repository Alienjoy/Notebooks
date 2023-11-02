pyTorch的官方[教程](https://pytorch.org/tutorials/)

# 1.pyTorch的导入

```python
import torch
import torch.nn as nn
import torch.nn.functional as F

from mpl_toolkits.mplot3d import Axes3D
import matplotlib.pyplot as plt

import numpy as np

torch.manual_seed(446)
np.random.seed(446)
```

# 2.pyTorch于numpy的区别

```python
# we create tensors in a similar way to numpy nd arrays
x_numpy = np.array([[0.1, 0.2, 0.3],[0.1, 0.2, 0.3]])
x_torch = torch.tensor([[0.1, 0.2, 0.3],[0.1, 0.2, 0.3]])
print('x_numpy, x_torch')
print(x_numpy,'\n', x_torch)
print()

# to and from numpy, pytorch
print('to and from numpy and pytorch')
print(torch.from_numpy(x_numpy), x_torch.numpy())#torch的方法，从torch转为numpy
print()

# we can do basic operations like +-*/
y_numpy = np.array([3,4,5.])
y_torch = torch.tensor([3,4,5.])
print("x+y")
print(x_numpy + y_numpy, x_torch + y_torch)
print()

# many functions that are in numpy are also in pytorch
print("norm")
print(np.linalg.norm(x_numpy), torch.norm(x_torch,))#norm为范数，求矩阵的范数，默认为2范数
print()

# to apply an operation along a dimension,
# we use the dim keyword argument instead of axis
print("mean along the 0th dimension")
x_numpy = np.array([[1,2],[3,4.]])
x_torch = torch.tensor([[1,2],[3,4.]])
print(np.mean(x_numpy, axis=0), torch.mean(x_torch, dim=0))
```

[np.linalg.norm\(\)的使用方法](https://blog.csdn.net/hqh131360239/article/details/79061535)

输出为：

```python 
x_numpy, x_torch
[[0.1 0.2 0.3]
 [0.1 0.2 0.3]]
tensor([[0.1000, 0.2000, 0.3000],
        [0.1000, 0.2000, 0.3000]])

to and from numpy and pytorch
tensor([[0.1000, 0.2000, 0.3000],
        [0.1000, 0.2000, 0.3000]], dtype=torch.float64) [[0.1 0.2 0.3]
 [0.1 0.2 0.3]]

x+y
[[3.1 4.2 5.3]
 [3.1 4.2 5.3]] tensor([[3.1000, 4.2000, 5.3000],
        [3.1000, 4.2000, 5.3000]])

norm
0.5291502622129182 tensor(0.5292)

mean along the 0th dimension
[2. 3.] tensor([2., 3.])
```



# 3.tensor张量的形状变换

```python
# "MNIST"
N, C, W, H = 10000, 3, 28, 28#N=number C=channel通道，W=width宽度，H=height高度
X = torch.randn((N, C, W, H))#rand为范围的意思，就是张量的尺寸

print(X.shape)
print(X.view(N, C, 784).shape)
print(X.view(-1, C, 784).shape) # 只有一个维度的尺寸可以写为-1，则pytorch会自动计算
```

输出：

```python
torch.Size([10000, 3, 28, 28])
torch.Size([10000, 3, 784])
torch.Size([10000, 3, 784])
```

# 4.不同纬度的矩阵进行计算

可以进行相加的两个tensor要符合broadcastable，直译就是可以广播的

符合broadcastable的两个tensor要满足以下两个条件：

- 每一个张量至少有一维
- 当遍历维度大小(从末尾维度开始)时,（维度大小必须相等,其中一个为1,或者其中一个不存在，满足这三个条件），例如5\*2的和5\*4的不可以相加，5\*1的和5\*4可以相加

```python

x=torch.empty(5,1,4,1)#x tensor的大小为5*1*4*1，
y=torch.empty(  3,1,1)#y tensor的大小为 3*1*1，会被自动转为1*3*1*1
print((x+y).size())
```

输出：

```python
torch.Size([5, 3, 4, 1])#按照比较大的纬度为主
```

# 5.计算参数的gradient 梯度

```python
a = torch.tensor(2.0, requires_grad=True) # we set requires_grad=True to let PyTorch know to keep the graph
b = torch.tensor(1.0, requires_grad=True)
c = a + b
d = b + 1
e = c * d
print('c', c)
print('d', d)
print('e', e)
```

# 6.使用GPU或则CPU来计算

```python
cpu = torch.device("cpu")
gpu = torch.device("cuda")#英伟达的cuda架构

x = torch.rand(10)
print(x)
x = x.to(gpu)
print(x)
x = x.to(cpu)
print(x)
```

输出：

```python
tensor([0.3959, 0.6177, 0.7256, 0.0971, 0.9186, 0.8277, 0.4409, 0.9344, 0.8967,
        0.1897])
tensor([0.3959, 0.6177, 0.7256, 0.0971, 0.9186, 0.8277, 0.4409, 0.9344, 0.8967,
        0.1897], device='cuda:0')#表示使用第一张GPU
tensor([0.3959, 0.6177, 0.7256, 0.0971, 0.9186, 0.8277, 0.4409, 0.9344, 0.8967,
        0.1897])
```

# 7.pyTorch计算梯度

```python
def f(x):
    return (x-2)**2

def fp(x):#自己定义的求梯度的函数
    return 2*(x-2)

x = torch.tensor([1.0], requires_grad=True)#requires_grad=True是让pyTorch来保存图形的。

y = f(x)
y.backward()#对y求它的梯度

print('Analytical f\'(x):', fp(x))#调用自己定义的求梯度函数
print('PyTorch\'s f\'(x):', x.grad)#调用pyTorch的求y对x的梯度的方法
```

输出：

```python
Analytical f'(x): tensor([-2.], grad_fn=<MulBackward0>)
PyTorch's f'(x): tensor([-2.])
```



```python
def g(w):
    return 2*w[0]*w[1] + w[1]*torch.cos(w[0])

def grad_g(w):
    return torch.tensor([2*w[1] - w[1]*torch.sin(w[0]), 2*w[0] + torch.cos(w[0])])

w = torch.tensor([np.pi, 1], requires_grad=True)#np.pi=pai

z = g(w)
z.backward()

print('Analytical grad g(w)', grad_g(w))
print('PyTorch\'s grad g(w)', w.grad)
```

输出：

```python
Analytical grad g(w) tensor([2.0000, 5.2832])
PyTorch's grad g(w) tensor([2.0000, 5.2832])
```

# 8.pyTorch使用梯度

```python
x = torch.tensor([5.0], requires_grad=True)
step_size = 0.25

print('iter,\tx,\tf(x),\tf\'(x),\tf\'(x) pytorch')
for i in range(15):
    y = f(x)
    y.backward() # compute the gradient
    
    print('{},\t{:.3f},\t{:.3f},\t{:.3f},\t{:.3f}'.format(i, x.item(), f(x).item(), fp(x).item(), x.grad.item()))
    
    x.data = x.data - step_size * x.grad # 使用梯度下降法更新x
    
    # We need to zero the grad variable since the backward()
    # call accumulates the gradients in .grad instead of overwriting.
    # The detach_() is for efficiency. You do not need to worry too much about it.
    x.grad.detach_()#这是为了提高效率
    x.grad.zero_()#需要将gradient改为0，因为backward()是累加而不是覆盖
```

输出：

```
iter, x, f(x),	f'(x),	f'(x) pytorch
0,  5.000,	9.000,	6.000,	6.000
1,	3.500,	2.250,	3.000,	3.000
2,	2.750,	0.562,	1.500,	1.500
3,	2.375,	0.141,	0.750,	0.750
4,	2.188,	0.035,	0.375,	0.375
5,	2.094,	0.009,	0.188,	0.188
6,	2.047,	0.002,	0.094,	0.094
7,	2.023,	0.001,	0.047,	0.047
8,	2.012,	0.000,	0.023,	0.023
9,	2.006,	0.000,	0.012,	0.012
10,	2.003,	0.000,	0.006,	0.006
11,	2.001,	0.000,	0.003,	0.003
12,	2.001,	0.000,	0.001,	0.001
13,	2.000,	0.000,	0.001,	0.001
14,	2.000,	0.000,	0.000,	0.000

```

# 9.pyTorch做linear regression

```python
#产生一批简单的数据集，添加了一些噪声
d = 2
n = 50
X = torch.randn(n,d)
true_w = torch.tensor([[-1.0], [2.0]])
y = X @ true_w + torch.randn(n,1) * 0.1#产生数据集，并添加噪声，y约等于Xdot(W)
print('X shape', X.shape)
print('y shape', y.shape)
print('w shape', true_w.shape)
```

输出：

```python
X shape torch.Size([50, 2])
y shape torch.Size([50, 1])
w shape torch.Size([2, 1])
```

### 比较人工的方法和pytorch的方法计算梯度：

```python
# define a linear model with no bias
def model(X, w):
    return X @ w

# the residual sum of squares loss function
def rss(y, y_hat):
    return torch.norm(y - y_hat)**2 / n

# analytical expression for the gradient
def grad_rss(X, y, w):
    return -2*X.t() @ (y - X @ w) / n

w = torch.tensor([[1.], [0]], requires_grad=True)
y_hat = model(X, w)

loss = rss(y, y_hat)
loss.backward()

print('Analytical gradient', grad_rss(X, y, w).detach().view(2).numpy())#从pytorch转为numpy，view是对数据进行reshape，转为一个二维向量，见上面
print('PyTorch\'s gradient', w.grad.view(2).numpy())

```

输出：

```python
Analytical gradient [ 4.342543  -3.5023162]
PyTorch's gradient [ 4.342543 -3.502316]
```

### 利用梯度下降法由生成的数据计算w

```python
step_size = 0.1

print('iter,\tloss,\tw')
for i in range(20):
    y_hat = model(X, w)
    loss = rss(y, y_hat)
    
    loss.backward() # compute the gradient of the loss
    
    w.data = w.data - step_size * w.grad # do a gradient descent step
    
    print('{},\t{:.2f},\t{}'.format(i, loss.item(), w.view(2).detach().numpy()))
    
    # We need to zero the grad variable since the backward()
    # call accumulates the gradients in .grad instead of overwriting.
    # The detach_() is for efficiency. You do not need to worry too much about it.
    w.grad.detach()
    w.grad.zero_()

print('\ntrue w\t\t', true_w.view(2).numpy())
print('estimated w\t', w.view(2).detach().numpy())
```

输出：

```
iter,	loss,	w
0,	7.82,	[0.13149136 0.70046324]
1,	2.84,	[-0.11822014  0.9229876 ]
2,	1.84,	[-0.31444427  1.1054724 ]
3,	1.19,	[-0.4684834  1.2552956]
4,	0.77,	[-0.58927345  1.3784461 ]
5,	0.50,	[-0.68387645  1.4797904 ]
6,	0.33,	[-0.75787055  1.563287  ]
7,	0.22,	[-0.8156596  1.632159 ]
8,	0.15,	[-0.86071837  1.6890337 ]
9,	0.10,	[-0.89578694  1.736055  ]
10,	0.07,	[-0.9230244  1.7749742]
11,	0.05,	[-0.94413096  1.8072236 ]
12,	0.03,	[-0.9604442  1.8339758]
13,	0.02,	[-0.9730157  1.8561921]
14,	0.02,	[-0.9826713  1.8746614]
15,	0.01,	[-0.99005884  1.8900318 ]
16,	0.01,	[-0.99568594  1.9028363 ]
17,	0.01,	[-0.99994993  1.913514  ]
18,	0.01,	[-1.0031612  1.9224268]
19,	0.01,	[-1.0055621  1.9298735]

true w		 [-1.  2.]#我们用的是真实的w生产的参数
estimated w	 [-1.0055621  1.9298735]#用梯度下降法计算出来的参数
```

# 10.torch.nn的module模块

一般的CNN卷积神经网络，RNN，linear的module

```python
d_in = 3
d_out = 4
linear_module = nn.Linear(d_in, d_out)

example_tensor = torch.tensor([[1.,2,3], [4,5,6]])
# applys a linear transformation to the data
transformed = linear_module(example_tensor)
print('example_tensor', example_tensor.shape)
print('transormed', transformed.shape)
print()
print('We can see that the weights exist in the background\n')
print('W:', linear_module.weight)
print('b:', linear_module.bias)
```

输出：

```
example_tensor torch.Size([2, 3])
transormed torch.Size([2, 4])

We can see that the weights exist in the background

W: Parameter containing:
tensor([[ 0.5260,  0.4925, -0.0887],
        [ 0.3944,  0.4080,  0.2182],
        [-0.1409,  0.0518,  0.3034],
        [ 0.0913,  0.2452, -0.2616]], requires_grad=True)
b: Parameter containing:
tensor([0.5021, 0.0118, 0.1383, 0.4757], requires_grad=True)
```

# 11.激活函数

```python
activation_fn = nn.ReLU() # 使用ReLU激活函数
example_tensor = torch.tensor([-1.0, 1.0, 0.0])
activated = activation_fn(example_tensor)#把数据输入激活函数
print('example_tensor', example_tensor)
print('activated', activated)
```

输出：

```
example_tensor tensor([-1.,  1.,  0.])
activated tensor([0., 1., 0.])
```

# 12.把一系列的操作包成一个模块(module)

```python
d_in = 3
d_hidden = 4
d_out = 1
model = torch.nn.Sequential(
                            nn.Linear(d_in, d_hidden),
                            nn.Tanh(),
                            nn.Linear(d_hidden, d_out),
                            nn.Sigmoid()
                           )

example_tensor = torch.tensor([[1.,2,3],[4,5,6]])
transformed = model(example_tensor)
print('transformed', transformed.shape)
```

把新建model这个事集合成一个module模块，用Sequential方法

# 13.获取model的参数

```python
params = model.parameters()

for param in params:
    print(param)
```

输出上面model上每一层的参数：

```
Parameter containing:
tensor([[-0.3128,  0.2707, -0.3952],
        [ 0.1285,  0.1777, -0.4675],
        [ 0.0452, -0.5630, -0.1999],
        [ 0.5431,  0.0524,  0.1126]], requires_grad=True)
Parameter containing:
tensor([ 0.2683, -0.2361,  0.2769, -0.1380], requires_grad=True)
Parameter containing:
tensor([[ 0.4902, -0.0928, -0.2907,  0.0734]], requires_grad=True)
Parameter containing:
tensor([-0.0394], requires_grad=True)

```

# 14.lossfunction

loss函数的使用

```python
mse_loss_fn = nn.MSELoss()

input = torch.tensor([[0., 0, 0]])
target = torch.tensor([[1., 0, -1]])

loss = mse_loss_fn(input, target)#mse均方误差

print(loss)
```

输出：

```
tensor(0.6667)
```

# 15.优化梯度下降法

torch.optim使用方法

```python
# create a simple model
model = nn.Linear(1, 1)

# create a simple dataset
X_simple = torch.tensor([[1.]])
y_simple = torch.tensor([[2.]])

# create our optimizer
optim = torch.optim.SGD(model.parameters(), lr=1e-2)
mse_loss_fn = nn.MSELoss()

y_hat = model(X_simple)
print('model params before:', model.weight)
loss = mse_loss_fn(y_hat, y_simple)
optim.zero_grad()
loss.backward()
optim.step()
print('model params after:', model.weight)
```

# 16.使用自动计算梯度，和pyTorch的模块的梯度下降法来做linear regression

现在,让我们将我们所学的以 PyTorchic 方式解决线性回归的方法结合起来

```python 
step_size = 0.1

linear_module = nn.Linear(d, 1, bias=False)

loss_func = nn.MSELoss()

optim = torch.optim.SGD(linear_module.parameters(), lr=step_size)

print('iter,\tloss,\tw')

for i in range(20):
    y_hat = linear_module(X)
    loss = loss_func(y_hat, y)
    optim.zero_grad()
    loss.backward()
    optim.step()
    
    print('{},\t{:.2f},\t{}'.format(i, loss.item(), linear_module.weight.view(2).detach().numpy()))

print('\ntrue w\t\t', true_w.view(2).numpy())
print('estimated w\t', linear_module.weight.view(2).detach().numpy())
```

输出：

```
iter,	loss,	w
0,	2.99,	[-0.5453574   0.51412684]
1,	2.02,	[-0.666086    0.75222915]
2,	1.37,	[-0.75831056  0.9504565 ]
3,	0.94,	[-0.82842976  1.1156546 ]
4,	0.64,	[-0.8814486  1.2534634]
5,	0.44,	[-0.92127615  1.3685349 ]
6,	0.31,	[-0.9509604  1.4647106]
7,	0.22,	[-0.9728737  1.5451664]
8,	0.15,	[-0.98885876  1.6125307 ]
9,	0.11,	[-1.0003437  1.6689818]
10,	0.08,	[-1.0084321  1.7163262]
11,	0.06,	[-1.0139749  1.7560644]
12,	0.04,	[-1.0176253  1.7894436]
13,	0.03,	[-1.0198835  1.8175017]
14,	0.02,	[-1.0211303  1.8411033]
15,	0.02,	[-1.0216544  1.8609697]
16,	0.02,	[-1.0216731  1.8777025]
17,	0.01,	[-1.0213491  1.8918046]
18,	0.01,	[-1.020803   1.9036964]
19,	0.01,	[-1.020123   1.9137299]

true w		 [-1.  2.]
estimated w	 [-1.020123   1.9137299]
```

### 17.使用SGD随机梯度下降法

```python
step_size = 0.01

linear_module = nn.Linear(d, 1)
loss_func = nn.MSELoss()
optim = torch.optim.SGD(linear_module.parameters(), lr=step_size)
print('iter,\tloss,\tw')
for i in range(200):
    rand_idx = np.random.choice(n) # take a random point from the dataset
    x = X[rand_idx] 
    y_hat = linear_module(x)
    loss = loss_func(y_hat, y[rand_idx]) # only compute the loss on the single point
    optim.zero_grad()
    loss.backward()
    optim.step()
    
    if i % 20 == 0:
        print('{},\t{:.2f},\t{}'.format(i, loss.item(), linear_module.weight.view(2).detach().numpy()))

print('\ntrue w\t\t', true_w.view(2).numpy())
print('estimated w\t', linear_module.weight.view(2).detach().numpy())
```

输出：

```
iter,	loss,	w
0,	4.46,	[-0.20530999  0.66900945]
20,	1.28,	[-0.3492172  0.8908058]
40,	0.73,	[-0.513422   1.1883926]
60,	0.51,	[-0.6704745  1.5351907]
80,	0.16,	[-0.7813061  1.6464837]
100,	0.20,	[-0.8568147  1.7569876]
120,	0.03,	[-0.90830195  1.8347709 ]
140,	0.00,	[-0.9449066  1.888105 ]
160,	0.00,	[-0.96574944  1.9163204 ]
180,	0.01,	[-0.98202056  1.9221277 ]

true w		 [-1.  2.]
estimated w	 [-0.98299205  1.9443793 ]
```

[教程](https://www.youtube.com/watch?v=kQeezFrNoOg)中做了一个复杂函数的实验

# 18.加了momentum动量的SGD

见[colab教程](https://colab.research.google.com/drive/1Xed5YSpLsLfkn66OhhyNzr05VE89enng)

# 19,做分类的时候的loss 使用cross entropy

见[colab教程](https://colab.research.google.com/drive/1Xed5YSpLsLfkn66OhhyNzr05VE89enng)

# 20.使用pyTorch的dataset

见[colab教程](https://colab.research.google.com/drive/1Xed5YSpLsLfkn66OhhyNzr05VE89enng)