> 本文内容由[Simics](https://zh.wikipedia.org/wiki/Simics)转换而来。


**Simics** 是一种完整系统模拟技术，为软件和系统开发人员、架构师、测试工程师提供为各种目的构建和使用[虚拟系统或创建多个虚拟连接系统的方法](https://zh.wikipedia.org/wiki/虚拟系统 "wikilink")。\[1\]Simics最初由瑞典计算机科学研究院（SICS）开发，后于1998年派生出Virtutech公司进行商业化开发 \[2\]。现在是风河公司的产品\[3\]。

Simics能仿真诸如Alpha、AMD64、ARM、ARM64、EM64T、IA-64、MIPS（32位和64位）、MSP430、Powerpc（32位和64位）、POWER、SPARC-V8/V9、x86等多种系统，并且可以在这些仿真硬件上运行多种操作系统，包括MS-DOS、Windows、Vxworks、OSE、Solaris、FreeBSD、Linux、QNX和RTEMS等。NetBSD公司的AMD64接口在芯片公开发行之前最初是用Simics开发的。\[4\]用Simics进行仿真的目的经常是使用Simics虚拟一些特定类型的嵌入式硬件平台来开发软件。

Simics 3.0，发布于2005年秋，包含下列新技术：

  - 设备建模语言（DML）
  - 设备建模语言编译器（DMLC）
  - Hindsight -virtutech宣称其为世界上第一个支持回溯操作的通用开发工具

DML语言的加入提供了一个更便捷的方式去开发和配置一些像ASICs和FPGAs这样的非标准器件。在现代系统中DML代码极大的增强了管理成百乃至上千个寄存器的自动化程度。DMLC是DML语言的编译器，它把DML语言转化成高效的设备模型，使得Simics在仿真一个完整的电子系统时的速度可以达到每秒运行数十万指令以上。DML使程序开发员可以提早进行程序开发，从而节约时间并且削减了产品的开发周期。

Virtutech已经把Simics 3.0纳入了Eclipse框架。对于用Eclipse作为他们的[集成开发环境](../Page/集成开发环境.md "wikilink")（IDE）的客户来说，Simics能提供全系统仿真，包括回溯调试和Hindsight执行功能。

目前Simics的最新版本是5.0，同时支持Windows和Linux平台。

## 来源参考

<references/>

"On February 5, 2010, Wind River, a wholly owned subsidiary of Intel Corporation, announced it will add the Virtutech product line to its embedded software product portfolio after the completion of Intel Corporation's acquisition of Virtutech. Read the press release. This process is now complete and Simics is now a Wind River product." From <https://www.simics.net/> 在2010年2月5日，Wind River，Intel旗下的一个全资子公司宣布，当Intel完全取得Virtutech之后，他们将把Virtutech产品线加入到它的嵌入式软件产品中。 而现在，这个过程已经完成，Simics现在是Wind River产品了。

## 外部链接

  - [Simics Homepage](http://www.virtutech.com/products/)

  - [Simics Unleashed – Applications of Virtual Platforms](https://archive.is/20131210052527/https://noggin.intel.com/technology-journal/2013/172/simics-unleashed-%E2%80%93-applications-virtual-platforms) (英特爾技術期刊專題報告)

[Category:虛擬化軟體](https://zh.wikipedia.org/wiki/Category:虛擬化軟體 "wikilink") [Category:矽谷公司](https://zh.wikipedia.org/wiki/Category:矽谷公司 "wikilink")

1.  [1](http://www.intel.com/p/zh_CN/embedded/hwsw/software/simics#overview), 英特尔嵌入式-\>硬件与软件-\>软件
2.  [Simics Hindsight: Reverse Execution for Software Debugging](http://www.virtual-strategy.com/article/articleview/842/1/2), Virtual Strategy Magazine, May 4, 2005
3.  [2](http://www.windriver.com/products/simics/)
4.  [Simics used to port an OS](http://netbsd.org/Ports/amd64/)