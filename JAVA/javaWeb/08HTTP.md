# http响应消息

### 响应消息数据格式

1. 响应行

   1. 格式

      - 协议/版本 响应状态码 状态码描述

      - HTTP/1.1 200 ok
      - 响应状态码
        1. 1xx：服务器接收客户端消息，但是没有接收完成。会给客户端发一个1xx
        2. 2xx：代表成功
        3. 3xx：302代表重定向，304代表访问缓存
        4. 4xx：客户端错误，404代表请求路径没有对应的资源
        5. 5xx：服务器端错误，500服务器出现异常。

2. 响应头（键值对）

   1. 头名称: 值
   2. Content-Type是数据格式和编码格式
   3. Content-disposition：服务器告诉客户端以什么格式打开响应体数据
      - in-line：默认值,在当前页面内打开
      - attachment;filename=xxx：以附件形式打开响应体。文件下载

3. 响应空行

   1. 空行

4. 响应体

```java
HTTP/1.1 200 ok
Date: Tue, 17 Aug 2021 12:28:41 GMT
Accept-Ranges: bytes
ETag: W/"500-1629173461559"
Last-Modified: Tue, 17 Aug 2021 04:11:01 GMT
Content-Type: text/html;charset=utf-8
Content-Length: 500
X-DNS-Prefetch-Control: off

<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>张书恒的首页</title>
</head>
<body>
<form action="ServletDemo3" method="post">
    <input type="text" placeholder="请输入姓名" name="userName"><br>
    <input type="text" placeholder="请输入密码" name="password"><br>
    <input type="checkbox" name="hobby" value="music">音乐
    <input type="checkbox" name="hobby" value="game">游戏<br>
    <input type="submit" value="注册">
</form>
</body>
</html>
```

# Response对象

Response对象功能：设置响应消息
1. 设置响应行
	1. 格式：HTTP/1.1 200 ok
	2. 设置状态码：setStatus(int sc) 
2. 设置响应头：setHeader(String name, String value) 
	
3. 设置响应体：
	* 使用步骤：
		1. 获取输出流
			* 字符输出流：PrintWriter getWriter()

			* 字节输出流：ServletOutputStream getOutputStream()

		2. 使用输出流，将数据输出到客户端浏览器

### 重定向（我后台干完活后回到前台）

```
//重定向的方法
response.sendRedirect("/project1/servletResponse2");
//转发的方法
request.getRequestDispatcher("/servletResponse2").forward(request,response);

```

### 转发和重定向的区别

[转发和重定向的区别](https://pan.baidu.com/play/video#/video?path=%2F%E5%BC%A0%E4%B9%A6%E6%81%92%2F%E5%B0%9A%E7%A1%85%E8%B0%B7Java%E5%AD%A6%E7%A7%91%E5%85%A8%E5%A5%97%E6%95%99%E7%A8%8B%EF%BC%88%E6%80%BB207.77GB%EF%BC%89%2F2.%E5%B0%9A%E7%A1%85%E8%B0%B7%E5%85%A8%E5%A5%97JAVA%E6%95%99%E7%A8%8B--%E5%BE%AE%E6%9C%8D%E5%8A%A1%E6%A0%B8%E5%BF%83%EF%BC%8846.39GB%EF%BC%89%2F2.%E5%B0%9A%E7%A1%85%E8%B0%B72021%E5%85%A8%E6%96%B0SpringMVC%E6%95%99%E7%A8%8B%2F%E8%A7%86%E9%A2%91%2F46_%E5%B0%9A%E7%A1%85%E8%B0%B7_SpringMVC_SpringMVC%E8%A7%86%E5%9B%BE%EF%BC%9ARedirectView.mp4&t=46)

请求转发的地址不会改动，始终是刚开始的地址, 请求重定向在跳转后，地址栏会变为目标地址

请求转发是一次请求，跳转操作在服务器内部发生；请求重定向是两次请求，跳转操作是在浏览器与服务器之间发生

请求**转发**可以使用 request.setAttribute 进行值的传，request.forward()；请求重定向需要使用 session.setAttribute 进行值的传递，因为如果用request的话，是两次请求，第一次请求的数据就没了

1. 重定向的特点：redirect
      1. 地址栏发生变化
      2. 重定向可以访问其他站点(服务器)的资源
      3. 重定向是两次请求。不能使用request对象来共享数据，如果要共享数据的话使用session

<img src="/Users/zhangshuheng/Desktop/Notebooks/JAVA/javaWeb/08HTTP.assets/image-20210818101338584.png" alt="image-20210818101338584" style="zoom:50%;" />

   1. 转发的特点：forward
         1. 转发地址栏路径不变
         2. 转发只能访问当前服务器下的资源
         3. 转发是一次请求，可以使用request对象(不是cookie也不是session)setAttribute方法来共享数据

<img src="/Users/zhangshuheng/Desktop/Notebooks/JAVA/javaWeb/08HTTP.assets/image-20210818101516146.png" alt="image-20210818101516146" style="zoom:50%;" />

### 路径写法

1. 相对路径：通过相对路径不可以确定唯一资源
				* 如：`./index.html`
				* 不以`/`开头，以`.`开头路径
				* 规则：找到当前资源和目标资源之间的相对位置关系
				   * `./ `：表示当前目录，**可以省略，就是说直接写目录表示相对路径**
				  * `../`：后退一级目录
	
2. 绝对路径：通过绝对路径可以确定唯一资源
  * 如：`http://localhost/day15/responseDemo2` 简写`/day15/responseDemo2`
  * 以`/`开头的路径

  * 规则：判断定义的路径是给谁用的？判断请求将来从哪儿发出
    		* 路径给客户端使用的话（重定向）：**需要加虚拟目录**(就是完整的路径，因为重定向可以访问其他站点(服务器)的资源，就要写全资源的访问路径`/day15/responseDemo2`)
        			* 建议虚拟目录动态获取：

  		  ```
  		  String contextPath = request.getContextPath();//获取虚拟目录
  		  response.sendRedirect(contextPath+"/servletResponse2");//拼接在一起构成重定向的绝对路径
  		  ```
  		
  		* <a> , <form> 重定向...
  		
  	* 路径给服务器使用的话（转发）：**不需要加虚拟目录**，(例如上面的例子就直接写`/responseDemo2`)
  		* 转发路径
  		* @WebServlet("/servletResponse3")，WebServlet注解使用的也是绝对路径，是省略了虚拟目录的绝对路径

### 字符输出流

步骤：

1. 设置中文编码

   ```
   response.setContentType("text/html;charset=utf-8");
   ```

2. 获取字符输出流并输出数据

   ```
   response.getWriter().write("<h1>字符输出流也可以输出的字符会被浏览器解析，相当于输出了html文档的内容</h1>");
   ```

### 字节输出流

步骤：

1. 设置中文编码

   ```
   response.setContentType("text/html;charset=utf-8");
   ```

2. 获取字节输出流并输出数据

   ```
   response.getOutputStream().write("这是使用字节输出流输出的数据".getBytes());
   ```

   

### ServletContext

 概念：代表整个web应用，可以和程序的容器(服务器)来通信
1. 获取ServletContext对象：

   1. 通过request对象获取`request.getServletContext();`
   2. 通过HttpServlet获取`this.getServletContext();`

2. **ServletContext对象的功能**：

3. 获取MIME类型

      1. MIME类型格式   大类型/小类型 如text/html image/jpeg
          2. 方法：`String getMimeType(String file)`就是使用`ServletContext对象.getMimeType(html)`会返回text/html

4. 域对象：共享数据（下面是域对象的都有的通用方法）


- setAttribute(String name,Object value)

- getAttribute(String name)

- removeAttribute(String name)作用域是所有用户，不建议使用。

1. 获取文件的真实（服务器）路径

      1. 方法：String getRealPath(String path)

      ```
      String b = context.getRealPath("/b.txt");//web目录下资源访问
      System.out.println(b);
      
      String c = context.getRealPath("/WEB-INF/c.txt");//WEB-INF目录下的资源访问
      System.out.println(c);
      
      String a = context.getRealPath("/WEB-INF/classes/a.txt");
      //src目录下的资源访问,src路径下的文件会被部署到/WEB-INF/classes目录，classloader只能获取src目录下的
      System.out.println(a);
      ```

      

# 四大域对象分别是  

PageContext（PageContextImpl类） 当前jsp页面范围内有效

request（HttpServletRequest类）      一次请求内有效

session（HttpSession类）                 一整个会话中都有效（打开浏览器到浏览器关闭）

applicantion（ServletContext类） 整个web工程范围内都有效（web工程不停止，数据都在）
