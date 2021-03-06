**stdlib.h**是[C标准函数库的](https://zh.wikipedia.org/wiki/C标准函数库 "wikilink")[头文件](../Page/头文件.md "wikilink")，声明了数值与字符串转换函数, 伪随机数生成函数, 动态内存分配函数, 进程控制函数等公共函数。 [C++](../Page/C++.md "wikilink")程序应调用等价的`cstdlib`头文件.

## 常量

`stdlib.h`中定义的常量:

| 名字                                   | 值                            | 描述                                                                                                                      |
| ------------------------------------ | ---------------------------- | ----------------------------------------------------------------------------------------------------------------------- |
| [`NULL`](../Page/NULL.md "wikilink") | 一般定义为`0`, 或`0L`, 或`(void*)0` | 表示[空指针常量的](https://zh.wikipedia.org/wiki/空指针 "wikilink")[巨集](../Page/巨集.md "wikilink"); 换句话说，一个常量用来表示一个总是指向无效的内存地址的指针值。 |
| `EXIT_FAILURE`                       | 一个非`0`值                      | 用来指示程序失败的结束，一般用于`exit()`.                                                                                               |
| `EXIT_SUCCESS`                       | `0`                          | 用来指示程序成功的结束，一般用于`exit()`..                                                                                              |
| `RAND_MAX`                           | `>= 32767`                   | 函数`rand()`所能返回的最大的值.                                                                                                    |
| `MB_CUR_MAX`                         |                              | 当前locale中多字节字符的最大字节数目                                                                                                   |

## 数据类型

`stdlib.h`中定义的[数据类型](https://zh.wikipedia.org/wiki/数据类型 "wikilink")：

| 名字                           | 描述                                                                                |
| ---------------------------- | --------------------------------------------------------------------------------- |
| `size_t`                     | 算子[`sizeof`](https://zh.wikipedia.org/wiki/sizeof "wikilink")返回结果的数据类型，实际上是无符号整型. |
| `div_t` ， `ldiv_t`，`lldiv_t` | 函数`div`, `ldiv`, `lldiv`的返回结果的数据类型，实际上是包含两个整数的结构类型.                               |

## 函数

`stdlib.h`中声明的库函数可分为六类：类型转换、伪随机数、动态内存分配与回收管理、进程控制、搜索及排序、简单数学。

| 名字                        | 描述                                                                                                                                                                                                                               |
| ------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| <big>类型转换</big>           |                                                                                                                                                                                                                                  |
| `atof`                    | 把[字符串](../Page/字符串.md "wikilink")转换为双精度浮点数。相当于`strtod(s, (char**)NULL)`.                                                                                                                                                         |
| `atoi`                    | 把字符串转换为整型. 相当于`(int)strtol(s, (char**)NULL, 10)`.                                                                                                                                                                                |
| `atol`                    | 把字符串转换为长整型. Equivalente a `strtol(s, (char**)NULL, 10)`.                                                                                                                                                                         |
| `atoll`                   | 把字符串转换为长长整型. Equivalente a `strtol(s, (char**)NULL, 10)`. 这是[C99新增加的库函数](https://zh.wikipedia.org/wiki/C99 "wikilink")。                                                                                                          |
| `strtod`                  | 把字符串转换为双精度浮点数，检查结果是否溢出，并返回字符串不能转换部分的地址.                                                                                                                                                                                          |
| `strtof`                  | 把字符串转换为单精度浮点数，检查结果是否溢出，并返回字符串不能转换部分的地址.                                                                                                                                                                                          |
| `strtold`                 | 把字符串转换为长双精度浮点数，检查结果是否溢出，并返回字符串不能转换部分的地址.                                                                                                                                                                                         |
| `strtol`                  | 把字符串转换为长整型，检查结果是否溢出，并返回字符串不能转换部分的地址.                                                                                                                                                                                             |
| `strtoll`                 | 把字符串转换为`long long int`，检查结果是否溢出，并返回字符串不能转换部分的地址.                                                                                                                                                                                 |
| `strtoul`                 | 把字符串转换为无符号长整形，检查结果是否溢出，并返回字符串不能转换部分的地址.                                                                                                                                                                                          |
| `strtoull`                | 把字符串转换为`unsigned long long int`，检查结果是否溢出，并返回字符串不能转换部分的地址.                                                                                                                                                                        |
| <big>伪随机数序列生成</big>       |                                                                                                                                                                                                                                  |
| `rand`                    | 返回在0到RAND_MAX之间的伪随机数. 不接受参数作为随机数种子，因此产生的伪随机数列相同，有利于程序调试。                                                                                                                                                                        |
| `srand`                   | 初始化`rand()`接受无符号整型参数作为伪随机数种子.如果种子相同，伪随机数列也相同。                                                                                                                                                                                    |
| <big> 内存的分配与释放</big>      |                                                                                                                                                                                                                                  |
| `aligned_alloc`           | 边界对齐的动态内存分配.                                                                                                                                                                                                                     |
| `calloc`                  | 数组的动态内存分配，且初始化为全零                                                                                                                                                                                                                |
| `malloc`                  | 动态内存分配，其内容不初始化                                                                                                                                                                                                                   |
| `realloc`                 | 释放老的动态内存块，按照给出的尺寸分配新的动态内存块，老的内存块的内容尽量复制到新的内存块                                                                                                                                                                                    |
| `free`                    | 系统释放动态分配的内存. 如果是空指针，则无动作发生；如果指针所指不是动态分配的内存块或者是已释放的内存块，则行为是未定义的。                                                                                                                                                                  |
| <big> 进程控制/与运行环境的沟通</big> |                                                                                                                                                                                                                                  |
| `abort`                   | 导致程序非正常的结束，各种流缓冲区与临时文件直接放弃。实际上抛出`raise(SIGABRT)`，缺省的信号处理行为是使用退出代码3执行终止（terminate）操作。如果`SIGABRT`被捕捉且信号处理程序不返回，则程序将不终止.                                                                                                            |
| `atexit`                  | 登记一个函数，当程序使用`exit`正常退出时被登记的函数自动被调用.                                                                                                                                                                                              |
| `exit`                    | 程序正常终止。首先`atexit()`登记的函数按照登记的逆序被调用；如果多次调用`atexit`登记了多个函数，按照登记的逆序调用这些函数。如果一个函数被登记了多次，则程序正常退出时该函数也将被调用多次。然后所有缓冲区中的数据被写回(flushed)；所有打开着的流被关闭；`tmpfile`函数创建的文件被删除。最后，控制权返回给调用环境，返回数值表示程序返回时的状态，0表示`EXIT_SUCCESS`, 1表示`EXIT_FAILURE`. |
| `at_quick_exit`           | 登记一个函数，当程序使用`quick_exit`正常退出时被登记的函数自动被调用.                                                                                                                                                                                        |
| `_Exit`                   | 程序正常终止, 但`atexit()`, `at_quick_exit()`, `signal()`登记的函数不被调用; 打开的流、文件是否被关闭，由编译器的实现者决定                                                                                                                                             |
| `getenv`                  | 获得某一个环境变量的字符串值，如果该环境变量不存在，返回`NULL`.                                                                                                                                                                                              |
| `quick_exit`              | 程序正常终止, 但`atexit()`, 登记的函数不被调用; `at_quick_exit()`登记的函数按登记顺序的逆序被调用。                                                                                                                                                               |
| `system`                  | 把参数作为外部环境的命令执行。 如果参数为空，则判断外部环境是否有命令解释器。                                                                                                                                                                                          |
| <big> 搜索与排序 </big>        |                                                                                                                                                                                                                                  |
| `bsearch`                 | 折半搜索.                                                                                                                                                                                                                            |
| `qsort`                   | 快速排序.                                                                                                                                                                                                                            |
| <big> 整数算术</big>          |                                                                                                                                                                                                                                  |
| `abs, labs, llabs`        | 计算整数的绝对值.                                                                                                                                                                                                                        |
| `div, ldiv, lldiv`        | 计算整数除法的商与余数.                                                                                                                                                                                                                     |
| <big> 多字节字符/宽字符转换</big>   |                                                                                                                                                                                                                                  |
| `mblen`                   | 计算多字节字符的长度并确定是否为有效字符 .                                                                                                                                                                                                           |
| `mbtowc`                  | 多字节字符转换为宽字符.                                                                                                                                                                                                                     |
| `wctomb`                  | 宽字符转换为多字节字符.                                                                                                                                                                                                                     |
| <big> 多字节字符串/宽字符串转换</big> |                                                                                                                                                                                                                                  |
| `mbstowcs`                | 多字节字符串转换为宽字符串.                                                                                                                                                                                                                   |
| `wcstombs`                | 宽字符串转换为多字节字符串.                                                                                                                                                                                                                   |

[Category:C标准库头文件](https://zh.wikipedia.org/wiki/Category:C标准库头文件 "wikilink")