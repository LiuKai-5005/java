# Java

从`Python`到`Java`主要是由于实际开发和应用还是`Java`使用率较高，类似于`美图秀秀`vs`Photoshop`，属于降维打击。
特别是面试经常问到的：

>>核心问题和相关知识点：掌握开发中常用类如集合、IO流、时间日期等操作；掌握Java异常处理机制，熟悉Java多线程开发；掌握网络基础知识，了解Socket原理，TCP、UDP协议；掌握java基本语法完成单机程序的编写；熟悉Java新特性，如Lambda、Stream流等操作

链接：https://www.zhihu.com/question/56110328/answer/370752381


8种基本数据类型：`byte`，`int`，`short`，`long`，`float`，`double`，`char`，`boolean`



计算机内存的最小存储单元是字节 二进制 `00000000` ~ `11111111`, 成十进制是 `0~255`，换算成十六进制是`00`~`ff`
* 1 `byte` = 8 `bit` 
* 1 `K` = 1024 `byte` 
* 1 `M` = 1024 `K` 
<br>
内存单元从0开始编号，称为内存地址。每个内存单元可以看作一间房间，内存地址就是门牌号。

不同的数据类型占用的字节数不一样。
```
       ┌───┐
  byte │   │
       └───┘
       ┌───┬───┐
 short │   │   │
       └───┴───┘
       ┌───┬───┬───┬───┐
   int │   │   │   │   │
       └───┴───┴───┴───┘
       ┌───┬───┬───┬───┬───┬───┬───┬───┐
  long │   │   │   │   │   │   │   │   │
       └───┴───┴───┴───┴───┴───┴───┴───┘
       ┌───┬───┬───┬───┐
 float │   │   │   │   │
       └───┴───┴───┴───┘
       ┌───┬───┬───┬───┬───┬───┬───┬───┐
double │   │   │   │   │   │   │   │   │
       └───┴───┴───┴───┴───┴───┴───┴───┘
       ┌───┬───┐
  char │   │   │
       └───┴───┘
```

`byte`恰好就是一个字节，而`long`和`double`需要8个字节。


注意`char`类型使用单引号`'`，且仅有一个字符，要和双引号`"`的字符串`String`类型区分开

## 常量
常量的作用是用有意义的变量名来避免魔术数字`Magic number`，例如，不要在代码中到处写`3.14`，而是定义一个常量。如果将来需要提高计算精度，我们只需要在常量的定义处修改，例如，改成`3.1416`，而不必在所有地方替换`3.14`。

根据习惯，常量名通常全部大写 `PI`。


## 整数运算
两个整数相除只能得到结果的整数部分

```java
public class Main {
    public static void main(String[] args) {
        int i = 3 / 2; // 1.5 --> 1
        int n = -3 / 2; // -1.5 --> -1
        System.out.println(i);
        System.out.println(n);
    }
}
```
### 溢出
特别注意：整数的除法对于除数为0时运行时将报错，但编译不会报错。<br>
整数由于存在范围限制，如果计算结果超出了范围，就会产生溢出，而溢出不会出错.

### 自增/自减
```java
public class Main {
    public static void main(String[] args) {
        int n = 3300;
        n++; // 3301, 相当于 n = n + 1;
        n--; // 3300, 相当于 n = n - 1;
        int y = 100 + (++n); // 不要这么写
        System.out.println(y);
    }
}
```
### 位运算
异或运算的规则是，如果两个数不同，结果为`1`，否则为`0`. 相同则为零，不同则为一。找不同专用。
位操作，也就是`01`操作的 与`&` 或 `~` 异或 `^`


右移`>>` 左移`<<`


### 运算优先级
在Java的计算表达式中，运算优先级从高到低依次是：
```
()
! ~ ++ --
* / %
+ -
<< >> >>>
&
|
+= -= *= /=
```
### 浮点数运算
浮点数虽然表示的范围大，但是，浮点数有个非常重要的特点，就是浮点数常常无法精确表示。
在一个复杂的四则运算中，两个整数的运算不会出现自动提升的情况
需要特别注意，在一个复杂的四则运算中，两个整数的运算不会出现自动提升的情况。例如：
```java
double d = 1.2 + 24 / 5; // 5.2
```
计算结果为5.2，原因是编译器计算24 / 5这个子表达式时，按两个整数进行运算，结果仍为整数4。

### 溢出
整数运算在除数为0时会报错，而浮点数运算在除数为0时，不会报错，但会返回几个特殊值：

`NaN`表示`Not a Number`
`Infinity`表示无穷大
`-Infinity`表示负无穷大
例如：
```
double d1 = 0.0 / 0; // NaN
double d2 = 1.0 / 0; // Infinity
double d3 = -1.0 / 0; // -Infinity
```

可以将浮点数强制转型为整数。在转型时，浮点数的小数部分会被丢掉。如果转型后超过了整型能表示的最大范围，将返回整型的最大值。

Java还提供一个三元运算符b ? x : y，它根据第一个布尔表达式的结果，分别返回后续两个表达式之一的计算结果。示例：

### 短路运算
布尔运算的一个重要特点是短路运算。
* `false && x`的结果总是`false`
* `true || x`的结果总是`true`
如果一个布尔运算的表达式能提前确定结果，则后续的计算不再执行，直接返回结果。

### 三元运算符
```
// 三元运算
public class Main {
    public static void main(String[] args) {
        int n = -100;
        int x = n >= 0 ? n : -n;
        System.out.println(x);
    }
}
```
>> 100

上述语句的意思是，判断`n >= 0`是否成立，如果为`true`，则返回`n`，否则返回`-n`。这实际上是一个求绝对值的表达式。

## 字符和字符串
在Java中，字符`char`和字符串`String`是两个不同的类型<br>
一个`char`保存一个Unicode字, Java在内存中总是使用Unicode表示字符
```java
char c1 = 'A'; // 字母“A”的Unicodde编码是65
int n1 = 'A'; // 字母“A”的Unicodde编码是65







