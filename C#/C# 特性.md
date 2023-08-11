

# C# 特性

## 定义

---

以下为微软官方doc内容：

使用特性，可以有效地将元数据或声明性信息与代码（程序集、类型、方法、属性等）相关联。 将特性与程序实体相关联后，可以在运行时使用*反射*这项技术查询特性。 有关详细信息，请参阅[反射 (C#)](https://docs.microsoft.com/zh-cn/dotnet/csharp/programming-guide/concepts/reflection)。

特性具有以下属性：

- 特性向程序添加元数据。 *元数据*是程序中定义的类型的相关信息。 所有 .NET 程序集都包含一组指定的元数据，用于描述程序集中定义的类型和类型成员。 可以添加自定义特性来指定所需的其他任何信息。 有关详细信息，请参阅[创建自定义特性 (C#)](https://docs.microsoft.com/zh-cn/dotnet/csharp/programming-guide/concepts/attributes/creating-custom-attributes)。
- 可以将一个或多个特性应用于整个程序集、模块或较小的程序元素（如类和属性）。
- 特性可以像方法和属性一样接受自变量。
- 程序可使用反射来检查自己的元数据或其他程序中的元数据。 有关详细信息，请参阅[使用反射访问特性 (C#)](https://docs.microsoft.com/zh-cn/dotnet/csharp/programming-guide/concepts/attributes/accessing-attributes-by-using-reflection)。

---

## 声明

```C#
public class SampleAttribute : Attribute //继承Attribute,类名通常以Attribute结尾
{
    public string info;
    
    public SampleAttribute(string info){
        this.info=info;
    }
}
```

## 使用

```c#
[Sample("这是存储数字的变量的info")]
public int num;
//通过[特姓名]来使用特性,如果特性名以Attribute结尾则调用时可以省略Attribute
//也可通过[特性名(参数)]来调用构造函数来初始化
```

```c#
//判断是否使用了特性
//Type类的方法,第一个参数是属性的Type,第二个参数代表是否需要搜索继承链上是否存在特性(往父类搜索)
//返回布尔值
type.IsDefined(typeof(SampleAttribute),false);

//得到特性
//Type类的方法,第一个代表是否需要搜索继承链上是否存在特性(往父类搜索)
//返回一个obj数组
list = type.GetCustomAttributes(true);
```

### 特性的限制`[AttributeUsage()]`

操作方法就是给特性类加特性

```C#
//参数一: AttributeTargets—特性能够用在哪些地方
//参数二: AllowMultiple一是否允许多个特性实例用在同一个目标上
//参数三: Inherited—特性是否能被派生类和重写成员继承
[AttributeUsage(AttributeTargets.Class|AttributeTargets.Field,AllowMultiple = true, Inherited=true)]
//该特性可以被应用到class和Field上,允许同一个特性的多个实例加载到同一个目标上,并且有需该特性被派生类和重写成员继承
public class CustomAttribute : Attribute 
{
	;
}

```

```C#
//关于AttributeTargets
// 摘要:
//     Specifies the application elements on which it is valid to apply an attribute.
[Flags]
public enum AttributeTargets
{
    Assembly = 0x1,
    //
    // 摘要:
    //     Attribute can be applied to a module. Module refers to a portable executable
    //     file (.dll or.exe) and not a Visual Basic standard module.
    Module = 0x2,
    Class = 0x4,
    Struct = 0x8,
    Enum = 0x10,
    Constructor = 0x20,
    Method = 0x40,
    Property = 0x80,
    Field = 0x100,
    Event = 0x200,
    Interface = 0x400,
    Parameter = 0x800,
    Delegate = 0x1000,
    ReturnValue = 0x2000,
    //
    // 摘要:
    //     Attribute can be applied to a generic parameter. Currently, this attribute can
    //     be applied only in C#, Microsoft intermediate language (MSIL), and emitted code.
    GenericParameter = 0x4000,
    All = 0x7FFF
}
```

### 一些特性

#### `[Obsolete("string")]`

过时特性:标注使用的方法等成员已过时

参数一：调用的方法时提示的内容

参数二：调用方法时是否报错，false则为warning，true则为error（编译前就报错）

#### 调用者信息特性

```c#
//哪个文件调用?
//CallerFilePath特性
//哪一行调用?
//CallerLineNumber特性
//哪个函数调用?
//CallerMemberName特性
//需要引用命名空间using System.Runtime.CompilerServices;
//且只能应用在有默认值的string参数上
//一般作为函数参数的特性
```

#### 条件编译特性

```C#
//条件编译特性
//Conditional
//它会和预处理指令#define配合使用
//需要引用命名空间using System.Diagnostics;//主要可以用在一些调试代码上
//有时想执行有时不想执行的代码(比如在不同平台使用不同的代码)
```

#### 外部DLL包函数

```c#
//DllImport
//只能放置在方法声明上。 
//用来标记非.Net(C#)的函数，表明该函数在一个外部的DLL中定义。
//一般用来调用c或者C++的Dll包写好的方法
//需要引用命名空间using system.Runtime.Interopservices
using system.Runtime.Interopservices;
[DllImport("Test.dll")]
public static extern int Add(int a, int b);//不能有大括号
//用 DllImport 属性修饰的方法必须具有 extern 修饰符。

//DllImport会按照顺序自动去寻找的地方：
//1、exe所在目录
//2、System32目录
//3、环境变量目录
//所以只需要你把引用的DLL 拷贝到这三个目录下，就可以不用写路径了。或者可以这样server.MapPath(.\bin\*.dll)web中的，同时也是应用程序中的，后来发现用[DllImport(@"C:\OJ\Bin\Judge.dll")]这样指定DLL的绝对路径就可以正常装载。

/*
DllImport具有五个命名参数：  
a、CallingConvention参数指示入口点的调用约定。
如果未指定 CallingConvention，则使用默认值CallingConvention.Winapi。

b、CharSet 参数指示用在入口点中的字符集。
如果未指定 CharSet，则使用默认值CharSet.Auto。

c、EntryPoint 参数给出 dll 中入口点的名称。
如果未指定EntryPoint，则使用方法本身的名称。      

d、ExactSpelling 参数指示 EntryPoint是否必须与指示的入口点的拼写完全匹配。
如果未指定 ExactSpelling，则使用默认值 false。

e、PreserveSig参数指示方法的签名应当被保留还是被转换。当签名被转换时，它被转换为一个具有 HRESULT返回值和该返回值的一个名为 retval的附加输出参数的签名。
如果未指定 PreserveSig，则使用默认值 true。      

f、SetLastError 参数指示方法是否保留Win32"上一错误"。

```

