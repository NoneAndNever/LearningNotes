# Unity 笔记-002

## Inspector

### Tag&Layer

#### 相同点

都是用于标记GameObject的，每一个GameObject都只能有一个Tag和一个Layer

#### 不同点

- **数量限制**

**Tag**没有数量限制，**Layer**上限32个，且且前 8 个预设不可让使用者变更

- **定义方式**

**Tag**使用**字符串**来定义，而**Layer**使用一个**32位元的值**来定义，通过设置每一位的01来控制Layer的选择与否

- **判定方式**

**Tag**通过**字符串**比对进行比较，只能**单**个判断，而**Layer**通过**位运算**进行比较，可以**复选**判断。Unity内建的任何Component都没有暴露的栏位指定使用**Tag**，故通常通过直接寻找指定**Tag**对应的**字符串**，如使用GameObject.FindWithTag或者GameObject.CompareTag()来进行判断比对
与之相对的**Layer**则存在例如LayerMask这种类型可以通过public后在inspector窗口进行勾选的复选操作，或者在代码内+=不同的layer来进行复选操作，同时比较的时候通过利用位运算子来使 layer 栏位值往右移位并与 1 进行逻辑运算来判断 layer 是否相符

- **安全性**

**Layer**相对于**Tag**更加安全些，**Tag**在比较时字符串必须完全相等才能进行比较，字符串但凡打错一个字符都没用

- **比较的便携性及效率 **

在比较单个**Tag/Layer**时，**Tag**相对于**Layer**更方便些，无需另外声明对象便可直接进行比较，而**Layer**的比较必需LayerMask类型的变量，就算进行单个比较也是
而进行复项比较时，**Layer**的**32位元值**的优势便体现出来了，更方便并且效率高于**Tag**的多次字符串比较

- **用途**

**Tag：**

方便查找游戏物件（如GameObject.FindWithTag()）

与其他游戏物件碰触时的判断（如Collider.CompareTag()）

**Layer：**

让 Camera 指定哪些物件要被画出来。

让 Light 指定哪些物件要被照明。

让物理射线确认哪些物件要被侦测到。（Physics）

- **More**

**Layer**可以通过在编辑器Scene窗口设定来设置SceneView中可以看到的层，在物品数量繁多时会方便很多。
