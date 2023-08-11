# C# 排序

## 冒泡排序(Bubble Sort)

时间复杂度：$O(n^2)$

```c#
//让arr数组 从左到右 从大到小 降序 排序
for(int i = 0; i < arr.Length; i++)
{
    for(int j = 0; j < arr.Length - 1 - i; j++)
    {
        if(arr[j]<arr[j+1])	//若要从小到大则变成>
        {
        	int tmp=arr[j];
            arr[j]=arr[j+1];
            arr[j+1]=tmp;
            //等同于(arr[j], arr[j+1]) = (arr[j+1], arr[j]);
        }
	}
}

//让arr数组 从右到左 从大到小 降序 排序
for(int i = 0; i < arr.Length; i++)
{
    for(int j=arr.Length-1; j > i; j--)
    {
        if(arr[j-1]<arr[j])	//若要从小到大则变成>
        {
        	(arr[j-1], arr[j]) = (arr[j], arr[j-1]);
        }
	}
}

```
### 归纳

无论从左到右还是从右到左外圈循环总是`for(int i = 0; i < arr.Length; i++)`

左右的顺序则由`j`的初值和末值决定，`0`到`arr.Length-i-1`是从左到右；`arr.Length-1`和`i`是从右到左

左小于右交换为从从大到小降序，右小于左是从小到大升序排序

### 优化

#### 长度检验

```c#
if(arr=null || arr.Length<2)
    return arr;
```

#### flag标记法

```c#
bool isSort=true;//用一个布尔变量标记是否已经有序，已经有序则没必要进行后续的比较了
for(int i = 0; i < arr.Length && isSort; i++)
{
    isSort=true;//每个循环前默认重置会true
    for(int j = 0; j < arr.Length - 1  - i; j++)
    {
        if(arr[j]<arr[j+1])
        {
        	(arr[j], arr[j+1]) = (arr[j+1], arr[j]);
            isSort=false;//如果有进行交换则说明还未有序，继续循环
        }
	}
}
```

#### 双向冒泡排序

```C#
for(int i = 0; i < (arr.Length+1)/2; i++)
{
    for(int j = i; j < arr.Length - 1 - i; j++)
    {
        if(arr[j]<arr[j+1])
        {
            (arr[j], arr[j+1]) = (arr[j+1], arr[j]);
        }
    }
    for(int j=arr.Length-1-i; j > i; j--)
    {
        if(arr[j-1]<arr[j])
        {
            (arr[j-1], arr[j]) = (arr[j], arr[j-1]);
        }
    }
}

--------------------------------------------
    
int left=0;
int right=arr.Length-1;
while(left<right)
{
    for(int i=left;i<right;i++)
    {
        if(arr[i]<arr[i+1])
        {
            (arr[i], arr[i+1]) = (arr[i+1], arr[i]);
        }
    }
    right--;
    for(int i=right;i>left;i--)
    {
        if(arr[i-1]<arr[i])
        {
            (arr[i], arr[i-1]) = (arr[i-1], arr[i]);
        }
    }
    left++;
}
```

#### 标记有序末尾

```C#
int border = arr.Length;//标记边界
int lastSortIndex = border;//标记最后一次交换的位置
for(int i = 0; i < border; i++)
{
    for(int j = 0; j < border - 1 - i; j++)
    {
        if(arr[j]<arr[j+1])
        {
            (arr[j], arr[j+1]) = (arr[j+1], arr[j]);
            lastSortIndex = j;
        }
    }

    border = lastSortIndex;
}
```

#### 终极版

```C#
public static int[] bubbleSort(int[] arr) {
     if (arr == null || arr.length < 2) {
          return arr;
     }
    //记录最后一次交换的位置
    int lastExchangeIndex = 0;
    //无序数列的边界，每次比较只需要比到这里为止
    int sortBorder = arr.length - 1;
    
    for (int i = 0; i < arr.length - 1; i++) {
         bool isSorted  = true;//有序标记，每一轮的初始是true
         for (int j = 0; j < sortBorder; j++) {
             if (arr[j + 1] < arr[j]) {
                 isSorted  = false;//有元素交换，所以不是有序，标记变为false
                 (arr[j], arr[j+1]) = (arr[j+1], arr[j]);
                 lastExchangeIndex = j;
             }
         }
        sortBorder = lastExchangeIndex
         //一趟下来是否发生位置交换，如果没有交换直接跳出大循环
         if(isSorted )
              break;
     }
     return arr;
}

```

## 选择排序（Selection sort）

时间复杂度: $O(n^2)$

```c#
//从左到右 从大到小 降序排序
for(int i=0;i<arr.Length-1;i++)
{
    int max=i;//记录最大数据的下标位置
    for(int j=i;j<arr.Length;j++)
    {
        if(arr[max]<arr[j])//遍历寻找最大值的下标
            max=j;
    }

    if (max != i)
        (arr[i], arr[max]) = (arr[max], arr[i]);
}

//从右到左 从大到小 降序排序
for(int i=arr.Length-1;i>0;i--)
{
    int min=i;//记录最大数据的下标位置
	for(int j=i;j>=0;j--)
    {
        if(arr[min]>arr[j])//遍历寻找最大值的下标
            min=j;
    }

    if (min != i)
        (arr[i], arr[min]) = (arr[min], arr[i]);
}
```

### 归纳

从左到右	`for(int i=0;i<arr.Length-1;i++)`

从右到左	`for(int i=arr.Length-1;i>0;i--)`

找最大项就是`max`,最小项就是`min`

#### 注意点

注意外圈循环的方向,升序降序的要求和标记的是最大值还是最小值

### 优化

#### 双向选择排序

```C#
for(int i=0;i<(arr.Length+1)/2;i++)
{
    int max=i;//记录最大数据的下标位置
    int min=arr.Length-1-i;
    for(int j=i;j<arr.Length;j++)
    {
        if(arr[max]<arr[j])//遍历寻找最大值的下标
            max=j;
        if(arr[min]>arr[j])//遍历寻找最大值的下标
            min=j;
    }
    if (max != i)
    {
        (arr[i], arr[max]) = (arr[max], arr[i]);
        if(i==min)
            min=max;//如果max交换的时候把最小值给交换走了,则同时切换min的下标指向
    }

    if (min != arr.Length-1-i)
        (arr[arr.Length-1-i], arr[min]) = (arr[min], arr[arr.Length-1-i]);
}
```

