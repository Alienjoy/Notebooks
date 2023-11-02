# JSP

```jsp
//JSP是页面
<% java代码%>

//EL表达式，是JSP的内置对象
${键名.属性}

//jquery，是Java Script的框架，是动态效果
$("#submit-btn").click(function () {
}

//AJAX，加载部分网页内容
$.ajax()
```



JSP=java server pages叫做java服务器端页面

JSP本质上是一个Servlet，就是服务器端小程序

<img src="/Users/zhangshuheng/Desktop/Notebooks/JAVA/javaWeb/10JSP.assets/image-20210819145047917.png" alt="image-20210819145047917" style="zoom:50%;" />

Tomcat先把.jsp文件转为java文件，然后再把java文件编译为字节码文件.class 作为servlet，存放的目录在tomcat的work目录下。

jsp脚本，jsp定义java代码的方式。就是类似于public class ServletDemo1 implements Servlet

1. <%  java 代码%>定义的java代码，在service方法中。service(实现Servlet接口)方法中可以定义什么，该脚本中就可以定义什么。
2. <%!  java 代码%>定义的java代码，在jsp转换后的java类的成员位置。
3. <%=  java 代码%>定义的java代码，会输出到页面上。输出语句中可以定义什么，该脚本中就可以定义什么。

### jsp的内置对象

内置对象就是不需要创建就可以直接使用的对象。

1. requset
2. response
3. out对象，与response.getWriter()差不多。但是response.getWriter()会先于out输出。

# JSP

### 指令：

```JSP
<%--这种方法定义的java相当于是在Servelet接口中重写service方法中定义的--%>
<%
    System.out.println("hello jsp");
    int i=10;
%>
<%--这是定义成员变量和成员方法的地方--%>
<%!
    int i=5;
    int j=9;
%>
<%--这是用来在界面中输出的方法--%>
<%= i%>
<%= j%>
等价于response.getWriter().write(

<%@ 指令名称 属性名1=属性值1 属性名2=属性值2 ... %>
```



作用：用于配置JSP页面，导入资源文件
	* 格式：
		`<%@ 指令名称 属性名1=属性值1 属性名2=属性值2 ... %>`

* 指令名称分类：
  1. **page：配置JSP页面的**

    * contentType：等同于response.setContentType()
  
    	1. 设置响应体的mime类型以及字符集
    	2. 设置当前jsp页面的编码（只能是高级的IDE才能生效，如果使用低级工具，则需要设置pageEncoding属性设置当前页面的字符集）
    * import：导包
    * errorPage：当前页面发生异常后，会自动跳转到指定的错误页面
    * isErrorPage：标识当前也是是否是错误页面。
      1. true：是，可以使用内置对象exception
      2. false：否。默认值。不可以使用内置对象exception
  
  2. **include	： 页面包含的。导入页面的资源文件**
  
     `<%@include file="top.jsp"%>`
  
  3. **taglib	： 导入资源**
  
     `<%@ taglib prefix="c" uri="http://java.sun.com/jsp/jstl/core" %>`
  
     prefix：前缀，自定义的

### JSP内置对象

```
内置对象
	* 在jsp页面中不需要创建，直接使用的对象
	* 一共有9个：
			变量名					真实类型						作用
		* pageContext				PageContext					当前jsp页面共享数据，指的是当前页面的范围，还可以获取其他八个内置对象
		* request					HttpServletRequest			一次请求访问的多个资源(转发)
		* session					HttpSession					一次会话的多个请求间
		* application				ServletContext				所有用户间共享数据
		---------------前四个为域对象
		* response					HttpServletResponse			响应对象
		* page						Object						当前页面(Servlet)的对象  this
		* out						JspWriter					输出对象，数据输出到页面上
		* config					ServletConfig				Servlet的配置对象
		* exception					Throwable					异常对象
```

# mvc

- M：Model，模型。JavaBean
  - 完成具体的业务操作，如：查询数据库，封装对象

*  V：View，视图。JSP
	* 展示数据
* C：Controller，控制器。Servlet
  * 获取用户的输入
  * 调用模型
  * 将数据交给视图进行展示

# EL表达式Expression Language 表达式语言

语法：`${表达式}`，注意如果要忽略EL表达式的话使用`\${表达式}`

使用方法：

1. **运算**
   1. 算术运算符：+ - * / % div  mod
   2. 比较运算符：
   3. 逻辑运算符：
   4. 空运算符：
   
2. **获取值**
   
   **方式1**：${域名称.键名}：从指定域中获取指定键的值
   
   1. 域名称     							--->JSP内置对象
   2. pageScope				         --> page
   3. requestScope 	              --> request
   4. sessionScope 			       --> session
   5. applicationScope             --> application（ServletContext）
   6. pageContext：                 -- >pageContext   获取jsp其他八个内置对象       `${pageContext.request.contextPath}`动态获取虚拟目录
   
   **方式2**：${键名}：表示依次从最小的域中查找是否有该键对应的值，直到找到为止。
   
3. **获取对象、List集合、Map集合的值**

   	1. 对象：${域名称.键名.属性名}
   				* 本质上会去调用对象的getter方法
   	2. List集合：${域名称.键名[索引]}
   	3. Map集合：  
   		* ${域名称.键名.key名称}
   	  * ${域名称.键名["key名称"]}

4. **empty运算符**

   `${empty list}`判断字符串、集合、数组对象是否为null或者长度为0

   `${not empty str}`表示判断字符串、集合、数组对象是否不为null 并且 长度>0

5. **隐式对象**

   1. pageContext：获取jsp其他八个内置对象`${pageContext.request.contextPath}`动态获取虚拟目录

# JSTL

JavaServer Pages Tag Library  JSP标准标签库

作用：用于简化和替换jsp页面上的java代码

