# 1.Recurrent Neural Network 

Recurrent Neural Network 递归神经网络，有记忆力的neural network，他会考虑输入数据的前一个数据

```python
1 of n encoding
lexicon字典={dog,cat,elephant}
则：
dog=[1,0,0]
cat=[0,1,0]
elephant=[0,0,1]

beyond 1 of n encoding
lexicon字典={dog,cat,elephant,other}
其他的所有不是lexicon中的词汇都属于other
```

RNN会保存每次neural的输出，作为下一次的neural的输入，

<img src="https://i.loli.net/2021/03/28/pkTg1JbqKNVsuXv.png" alt="ML Lecture 21-1_ Recurrent Neural Network (Part I) 00-08-59 .png" style="zoom:50%;" />

当然递归神经网络也可以是深度的，

<img src="https://i.loli.net/2021/03/28/lYhRNzkTB6nJoKG.png" alt="ML Lecture 21-1_ Recurrent Neural Network (Part I) 00-14-17 .png" style="zoom:50%;" />

当然也可以把输出存起来作为下次的输入，则这种recurrent neural network叫做Jordan Network

当然数据的输入方向可以是反向输入的，这样它就相当于看过这个输入之前和之后的输入数据。

# 2.memory存储器的结构，LSMT架构的RNN

long short-term memory（LSTM）长的短期记忆存储器

<img src="https://i.loli.net/2021/03/28/Sk3dVLhumJaD7sU.png" alt="ML Lecture 21-1_ Recurrent Neural Network (Part I) 00-20-53 .png" style="zoom:50%;" />

<img src="https://i.loli.net/2021/03/28/31lad65CEHBLqvu.png" alt="ML Lecture 21-1_ Recurrent Neural Network (Part I) 00-34-06 .png" style="zoom:50%;" />

x乘zf，zi，z，zo后的输出参数的个数等于memory cell的个数一样

<img src="https://i.loli.net/2021/03/28/JGvkChHgTzmuB8q.png" alt="ML Lecture 21-1_ Recurrent Neural Network (Part I) 00-43-25 .png" style="zoom:50%;" />

原理：

<img src="https://i.loli.net/2021/03/28/lBQNoH8Mf5LAsXT.png" alt="ML Lecture 21-1_ Recurrent Neural Network (Part I) 00-45-09 .png" style="zoom:50%;" />

<img src="https://i.loli.net/2021/03/28/bm2Pe9xp7SOWNnr.png" alt="ML Lecture 21-1_ Recurrent Neural Network (Part I) 00-46-56 .png" style="zoom:50%;" />



keras支持的RNN有LSTM，GRU（相较于LSTM gate的数量只有两个），SimpleRNN（就是本文第一章中描述的那样的结构）



# 3.RNN的训练特性

RNN的total loss 会不断的波动。

<img src="https://i.loli.net/2021/03/29/8hPCzk7f9n1tgH6.png" alt="ML Lecture 21-2_ Recurrent Neural Network (Part II) 00-08-38 .png" style="zoom:50%;" />

因为memory在经过多次的递归之后，memory中的数的变化会非常的剧烈，例如$1.01^{1000}=20000,0.99^{1000}=0$

<img src="https://i.loli.net/2021/03/29/ukB7sDnEegNFmcL.png" alt="ML Lecture 21-2_ Recurrent Neural Network (Part II) 00-17-11 .png" style="zoom:50%;" />

解决方法：把RNN为LSTM，因为LSTM可以处理gradient vanish的问题，拓展 [Gradient Vanish](https://blog.csdn.net/zchang81/article/details/70227946)

> Gradient Vanish 这个问题是由激活函数不当引起的，多层神经网络使用Sigmoid系激活函数，会使得误差从输出层开始呈指数衰减，靠近输出层的隐层训练的比较好，而靠近输入层的隐层几乎不能训练。
>
> 以5层结构为例，大概仅有第5层输出层，第4层，第3层被训练的比较好。误差传到第1、2层的时候，几乎为0。这时候5层相当于3层，前两层完全在打酱油。并且由于神经网络的正向传播是从随机初始化的1、2层开始的，这意味着，起初必须还得经过还是一片随机的的1、2层。这样，无论你后面3层怎么训练，都不能够收敛。
>
> 2012年，Hinton组的Alex Krizhevsky率先将受到Gradient Vanish影响较小的CNN中大规模使用新提出的ReLu函数。
>
> 2014年，Google研究员贾扬清则利用ReLu这个神器，成功将CNN扩展到了22层巨型深度网络。

原因是LSTM的memory是

# 4.RNN应用

- 语音辨识，解决叠字的方法叫做[CTC](https://blog.csdn.net/liuxiaoheng1992/article/details/83660557)，输入的sequence比较长，输出的sequence比较短
- 做翻译，sequence to sequence 

