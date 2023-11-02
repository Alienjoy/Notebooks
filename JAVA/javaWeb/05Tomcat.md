- 

# Tomcat

[安装tomcat](https://blog.csdn.net/qq_35106903/article/details/78860121)

部署项目三种方法：

1. 将项目打包成一个war包，导入到webapps目录下，它会自动解压，同时删除的时候只需要删除war文件就可以，会自动删除解压好的文件夹。
2. 配置conf/server.xml文件在`<Host>`标签体中配置`<Context docBase="D:\hello" path="/hehe" />`，其中docBase:项目存放的路径 path：虚拟目录
3. 在`conf\Catalina\localhost`创建任意名称的xml文件。在文件中编写`<Context docBase="D:\hello" />`虚拟目录：xml文件的名称

java动态项目的目录结构：

- 项目的根目录
  - WEB-INF目录：
    -  web.xml：web项目的核心配置文件
    - classes目录：放置字节码文件的目录
    - lib目录：放置依赖的jar包(tomcat真懒，只会在自己web inf 下面的lib目录里找jar包)

### intellij 创建JavaWeb

1. [新建JavaWeb项目](https://blog.csdn.net/MinggeQingchun/article/details/112037693)
2. 配置运行环境

![截屏2021-08-16 下午4.11.07](/Users/zhangshuheng/Desktop/Notebooks/JAVA/javaWeb/05Tomcat.assets/截屏2021-08-16 下午4.11.07.png)

![截屏2021-08-16 下午4.12.14](/Users/zhangshuheng/Desktop/Notebooks/JAVA/javaWeb/05Tomcat.assets/截屏2021-08-16 下午4.12.14.png)

![截屏2021-08-16 下午4.14.26](/Users/zhangshuheng/Desktop/Notebooks/JAVA/javaWeb/05Tomcat.assets/截屏2021-08-16 下午4.14.26.png)

# Tomcat部署

1. 把项目out目录下的artifacts文件夹下的文件压缩成一个zip压缩包，然后改后缀名为war，注意不要把整个文件夹压缩成一个压缩包

<img src="/Users/zhangshuheng/Desktop/Notebooks/JAVA/javaWeb/05Tomcat.assets/截屏2021-08-19 下午9.14.09.png" style="zoom:50%;" />

2. 把war文件拷贝到tomcat安装目录下的webapps文件夹下，war文件的文件名就是虚拟目录
3. 在tomcat/bin文件夹下打开终端执行`sudo sh startup.sh`开启tomcat
4. 在浏览器中输入localhost:8080/war文件名/servlet名进行访问
5. 关闭tomcat的方法是`sudo sh shutdown.sh`
6. 注：tomcat/work文件夹是tomcat运行过程中产生的数据保存的文件夹。

