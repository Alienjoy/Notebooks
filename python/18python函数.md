# iter()函数

语法：

```python
iter(object[, sentinel])
```

举例：

```python
>>>lst = [1, 2, 3]
>>> for i in iter(lst):
	     print(i)

1
2
3
```

# next()函数

**next()** 函数要和生成迭代器的 **iter()** 函数一起使用。

语法：

```python
next(iterable[, default])
参数说明：
iterable -- 可迭代对象
default -- 可选，用于设置在没有下一个元素时返回该默认值，如果不设置，又没有下一个元素则会触发 StopIteration 异常。
```

实例：

```python
# 首先获得Iterator对象:
it = iter([1, 2, 3, 4, 5])
# 循环:
while True:
    try:
        # 获得下一个值:
        x = next(it)#注意刚开始的next是index 0的前一个
        print(x)
    except StopIteration:
        # 遇到StopIteration就退出循环
        break
```

