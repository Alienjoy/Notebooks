# 1、os模块和os.path模块

os模块与操作系统有关

![截屏2021-03-08 下午5.02.56.png](https://i.loli.net/2021/03/08/Wx2uOsErlPTmfGX.png)

![截屏2021-03-08 下午5.09.01.png](https://i.loli.net/2021/03/08/vsl4pRyumBEHPoX.png)

 ```python
import os
path=os.getcwd()
lst_file=os.walk(path)
print(lst_file)
for dirpath,dirnames,filenames in lst_file:

    for item1 in dirnames:
        print(os.path.join(dirpath, item1))#输出lst_file下的所有文件夹
    for item1 in filename:
        print(os.path.join(dirpath,item1))#输出lst_file下的所有文件
    print('-------------')
 ```

```python
#python可以同时为多个变量赋值
tuple1=((12,123),(32,34))
for item1,item2 in tuple1:
    print(item1)
    print(item2)
```

