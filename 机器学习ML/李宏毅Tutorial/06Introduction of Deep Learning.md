# 1.step 1 of deep learning

### neural network structure：

<img src="https://i.loli.net/2021/03/20/OiS35TZgCIlM7eJ.png" alt="image.png" style="zoom: 25%;" />

because different parameters of neural network define different function

deep=many hidden layers

### the function of neural network

<img src="https://i.loli.net/2021/03/20/OhzI5Ek3fRoLDnM.png" alt="截屏2021-03-20 下午3.59.40.png" style="zoom: 25%;" />

<img src="https://i.loli.net/2021/03/20/6mZ3loA5HtWMXNG.png" alt="截屏2021-03-20 下午3.59.50.png" style="zoom:25%;" />

# step2:goodness of function

loss of an example is cross entropy of predict and true lable

<img src="https://i.loli.net/2021/03/20/equPTK14JgyR3L8.png" alt="截屏2021-03-20 下午4.06.02.png" style="zoom:25%;" />

total loss equals the sum of loss of an example

<img src="https://i.loli.net/2021/03/20/OqFJ4sbNVCQRExg.png" alt="截屏2021-03-20 下午4.10.17.png" style="zoom: 25%;" />

use Gradient descent minimize total loss

# step3:pick the best function

### key: compute gradient

<img src="https://i.loli.net/2021/03/20/dnpPhcrmN8GjQvE.png" alt="image.png" style="zoom:25%;" />

### 计算梯度的方法：Backpropagation

tensorflow pytorch

# 4.how the backpropagation反向传播 work

problem 参数很多

怎么计算梯度：chain rule 链式规则

<img src="https://i.loli.net/2021/03/20/12W3KxdUamHpSqn.png" alt="ML Lecture 7_ Backpropagation 00-05-03 .png" style="zoom: 50%;" />

计算：

c是cross entropy的意思，total是sum所有data的cross entropy，so calculate一个data的cross entropy就可以同理得到total loss



**forward pass**：就是计算每个z对w的导数，其实就是等于w前面的那个数

c对w求导根据链式规则，它等于c对z求导，乘z对w求导，其实就是每个w的前面的输入值

<img src="https://i.loli.net/2021/03/20/kiSBDQJyhgjc4lO.png" alt="ML Lecture 7_ Backpropagation 00-10-02 .png" style="zoom:50%;" />

**Backward pass**：就是计算c对z求导，其实他就是等于c对a求导，然后乘上a对z求导，a又是z的sigma函数，后面的就是同理可以算出来

<img src="https://i.loli.net/2021/03/20/ED7BUFAu3Pr1hQm.png" alt="ML Lecture 7_ Backpropagation 00-15-58 .png" style="zoom:50%;" />

图像解释：

<img src="https://i.loli.net/2021/03/20/bE1C4Npz3rjo7Qm.png" alt="ML Lecture 7_ Backpropagation 00-21-04 .png" style="zoom:50%;" />

总结：

<img src="https://i.loli.net/2021/03/20/Il3AyQ1pYOuJSv6.png" alt="ML Lecture 7_ Backpropagation 00-31-20 .png" style="zoom:50%;" />

