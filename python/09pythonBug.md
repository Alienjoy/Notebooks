# 1、Bug

调试bug可以使用print方法，或者是注释掉报错部分的代码

处理异常的机制

```python
try:
	#可能会出现异常的代码
except 异常类型:
	#异常处理代码
```



多个exception结构，首先要处理子类的异常，然后再处理父类的异常

```python
try:
	#可能会出现异常的代码
except 异常类型:
	#异常处理代码
except 异常类型:
	#异常处理代码
except 异常类型:
	#异常处理代码
except BaseException as e:#最后可以添加BaseException
	print(e)
```



try..exception...else结构，exception和else执行会二选一

```python
try:
	#可能会出现异常的情况
except 异常类型:
	#异常代码处理逻辑
else:
	#如果不出现异常则执行这段代码
```



try..exception...else...fianlly结构，exception和else执行会二选一，finally无论是否出错都会执行

```python
try:
	#可能会出现异常的情况
except 异常类型:
	#异常代码处理逻辑
else:
	#如果不出现异常则执行这段代码
finally:
  #无论是否出错都会执行这段代码

```

# 2、python中常见的错误类型

| 序号 | 错误类型          | 描述              |
| ---- | ----------------- | ----------------- |
| 1    | ZeroDivisionError | 除数不能为0错误   |
| 2    | IndexError        | 数据索引报错      |
| 3    | KeyError          | 映射中没有这个键  |
| 4    | NameError         | 未声明/初始化对象 |
| 5    | SyntaxError       | python语法错误    |
| 6    | ValueError        | 传入无效的参数    |

# 3、traceback的使用

```python
import traceback
try:
    print(10/0)
except:
    traceback.print_exc()
```



