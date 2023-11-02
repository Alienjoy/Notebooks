# Servlet（Server Applet）服务器小程序

1. 创建JavaEE项目
2. 定义一个类，实现Servlet接口
   - public class ServletDemo1 implements Servlet
   - [注意要导入servlet依赖jar包](https://liuyanzhao.com/5971.html)
3. 实现接口中的抽象方法
4. 配置Servlet

```
可以在注解中配置
在web.xml中配置：
	    <!--配置Servlet -->
	    <servlet>
	        <servlet-name>demo1</servlet-name>
	        <servlet-class>cn.itcast.web.servlet.ServletDemo1</servlet-class>
	    </servlet>
	
	    <servlet-mapping>
	        <servlet-name>demo1</servlet-name>
	        <url-pattern>/demo1</url-pattern>
	    </servlet-mapping>
```

# 声明周期

Servlet被创建会执行`init`	

被创建的时机：

1. 第一次被访问时，创建
    `<load-on-startup>`的值为负数
2. 在服务器启动时，创建
    `<load-on-startup>`的值为0或正整数

Servlet提供服务会执行`service`，在每次执行的时候都会被执行一次

Servelet被销毁的时候会执行`destroy`方法

# servlet3.0

 步骤：

1. 创建JavaEE项目，选择Servlet的版本3.0以上，可以不创建web.xml

2. 定义一个类，实现Servlet接口
3. 复写方法
4. 在类上使用@WebServlet注解，进行配置
   1. @WebServlet("资源路径也叫做虚拟目录")

# HttpServlet

1. 定义类继承HttpServlet
2. 重写doGet和doPost
