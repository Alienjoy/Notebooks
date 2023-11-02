# JSON 见代码

JSON就是一段按照一定规则写的字符串，可以解析出数据

javascript的对象表示法  **J**ava**S**cript **O**bject **N**otation

JSON 是用于存储和传输数据的格式。

JSON 通常用于服务端向网页传递数据 。

## 语法

```
		* 数据在名称/值对中：json数据是由键值对构成的
			* 键用引号(单双都行)引起来，也可以不使用引号
			* 值得取值类型：
				1. 数字（整数或浮点数）
				2. 字符串（在双引号中）
				3. 逻辑值（true 或 false）
				4. 数组（在方括号中）	{"persons":[{},{}]}
				5. 对象（在花括号中） {"address":{"province"："陕西"....}}
				6. null
		* 数据由逗号分隔：多个键值对由逗号分隔
		* 花括号保存对象：使用{}定义json 格式
		* 方括号保存数组：[]
```

## 获取数据

```
		1. json对象.键名
		2. json对象["键名"]
		3. 数组对象[索引]
		4. 遍历
				 		//1.定义基本格式
		        var person = {"name": "张三", age: 23, 'gender': true};
		
		        var ps = [{"name": "张三", "age": 23, "gender": true},
		            {"name": "李四", "age": 24, "gender": true},
		            {"name": "王五", "age": 25, "gender": false}];
		            //获取person对象中所有的键和值
		        
		       //for in 循环
		       for(var key in person){
		            //这样的方式获取不行。因为相当于  person."name"
		            //alert(key + ":" + person.key);
		            alert(key+":"+person[key]);
		        }
		
		       //获取ps中的所有值
		        for (var i = 0; i < ps.length; i++) {
		            var p = ps[i];
		            for(var key in p){
		                alert(key+":"+p[key]);
		            }
		        }
```

## JAVA对象转json

```
1. 导入jackson的相关jar包
2. 创建Jackson核心对象 ObjectMapper
3. 调用ObjectMapper的相关方法进行转换
	1. 转换方法：
		* writeValue(参数1，obj):
      参数1：
      File：将obj对象转换为JSON字符串，并保存到指定的文件中
      Writer：将obj对象转换为JSON字符串，并将json数据填充到字符输出流中
      OutputStream：将obj对象转换为JSON字符串，并将json数据填充到字节输出流中
    * writeValueAsString(obj):将对象转为json字符串
```

```
2. 注解：
		1. @JsonIgnore：排除属性。
		2. @JsonFormat：属性值得格式化
				* @JsonFormat(pattern = "yyyy-MM-dd")

3. 复杂java对象转换
					1. List：数组
					2. Map：对象格式一致
```

```
服务器响应的数据，在客户端使用时，要想当做json数据格式使用。有两种解决方案：
		1. $.get(type):将最后一个参数type指定为"json"
		2. 在服务器端设置MIME类型
			response.setContentType("application/json;charset=utf-8");
```

