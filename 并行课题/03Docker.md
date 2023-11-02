### 2、docker拉取tomcat镜像并运行

```shell
docker search tomcat#docker查询镜像
docker pull tomcat:8.5.76
docker pull tomcat#docker拉取镜像
docker images         #查看本地已有镜像
docker ps             #查看本地正在运行的容器
docker ps -a          #查看本地所有的容器
#运行tomcat镜像
docker run --name tomcat -p 80:8080 -v /usr/local/tomcat/uploads:/usr/local/tomcat/uploads -d tomcat:8.5.76
#--name：容器名   -p:端口映射，将容器中tomcat的8080映射到linux的8088端口  -d 后台运行
# $PWD/test:/usr/local/tomcat/webapps/test 表示将当前目录下的test文件夹映射到容器tomcat的webapps文件夹下
#最后的tomcat表示镜像的名字，一个镜像可以生成多个容器靠--name tomcat1区分

#如果没有映射文件夹可以
docker cp ROOT.war tomcat:/usr/local/tomcat/webapps/
#查看日志
docker logs tomcat#其中tomcat为容器的的名字
#在容器中运行shell
docker exec -it tomcat bash

#退出tomcat容器
exit
#运行现有的容器
docker start tomcat
#停止现有的容器
docker stop tomcat
#在本地发送http请求
curl http://www.example.com 
https://zhuanlan.zhihu.com/p/71888942
# linux 查找文件
https://m.php.cn/article/475644.html
#查看docker日志
docker logs 容器名
#查看容器局域网ip
docker inspect tomcat
#docker安装的tomcat默认webapps下是空的，所以会404
https://blog.csdn.net/qq_40891009/article/details/103898876

```

### 3、docker安装mysql

https://www.runoob.com/docker/docker-install-mysql.html

```shell
#1
docker pull mysql:latest
docker run -itd --name mysql -p 3306:3306 -e MYSQL_ROOT_PASSWORD=root1423 mysql
#参数说明：

#-p 3306:3306 ：映射容器服务的 3306 端口到宿主机的 3306 端口，外部主机可以直接通过 宿主机ip:3306 访问到 MySQL 的服务。
#MYSQL_ROOT_PASSWORD=123456：设置 MySQL 服务 root 用户的密码。
#2、
docker exec -it mysql bash
#3、导入数据
docker cp blog.sql mysql:/root
```

### 4、docker安装redis

```shell
docker run -itd --name redis -p 6379:6379 redis#配置容器并启动
docker exec -it redis /bin/bash#进入docker

```



```
我们通过 docker 的两个参数 -i -t，让 docker 运行的容器实现"对话"的能力：

runoob@runoob:~$ docker run -i -t ubuntu:15.10 /bin/bash
root@0123ce188bd8:/#

各个参数解析：
-t: 在新容器内指定一个伪终端或终端。
-i: 允许你对容器内的标准输入 (STDIN) 进行交互。
注意第二行 root@0123ce188bd8:/#，此时我们已进入一个 ubuntu15.10 系统的容器
我们尝试在容器中运行命令 cat /proc/version和ls分别查看当前系统的版本信息和当前目录下的文件列表

root@0123ce188bd8:/#  cat /proc/version
Linux version 4.4.0-151-generic (buildd@lgw01-amd64-043) (gcc version 5.4.0 20160609 (Ubuntu 5.4.0-6ubuntu1~16.04.10) ) #178-Ubuntu SMP Tue Jun 11 08:30:22 UTC 2019
root@0123ce188bd8:/# ls
bin  boot  dev  etc  home  lib  lib64  media  mnt  opt  proc  root  run  sbin  srv  sys  tmp  usr  var
root@0123ce188bd8:/# 
```

