# 1、pandas API

![截屏2021-03-13 下午5.26.59.png](https://i.loli.net/2021/03/13/jbB9dKi5OFvlYSC.png)

- `iloc` 根据索引值index获取DataFrame类型的数据的行和列

  ```pthon
  women=train_data.iloc[:,[1,3,4]]#读取所有的行，读取列索引值为1，3，4的column
  women=train_data.iloc[:,2:5]#读取所有的行，读取列索引值[2,5)的column
  ```

  

- `loc`根据feature（表头）和rows的index来获取DataFrame类型数据的行和列。更多使用方法见API

```python
women=train_data.loc[train_data['Sex']=='female']['Survived']#读取train_data中Sex那一列中为'female'的行，和feature=='Survived'的那一列
#也可以
women=train_data.loc[train_data.Sex=='female']['Survived']#读取train_data中Sex那一列中为'female'的行，和feature=='Survived'的那一列
```



- 