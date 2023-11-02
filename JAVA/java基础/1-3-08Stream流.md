# Stream流

### 获取Stream流的方法

1. 使用Collection类的steam()方法
2. 使用Stream类的静态方法`static <T> Stream<T> of(T... values)`其中T为type of stream element，...表示可变参数，就是参数的数量不固定

### Stream流中的常用方法

- 延迟方法:（intermediate operation）返回值类型仍然是 Stream接口自身类型的方法,因此支持链式调用。(除了终结方法外,其余方法均为延迟方法。），就是对Stream流中元素进行筛选。
- 终结方法（terminal operation）:返回值类型不再是 Stream接口自身类型的方法,因此不再支持类似 StringBuilder那样的链式调用。本小节中,终结方法包括 count和 foreach方法。就是流的出口

```java
void forEach(Consumer<? super T> action)//用来遍历数组中的每一个数据
Stream<Integer> stream = Stream.of(1, 2, 3, 5, 6);
//lambda表达式，forEach的参数是Consumer接口的实现类，因为Consumer是一个函数式接口，所以可以使用Lambda来实现
stream.forEach((num)->{
  System.out.println(num);
});
```

```java
Stream<T> filter (Predicate<? super T> predicate)//Predicate接口是一种函数式接口@FunctionalInterface
stream.filter(num->num>3).forEach((num)->{
  System.out.println(num);
});
```

tip:Stream流数据属于管道流，只能使用一次，使用完毕就会关闭了。

如果需要将流中的元素映射到另外一个流中，需要使用map方法。

```java
<R> Stream<R> map(Function<? super T,?,extends R> mapper)// 其中R为The element type of the new stream。
//其中public interface Function<T,R>，Function为函数式接口，其中的R apply(T t)方法是把T类型的数据转为R类型，这种转换的方法为映射
  
Stream<String> stream = Stream.of("1", "2", "4", "5");
//Lambda表达式重写Function这个函数式接口中的抽象方法R apply(T t);
//转为新的Stream流
Stream<Integer> stream1 = stream.map((String s) -> {
  return Integer.parseInt(s);
});
```

Stream中统计个数的方法count:`long count()`，它是一个终结方法terminal operation

```java
ArrayList<Integer> arrayList = new ArrayList<>();
Collections.addAll(arrayList,12,2,45,6,123,66);
long count = arrayList.stream().filter(num -> num > 20).count();//count方法统计stream流中数据的个数
System.out.println(count);
```

Stream中取用前几个的方法limit `Stream<T> Limit(Long maxsize)`

```java
Stream<String> stream = Stream.of("1", "2", "4", "5");
stream.limit(3).forEach(num-> System.out.println(num));//limit方法用来取stream流的前几个元素
```

Stream中跳过前n个元素的方法skip`Stream<T> skip(Long n)`

```java
Stream<String> stream = Stream.of("1", "2", "4", "5");
stream.skip(2).forEach(num-> System.out.println(num));//跳过前两个元素
```

把两个流合成一个流的方法concat`static <T> Stream<T> concat(Stream<? extends T> a,Stream<? extends T> b)`

```JAVA
Stream<Integer> stream = Stream.of(1, 7, 8, 2, 4, 5, 6, 3);
Stream<Integer> stream1 = Stream.of(10, 20, 40, 50, 60, 70, 80);
Stream<Integer> concat = Stream.concat(stream, stream1);    
concat.forEach(num -> System.out.println(num));
```

