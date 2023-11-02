# 会话技术

会话技术是在一次会话的多次请求间共享数据，就是保存cookies，把你的数据记录下来。

会话技术：

- 在客户端会话技术Cookie，就是将数据保存到客户端。例如记住密码
- 在服务器端会话技术Session

Cookie底层也是使用HTTP实现的，原理是使用请求头的`Set-Cookie: userName=zhangshuheng`和响应头的`Cookie: userName=zhangshuheng; Idea-e2250cda=8d4559d4-7c22-42bc-b031-7ac731cd62b6`来实现的。

### Cookie

使用步骤（服务器端创建和使用）：

1. 创建Cookie对象，并绑定数据
   - 使用Cookie类的构造方法`Cookie(String name, String value)`创建Cookie对象并绑定数据
2. 发送Cookie对象给浏览器
   - 在Response对象中使用`void addCookie(Cookie cookie)`，发送Cookie对象给浏览器
3. 接收浏览器发过来的Cookie对象，获取数据
   - 在request对象中使用`Cookie[] getCookies()`方法获取Cookies
4. 设置Cookie对象的生命周期（cookie对象调用）
   - `void setMaxAge(int maxAge)`，maxAge为正数表示存储的秒数，负数表示默认值是关闭浏览器则被销毁，0表示删除cookie
5. 默认多个web项目之间是不能共享cookie的，注意是多个项目（意思就是多个虚拟目录之间，就是一个tomcat下的多个servlet之间）
   1. 想要多个目录共享cookie则可以设置`setPath("/")`表示共享目录为整个项目的根目录，默认是`setPath("/project1")`

作用：

1. cookie一般用于存出少量的不太敏感的数据
2. 在不登录的情況下，完成服务器对客户端的身份识别

3. 

# Session

Session是服务器会话技术，是保存在服务器端的对象中。是在**一次会话**中共享数据

 	1. 获取HttpSession对象：
 	  	1. HttpSession session = request.getSession();
 	2. 使用HttpSession对象：
 	  	1. Object getAttribute(String name) 
 	  	2. 
 	      void setAttribute(String name, Object value)
 	  	3. void removeAttribute(String name)  

实现原理：

是根据cookie中的JSESSIONID的值来确定session的。如果cookie中没有JSESSIONID则会创建一个新的Session对象。

<img src="/Users/zhangshuheng/Desktop/Notebooks/JAVA/javaWeb/09Cookie&session.assets/image-20210819161907911.png" alt="image-20210819161907911" style="zoom:50%;" />

### 持久化存储Session

给cookie设置JSESSIONID并设置setMaxAge(60*60)则可以持久化保存cookie，则就相当于持久化保存了Session

客户端不关闭，服务器关闭后，两次获取的session是同一个吗？

答：不是同一个，但是要确保数据不丢失。tomcat自动完成以下工作
   * session的钝化：
     			* 在服务器正常关闭之前，将session对象序列化到硬盘上
*  session的活化：
  * 在服务器启动后，将session文件转化为内存中的session对象即可。

### session什么时候被销毁？
		1. 服务器关闭
		2. session对象调用invalidate() 。
		3. session默认失效时间 30分钟
			选择性配置修改	
			<session-config>
		        <session-timeout>30</session-timeout>
		    </session-config>

