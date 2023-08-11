# C# 数据类型

## 基本数据类型

### 速览

| 无符号类型 | byte  | ushort | uint    | ulong |
| ------ | ------ | ------ | ------- | ------ |
| **有符号类型** | **sbyte** | **short**  | **int**     | **long**  |
| **浮点型**     | **float** | **double** | **decimal** ||
| **特殊类型**   | **bool**  | **char**   | **string**  |       |

### 整型

#### `byte`和`sbyte`

#### `short`和`ushort`

#### `int`和`uint`

#### `long`和`ulong`

### 浮点型

| C# Alias | .Net Type | Size | Precision | Range |
| --- | --- | --- | --- | --- |
| float | `System.Single` | 4 bytes | 7 digits | $±1.5 * 10^{-45}$ ~ $±3.4 * 10^{38}$ |
| double | `System.Double` | 8 bytes | 15-16 digits | $±5.0 * 10^{-324}$ ~ $±1.7 * 10^{308}$ |
| decimal | `System.Decimal` | 16 bytes | 28-29 decimal places | $±1.0 * 10^{-28}$ ~ $±7.9 * 10^{28}$ |

> **注意：**根据经验，`decimal`用于计数值，而`float/double`用于测量值。

#### `float`

#### `double`

#### `decimal`

> 与 double/float 类型不同，试图增加`decimal`超出其限制的值会导致`System.OverflowException`.

### 特殊类型

#### `bool`

#### `char`

#### `string`
