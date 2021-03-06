> 本文内容由[IRQL](https://zh.wikipedia.org/wiki/IRQL)转换而来。


**IRQL**是**Interrupt Request Level**的缩写，即中断请求级别。是[Windows操作系统使用的处理器](../Page/Windows_NT.md "wikilink")[中断级别](https://zh.wikipedia.org/wiki/中断 "wikilink")。

## 简介

Windows操作系统运行的处理器架构中，硬件产生信号发给. 中断控制器发送 (IRQ)及相应的优先级给CPU，CPU设置一个掩码(mask)屏蔽低优先级的其他中断请求到挂起状态(pending state),直到CPU释放控制给中断控制器。如果到来的中断有更高优先级，那么当前中断被挂起，CPU处理高优先级的中断。\[1\]

Windows把硬件中断与软件中断都映射到内部的中断表内。这就是中断请求级别IRQL。多核处理器的每个内核有自己单独的IRQL。[异步过程调用](../Page/异步过程调用.md "wikilink")、用户态线程、内核模式操作都可以被中断，因此它们的IRQL低于线程调度器（或称分派器）。\[2\]

## 级别

在[DDK帮助文档中有IRQL的级别](https://zh.wikipedia.org/wiki/DDK "wikilink")：

|               | IRQL               | 宏                                                                                                                                          | 描述                                                                               |
| ------------- | ------------------ | ------------------------------------------------------------------------------------------------------------------------------------------ | -------------------------------------------------------------------------------- |
| 软件IRQL        | 0                  | PASSIVE_LEVEL                                                                                                                             | 最低级别, 没有被屏蔽的中断。线程执行用户模式，可以访问[分页内存](https://zh.wikipedia.org/wiki/分页 "wikilink")。 |
| LOW_LEVEL    |                    |                                                                                                                                            |                                                                                  |
| 0             | intermediate level | 运行在临界区内的线程。调用KeGetCurrentIrql返回PASSIVE_LEVEL。调用KeAreApcsDisabled来检查是否在临界区内。在本层或更高层的驱动程序不能suspended。                                       |                                                                                  |
| 1             | APC_LEVEL         | 异步调用层。当有[异步过程调用](../Page/异步过程调用.md "wikilink")APC发生时，处理器提升到APC级别，因而就屏蔽了其它APC。可以访问分页内存。用KeAcquireFastMutex与KeReleaseFastMutex函数调用可以进入/退出本层。 |                                                                                  |
| 2             | DISPATCH_LEVEL    | 分发派遣层。DPC和更低的中断被屏蔽，不能访问分页内存，因为缺页中断也是在这个层。线程调度器也在此层，调度时只考虑优先级，因此APC_LEVEL上的线程被阻塞后，可以调度执行PASSIVE_LEVEL线程。                                  |                                                                                  |
| 硬件IRQL        | 3-26               | DIRQL (Device IRQL)                                                                                                                        | 设备IRQL 几乎所有的中断被屏蔽                                                                |
| 27            | PROFILE_LEVEL     | 使用PRILFILE的定时器                                                                                                                             |                                                                                  |
| 28            | CLOCK1_LEVEL      | 未在X86使用                                                                                                                                    |                                                                                  |
| CLOCK2_LEVEL | 内部定时器2             |                                                                                                                                            |                                                                                  |
| SYNCH_LEVEL  | 同步层                |                                                                                                                                            |                                                                                  |
| 29            | IPL_LEVEL         | 中断内部处理层                                                                                                                                    |                                                                                  |
| 30            | POWER_LEVEL       | 电源故障层                                                                                                                                      |                                                                                  |
| 31            | HIGH_LEVEL        | 最高中断层                                                                                                                                      |                                                                                  |

## API

内核函数KeGetCurrentIRQL取得处理器当前的IRQL。

## 参见

  -
  -
## 参考文献

<references />

[Category:Microsoft_Windows](https://zh.wikipedia.org/wiki/Category:Microsoft_Windows "wikilink")

1.
2.