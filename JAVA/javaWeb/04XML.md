# XML可扩展标记语言

```xml
<?xml version="1.0" encoding="utf-8" ?>
<users>
    <user id="1">
        <name>张书恒</name>
        <age>25</age>
    </user>
    <user id="2">
        <name>张书校</name>
        <age>20</age>
    </user>
</users>
```

encoding 是告诉浏览器的编码

文本加入要以原本的形式显示（就是不需要转义字符的话）需要使用Cdata区，CDATA 格式为 `"<![CDATA[文本]]>"` 

属性id值唯一，上述代码中的id并不是代表id，它是自定义的标签

### 约束

约束：规定xml文档的书写规则
分类：

1. DTD:一种简单的约束技术
2. Schema:一种复杂的约束技术    **XML Schema Definition，XSD**

使用方式见代码

# 2、解析

解析：操作xml文档，将文档中的数据读取到内存中

操作xml文档
1. 解析(读取)：将文档中的数据读取到内存中
2. 写入：将内存中的数据保存到xml文档中。持久化的存储

解析xml的方式：
 	1. DOM：将标记语言文档一次性加载进内存，在内存中形成一颗dom树
     - 优点：操作方便，可以对文档进行CRUD的所有操作
     - 缺点：占内存
	2. SAX：逐行读取，基于事件驱动的。
    - 优点：不占内存。
        - 缺点：只能读取，不能增删改

### xml常见的解析器：

1. JAXP：sun公司提供的解析器，支持**dom**和**sax**两种思想

2. DOM4J：一款非常优秀的解析器**DOM**
3. Jsoup：jsoup 是一款Java 的HTML解析器（是用来解析html，但是也可以解析xml），可直接解析某个URL地址、HTML文本内容。它提供了一套非常省力的API，可通过**DOM**，CSS以及类似于jQuery的操作方法来取出和操作数据。
4. PULL：Android操作系统内置的解析器，sax方式的。

# JSoup快速入门：

https://www.jianshu.com/p/a4b5da6f60c9

步骤：
	1. 导入jar包
	2. 获取Document对象
	3. 获取对应的标签Element对象
	4. 获取数据

其中：

- Jsoup：是一个工具类，使用静态方法parse可以解析html或xml文档，返回Document

  - 可以解析本地和网络的xml和html文档，可以开发爬虫小程序

- Document：是一个文档对象。代表内存中的dom树，可以使用getElementsByTag等方法获取Elements对象

  - getElementById(String id)：根据id属性值获取唯一的element对象
  - getElementsByTag(String tagName)：根据标签名称获取元素对象集合
  -  getElementsByAttribute(String key)：根据属性名称获取元素对象集合
  -  getElementsByAttributeValue(String key, String value)：根据对应的属性名和属性值获取元素对象集合

- Elements：元素Element对象的集合。可以当做` ArrayList<Element>`来使用

  1. 获取子元素对象
     - getElementById(String id)：根据id属性值获取唯一的element对象
     - getElementsByTag(String tagName)：根据标签名称获取元素对象集合
     - getElementsByAttribute(String key)：根据属性名称获取元素对象集合
     - getElementsByAttributeValue(String key, String value)：根据对应的属性名和属性值获取元素对象集合

  2. 获取属性值
     - String attr(String key)：根据属性名称获取属性值
  3. 获取文本内容
     * String text():获取文本内容
     * String html():获取标签体的所有内容(包括字标签的字符串内容)

- Node：节点对象

  - 是Document和Element的父类

  ### 快捷查询

  1. selector:选择器
     1. 使用的方法：Elements	select(String cssQuery)
     2. 语法：参考Selector类中定义的语法https://www.javadoc.io/doc/org.jsoup/jsoup/latest/org/jsoup/select/Selector.html
  2. XPath
     1. 使用方法
     2. 语法https://www.w3cschool.cn/xpath/xpath-syntax.html