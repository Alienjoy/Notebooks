# Filter

创建Filter的模板

<img src="/Users/zhangshuheng/Desktop/Notebooks/JAVA/javaWeb/11Filter.assets/image-20210916212033327.png" alt="image-20210916212033327" style="zoom:50%;" />过滤器

```
//放行前使用的是servletRequest
filterChain.doFilter(servletRequest,servletResponse);//放行
//放行后使用的是servletResponse
```

init方法生命周期：在服务器启动时会创建Filter对象。此方法会被执行

doFilter生命周期：每一次执行"被拦截资源"时执行，执行完被拦截资源后会放行，放行后接着执行之后的代码。

destory方法生命周期：在服务器关闭后，销毁Filter对象。此方法会被执行

## 过滤器配置

### 拦截路径配置

具体资源路径，如`/index.jsp`

拦截目录，如`/user/*`，注意这个`/user`是在servlet中配置的`@WebServlet("/user/servletDemo1")`

后缀名拦截，如`*.jsp`

拦截所有资源，如`/*`

### 拦截方式配置

拦截方式：资源被访问的方式

- 注解配置：设置dispatcherTypes属性`@WebFilter(value = "/*",dispatcherTypes = DispatcherType.FORWARD)`
  - REQUEST：默认值。浏览器直接请求资源
  - FORWARD：转发访问资源
  - INCLUDE：包含访问资源
  - ERROR：错误跳转资源
  - ASYNC: 异步访问资源

## 过滤器链

使用多个过滤器，过滤器的顺序是按照过滤器名来自动排序

## 设计模式

见代码

# 监听器

