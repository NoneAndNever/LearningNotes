# C#变长参数和可选参数

## 变长参数

关键字: params

### 格式



```C#
void func(params int[] args){}

func();//right
func(1,2,3,4)//also right
----------------------------------------
void func(int arg,params int[] args){}

func();//right
func(1,2,3,4)//also right, arg=1; args={2,3,4}

 
```



#### 注意事项

- `params`后必须为数组,数组可以为任意类型
- 函数参数中可以有别的参数和`params`关键字修饰的参数
- `params`修饰的参数必须放在最后一个参数位置,前面可以有任意多个参数
- 函数参数中最多只能出现一个`params`关键字
- 不同于`in`,`out`,`ref`,关键字,`params`关键字修饰的参数无法重载函数



## 可选参数(参数默认值)

### 格式

`void func(int num, string s="default")`

#### 注意事项

- 如果和普通参数混用,则必须要在普通参数之后

例如``void func(int n=0, int num, string s="default")``则是错误的\

- 可以和变长参数同时使用,最前面是普通参数,其后是可选参数,最后一个
