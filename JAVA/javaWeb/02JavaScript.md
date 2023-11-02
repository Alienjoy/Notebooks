# JavaScript

javaScript=ECMA+BOM+DOM

# ECMA客户端脚本语言的标准

JavaScript

**基本数据类型：**

1. number。数字小数，整数，NaN(假如一个不是数字的字符串转换为数字，则转换为NaN)
2. string。字符字符串
3. boolean。true，false
4. null，一个对象空的占位符
5. undefined，未定义，如果一个变量只声明了，但是没有初始化则是undefined

**引用数据类型**

1. 对象

变量：一小块存储数据的内存空间

js是弱类型，开辟变量存储空间是不指定数据类型

语法： var 变量名=变量值

### 运算符

**一元运算符**

```java
++,--
```

**算术运算符**

**赋值运算符**

**比较运算符**    > < >= <=

**逻辑运算法 **     && || !

### JavaScript基本对象

Function对象
Array 对象
Boolean 对象
Date 对象
Math 对象
Number 对象
String 对象
RegExp 对象，正则表达式对象
全局属性和函数

# BOM&DOM

### DOM文档对象模型document object model

<img src="/Users/zhangshuheng/Desktop/Notebooks/JAVA/javaWeb/02JavaScript.assets/image-20210812200008557.png" alt="image-20210812200008557" style="zoom:50%;" />

<img src="/Users/zhangshuheng/Desktop/Notebooks/JAVA/javaWeb/02JavaScript.assets/nodetree.gif" alt="DOM node tree"  />

通过标签的Id获取对象

document.getElementById("ID");

DOM分为核心DOM和HTML DOM 

1. **Document对象**

   1. 获取对象：window.document，或者是document
   2. 获取element对象方法：
      1. 获取元素对象getElementById，根据id值获取元素的对象
      2. getElementsByTagName，通过tag的名字获取元素对象的数组
      3. getElementsByClassName，通过className获取元素对象的数组
      4. getElementsByName，通过name这个属性来获取元素对象的数组

   3. 创建其他DOM对象
      1. createAttribute()，创建一个属性节点
      2. createComment() ，创建注释节点
      3. createElement() ，创建元素节点
      4. createTextNode()，创建文本节点。

2. **元素对象**

   1. 方法
      1. removeAttribute() ，从元素中删除指定的属性
      2. setAttribute()，设置或者改变元素属性。

3. **节点对象**

   1. CRUD DOM树
      1. appendChild()，把新的子节点添加到节点的子节点列表末尾。
      2. removeChild() ，删除子节点
      3. replaceChild()	替换子节点。

### BOM浏览器对象模型

浏览器对象

Window窗口对象

地址栏对象

历史记录对象

显示器屏幕对象

### HTML DOM

innerHTML 属性**设置**或**返回**表格行的开始和结束标签之间的 HTML。

追加HTML代码使用+=

### DOM事件

