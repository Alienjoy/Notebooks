# 为什么要做Deep

DNN=deep neural network

比较神经网络的是更深还是更宽的的性能更好的时候要保证参数尽量一样多

因为神经网络更深的话，高层次的neural可以调用低层次的neural组成的function。

例如有个分类长头发男生，短头发男生，长头发女生，短头发女生的分类器，可以先设置两个子分类器分别是  长头发&短头发分类器，男生&女生分类器，然后再调用这两个分类器就可以很方便的分出四个class，这就是为什么更深的neural network会performance更好。就是模组化

<img src="https://i.loli.net/2021/03/24/1d6c8PvbKINZAGk.png" alt="ML Lecture 11_ Why Deep_ 00-06-58 .png" style="zoom: 50%;" />





# universality theory 普遍性理论

universality theory 就是任何的连续的network都可以用一层hidden layer组成，只要那一层的network足够宽的话。

