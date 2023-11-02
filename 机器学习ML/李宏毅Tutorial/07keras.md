# 1.keras

[keras](https://keras.io/zh/)其实就是使用了tensorflow和theano的api

使用keras的方法：

```python
#导入
from keras.models import Sequential

model = Sequential()

#添加层
from keras.layers import Dense

model.add(Dense(units=64, activation='relu', input_dim=100))#Dense意思是全联接层的意思，activation是激活函数的问题，Dense可以改成convolution
model.add(Dense(units=10, activation='softmax'))#unit是单元的意思，就是nerual神经元的意思，有几个神经元就有几个输出。
#activation可以选择softplus，softsign，sigmoid，tanh，hard_sigmoid,linear

#李宏毅老师教的添加层的方法，keras的老版本的version1
#添加输入层
model.add(Dense(input_dim=25*25,output_dim=500))
model.add(Dense(activation='sigmoid'))
#添加中间层
model.add(Dense(output_dim=500))#因为上一层的输出就是下一层的输入，所以不用定义这一层的输入维
model.add(Dense(activation='sigmoid'))
#添加输出层
model.add(Dense(output_dim=10))
model.add(Dense(activation='softmax'))


#配置configuration学习过程
model.compile(loss='categorical_crossentropy',
              optimizer='sgd',#sgd是随机梯度下降法，可以是adma
              metrics=['accuracy'])#metrics是指标的意思

#开始训练
model.fit(x_train,y_train,batch_size=32,nb_epoch=10)#就是做把总样本使用十次，样本分批batch处理，十个样本是一个batch是应用了多线程，假如有100000个data，则batch=8，参数一共迭代100000/8*10次。用batch的原因就是GPU可以进行平行运算。
#它的loss是一批里面十个data的total_loss，然后对total_batch进行对w求导，得出gradient梯度来更新一次parameter
#如果batch=1则就等于SGD（Stochastic Gradient descent）随机梯度下降法。
```

存储和读取model



测试model的accuracy

```python
score=model.evaluate(x_test,y_test)
print('Total loss on Testing set is {}'.format(score[0]))
print('Accuracy  on Testing set is {}'.format(score[1]))
```

预测结果

```python
result=model.predict(x_test)
```

