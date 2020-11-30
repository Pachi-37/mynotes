# Java笔记



### 第一部分：基础知识

##### Package

包的本质可以理解为文件夹

> com.company.project

##### 包的强制命名规范

- 包名统一使用小写，点分隔符之间有且仅有一个自然语义的英文单词
- 包名统一使用单数



### 注释和文档

- 行注释
  - `//`
- 段注释
  - `/**/`
- 方法注释和类注释
  - `/** */`



##### 生成Java文档

`javadoc`

相关参数

- `javadoc -d`
  - 文档的存放目录，如果不使用该参数导致直接生成在当前目录
-  `-version` 和 `-author`
  - 如果没有这两个参数，生成的文档不包括版本和作者信息
- `-splitindex`
  - 将索引分别为每个字母对应一个文件，且该文件包含索引的内容
- `-windowtitle`
  - 为文档添加一个标题，如果不指定默认显示——（生成的文档（无标题））

##### 文档和文档注释的格式化

生成的文档为HTML格式，这些HTML格式的表示符号不是Javadoc加的，而是我们自己写注释的时候写上去的

> 文档注释的正文并不是直接复制到输出文件，而是读取每一行之后，删除`*`及以前的空格，再输入到文档
>
> 文档注释只能说明紧接其后的类，属性或者方法，如果不是紧跟着，可能导致文档错误

##### 分层

- 第一部分——简述

  - 简述部分写在一段文档注释的最前面，第一个`.` 之前包括`.`

  > 有些时候，即使正确的以一个点号分割，javadoc任然可能出错，为了解决这个问题可以使用`<p>`将第一部分和第二部分分隔开

- 第二部分——详细说明

  - 该部分对属性和方法进行详细的说明

- 第三部分——特殊说明

  - 版本，参数，返回值等

##### Javadoc标记

| 标记         | 范围                   | 作用                     |
| ------------ | ---------------------- | ------------------------ |
| `@author`    | 对类的说明             | 标明开发该模块的作者     |
| `@version`   | 对类的说明             | 开发该类模块的版本       |
| `@see`       | 对类，属性，方法的说明 | 参考转向（主题）         |
| `@param`     | 对类的说明             | 对方法中某参数的说明     |
| `@return`    | 对类的说明             | 对方法返回值的说明       |
| `@exception` | 对类的说明             | 对方法可能抛出的异常说明 |

###### `@see`的三种用法

- `@see 类名/#方法名/#属性名`

  - 类名与全类名

    - 如果 Java 源文件中的 `import` 语句包含了的类，可以只写出类名，其他的则需要写出全类名

    ```java
    @see String
    @see java.alng.String
    ```

    

    > 使用 `javac` 命令来判断

  - 方法名或属性名

    - 如果是方法名则需要写出方法名以及参数类型，没有参数的方法写一对括号

    ```java
    @see show(boolean)
    @see show()
    ```

- `@author` `@version`

  - `@author` 可以多次使用，指明多个作者
  - `@vesion` 可以多次使用，不过只有第一次生效

- `@param`、`@return` 和 `@exception`

  - 只能用于方法 
  - `@exception` 后面应有简述的异常类名，说明中应指出抛出异常的原因;需要注意的是，异常类名应该根据源文件的 import 语句确定是写出类名还是类全名。



##### 注释规范

原则：注释形式统一，注释内容简明

注释条件

- 基本注释（*）

  - 类（接口）的注释
  - 构造器函数的注释
  - 方法的注释
  - 全局变量的注释
  - 字段，属性的注释

  > 简单的内容简单注释，注释内容不大于10个字，持久化对象或VO对象的getter、setter不需要注释

  - 典型算法必须有注释
  - 代码不明晰处必须有注释
  - 代码修改处添加修改标识符的注释
  - 为他人提供的接口必须加详细注释

### String类型

##### 创建字符串

```java
String str = "String";

char[] helloArray = { 'r', 'u', 'n', 'o', 'o', 'b'};
String helloString = new String(helloArray);  
```



##### 获取字符串的长度

用于获取有关对象的方法称为访问器方法

```java
String test = "Test";
int len = test.length();
```

##### 连接字符串

```java
"tmp".concat("str");

# 使用 `+` 连接字符串
```



##### 常用的方法

```
char charAt(int index)
//返回索引处的char值

int compareTo(Object o)
//把这个字符串和另一个对象比较，返回它们之间的差值
    
int compareToIgnoreCase(String str)
//比较两个字符串，不考虑大小写
    
boolean contentEquals(StringBuffer sb)
//当字符串与指定的StringBuffer有相同顺序的字符时候返回真

isEmpty()
判断字符串是否为空。
```



### 自动类型转换

##### 分类

- 简单数据类型之间的转换

  - 低级到高级的自动类型转换

  > 将double型变量赋值给float变量，不加强转的话会报错
  >
  > char 类型转换为整型，将会转换为 ASCII 码

  - 高级到低级的牵制类型转换

  > 溢出或精度下降

  - 包装类过渡类型转换

- 字符串和其他数据类型

> 几乎从java.lang.Object类派生的所有类提供了toString()方法

- 其他使用数据类型



### 导包（import）

`java.lang`包默认不需要导入，可以直接使用

导包路径不对可能无法使用指定的类

导包导错了可能会找不到一些属性或方法

### 数组(静态数组)

##### 定义数组

```java
// 初始化
int a[] = {};
// 分配内存空间
dataType [] arrayReFVar = new dataType[arraySize];
```

##### 打印数组

```java
// 循环遍历
for(int i = 0; i < array.length; i++){
    System.out.println();
}
// foreach
for(dataType element: myList){
    System.out.println(element);
}
```

##### 数组作为函数的参数



### Java.util.Arrays

```java
public static int binarySearch(Object a, Object key)
// 使用二分查找算法在指定数组中查找指定的对象，并返回索引值（该数字必须要提前排列好）

public static boolean equals(long[] a ,long[] b)
//数组中指定元素相等，则返回true
    
public static void fill(int[] a,int val )
//将给定的值填充到数组中
    
public static void sort(Object[] a) 
//指定的对象按自然排序升序排列
```



### 方法的重载

方法名相同，参数个数或参数类型不同