# JAVA学习笔记-001-第一个程序

## 程序开发步骤（编写-编译-运行）

### 编写-源程序（.java）

1. 新建一个文件，名为HelloWorld.java
2. 右键编辑
3. 输入以下代码

```java
public class HelloWorld{
    public static void main(String[] args){
        System.out.println("Hello World!");
    }
}
```



### 编译-Java字节码文件（.class）

在当前java文件目录打开cmd窗口

输入

```
javac HelloWorld.java
```

如果一切输入正确，应该会在当前目录生成一个HelloWorld.class文件

如果没有，或者报错，那么请根据报错信息检查自己哪一步写错了

### 运行

继续在当前cmd窗口输入

```
java HelloWorld
```

PS:不能加后缀名.class,并且大小写要严格对应



最后，一切大功告成了，看看你的程序是否输出了

```
Hello World!
```

是的话，恭喜

