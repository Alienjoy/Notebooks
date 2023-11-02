# 1、Mac安装git

1. 使用homebrew安装git
   ```shell
   brew install git
   ```

2. 查看git是否安装成功及版本号
   ```shell
   git --version
   ```

# 2、本地配置ssh key

1. 生成ssh key

   ```shell
   ssh-keygen -t rsa -C "zhangshuheng@yahoo.com"
   ```

   生成不同的名称的key

   https://www.cnblogs.com/Laoevil/p/16220880.html

2. 查看生成的key，并复制

   ```shell
   cat ~/.ssh/id_rsa.pub
   ```

3. 将复制到的key添加到github

   ![image-20220726135620076](02Git%E6%95%99%E7%A8%8B.assets/image-20220726135620076.png)

4. 设置username和email，因为GitHub每次commit都会记录它们

   ```shell
   git config --global user.name "Alienjoy"
   git config --global user.email "zhangshuheng@yahoo.com"
   git config --global --list
   ```

5. 查看是否配置成功

   ```shell
   ssh -T git@github.com
   ```

# 3、git的基本使用

1. 新建git 

   ```shell
   git init
   ls -a
   ```

2. 将当前目录所有文件添加到git暂存区

   ```shell
   git add . 
   ```

3. 提交并备注提交信息

   ```shell
   git commit -m "my first commit" 
   ```

4. 进入要上传的仓库，添加远程地址

   ```shell
   git remote add origin git@github.com:Alienjoy/blog.git
   ```

5. 提交代码到master分支

   ```shell
   git push origin master
   ```

