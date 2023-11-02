# 1、导入模块（.py文件）

```python
import 模块名 [as 别名]#方法1，导入整个包，[]表示可有可无

from 模块名 import 函数/变量/类#方法2，导入包的一部分

```

自定义的模块，如果有代码则在导入的时候会执行，如果不希望代码执行，则需要用

```python
#名为calc的模块，包含函数，类和语句，
if __name__ == '__main__':
    print(add(2, 3))
```

如果主程序：

```python
import calc #则会执行calc中的语句，不会执行函数和类，但是如果不想在导入模块的时候执行语句则需要用上面的if __name__ == '__main__':方法
```

# 2、导包

python结构

![未命名文件-2.png](https://i.loli.net/2021/03/08/ikpyHXZtDMj71cu.png)

包跟目录的区别是，包中包含`__init__.py`文件

```python
#包的导入
import 包名.模块名
import 包名
import 模块名

#利用from。。。import 。。。
from 包名 import 模块名
from 包名.模块名 import 变量/函数名
```

# 3、python中常用模块

| 模块名 | 描述               |
| ------ | ------------------ |
| sys    | 与python解释器相关 |
| time   | 与时间相关         |
|        |                    |
|        |                    |
|        |                    |
|        |                    |
|        |                    |

# 4、第三方模块的安装和使用

```python
#第三方模块的安装
pip install 模块名

#第三方模块的使用
import 模块名
```

[Pycharm导入

[第三方模块](https://www.jianshu.com/p/bf204b24b557)

