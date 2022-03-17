# JAVA学习笔记-007-String类及相关方法

## 方法

### equals()和compareTo()和==

当我们比较字符串的时候，常常会用到equals()这个方法，compareTo()也可以用来比较字符串，那么equals和compareTo()有什么区别呢？

实际上，equals是

compareTo也可用于判断字符串是否相等，但是它遵循一个规则——先比较字符串



直观点，让我们进入代码
#### “==”
```java
String a = "Hello";
String b = "Hello";
String c = new String "Hello";
String d = "Hello";
String e = "Apple";

System.out.println(a==b);
System.out.println(a==c);
System.out.println(c==d);
System.out.println(a==d);
System.out.println(a==e);

输出结果：
    true	//a==b(a和b的地址相同(Java共享字符串))
    false	//a!=c(a和c的地址不同)
    false	//c!=d(c和d的地址不同)
    true	//a==d(a和d的地址相同(Java共享字符串))
    false	//a!=e(a和e的地址不同)
```


#### “compareTo()”

##### 当两个字符串完全相同

```java
String a = "Hello";
String b = "Hello";
System.out.println(a.compareTo(b)+“,”+b.compareTo(a));

输出结果：0,0;
```

##### 当两个字符串头部相同

- 类型1

```java
String a = "Hello";
String b = "He";
System.out.println(a.compareTo(b)+“,”+b.compareTo(a));

输出结果：3,-3;
//先逐位逐字符比较，全都相等比较字符串长度，输出a的字符串长度与b的字符串长度之差(比较者减被比较者)
```

- 类型2

```java
String a = "Hello";
String b = "Hee";
System.out.println(a.compareTo(b)+“,”+b.compareTo(a));

输出结果：7,-7;
//逐字符比较，到第三个字符不等，遂比较第三位的字符ASCII码的差值并输出(比较者减去被比较者)
```

```java
String a = "Hello";
String b = "Heepepepepe";
System.out.println(a.compareTo(b)+“,”+b.compareTo(a));

输出结果：7,-7;
//逐字符比较，到第三个字符不等，遂比较第三位的字符ASCII码的差值并输出(比较者减去被比较者)
```

##### 当两个字符串完全不同

```java
String a = "Hello";
String b = "Apple";
System.out.println(a.compareTo(b)+“,”+b.compareTo(a));

输出结果：7,-7;
//逐字符比较，到第一个字符不等，遂比较第一位的字符ASCII码的差值并输出(比较者减去被比较者)
```

#### “equals()”

```java
String a = "Hello";
String b = "Hello";
String c = new String "Hello";
String d = "Apple";

System.out.println(a.equals(b));
System.out.println(a.equals(c));
System.out.println(a.equals(d));

输出结果：
    true	//a==b(a和b的字符相同)
    true	//a!=c(a和c的字符相同)
    false	//c!=d(a和d的字符不同)
```