# jdk1.8新特性

## 新特性简介

> - 速度更快
> - 代码更少（lambda表达式）
> - 强大的Stream API
> - 便于并行
> - 最大化的减少空指针异常 Optional

## lambda表达式

**为什么使用Lambda表达式**

> lambda表达式基础语法：Java8中引入了一个新的操作符“->”该操作符称为箭头操作符或Lambda操作符
>
> 箭头操作符将Lambda表达式拆分成两部分：
>
> 左侧：Lambda表达式的参数列表
>
> 右侧：Lambda表达式中所需执行的功能，即Lambda体

**语法格式一：无参数，无返回值**

```java
 @Test
    public void test1(){
        Runnable r = new Runnable() {
            @Override
            public void run() {
                System.out.println("hello");
            }
        };
        r.run();
        System.out.println("--------------------");
        Runnable r1 = () -> System.out.println("lambda");
        r1.run();
    }
```

### java8内置的四大核心函数式接口

> Consumer<T>:消费型接口
>
> ​			void accept
>
> Supplier<T>供给型接口
>
> ​			T get();
>
> Function<T,R>:函数式接口
>
> ​			R apply(T t);
>
> Predicate<T>：断言型接口
>
> ​			boolean test(T t);

## Java流

流（Stream）到底是什么？



> Stream的操作三个步骤
>
> - 创建Stream
> - 中间操作
> - 终止操作



**创建Stream**

1. 可以通过`Collection `系列集合提供的`Stream() `或`parallelStream()`

   ```java
   List<String> list = new ArrayList<>();
           Stream<String> stream = list.stream();
   ```

2. 通过`Arrays`中的静态方法`stream()`获取数组流

   ```java
    Employee[] employees = new Employee[10];
           Stream<Employee> employeeStream = Arrays.stream(employees);
   ```

3. 通过Stream 类中的静态方法`of()`

   ```java
   Stream<String> aa = Stream.of("aa", "cc", "vv");
   ```

4. 创建无限流

   ```java
   Stream<Integer> iterate = Stream.iterate(0, (x) -> x + 2);
   ```

**中间操作**

 **筛选与切面**

- filter-接收Lambda

- limit-截断流
- skip(n)-跳过元素
- distinct-筛选

