# 1、字典dictionary

类似java中的map有键和值组成

key不允许重复，value允许重复，字典中的元素是无序的，字典中的key必须是不可变对象

### 字典的创建

方式1:`字典名={'一百':100,'二百': 200}`。方式2:内置函数`dict(name='张三',age=14)`因为等号为赋值符号，所以等号左边不加任何符号，会自动补上。

`hash(key)`作用是查找key对应的数据在内存中的地址

### 字典值的获取

方法1:`字典名['键名']`。方法2：`字典名.get('键名')`用get方法获取

区别：方法1获取不存在的键值对会报错，而方法二利用get方法获取不存在的键值对会返回None

另外：`字典名.get('键名',99)`如果没找到对应的键名，会返回设置的默认值99

### 判断键是否在字典当中

`键名 in 字典名`判断键是否在字典当中，如`'一百' in score`如果在的话会返回true，否则会返回false

`键名 not in 字典名`判断键是否在字典当中，如`'一百' not in score`如果不在的话会返回true，否则会返回false

### 字典元素的删除

`del 字典名['键名']`删除指定的键值对

`字典名.clear()`清空字典

### 字典元素的修改

`字典名['键名']=新的值`

# 2、字典的视图操作

### 获取字典的视图

`字典名.keys()`获取字典的所有键，返回值为`dict_keys`的数据类型，可以用`list(字典名.keys())`转化为列表类型。

`字典名.values()`获取字典的所有值，返回值为`dict_values`的数据类型，可以用`list(字典名.values())`转化为列表类型。

`字典名.items()`获取字典的所有键值对，也可以用`list(字典名.items())`进行强制类型转换为列表类型。转换之后的列表的数据类型为元组

# 3、字典元素的获取

```python
for item in 字典名:
	print(item)#获取的是字典的键
  print(字典名[item])#获取的是字典的值
  print(字典名.get(item))#获取的是字典的值
```



​	

