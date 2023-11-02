# 微服务

### 项目总结

```txt
基于mybatis plus对数据库进行增删改查，使用redis配置类与cacheable注解对访问频率较高的数据进行缓存。同时将验证码放在redis中进行登录验证，用nacos作为注册中心，gatway网关来做请求路由和访问权限控制。spring cloud feign组件实现各微服务之间的远程调用和负载均衡，
Spring cloud feign是轻量级restful的http服务器客户端，实现了ribbon做负载均衡，和hytrix做服务降级。
```



将单一的应用程序划分为一组服务，每个服务运行在独立的进程中

微服务模块

1建module

2 改POM 

3写YML

4主启动 

5业务类

<img src="06Spring%20Cloud.assets/image-20220506164419887.png" alt="image-20220506164419887" style="zoom: 67%;" />

![image-20220624210932818](06Spring%20Cloud.assets/image-20220624210932818.png)

###  服务端负载均衡

<img src="06Spring%20Cloud.assets/image-20220625101031463.png" alt="image-20220625101031463" style="zoom:50%;" />

### 本地负载均衡客户端

<img src="06Spring%20Cloud.assets/image-20220625101414715.png" alt="image-20220625101414715" style="zoom:50%;" />

<img src="06Spring%20Cloud.assets/image-20220507202553869.png" alt="image-20220507202553869" style="zoom: 50%;" />

# 配置中心读取github出错

<img src="06Spring%20Cloud.assets/image-20220508103122294.png" alt="image-20220508103122294" style="zoom:50%;" />

# springcloud alibaba

![image-20220508110952408](06Spring%20Cloud.assets/image-20220508110952408.png)

# Nacos

Nacos等价于Eureka+Config+Bus

# CAP

Consistency（一致性）、 Availability（可用性）、Partition tolerance（分区容错性），三者不可得兼

CP就是保次一致，但是不能用，只有等另外一个cp队友来了你才能吃饭，不然只能等着。

AP就是可用性，就是来了先吃着，不用等堵车的人。

# 熔断和降低

熔断就是达到错误的条件后就不能用了，然后经过一段时间会自动恢复

降级就是不能用后返回一个友好的提示。

<img src="06Spring%20Cloud.assets/image-20220625094441627.png" alt="image-20220625094441627" style="zoom:50%;" />

# Spring Boot 的核心配置文件有哪几个？它们的区别是什么？

applicaiton.yml是用户级的资源配置项 

bootstrap.yml是系统级的， 优先级更加高 

# 配置文件加载顺序

从上到下加载，

对于key不同，则直接生效；

对于key相同的同名配置项，后加载会覆盖掉前加载，故而最终为后加载的配置项生效

```
bootstrap.yaml
bootstrap.properties
bootstrap-{profile}.yaml
bootstrap-{profile}.properties
application.yaml
application.properties
application-{profile}.yaml
application-{profile}.properties
nacos配置中心共享配置（通过spring.cloud.nacos.config.shared-configs指定）
nacos配置中心扩展配置（通过spring.cloud.nacos.config.extension-configs指定）
Nacos配置中心该服务配置（通过spring.cloud.nacos.config.prefix和spring.cloud.nacos.config.file-extension指定）
Nacos配置中心该服务-{profile}配置（通过spring.cloud.nacos.config.prefix和spring.cloud.nacos.config.file-extension、以及spring.profiles.active指定）
```

https://blog.csdn.net/ctwy291314/article/details/129330381
https://blog.csdn.net/zyplanke/article/details/131101840

# spring spring cloud spring boot的区别

spring是一个java应用程序开发框架，主要功能是控制反转和依赖注入，可以开发一个松耦合的应用。

springboot通过自动配置和启动项来减少复杂的配置，快速开发spring应用，开箱即用。

spring cloud是一系列微服务框架的集合，如服务注册，配置中心，负载均衡，短路器都可以用springboot 开发风格一键启动。

springmvc是一个构建java web的框架，提供一种分离式方法开发web应用。

swagger是一个API接口文档工具。

