> 本文内容由[ABAP](https://zh.wikipedia.org/wiki/ABAP)转换而来。


**ABAP**（高级商务应用编程）是一种[高级语言](https://zh.wikipedia.org/wiki/高级语言 "wikilink")，由[德国](../Page/德国.md "wikilink")[软件](../Page/软件.md "wikilink")公司[SAP开发](../Page/SAP公司.md "wikilink")。目前，和最近引入的Java一起，ABAP主要用作SAP的编程。这个服务器软件是SAP [NetWeaver](../Page/NetWeaver.md "wikilink")平台的一部分，这个平台主要用来开发商务应用。ABAP支持有面向过程和面向对象。

## 历史

ABAP作为一种面向特定应用的[第四代编程语言最早在](https://zh.wikipedia.org/wiki/第四代编程语言 "wikilink")20世纪80年代开发。它原本是作为一种报表语言应用在[SAP R/2上](https://zh.wikipedia.org/wiki/SAP_R/2 "wikilink")，这是一个帮助大型公司在大型机上建立原材料管理和财务会计管理商务应用的平台。ABAP本来也是德语***A**llgemeiner **B**erichts**a**ufbereitungs**p**rozessor*的缩写，意思是“通用报表预处理器”。ABAP第一次引入了“逻辑数据库”的概念，它在基本的数据库层提供了更高级的抽象。

ABAP编程语言最初被SAP的开发者用于开发[SAP R/3平台](https://zh.wikipedia.org/wiki/SAP_R/3 "wikilink")。但它也被设计让SAP的客户用于增强SAP的软件应用–客户可以用ABAP编程开发自定义的报表和界面。这个编程语言对于程序员来说很容易学习但并不是一个非程序设计人员可以直接使用的工具。编写ABAP程序需要良好的编程技巧和关系数据库方面的知识，如果知道面向对象设计的概念更好。

虽然SAP最早于1992年就发布了[R/3](https://zh.wikipedia.org/wiki/SAP_R/3 "wikilink")，但ABAP现在仍可以用于为[R/3系统编写程序](https://zh.wikipedia.org/wiki/SAP_R/3 "wikilink")。在20世纪90年代，随着计算机硬件的发展，越来越多的SAP的应用软件和系统都用ABAP来实现。一直到2001年，几乎所有的基本功能都是由ABAP编程实现的。在1999年，SAP在发布R/3 4.6版的同时也发布了一个对ABAP的面向对象扩展，叫做ABAP Objects。

SAP最新的开发平台[NetWeaver](../Page/NetWeaver.md "wikilink")同时支持ABAP和[Java](../Page/Java.md "wikilink")。

## 实现

### ABAP程序运行在哪里?

所有的ABAP程序都驻留在SAP数据库里。他们不像Java或者C++程序那样存储在一个单独的外部文件里，在数据库里所有的ABAP代码都以两种形式存在：可以用ABAP workbench查看和编辑的源代码和由ABAP运行环境载入和解释的“编译”代码（技术上更精确地说是“产生”代码）。当一段ABAP源代码第一次被调用时会隐含的进行代码产生。如果稍后源代码改变了或者程序访问的对象改变了（比如数据库的表添加了新的字段），产生代码就会自动重新产生。

ABAP程序在运行时系统（SAP核心的一部分）的控制下运行在SAP应用服务器里。运行时系统负责处理ABAP语句，控制显示的逻辑序列和响应事件（比如，用户按一下屏幕上的一个按钮）。ABAP运行时系统的一个关键组件是数据库接口，它把ABAP的数据库无关语句（“开放SQL”）变成底层数据库管理系统可以理解的语句（“本地SQL”）。数据库接口处理ABAP程序和关系数据库之间所有的通信；它也有一些其他的作用，比如把经常访问的数据缓存到应用服务器本地的存储器里。

### SAP系统和部署方案

所有的SAP数据和软件都存在／运行于**SAP系统**的环境中。这个系统包括一个中心关系数据库和一个或多个访问该数据库里的数据和程序的应用服务器（“实例”）。一个SAP系统至少包括一个实例，但可以更多，主要看大小和性能上的需求。在一个多实例系统中，负载平衡机制来保证负载比较平均的分摊到各个可用的应用服务器上。
典型安装的[Web应用服务器](../Page/SAP_Web应用服务器.md "wikilink")（**部署方案**）包括三个系统：一个用于开发，一个用于测试和质量保证，一个用于生产。这个部署方案可以包含更多的系统，比如一个单独用于单元测试和产前测试的系统，或者也可以不完全包含这三个系统，比如只有开发和生产，没有单独的质量保证系统；但三个是最常见的。ABAP程序的创建和首次运行都在开发系统里。然后被分发到部署方案的其他系统里。这些都是在变化和传输系统（CTS）的控制下进行的。CTS是一个负责并发控制（比如防止两个开发人员同时修改同一段代码），版本管理和在质量保证和产品系统上部署程序的系统。

[Web应用服务器有三层组成](../Page/SAP_Web应用服务器.md "wikilink")：数据库层，应用层和表现层。这些层可以在同一台或不同的物理机器上运行。数据库层包括关系数据库及相关软件。应用层包括系统的实例。所有应用相关的过程，包括业务事务和ABAP开发，都运行在应用层。表现层处理和系统的用户之间的交互。对ABAP应用服务器的在线访问可以通过专用图形接口SAPGUI或者浏览器进行。

## ABAP程序的类型

ABAP有两种不同类型的程序：

### 报表程序

**报表程序**遵循一个相对简单的编程模型，用户可选的输入一系列参数（比如，在一个数据子集上的选择），然后程序根据输入的参数以一个交互式列表的形式产生一张报表。报表程序的输出之所以是交互式的是因为它不是一个被动的显示；它允许用户使用ABAP语言通过深入挖掘功能以获得某个数据更细节的视图，或者通过菜单命令触发更深入的处理，比如按不同的方式排序数据或者按某种选择条件过滤数据。这种表现报表的方法有很大的优势，特别是对于那些需要处理大量信息但又要以很灵活的方式来检查这些信息的用户，这样他们就不会再被限制到一种固定的显示形式或者大小上无法管理的列表形式的报表中了。这种方便的开发交互式报表的方式是ABAP语言的一大重要闪光点。
“报表”这个词有时会给人一种误解，其实创建数据可以在底层数据库修改而不仅仅是只读的报表程序是完全可以的。

### 在线程序

**在线程序**（也叫模块池）不产生列表。这些程序使用一系列的屏幕来定义更复杂的用户交互模式。术语“屏幕”是指用户看到的实际的物理图像。每个屏幕还有一个“流逻辑”；这是指由屏幕触发的ABAP代码，比如初始化屏幕，响应用户请求的应答和控制模块池的屏幕之间的序列的逻辑。每个屏幕都有自己的流逻辑，每个流逻辑都分为“PBO”（输出前处理）和“PAI”（输入后处理）部分。在SAP的文档中，术语“dynpro”（动态程序）用来表示这种屏幕和流逻辑的结合。
在线程序并不是通过名字调用的，而是和一段事务代码联系在一起。用户可以通过自定义，角色依赖，事务菜单来触发它们。

除了报表和在线程序外，以类库，功能库和子程序池的形式开发共享代码段也是可以的。

## ABAP Workbench

ABAP Workbench有几个不同的工具用于编辑容器对象。这些工具可以为你提供涵盖整个软件开发周期各阶段的辅助。创建和编辑容器对象的最重要的工具有：
**ABAP Editer**：编写程序代码
**ABAP Dictionary**：处理数据库表定义，检索全局类型
**Menu Painter**：设计用户界面（包括菜单栏，标准工具栏，应用栏，配置功能键）
**Screen Painter**：为用户对话框设计屏幕（动态程序）
**Function Builder**：显示和处理功能模块
**Class Builder**：显示和处理ABAP对象类

## 參看

  - [ERP software](https://zh.wikipedia.org/wiki/ERP_software "wikilink")
  - [asXML](https://zh.wikipedia.org/wiki/asXML "wikilink")

## 外部連結

  - [SAP Help Portal](http://help.sap.com)
  - [ABAP](http://arquivo.pt/wayback/20081022110438/https%3A//www.sdn.sap.com/irj/sdn/abap) in the [SAP Developer Network](http://www.sdn.sap.com)
  - [Useful SAP articles](http://theblogwhichsaysall.blogspot.com/search/label/SAP)
  - [SAP Tutorials](https://sapbrainsonline.com)
  - [ABAP Objects](http://help.sap.com/saphelp_nw2004s/helpdata/en/ce/b518b6513611d194a50000e8353423/frameset.htm)

[Category:SAP公司产品](https://zh.wikipedia.org/wiki/Category:SAP公司产品 "wikilink") [Category:程序设计语言](https://zh.wikipedia.org/wiki/Category:程序设计语言 "wikilink")