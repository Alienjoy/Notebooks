# 1、类和对象

对象又叫做实例，python中一切皆对象

### 类的定义

类的组成：

- 类属性
- 实例方法
- 静态方法
- 类方法

```python
#类的创建
class Student:
    name = '张书恒'  # 直接写在类中的变量称为类属性，所有对象共用这个
    def __init__(self,age,score):
        self.age=age#供对象使用的变量
        self.score=score
    # 实例方法，在类之外定义的成为函数，在类之内称为方法。
    def eat(self):
        print('学生吃饭')

    # 静态方法
    @staticmethod
    def staticstudy():
        print('学生学习')

    # 类方法
    @classmethod
    def classdrink(cls):
        print('学生喝水')
stu=Student(10,90)

print(stu.age)
print(stu.score)

print(stu.eat())#或者
print(Student.eat(stu))
```

### 类属性

类属性：类中方法外的变量称为类属性（就是类中的定义的常量），被该类的所有对象共享

```python
#可以用类名来直接调用
Student.name
#也可以使用对象名来调用
stu.name
```

### 类方法

类方法的调用是使用类名来调用

```python
Student.classdrink()
```

### 静态方法

静态方法的使用也是通过类名来调用

```python
Student.staticstudy
```

### 动态绑定

可以对一个类的对象单独设置变量

```python
stu.gender='女'
#则stu1不可以使用stu1.gender
```

动态绑定方法

```python
def show():
  print('这是动态绑定的方法')
stu.show=show
stu.show()#就可以使用show方法了
```

# 2、面向对象的三大特征

封装，继承，多态

```java
//java继承：
public class 子类名 extends 父类名{

}

//java多态：父类名 对象名= new 子类名
```

### 封装

```python
class Student:
    def __init__(self,name,age):
        self.name=name
        self.__age=age#使用两个连续的下划线表示不希望在类的外部被使用
```

### 继承

```python
class 子类名(父类1名，父类2名，父类3名):
  pass
```

所有类默认继承object类，python可以**多继承**

```python
class Person(object):
    def __init__(self,name,age):
        self.name=name
        self.age=age
    def showInfo(self):
        print(self.name,self.age)
        
class Student(Person):
    def __init__(self,name,age,score):
        super().__init__(name,age)
        self.score=score
        
stu=Student('张三',18,99)
stu.showInfo()
```

**方法重写**

```python
class Student(Person):
    def __init__(self, name, age, score):
        super().__init__(name, age)
        self.score = score

    def showInfo(self):#方法重写
        print(self.name, self.age,self.score)
```

### object类

 直接`print(对象名)`相当于`print(对象名.__str__())`，重写了`__str__`方法

### 特殊属性和方法

| 特殊属性 | 名称                  | 作用                             |
| -------- | --------------------- | -------------------------------- |
|          | `类名.__dict__`       | 获得类对象属性和方法的字典       |
|          | `对象名.__dict__`     | 获取对象的属性（就是变量）的字典 |
|          | `对象名.__class__`    | 获得对象所属于的类               |
|          | `类名.__bases__`      | 获取类的父类                     |
|          | `类名.__mro__`        | 类的层次结构                     |
|          | `类名.__subclasses__` | 获取类的子类                     |

| 特殊方法 | 名称       | 作用                                                         |
| -------- | ---------- | ------------------------------------------------------------ |
|          | `__add__`  | 两个对象的`+`运算，其实就是调用了对象的`__add__`方法         |
|          | `__len__`  | 重写`__len__`方法，方法体为`len(self.name)`，就可以使用len(对象名) |
|          | `__new__`  | 用来创建对象                                                 |
|          | `__init__` | 用来对创建的对象初始化                                       |



### 类的赋值操作

```python
person1=Person()
person2=person1
#则只创建了一个对象，person1和person2都是指向同一个对象
```

### 浅拷贝，深拷贝

```python
#浅拷贝，只拷贝对象的内容，对象所包含的子对象不拷贝
computer1=Computer(cpu,disk)#cpu和disk都为对象

import copy
computer2=copy.copy(computer1)#只会拷贝comter1对象，不拷贝cpu和disk对象

#深拷贝，既拷贝对象的内容，又拷贝子对象的内容
import copy
computer3=copy.deepcopy(computer1)#拷贝comter1对象，也拷贝cpu和disk对象


```

