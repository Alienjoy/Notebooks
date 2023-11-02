# 框架

![image-20220127174527872](/Users/zhangshuheng/Desktop/Notebooks/JAVA/框架/Mybatis.assets/image-20220127174527872.png)

# Mybatis，用来操作数据库的，负责增删改查的操作

Mybatis是一个持久层框架，封装了JDBC操作的很多细节，使开发者只需要关注sql语句本身，不需要关注创建驱动，创建连接等过程。它使用ORM思想实现了对结果集的封装。

## ORM 

object relational mapping对象关系映射

把实体类中属性和数据库表中字段进行对应起来				

| user数据库表 |  User类  |
| :----------: | :------: |
|      id      | user_id  |
|   userName   | userName |

## Mybatis环境搭建

第一步：创建maven工程并导入坐标

第二步：创建实体类和dao的接口

第三步：创建Mybatis的主配置文件

​	SqlMapConifg.xml

第四步：创建映射配置文件

​	IUserDao.xml

## 环境搭建的注意事项

	第一个：创建IUserDao.xml 和 IUserDao.java时名称是为了和我们之前的知识保持一致。
	  在Mybatis中它把持久层的操作接口名称和映射文件也叫做：Mapper
	  所以：IUserDao 和 IUserMapper是一样的
	第二个：在idea中创建目录的时候，它和包是不一样的，就是new package和new directory
	  包在创建时：com.itheima.dao它是三级结构
	  目录在创建时：com.itheima.dao是一级目录，
	第三个：mybatis的映射配置文件位置必须和dao接口的包结构相同
	第四个：映射配置文件的mapper标签namespace属性的取值必须是dao接口的全限定类名
	第五个：映射配置文件的操作配置（select），id属性的取值必须是dao接口的方法名
	
	当我们遵从了第三，四，五点之后，我们在开发中就无须再写dao的实现类。

## Mybatis入门程序分析

```
//1.读取SqlMapConfig.xml配置文件
InputStream inputStream = Resources.getResourceAsStream("SqlMapConfig.xml");
//2.创建 SqlSessionFactory 的builder对象,sql会话工厂
SqlSessionFactoryBuilder builder = new SqlSessionFactoryBuilder();
//3.使用builder对象创建工厂对象SqlSessionFactory
SqlSessionFactory factory = builder.build(inputStream);
//4。使用SqlSessionFactory生产sqlSession对象
SqlSession session = factory.openSession();
//5。使用sqlSession创建dao（UserDao）接口的代理对象
UserDao userDao = session.getMapper(UserDao.class);
//6。使用代理对象执行查询所有方法
List<User> list = userDao.findAll();
for (User user : list) {
	System.out.println(user);
}

```

1. 读取配置文件的两种方式（不可以使用绝对路径和相对路径）
   - 使用类加载器，但是它只能读取类路径的配置文件
   - 使用ServletContext对象的getRealPath()

## OGNL表达式：

```

	Object Graphic Navigation Language
	对象	图	导航	   语言
	
	它是通过对象的取值方法来获取数据。在写法上把get给省略了。
	比如：我们获取用户的名称
		类中的写法：user.getUsername();
		OGNL表达式写法：user.username
	mybatis中为什么能直接写username,而不用user.呢：
		因为在parameterType中已经提供了属性所属的类，所以此时不需要写对象名
```

## 当要封装的实体类的成员变量名跟数据库的字段名不一致时结局方案

1. 修改sql语句，给查询到字段名起别名，使得跟实体类的成员变量名一致

```
select id as userId,name as userName,..... from user;
其中id，name是字段名字，userId，userName是实体类的成员变量名
```

2. 在UserDao.xml文件中新增加标签

```
<!-- 配置 查询结果的列名和实体类的属性名的对应关系 --> ,就是用来封装查询结果到实体类中的
    <resultMap id="userMap" type="uSeR">
        <!-- 主键字段的对应 -->
        <id property="userId" column="id"></id>
        <!--非主键字段的对应-->
        <result property="userName" column="username"></result>
        <result property="userAddress" column="address"></result>
        <result property="userSex" column="sex"></result>
        <result property="userBirthday" column="birthday"></result>
    </resultMap>
并把resultType由resultType="cn.njust.domain.User"
改成resultMap="userMap"//其中userMap是上面resultMap的id
```

## Mybatis执行源码分析

最终是执行 PreparedStatement类的execute，executeQuery(),executeUpdate()方法来实现的，他们三种方法的区别是：

```
execute:它能执行CRUD中的任意一种语句。它的返回值是一个 boolean类型,表示是否有结果集。有结果集是true,没有结果集是 fasle。
executeUpdate:它只能执行CUD语句,查询语句无法执行。他的返回值是影响数据库记录的行数
executeQuery:它只能执行 SELECT语句,无法执行増删改。执行结果封装的结果集Resultset对象
```

## URL

```
url属性：
            是要求按照Url的写法来写地址
            URL：Uniform Resource Locator 统一资源定位符。它是可以唯一标识一个资源的位置。
            它的写法：
               ` http://localhost:8080/mybatisserver/demo1Servlet`
                协议      主机     端口       URI
URI:Uniform Resource Identifier 统一资源标识符。它是在应用中可以唯一定位一个资源的。
```

## 配置的两种方式

```
    <properties resource="jdbcConfig.properties">
        <!--可以使用配置文件的方式（value="${jdbc.driver}"），也可以使用下面的Value的方式-->
    </properties>

    <!--使用typeAliases配置别名，它只能配置domain中类的别名 -->
    <typeAliases>
        <!--typeAlias用于配置别名。type属性指定的是实体类全限定类名。alias属性指定别名，当指定了别名就再区分大小写
        <typeAlias type="cn.njust.domain.User" alias="user"></typeAlias>-->

        <!-- 用于指定要配置别名的包，当指定之后，该包下的实体类都会注册别名，并且类名就是别名，不再区分大小写-->
        <package name="cn.njust.domain"></package>
    </typeAliases>
```

## Mybatis连接池

mybatis连接池提供了3种方式的配置：

```
配置的位置：
			主配置文件SqlMapConfig.xml中的dataSource标签，type属性就是表示采用何种连接池方式。
		type属性的取值：
			POOLED	 采用传统的javax.sql.DataSource规范中的连接池，mybatis中有针对规范的实现
			UNPOOLED 采用传统的获取连接的方式，虽然也实现Javax.sql.DataSource接口，但是并没有使用池的思想。
			JNDI	 采用服务器提供的JNDI技术实现，来获取DataSource对象，不同的服务器所能拿到DataSource是不一样。
				 注意：如果不是web或者maven的war工程，是不能使用的。
				 我们课程中使用的是tomcat服务器，采用连接池就是dbcp连接池。
```

## 事务（面试的时候）

```
什么是事务
	事务的四大特性ACID
	不考虑隔离性会产生的3个问题
	解决办法：四种隔离级别
	它是通过sqlsession对象的commit方法和rollback方法实现事务的提交和回滚
```



## 基于XML配置的动态SQL语句使用

```
mappers配置文件中的几个标签：会用即可
		<if>
		<where>
		<foreach
```

## Mybatis的多表操作

一对一（多对一）

```
SELECT u.*,a.money, a.id as aid FROM account a,`user` u WHERE a.UID=u.id;
```

一对多

```
SELECT u.*, a.id as aid, a.uid,a.money FROM `user` u LEFT JOIN account a ON u.id=a.uid;
```

多对多

```
SELECT r.ID as rid,r.role_name,r.role_desc,u.* FROM role r 
LEFT JOIN user_role ur ON r.id=ur.rid 
LEFT JOIN `user` u ON ur.UID=u.id;

SELECT u.*,r.ID as rid,r.ROLE_NAME,r.ROLE_DESC FROM user u 
LEFT JOIN user_role ur ON u.id=ur.uid 
LEFT JOIN `role` r ON ur.rid=r.id;
```

## Mybatis的延迟加载

在对应的四种表关系中：一对多，多对一，一对一，多对多

​	一对多，多对多：通常情况下我们都是采用延迟加载。

​	多对一，一对一：通常情况下我们都是采用立即加载。

## mybatis的缓存

```
适用于缓存：
			经常查询并且不经常改变的。
			数据的正确与否对最终结果影响不大的。
		不适用于缓存：
			经常改变的数据
			数据的正确与否对最终结果影响很大的。
			例如：商品的库存，银行的汇率，股市的牌价。
```

```
Mybatis中的一级缓存和二级缓存
		一级缓存：
			它指的是Mybatis中SqlSession对象的缓存。
			当我们执行查询之后，查询的结果会同时存入到SqlSession为我们提供一块区域中。
			该区域的结构是一个Map。当我们再次查询同样的数据，mybatis会先去sqlsession中
			查询是否有，有的话直接拿出来用。
			当SqlSession对象消失时，mybatis的一级缓存也就消失了。
一级缓存是 SqlSession 范围的缓存，当调用 SqlSession 的修改，添加，删除，commit()，close()等方法时会清空一级缓存
```

```
二级缓存:
			它指的是Mybatis中SqlSessionFactory对象的缓存。由同一个SqlSessionFactory对象创建的SqlSession共享其缓存。
			二级缓存的使用步骤：
				第一步：让Mybatis框架支持二级缓存（在SqlMapConfig.xml中配置）
				第二步：让当前的映射文件支持二级缓存（在IUserDao.xml中配置）
				第三步：让当前的操作支持二级缓存（在select标签中配置）
```

# Mapper接口中@Param的使用场景

```
使用@Param的四种情况
https://www.cnblogs.com/lenve/p/11229590.html
1、方法有多个参数，需要 @Param 注解
2、方法参数要取别名，需要 @Param 注解
3、XML 中的 SQL 使用了 $ ，那么参数中也需要 @Param 注解
4、那就是动态 SQL ，如果在动态 SQL 中使用了参数作为变量，那么也需要 @Param 注解，即使你只有一个参数。
```

