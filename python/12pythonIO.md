# 1、IO操作

### 读操作，open语法

```python
file=open(文件名[,读写模式,编码格式UTF-8等])#中括号表示可选
如：
file=open('a.txt','r')
print(file.readlines())
file.read()
file2.write(file1.read())
file.close()#记得关闭文件的操作
```

| 读写模式 | 模式                                                         |
| -------- | ------------------------------------------------------------ |
| r        | 只读                                                         |
| w        | 只写                                                         |
| a        | add追加，如果没有则新建                                      |
| b        | 二进制格式读取或写入，例如对图片，mp3文件进行操作，不能单独使用，要用rb或则wb |
| +        | 以读写的方式打开文件，不能单独使用，需要与其他的模式一起使用，如a+ |

### 文件对象的常用方法

| 方法名                  | 说明                                                         |
| ----------------------- | ------------------------------------------------------------ |
| read([size])            | 读取size字节大小的内容，如果省略size则读取文本的全部内容     |
| readline()              | 从文本中读取一行文字，返回字符串对象                         |
| readlines()             | 把每行的文字都作为独立的字符串对象，存储到列表当中           |
| write(str)              | 将字符串str写入文本文件中                                    |
| seek(offset [, whence]) | 将文件指针移动到新的位置，正表示向后移动，负表示向前移动，其中一个汉字代表两个字符，所以跳过一个汉字offset写2<br />whence不同值代表不同的含义<br />0：从文件头开始计算（默认值）<br />1：从当前位置开始计算<br />2：从文件末尾开始计算 |
| tell()                  | 返回文件指针的当前位置                                       |
| flush()                 | 把缓冲区的内容写入文件，但不关闭文件                         |
| close()                 | 把缓冲区的内容写入文件，同时关闭文件，释放文件对象相关内容   |

### with。。。as 。。上下文管理器

```python
with open('a.txt','r') as file:#等价于file=open('a.txt','r')
	file.read()#则不需要考虑是否要关闭
```

一个类实现了`__enter__()` `__exit__()`则该类的对象遵循了上下文管理器