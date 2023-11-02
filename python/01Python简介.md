# 1.转义字符
`\n`=newLine<br/>
`\r`=return<br/>
`\t`=tab<br/>
`\b=`backspace<br/>
`\\`=\ <br/>
`\'`=' <br/>
`\"`="

```python
../ 表示当前文件所在的目录的上一级目录
./ 表示当前文件所在的目录(可以省略)
#下层文件直接使用
文件夹名/training.csv
/ 表示当前站点的根目录(域名映射的硬盘目录)
```

args => arguments参数

kw / kwargs => key Word Arguments 关键字参数

# 2.数据类型
## a、基本数据类型
整数类型`int`（integer）、浮点类型`float`、布尔型`bool`（boolean）、字符串`str`<br/>
`float`小数存在不准确性，可以使用`Decimal('3.2')`类似这样的方式来解决。
`bool`的`true`表示1，`false`表示0。字符串可以用单引号`‘’`、双引号`“”`、三引号`""" """`或`''''''`，三引号可以换行

## b、数据类型转换
```python
str(int)#将int,bool,float类型专为str
str(bool)
str(float)

int(float)#将float,bool转为int,float只保留整数部分
int(bool)
int(str)#字符串只能为整数字符，可以为'32'，相当于解析

float(bool)#将bool，int转为float
float(int)
float(str)//字符串必须为数据字符串，可以为'32.3','43'
```
## 改变编码格式
```python
在代码最前面加上#coding:utf-8
```
# 3.输入输出
```python
name=input('这是提示语句')#默认输入的为str类型的数据
name=int(input('请输入年龄'))#强制转为int类型的数据
print(name,end='\t')#不换行输出
```
算数运算：加`+`，减`-`，乘`*`，除`/`，整除（向下取整）`//`，取模运算`%`，幂运算符`**`<br/>
赋值运算：`a,b,c=12,23,24`相当于`a=12,b=23,c=24`
# 4.比较运算符
python中特殊的是：`20<=sum and sum<=30`可以写为`20<=sum<=30`。
`==`比较的是value也就是值。`is`比较的是id标识。`is not`是id不相等的比较运算符
# 5.布尔运算符
`and`就是进行与运算，`or`就是进行或运算，`not`就是进行非运算，取反运算，`in`表示是否在里面，在里面的话为True，`not in`不在里面的话为True
# 6.按位运算符
`&`表示将数据转为二进制后按位与运算，`|`表示将数据专为二进制后按位或运算，`<<`表示左移运算符，数据转为二进制后左移最低位补0，`>>`表示右移运算符，数据转为二进制后右移最高位补0
# 7.对象的布尔值
`bool()`用来判断对象的bool值，在python中`flase` `0` `0.0` `None` `空字符串(str)` `空列表(list)` `空元组(tuple数组)` `空字典(dict字典)` `空集合(set)`的bool值都为false，其他对象的bool值均为true
# 8.分支结构
## 8.1单分支结构
`if`的语法结构
```python
if a>b:
    print('a>b')
    print('a大于b')
```
## 8.2多分支结构
`if...else`的语法结构
```python
if 条件表达式:
    条件执行体1
else
    条件执行体2
```
`if...elif...elif`的语法结构
```python
if 条件表达式:
    条件执行体1
elif
    条件执行体2
elif
    条件执行体3
...
[else]
    条件执行体n
```
`A if 条件表达式 else B`语法结构，如果条件表达式为true则执行A，如果条件表达式为flase则执行B

`pass`什么都不做，只是一个占位符
# 9.循环结构
`range()`内置函数，不需要加前缀就可以直接使用的函数叫做内置函数
```python
range(10)#表示[0,10)或者[0,9]
range(1,10)#表示[1,10)或者[1,9]
range(1,10,2)#表示从1开始，步长为2，为[1,3,5,7,9]
```


`while`的语法结构

```
while 条件表达式:
    循环体
```


`for...in`循环
又叫做for循环

```python
for index in 'abcdefg'
    print(index)
#会输出
a
b
c
...
```
```python
for index in range(10)
    print(index)
#会输出
0
1
2
....
9
```


如果不需要用到变量可

```python
for _ in range(10)
    print('会输出10次这句话')
```

---


`break`结束本层循环，`continue`结束本次循环，跳到下次循环

```python
while ...
    ...
    break
else
    ...
```
`while`循环正常结束的时候会执行`else`，如果遇到`break`的话则全部结束,不会执行`else`



```python
for ... in ...
    ...
    break
else
    ...
```
`for`循环正常结束的时候会执行`else`，如果遇到`break`的话则全部结束,不会执行`else`



