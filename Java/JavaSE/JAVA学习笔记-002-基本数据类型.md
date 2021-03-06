# JAVA学习笔记-002-基本程序

## 基本数据类型

### 整形

#### int

存储需求：4字节32位

取值范围：-2 147 483 648 ~ 2 147 483 647

#### long

存储需求：4字节32位

取值范围：-9 223 372 036 854 775 808 - 9 223 372 036 854 775 807

#### short

存储需求：4字节32位

取值范围：-32768 ~ 32767

#### byte

存储需求：1字节8位

取值范围：-128 ~ 127

---

长整型数值有一个后缀 L 或 l ( 如 4000000000L) 

十六进制数值有一个前缀 Ox 或 0X (如 OxCAFE) 

八进制有一个前缀 0 ( 如 010 )

从 Java 7 开始， 加上前缀 0b 或 0B 就可以写二进制数。还可以为数字字面量加下划线，如用 1_000_000(或0b1111\_ 0100\_ 0010\_ 1000\_ 0000 ) 表示一百万。这些下划线只是为了让人更易读。Java 编译器会去除这些下划线

---

#### 其他说明

**注：与C++不同， Java 没有任何无符号（unsigned) 形式的 int、 long、short 或 byte 类型。**

---

### 浮点型

#### float

存储需求：4字节32位

取值范围：大约 ± 3.402 823 47E+38F (有效位数为 6 ~ 7 位）


#### double

存储需求：8字节64位

取值范围：大约 ± 1.797 693 134 862 315 70E+308 (有效位数为 15 位)

---

#### 其他说明

float 类型的数值有一个后缀 F 或 f (例如，3.14F。)

没有后缀 F 的浮点数值（如 3.14 ) 默 认为 double 类型。

当然，也可以在浮点数值后面添加后缀 D 或 d (例如，3.14D) 。

---

绝大部分应用程序都采用 double 类型。在很多情况下，float 类型的精度很难满足需求。

---

 可以使用十六进制表示浮点数值。例如，0.125=2<sup>-3</sup> 可以表示成 0x1.0p-3。在十六进制表示法中， 使用 p 表示指数， 而不是 e。 注意， 尾数采用十六进制，指数采用十进制。指数的基数是 2，而不是 10。

---

浮点数值不适用于无法接受舍入误差的金融计算中。 例如，命令 System.out.println ( 2.0-1.1 ) 将打印出 0.8999999999999999, 而不是人们想象的 0.9。这种舍入误差的主要 原因是浮点数值采用二进制系统表示， 而在二进制系统中无法精确地表示分数 1/10。这 就好像十进制无法精确地表示分数 1/3 —样。如果在数值计算中不允许有任何舍入误差， 就应该使用 BigDecial类

---

### Char类型和Unicode

存储需求：4字节32位

取值范围：0 ~ 65535

---

#### 其他说明

转义序列 \u还可以出现在加引号的字符常量或字符串之外（而其他所有转义序列不可以）。

例如： 

```java
public static void main(String\u005B\ u00SD args) 
```

就完全符合语法规则， \u005B 和 \u005D 是 [ 和 ] 的编码。

---

char 类型原本用于表示单个字符。不过，现在情况已经有所变化。 如今，有些 Unicode 字符可以用一个 char值描述，另外一些 Unicode 字符则需要两个 char 值。

---

在 Java 中，char 类型描述了 UTF-16 编码中的一个代码单元。 我们强烈建议不要在程序中使用 char 类型，除非确实需要处理 UTF-16 代码单元。最好 将字符串作为抽象数据类型处理

---

### Boolean

存储需求：1位

boolean (布尔）类型有两个值：false 和 true, 用来判定逻辑条件 整型值和布尔值之间 不能进行相互转换。

---

在 C++ 中， 数值甚至指针可以代替 boolean 值。值 0 相当于布尔值 false, 非 0 值相当于布尔值 true, 在 Java 中则不是这样，, 因此， Java 程序员不会遇到下述麻烦：

``` Java
if (x = 0) // oops... meant x = 0
```

 在 C++ 中这个测试可以编译运行， 其结果总是 false: 而在 Java 中， 这个测试将不 能通过编译， 其原因是整数表达式 x = 0 不能转换为布尔值。

## 基本运算

### 运算符

#### 优先级


| 运算符 | 优先级 |   结合性    |
| :-------: | :---------: | :---------: |
| [] . () (方法调用) |    Title    | 从左向右 |
| ! - ++ + ( 一元运算）- ( 一元运算）（ _ )( 强制类型转换）new |    Text     | 从右向左 |
| * / % |    Text     | 从左向右 |
| + - |    Text     | 从左向右 |
| << >> <<< |    Text     | 从左向右 |
| <  <= > >= instanceof |    Text     | 从左向右 |
| == != |    Text     | 从左向右 |
| & |    Text     | 从左向右 |
| ^ |    Text     | 从左向右 |
| \| |    Text     | 从左向右 |
| && |    Text     | 从左向右 |
| \|\| |    Text     | 从左向右 |
| ? : |    Text     | 从左向右 |
| = += -= *= /= %=  &= \|= ^= <<= >>= >>>= |    Text     | 从左向右 |

