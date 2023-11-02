# Servlet HTTP

Hyper Text Tansfer Protocol超文本传输协议

基于TCP/IP默认端口号是80，是基于请求响应模型的。每次请求之间是相互独立的不能相互通信。

### 请求消息数据格式

1. 请求行

   1. 格式

      - 请求方式 请求url 请求协议/版本

      - GET /login.html	HTTP/1.1

   2. GET：

      - **请求参数**（?name=zhangsan）在请求行中，在url后。

   3. POST：

      - 请求参数在**请求体**中

2. 请求头（键值对）

   1. 请求头名称: 请求头值

3. 请求空行

   1. 空行，就是用于分割POST请求的请求头，和请求体的。

4. 请求体

   1. 封装POST**请求消息**的**请求参数**（请求参数=参数值，name=zhangsan）

```java
字符串格式：
//请求行
POST /servlet/login.html?name=zhangsan	HTTP/1.1  
//请求头
Host: localhost
User-Agent: Mozilla/5.0 (Windows NT 6.1; Win64; x64; rv:60.0) Gecko/20100101 Firefox/60.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,*/*;q=0.8
Accept-Language: zh-CN,zh;q=0.8,zh-TW;q=0.7,zh-HK;q=0.5,en-US;q=0.3,en;q=0.2
Accept-Encoding: gzip, deflate
Referer: http://localhost/login.html
Connection: keep-alive
Upgrade-Insecure-Requests: 1
//请求空行

//请求体
username=zhangsan	
```

### Request对象

1. request对象和response对象的原理
	1. request和response对象是由服务器创建的。我们来使用它们
	2. **request**对象是来**获取**请求消息，**response**对象是来**设置**响应消息
2. 继承体系

```
	ServletRequest		--	父接口
		|	子接口继承了父接口
	HttpServletRequest	-- 子接口
		|	tomcat类实现了子接口
	org.apache.catalina.connector.RequestFacade 类(tomcat)
```

3. 获取请求数据（POST /servlet/login.html?name=zhangsan	HTTP/1.1）

   1. **获取请求行数据**

      1. 获取请求方式（get或者post）` String getMethod()`
      2. **获取请求URI**（/servlet/login.htm）`String getRequestURI()`
      3. 获取请求URL（http://localhost:8080/servelet/login.html）`StringBuffer getRequestURL()`
      4. 获取虚拟目录（/servlet）`String getContextPath()`
      5. **获取servelet路径**（/login.html）`String getServeletPath()`
      6. 获取get方式的请求参数（?name=zhangsan）`String getQueryString()`
      7. 获取传输协议（HTTP/1.1）`String getProtocol()`
      8. 获取客户机的ip地址`String getRemoteAddr()`

   2. **获取请求头数据**

      1. 通过请求头的名称获取请求头的值`String getHeader(String name)`

         ```
         //user-agent和referer是比较重要的两个请求头
         user-agent:Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/605.1.15 (KHTML, like Gecko) Version/14.0.1 Safari/605.1.15
         referer:http://localhost:8080/servlet/login.html
         ```

      2. 获取所有的请求头名称`Enumeration<String> getHeaderNames()`  可以把Enumeration当作迭代器使用。

   3. **获取请求体数据**(只对POST方式生效，注意都是request对象)

      1. 获取输入流对象

         1. 对于表单等文字的数据使用，获取字符输入流`BufferedReader getReader() throws IOException`

            `userName=zhangsan&password=312312`

         2. 对于文件等数据使用，获取字节输入流`ServletInputStream getInputStream() throws IOException`

      2. 得到输入流对象后利用read或者readline方法读取数据

4. 其他方法

   ```
   request.getParameter()获取的是客户端设置的数据。就是获取页面发过来的数据。叫做请求。永远返回字符串，就是页面的输入信息。
   request.getAttribute()获取的是服务器设置的数据。 获取请求转发的数据，就是其他的java页面转发过来的数据。叫做共享数据。返回值是任意类型
   request.setAttribute(String name,Object o)用来设置共享数据。
   
   
   ```
   
   
   
   1. **获取请求参数通用方法**（可以写在doGet和doPost任一方法中）好处是doGet和doPost中方法都一样，只需要写一份方法就可以，在doPost中写`this.doGet(request,response)`
      1. `String getParameter(String name)`根据**请求参数**获取**参数值**例如getParameter("userName")则返回输入的用户名
      2. `String[] getParameterValues(String name)`根据**请求参数**获取**参数值数组**，主要是针对于多选框`hobby=readding&hobby=music`
      3. `Enumeration<String> getParameterNames()`获取所有**请求参数**的名称
      4. `Map<String,String[]> getParameterMap()`获取所有请求参数的**键值对map集合**
   2. **请求转发**(就是调用其他的程序)
      1. 通过request对象的方法获取请求转发的对象`RequestDispatcher getRequestDispatcher(String path)`
      2. 通过RequestDispatcher对象的方法`void forward(ServletRequest request,ServletResponse response)`来进行转发
      3. 特点：
         1. 浏览器地址没有发生变化
         2. 只能调用当前服务器内部资源（就是说只能调用当前project的文件）
         3. 转发是一次请求。
   3. **共享数据**（也就是在请求转发的时候传递参数）就是就转发的时候传递数据，重定向相当于两次请求。
      - 域对象：就是一个有作用域的对象
      - request这个对象的域，是一次请求的范围
      - request对象共享数据的方法
        1. `public void setAttribute(String name,Object o)`用来设置共享数据。String name,Object o为键值对
        2. `public Object getAttribute(String name)` 根据键获取值
        3. `removeAttribute(String name)`移除键值对。
   4. **获取ServletContext对象**。见下一个markdown
      1. `ServletContext getServletContext()`方法可以获取ServletContext对象

### BeanUtils

BeanUtils是一个工具类，用来简化数据的封装（把从response中get到的各种数据封装成一个对象）

使用BeanUtils工具类需要导包`commons-logging-1.2.jar`和`commons-beanutils-1.9.4.jar`

使用方法

```
Map<String, String[]> userMap = request.getParameterMap();
User userObj = new User();
try {
	BeanUtils.populate(userObj,userMap);//使用BeanUtils的静态方法
} catch (IllegalAccessException e) {
	e.printStackTrace();
} catch (InvocationTargetException e) {
	e.printStackTrace();
}
```

JavaBean是标准的Java类

完整方法：

BeanUtils.populate( Object bean, Map properties )，

这个方法会遍历map<key, value>中的key，如果bean中有这个属性，就把这个key对应的value值赋给bean的属性。

