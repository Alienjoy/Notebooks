# Maven

## 依赖管理，就是用来管理jar文件的。

[安装Maven常见问题](https://www.cnblogs.com/momo-nancy/p/nancy_0688.html)，其实intellij中已经集成了maven

[maven修改镜像](https://blog.csdn.net/shuai_ge_feng/article/details/106043078?utm_medium=distribute.pc_aggpage_search_result.none-task-blog-2~aggregatepage~first_rank_ecpm_v1~rank_v31_ecpm-2-106043078.pc_agg_new_rank&utm_term=mac+idea如何更改maven映像&spm=1000.2123.3001.4430)

[配置IDEA自带maven的仓库映像(mac设置和window设置)阿里云镜像](https://blog.csdn.net/shuai_ge_feng/article/details/106043078?utm_medium=distribute.pc_aggpage_search_result.none-task-blog-2~aggregatepage~first_rank_ecpm_v1~rank_v31_ecpm-2-106043078.pc_agg_new_rank&utm_term=mac+idea%E5%A6%82%E4%BD%95%E6%9B%B4%E6%94%B9maven%E6%98%A0%E5%83%8F&spm=1000.2123.3001.4430)

## Maven 命令

```
mvn clean//清除编译的文件
mvn compile//编译主程序
mvn test//编译主程序和测试程序
mvn package//编译主程序和测试程序，并打包
mvn install//编译主程序和测试程序，并打包，并把包安装到本地仓库
mvn deploy//发布打包好的程序
```

## Maven概念模型图

![maven概念模型图](/Users/zhangshuheng/Desktop/Notebooks/JAVA/javaWeb/16Maven.assets/maven概念模型图.png)

当pom.xml中报错的话可以通过刷新来解决。



![img](/Users/zhangshuheng/Desktop/Notebooks/JAVA/javaWeb/16Maven.assets/v2-6cb2ccedfa1b45f77ac75bd53fae00cc_1440w.jpg)

## maven使用tomcat中遇到的问题

为项目配置服务器

<img src="/Users/zhangshuheng/Desktop/Notebooks/JAVA/javaWeb/16Maven.assets/截屏2021-09-21 下午9.56.10.png" style="zoom:50%;" />

**maven使用tomcat要添加tomcat的插件，tomcat6不支持jdk1.8版本**

路径在`/Users/zhangshuheng/.m2/repository/org/apache/tomcat/maven/tomcat7-maven-plugin`

<img src="/Users/zhangshuheng/Desktop/Notebooks/JAVA/javaWeb/16Maven.assets/截屏2021-09-21 下午9.59.53.png" style="zoom:50%;" />

## 使用动态模板，快速输入代码

<img src="/Users/zhangshuheng/Desktop/Notebooks/JAVA/javaWeb/16Maven.assets/截屏2021-09-21 下午10.16.04.png" style="zoom:50%;" />

然后在代码编辑页面输入tomcat7就会自动生成模板文字