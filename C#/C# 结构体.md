# C# 结构体

## 定义

> A structure is a value type. The type is defined with the `struct` keyword. Structures are very similar to the classes; they differ in some aspects. Structures are meant to represent lightweight objects like `Point`, `Rectangle`, `Color` and similar. In many cases, structures may be more efficient than classes. Structures are value types and are created on the stack. Note that primitive data types like `int`, `bool`, `float` are technically `struct` types.
All `struct` types inherit from `System.ValueType` and further from `System.Object`. Structures are never abstract and they are always implicitly sealed. So struct types do not support inheritance. Therefore, the `struct` data member cannot be declared protected. The abstract and sealed modifiers are not permitted for a `struct` definition. A `struct` is not permitted to declare a parameter less constructor.
Structures can also contain constructors, constants, fields, methods, properties, indexers, operators, events, and nested types. However, if we need to implement more of these features, we might consider using a class instead. Structures can implement an interface. A `struct` can be used as a `nullable` type and can be assigned a null value.

结构是一种值类型。类型是用 `struct`关键字定义的。结构与类非常相似；它们在某些方面有所不同。结构旨在表示轻量级对象，如、`Point`,`Rectangle`, `Color`和类似的。在许多情况下，结构可能比类更有效。结构是值类型并在堆栈上创建。请注意，像  `int`,`bool`, `float`之类的原始数据类型在技术上属于`struct` 类型。

所有`struct`类型都继承`System.ValueType` 自`System.Object`。 结构从来都不是抽象的，它们总是隐含的密封。所以结构类型不支持继承。因此，`struct`不能将数据成员声明为`protected`。`struct`定义中不允许使用 abstract 和 sealed 修饰符。一个`struct`不允许声明无参数构造函数。

结构还可以包含构造函数、常量、字段、方法、属性、索引器、运算符、事件和嵌套类型。但是，如果我们需要实现更多这些功能，我们可能会考虑使用一个类来代替。结构可以实现接口。A`struct`可以用作 `nullable`类型并且可以分配一个空值。



## 组成

```C#
//结构还可以包含构造函数、常量、字段、方法、属性、索引器、运算符、事件和嵌套类型
//因为结构体类型总是隐式密封的，不能指定为密封的和抽象的，因此在定义结构时不能使用sealed和abstract关键字。默认访问修饰符为internal。
struct People{
    
    /*
    结构体成员不能被指定为抽象的、虚拟的、或者保护的对象
    因此结构体的成员不能使用如下访问修饰符：abstract、virtual和protected
	结构体的函数成员不能声明为abstract和virtual，但是可以使用override关键字，用以覆写它的基类System.ValueType中的方法。
	*/
    
    public string name;	 //结构体内成员变量无法直接初始化
    int age;			//未用public修饰的内部变量默认private
    bool sex;			//结构体中的变量可以是除其本身外任意类型
    
    
    
    /*构造函数
    1.无返回值,且必须有public修饰
    2.函数名必须和结构体名相同
    3.必须有参数，且必须对所有的成员变量初始化（除了下文提及的方法）
    4.当定义有参构造函数后，默认的无参构造函数不会消失,这点和类不同
    */
    public People(string name,int age,bool sex)
    {
        this.name=name;
        this.age=age;
        this.sex=sex;
    }
    /*
    但是也可以只初始化个别成员变量
    public People(string name):this()
    {
        this.name=name;//不写这行也不会报错
    }
    */

    public void PrintInfo(){
        Console.WriteLine("名为{0},{1},{2}岁.",name,age,sex)
    }
}
```



## 扩展

### 静态构造函数

结构类型也可以有静态构造函数，静态构造函数用于初始化静态数据成员。

结构和类的静态构造函数的触发规则不同，类的静态构造函数是在创建第一个实例或引用任何静态成员之前自动调用的，而结构的静态构造函数在以下情况调用：

1. 使用显式声明的静态构造函数进行实例化
2. 调用结构的方法或访问结构的静态数据成员(无论是读取还是赋值，访问实例数据成员不会触发，CLR自动调用静态的构造函数)。

## 类 & 结构

|条件|结构体|类|
| :--: | :--: | :--: |
|数据类型 | 值|引用类型|
| 是否必须使用new进行初始化 | 否 | 是 |
| 是否可声明无参数的构造函数 | 否 | 是 |
| 直接派生自什么类型 | System.ValueType | System.Object |
| 数据成员可不可以在声明的同时初始化 | 声明为const或static可以，数据成员不可以 | 可以 |
| 有无析构函数 | 无 | 有 |
| 可不可以从类派生 | 不可以 | 可以 |
| 可不可以实现接口 | 可以 | 可以 |
| 实例化时在堆还是栈分配内存 | 栈 | 堆。栈中保存引用 |
|该类型的的变量可不可以被赋值为null|不可以|可以|
|*可不可以定义私有的无参构造函数*|不可以|可以|
|是否总有一个默认的无参构造函数|是|当自定义构造函数后，原无参构造函数消失|