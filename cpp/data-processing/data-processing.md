## 数据处理


### 变量

为把信息存储在计算机中，程序必须记录3个基本属性：  
* 信息将存储在哪里
* 要存储什么值
* 存储何种类型的信息


**命名规则**  
* 在名称中只能使用字母字符、数字和下划线
* 名称的第一个字符不能是数字
* 区分字符大小写
* 不能将 C++ 关键字用作名称
* 以两个下划线打头或以下划线和大写字母打头的名称被保留给实现（编译器及其使用的资源）使用
* 以一个下划线开头的名称被保留给实现，用作全局标识符
* C++ 对于名称的长度没有限制，名称中所有的字符都有意义，但有些平台有长度限制



### 整型

整数就是没有小数部分的数字  



**类型宽度**  

* short 至少 16 位
* int 至少与 short 一样长
* long 至少 32 位，且至少与 int 一样长
* long long 至少 64 位，且至少与 long 一样长


由于在不同的系统中，这些类型的为数可能不同，所以就需要对其进行查询  


---


**sizeof 运算符**

sizeof 运算符返回类型或变量的长度，单位为字节


使用：

对于类型名，使用 sizeof 运算符时，应将名称放在括号中

但对变量名，使用 sizeof 运算符时，括号是可选的  
> 一般不加括号，用于辨别是判断的类型名还是变量名  

```cpp
cout << "int is " << sizeof (int) << " bytes." << endl;
cout << "short is " << sizeof n_short << " bytes." << endl;
```


---


**climits 头文件**

头文件 climits 包含了关于整数限制的信息  
头文件 climits 定义了**符号常量**来表示类型的限制


---


**climits 中的符号常量**

| 符号常量   | 表示                        |
|------------|-----------------------------|
| CHAR_BIT   | char 的位数                 |
| CHAR_MAX   | char 的最大值               |
| CHAR_MIN   | char 的最小值               |
| SCHAR_MAX  | signed char 的最大值        |
| SCHAR_MIN  | signed char 的最小值        |
| UCHAR_MAX  | unsigned char 的最大值      |
| SHRT_MAX   | short 的最大值              |
| SHRT_MIN   | short 的最小值              |
| USHRT_MAX  | unsigned short 的最大值     |
| INT_MAX    | int 的最大值                |
| INT_MIN    | int 的最小值                |
| UINT_MAX   | unsigned int 的最大值       |
| LONG_MAX   | long 的最大值               |
| LONG_MIN   | long 的最小值               |
| ULONG_MAX  | unsigned long 的最大值      |
| LLONG_MAX  | long long 的最大值          |
| LLONG_MIN  | long long 的最小值          |
| ULLONG_MAX | unsigned long long 的最大值 |


---


**初始化**

初始化将声明与赋值合并在一起

**应尽量对变量进行初始化**  
> 为了避免声明后忘记赋值产生的错误


---


**选择整数类型**  

通常，int 被设置为对目标机器而言最为**自然**的长度  

**自然长度**
: 是指计算机处理起来效率最高的长度  
> 如果没有非常有说服力的理由来选择其他类型，则应使用 int  


如果知道变量可能表示的整数值大于16位整数的最大可能值，则使用 long，即使系统上使用的 int 为32位  
> 因为在其他系统上，int 可能为16位  
> 这样不利于程序的移植  


如果需要存储的值超过20亿，可使用 long long  


当有大型整型数组时，并且需要节省内存，在存储数值范围允许的情况下，应使用 short，而不是 int，即使它们的长度一样  
> 假设要将程序从 int 为16位的系统移到 int 为32位的系统，则用于存储 int 数组的内存容量将加倍，但 short 数组不受影响  
> 能节省一点就是赢得一点  


---


**整型字面值**  

整型字面值（常量）是显式地书写的常量  
> 也就是 整型常量  


可以有三种不同的计数方式来书写整数：十进制，八进制，十六进制  
对于整型常量的书写：
* 第一位为 0，则表示八进制
    ```cpp
    int oct = 043;
    ```
* 前两位为 0x，则表示十六进制
    ```cpp
    int hexa = 0x43;
    ```
* 第一位不为0，则表示十进制
    ```cpp
    int dec = 43;
    ```



**默认情况下，cout 以十进制格式显示整数**  

如果想要将数字以其他格式显式，则可以使用 cout 的一些特性  
`endl` 是头文件 iostream 提供的控制符。同样，也提供了控制符 dec、hex 和 oct，分别用于指示 cout 以十进制、十六进制和八进制格式显式整数  

例如：
```cpp
cout << hex;
```

> 此例不会在屏幕上显式任何内容，而只是修改 cout 显示整数的方式  
> 之后 cout 显式的方式都以这种格式显式  
> 
> 控制符 hex 实际上是一条消息，告诉 cout 采取任何行为  



**常量的类型**  

除非有理由存储为其他类型（如使用了**特殊的后缀**来表示特定的类型，或者**值太大**，不能存储为 int），否则 **C++ 将整型常量存储为 int 类型**  

后缀是放在数字常量后面的字母，用于表示类型  
整数的后缀：  
* l 或 L：表示该整数为 long 常量
* u 或 U：表示该整数为 unsigned int 常量
* ul（大小写皆可）：表示该整数为 unsigned long 常量
* ll 或 LL：表示该整数为 long long 常量
* ull（大小写皆可）：表示该整数为 unsigned long long 常量


```cpp
int a = 22;                  // int 类型
int b = 22u;                 // unsigned int 类型
int c = 22L;                 // long 类型
int d = 22uL;                // unsigned long 类型
int e = 22LL;                // long long 类型
int f = 22uLL;               // unsigned long long 类型
```



对于不带后缀的十进制整数  
将使用下面几种类型中能够存储该数最小类型来表示：int、long、long long
> 因为以十进制描述的数有正负数

而对于不带后缀的十六进制和八进制整数  
将使用下面几种类型中能够存储该数最小类型来表示：int、unsigned int、long、unsigned long、long long 或 unsigned long long  
> 这是因为十六进制常用来表示内存地址，而内存地址是没有符号的




### 字符型

存储的依然是小整数  
但是在显示时，通过字符编码表来将存储的小整数与字符编码表中的字符进行对应  

**C++使用的是主机系统的编码**  

---

输入时，cin 将键盘输入的 M 转换为 77  
输出时，cout 将值 77 转换为所显示的字符 M  

**cin 和 cout 的自动转换行为是由变量类型引导的**  
值的类型将引导 cout 选择如何显示值  
> 正因为变量类型是 char，所以才会转换  
> 如果将 77 存储在 int 变量中，则 cout 将把它显示为 77（也就是来能够个字符 7）  

---

`cout.put()` 函数显示一个字符  

---

对于 char 类型，在不同的系统中，char 所表示的可能是 signed 类型，也可能是 unsigned 类型  
由于这种不确定性，可以对 char 所表示的类型进行指定  
```cpp
unsigned char bar;           // 定义 char 为 unsigned
signed char snark;           // 定义 char 为 signed
```
---

8 位 char 可以表示基本字符集  
wchar_t （宽字符类型）可以表示扩展字符集
> wchar_t 类型是一种整数类型，它有足够的空间，可以表示系统使用的最大扩展字符集  


cin 和 cout 将输入和输出看作是 char 流，因此不适合用来处理 wchar_t类型  
iostream 头文件的最新版本提供了作用相似的工具：wcin、wcout，可用于处理 wchar_t 流  

另外还可以通过加前缀 L 来指示宽字符常量和宽字符串：
```cpp
wchar_t bob = L'P';
wcout << L"tall" << endl;
```

由于 wchar_t 类型的长度随实现而异，而有时需要固定长度的类型，就有了 char16_t 和 char32_t 类型  
* char16_t：16 位无符号  
* char32_t：32 位无符号  

使用前缀 u 表示 char16_t 字符常量  
```cpp
char16_t ch1 = u'C';         // 存储为 16bit 格式
```

使用前缀 U 表示 char32_t 字符常量  
```cpp
char32_t ch2 = U'C';         // 存储为 32bit 格式
```



类型 char16_t 与 \u00F6 形式的通用字符名匹配
```cpp
char16_t ch3 = u'\u00F6';
```

类型 char32_t 与 \U0000222B 形式的通用字符名匹配  
```cpp
char32_t ch4 = U'\U0000222B';
```




### 布尔型

布尔类型分别用与定义的字面值 true 和 false 表示  

字面值 true 和 false 都可以通过提升转换为 int 类型，true 被转换为 1，而 false 被转换为 0  
```cpp
int ans = true;            // ans 的值为1
int promise = false;       // promise 的值为0
```

任何非零值都被转换为 true，而零被转换为 false  
```cpp
bool start = -100;         // start 代表 true
bool stop = 0;             // stop 代表 false
```





### 浮点型

浮点数能够表示小数值、非常大和非常小的值，其内部存储与整数存储完全不同  

浮点表示法有标准的小数点表示法和科学计数法  
标准小数点表示法用于正常书写  
科学计数法用于记录非常大或非常小的值  

---

C++ 有3种浮点类型，按照它们可以表示的有效数位和允许的指数最小范围来描述可分为：float、double、long double  
> 有效位：是数字中有意义的位  

对于有效位数的要求：  
* float 至少 32 位
* double 至少 48 位，且不少于 float
* long double 至少和 double 一样多


这三种类型的**有效位数**可以一样多  
通常，float 为 32 位，double 为 64 位，long double 为 80、96 或 128 位  

这三种类型的**指数范围**至少是 -37 到 37  

可以从头文件 cfloat 和 float.h 中找到系统限制  

---

**浮点常量**  

通常，浮点常量通常属于 double 类型  

如果希望常量为 float 类型，在常量后加上后缀 f 或 F  
如果希望常量为 long double 类型，在常量后加上后缀 l 或 L

例如：
```cpp
1.234f              // float 类型
2.34E20F            // float 类型
2.345566E28         // double 类型
2.2L                // long double 类型
```

---

**优缺点**  

优点：
1. 可以表示整数之间的值
2. 表示的范围大得多

缺点：
1. 运算的速度通常比整数运算慢
2. 精度降低



---




### const 限定符

为什么使用 const 而不是 #define？
1. const 能够明确指定类型
2. const 可以使用作用域规则将定义限制在特定的函数或文件中
3. const 可以用于更复杂的类型

---

符号名称指出了常量表示的内容  
> 例如：
> ```cpp
> cost int Months = 12;
> ```
>
> 12 表示了一年中有 12 个月份  

---

关键字 const 叫作限定符，因为它限定了声明的含义  

创建常量的通用格式：
```cpp
const type name = value;
```





### 类型转换


#### 初始化和赋值进行的转换

