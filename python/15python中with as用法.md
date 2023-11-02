# python中with...as的用法

with…as，就是个python控制流语句，像 if ，while一样。 
with…as语句是简化版的try except finally语句。

那我们先理解一下try…except…finally语句是干啥的。实际上，try…except语句和try…finally语句是两种语句，用于不同的场景。但是当二者结合在一起时，可以“实现稳定性和灵活性更好的设计”。

### 1.  try…except语句

用于处理程序执行过程中的异常情况，比如语法错误、从未定义变量上取值等等，也就是一些python程序本身引发的异常、报错。比如你在python下面输入 

```1/0
>>>1 / 0：
Traceback (most recent call last):
File "<stdin>", line 1, in <module>
ZeroDivisionError: division by zero

```

系统会给你一个ZeroDivisionError的报错。

说白了就是为了防止一些报错影响你的程序继续运行，就用try语句把它们抓出来(捕获)。 
try…except的标准格式：

```python
try:  
    ## normal block  
except A:  
    ## exc A block  
except:  
    ## exc other block  
else:  
    ## noError block  
```

程序执行流程是：

```
–>执行normal block 
–>发现有A错误，执行 exc A block(即处理异常) 
–>结束 
如果没有A错误呢？ 
–>执行normal block 
–>发现B错误，开始寻找匹配B的异常处理方法，发现A，跳过，发现except others(即except:)，执行exc other block 
–>结束 
如果没有错误呢？ 
–>执行normal block 
–>全程没有错误，跳入else 执行noError block 
–>结束
```


Tips: 我们发现，一旦跳入了某条except语句，就会执行相应的异常处理方法(block)，执行完毕就会结束。不会再返回try的normal block继续执行了。

```python
try:
    a = 1 / 2 #a normal number/variable
    print(a)
    b = 1 / 0 # an abnormal number/variable
    print(b)
    c = 2 / 1 # a normal number/variable
    print(c)
except:
    print("Error")
    
输出：
0.5
Error
```


结果是，先打出了一个0，又打出了一个Error。就是把ZeroDivisionError错误捕获了。

先执行try后面这一堆语句，由上至下： 
step1: a 正常，打印a. 于是打印出0.5 (python3.x以后都输出浮点数) 
step2: b, 不正常了，0 不能做除数，所以这是一个错误。直接跳到except报错去。于是打印了Error。 
step3: 其实没有step3，因为程序结束了。c是在错误发生之后的b语句后才出现，根本轮不到执行它。也就看不到打印出的c了

-------

但这还不是try/except的所有用法

except后面还能跟表达式的! 所谓的表达式，就是错误的定义。也就是说，我们可以捕捉一些我们想要捕捉的异常。而不是什么异常都报出来。

异常分为两类：

python标准异常
自定义异常
我们先抛开自定义异常(因为涉及到类的概念)，看看except都能捕捉到哪些python标准异常。请查看菜鸟笔记

```python
try:
    a = 1 / 2
    print(a)
    print(m)  # 此处抛出python标准异常
    b = 1 / 0 # 此后的语句不执行
    print(b)
    c = 2 / 1
    print(c)
except NameError:
    print("Ops!!")
except ZeroDivisionError:
    print("Wrong math!!")
except:
    print("Error")

输出：
0.5
Ops!!
```



当程序执行到`print(m)`的时候 发现了一个`NameError: name 'm' is not defined`，于是控制流去寻找匹配的`except`异常处理语句。发现了第一条匹配，执行对应`block`。执行完结束。

### 2. try…finallly语句

用于无论执行过程中有没有异常，都要执行清场工作。

好的 现在我们看看他俩合在一起怎么用!!

```python
try:  
    execution block  ##正常执行模块  
except A:  
    exc A block ##发生A错误时执行  
except B:  
    exc B block ##发生B错误时执行  
except:  
    other block ##发生除了A,B错误以外的其他错误时执行  
else:  
    if no exception, jump to here ##没有错误时执行  
finally:  
    final block  ##总是执行  


```

tips: 注意顺序不能乱，否则会有语法错误。如果用else就必须有except，否则会有语法错误。

```python
try:
    a = 1 / 2
    print(a)
    print(m) # 抛出NameError异常
    b = 1 / 0
    print(b)  
    c = 2 / 1
    print(c)
except NameError:
    print("Ops!!")  # 捕获到异常
except ZeroDivisionError:
    print("Wrong math!!")
except:
    print("Error")
else:
    print("No error! yeah!")
finally:      # 是否异常都执行该代码块
    print("Successfully!")
输出：

0.5
Ops!!
Successfully!

```


try语句终于搞清楚了! 那么可以继续with…as的探险了

3. with…as语句

with as 语句的结构如下：

```python
with expression [as variable]:  
    with-block  
```

看这个结构我们可以获取至少两点信息 1. as可以省略 2. 有一个句块要执行

![](https://img-blog.csdn.net/20180130173448179?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvcWlxaWNvcw==/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast) 

所谓上下文管理协议，其实是指with后面跟的expression。这个expression一般都是一个类的实体。这个类的实体里面要包含有对`__enter__`和`__exit__`函数的定义才行。

除了给类定义一些属性之外，还可以定义类的方法。也就是允许对类的内容有哪些操作，最直观的方法就是用dir()函数来看一个类的属性和方法。比如要查看字符串类有哪些属性和方法:

```python
dir(str)
['__add__', '__class__', '__contains__', '__delattr__', '__dir__', '__doc__', '__eq__', '__format__', '__ge__','__getattribute__', '__getitem__', '__getnewargs__', '__gt__', '__hash__', '__init__', '__init_subclass__', '__iter__', '__le__', '__len__', '__lt__', '__mod__', '__mul__', '__ne__', '__new__', '__reduce__', '__reduce_ex__', '__repr__', '__rmod__', '__rmul__', '__setattr__', '__sizeof__', '__str__', '__subclasshook__', 'capitalize', 'casefold', 'center', 'count', 'encode', 'endswith', 'expandtabs', 'find', 'format', 'format_map', 'index', 'isalnum', 'isalpha', 'isdecimal', 'isdigit', 'isidentifier', 'islower', 'isnumeric', 'isprintable', 'isspace', 'istitle', 'isupper', 'join', 'ljust', 'lower', 'lstrip', 'maketrans', 'partition', 'replace', 'rfind', 'rindex', 'rjust', 'rpartition', 'rsplit', 'rstrip', 'split', 'splitlines', 'startswith', 'strip', 'swapcase', 'title', 'translate', 'upper', 'zfill']

```

类，除了python内置的，当然还可以自己定义! 所以除了expression表示一些含有这两种方法的内置类，还可以自己定义类，让他们含有enter和exit方法。

可能大家一直奇怪，为什么有的方法，比如上图中的'split' 'title'什么的都没有下划线，而又有很多，，比如`__enter__`和`__exit__`要写下划线呢？

函数前单下划线

```
_XXX
```

此类函数只有类和子类能够访问调用，无法通过Import引入

函数前双下划线

```
__XXX
```

此类函数只有类对象本身能够访问

函数前后双下划线

```
__XXX__
```

此类函数为系统定义函数名，命名函数时尽量避免此类命名方式

对于变量前加下划线的解释请看https://www.cnblogs.com/Paul-watermelon/p/11165178.html

请参考博文http://blog.csdn.net/qiqicos/article/details/79208039

with…as语句执行顺序： 
–>首先执行expression里面的`__enter__`函数，它的返回值会赋给as后面的variable，想让它返回什么就返回什么，只要你知道怎么处理就可以了，如果不写as variable，返回值会被忽略。

–>然后，开始执行with-block中的语句，不论成功失败(比如发生异常、错误，设置sys.exit())，在with-block执行完成后，会执行expression中的`__exit__`函数。

当with...as语句中with-block被执行或者终止后，这个类对象应该做什么。如果这个码块执行成功，则exception_type,exception_val, trace的输入值都是null。如果码块出错了，就会变成像try/except/finally语句一样，exception_type, exception_val, trace 这三个值系统会分配值。

这个和try finally函数有什么关系呢？其实，这样的过程等价于：

```python
try:  
    执行 __enter__的内容  
    执行 with_block.  
finally:  
    执行 __exit__内容 
```

 那么`__enter__`和`__exit__`是怎么用的方法呢？我们直接来看一个栗子好了。 
程序无错的例子:

```python
class Sample(object):             # object类是所有类最终都会继承的类
    def __enter__(self):          # 类中函数第一个参数始终是self，表示创建的实例本身
        print("In __enter__()")
        return "Foo"
def __exit__(self, type, value, trace):
    print("In __exit__()")
    def get_sample():
    return Sample()

with get_sample() as sample:
    print("sample:", sample)
print(Sample)    # 这个表示类本身   <class '__main__.Sample'>
print(Sample())  # 这表示创建了一个匿名实例对象 <__main__.Sample object at 0x00000259369CF550>

```

输出结果：

```python
In __enter__()
sample: Foo
In __exit__()
<class '__main__.Sample'>
<__main__.Sample object at 0x00000226EC5AF550>

```

步骤分析: 
–> 调用`get_sample()`函数，返回Sample类的实例; 
–> 执行Sample类中的`__enter__()`方法，打印`"In__enter_()"`字符串，并将字符串`“Foo”`赋值给as后面的sample变量; 
–> 执行`with-block`码块，即打印`"sample: %s"`字符串，结果为`"sample: Foo" `
–> 执行`with-block`码块结束，返回`Sample`类，执行类方法`__exit__()`。因为在执行with-block码块时并没有错误返回，所以type,value,trace这三个arguments都没有值。直接打印`"In__exit__()"`

程序有错的例子：

    class Sample:
        def __enter__(self):
            return self
    def __exit__(self, type, value, trace):
        print("type:", type)
        print("value:", value)
        print("trace:", trace)
    
    def do_something(self):
        bar = 1 / 0
        return bar + 10
    with Sample() as sample:
        sample.do_something()



输出结果：

```python
type: <class 'ZeroDivisionError'>
value: division by zero
trace: <traceback object at 0x0000019B73153848>
Traceback (most recent call last):
  File "F:/机器学习/生物信息学/Code/first/hir.py", line 16, in <module>
    sample.do_something()
  File "F:/机器学习/生物信息学/Code/first/hir.py", line 11, in do_something
    bar = 1 / 0
ZeroDivisionError: division by zero
```



步骤分析: 
–> 实例化`Sample`类，执行类方法`__enter__()`，返回值self也就是实例自己赋值给sample。即sample是Sample的一个实例(对象); 
–>执行`with-block`码块: 实例`sample`调用方法`do_something()`; 
–>执行`do_something()`第一行` bar = 1 / 0`，发现`ZeroDivisionError`，直接结束`with-block`代码块运行 
–>执行类方法`__exit__()`，带入`ZeroDivisionError`的错误信息值，也就是`type,value, trace`，并打印它们。

————————————————
版权声明：本文为CSDN博主「Eden朱」的原创文章，遵循CC 4.0 BY-SA版权协议，转载请附上原文出处链接及本声明。
原文链接：https://blog.csdn.net/qiqicos/article/details/79200089