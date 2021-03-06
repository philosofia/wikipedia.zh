> 本文内容由[AUTOSAR](https://zh.wikipedia.org/wiki/AUTOSAR)转换而来。


**AUTOSAR**（汽车开放系统架构）联盟成立于 2003 年，联盟中的各个成员保持着汽车业内的开发合作关系。该联盟致力于为汽车电子控制装置开发一个开放的、标准化的软件架构。其目标包括不同车款和平台的延展性开发、软件迁移、有效性和安全需求的考量、各方合作关系的建立、自然资源的持续利用、整个“产品生命周期”的维护服务\[1\]\[2\]。

## 历史

AUTOSAR 由宝马集团（[BMW](../Page/BMW.md "wikilink")）、[博世公司](../Page/罗伯特·博世公司.md "wikilink")（Bosch）、[大陆集团](https://zh.wikipedia.org/wiki/Continental_GT "wikilink")（Continental）、[戴姆勒-克莱斯勒公司](https://zh.wikipedia.org/wiki/Daimler "wikilink")（DaimlerChrysler）、西门子威迪欧（[Siemens](https://zh.wikipedia.org/wiki/Siemens "wikilink") VDO）[汽车电子公司以及大众公司（Volkswagen）于](https://zh.wikipedia.org/wiki/Volkswagen_Group "wikilink") 2003年 7 月联合建立，旨在为汽车电气/电子构架开发一套开放的行业标准。2003 [年福特汽车公司（Ford Motor Company）加入联盟](../Page/福特汽车.md "wikilink")，成为其核心成员。2003 年 12 月，[标致雪铁龙汽车公司（Peugeot Citroën Automobiles S.A.）](https://zh.wikipedia.org/wiki/Peugeot "wikilink")[和丰田汽车公司（Toyota Motor Corporation）加入联盟](../Page/丰田汽车.md "wikilink")。2004 年 11 月通用汽车公司（[General Motors](../Page/通用汽车.md "wikilink")）成为其核心成员\[3\] 。

2008 年 2 月，西门子威迪欧（Siemens VDO）汽车电子公司被大陆集团（Continental）收购，不再是 AUTOSAR 独立核心成员\[4\]。

自 2003 年起，AUTOSAR 共推出了四版主要的标准化汽车软件构架和一个验收测试版。AUTOSAR 的开发成果可以分为三个阶段：

  - 第一阶段（2004-2006）：标准规范的初步开发阶段（1.0、2.0 和 2.1版）
  - 第二阶段（2007-2009）：标准规范中的架构及其方式的补充阶段（3.0、3.1 和 4.0版）
  - 第三阶段（2010-2013）：维持和部分改进阶段（3.2、4.1 和 4.2版） \[5\] \[6\]

2013 年 AUTOSAR 始终努力维持着现有标准规范，并对部分标准加以改进（包括 R4.2 版和验收测试标准 1.0）。

2016年，AUTOSAR开始着手自适应平台的开发工作。 2017年初发布首个版本（17-03），2017年10月和2018年3月相继发布版本17-10和18-03。 其目标是在2018年10月联合发布AUTOSAR经典平台、自适应平台和基础，以此为节点结束主要开发活动。

## 理念和目标

AUTOSAR 制订了一系列标准规范，包括基础软件模块规范介绍、应用接口定义规范以及基于标准交换格式创建共同发展方法论的规范。AUTOSAR 分层软件架构中的基础软件模块层能够应用于不同厂家生产的车辆以及不同供应商提供的电子部件，从而降低了研发费用、适应了日趋复杂的汽车电气和软件构架\[7\]。 在这一原则的指导下，AUTOSAR 致力于为新型电子系统开辟一条新路，这既可以进一步提高性能、增强安全性且更加环保，又能够方便汽车使用周期内软硬件的更换和升级。AUTOSAR 旨在为迎接未来新技术做好准备，在保障质量的前提下，提高成本效益\[8\]\[9\]。

## 软件架构

[缩略图](https://zh.wikipedia.org/wiki/File:Autosar_architecture.png "fig:缩略图") AUTOSAR采用三层架构\[10\]：

  - 基础软件：标准化的软件模块（大多数），本身并不参加实际工作，但能够为上层软件功能正常运行提供必需服务\[11\] 。
  - 运行环境([RTE](https://zh.wikipedia.org/wiki/运行时系统 "wikilink"))：源自网络扑拓结构中的中介软件，用以实现 [ECU](https://zh.wikipedia.org/wiki/ECU "wikilink") 内部及不同 ECU 间的通信交换（应用软件组件之间以及基础软件和应用软件之间）\[12\]。
  - 应用层：应用软件组件与运行环境相辅相成\[13\]。

## AUTOSAR方法论

  - 系统配置描述：包含所有系统信息以及不同ECU之间约定的信息（例如总线信号的定义）。
  - ECU信息抽取：包含从系统配置描述抽取的特定ECU所需要的信息（例如特定ECU获取的信号）。
  - ECU配置描述：包含特定ECU所需要的所有基础软件配置信息。 根据这些信息生成执行软件、基础软件模块代码以及软件组件代码。\[14\]

## 经典平台(Classic Platform)

AUTOSAR经典平台是基于OSEK标准的嵌入式实时ECU标准。 其可交付成果主要为规范。 AUTOSAR经典平台架构区分了在微控制器上运行的应用、运行时环境（RTE）和基础软件（BSW）这三个软件层之间的最高抽象级\[15\]。 应用软件层基本独立于硬件。 软件组件之间通过RTE进行通信，访问BSW也必须通过RTE，RTE可视为应用程序的完整接口。

BSW分为三个主要层次并具有复杂的驱动因素：

  - 服务层， <span lang="EN-US">2016</span>
  - ECU（电子控制单元）抽象层和 <span lang="EN-US">2016</span>
  - 微控制器抽象层。<span lang="EN-US">2016</span>

服务层划分为代表系统、内存和通信服务基础设施的多个功能组。

经典平台的一个基本概念是虚拟功能总线（VFB）。 该虚拟总线是尚未部署到特定ECU的RTE抽象集，这些RTE将应用程序与基础架构分离。 它通过专用端口进行通信，这意味着应用软件的通信接口必须映射到这些端口。 VFB处理单个ECU内和多个ECU之间的通信。 从应用程序角度来看，不需要了解有关低级别技术或依赖关系的详细知识。 这样就使得应用软件的开发和使用无需依赖硬件进行。

经典平台还可以使用Franca接口描述语言（IDL）集成GENIVI等非AUTOSAR系统。

## 自适应平台(Adaptive Platform)

为适应新用例的需求，AUTOSAR开发了自适应平台。 一个突出的例子是

高度自动化驾驶，在该环境中，驾驶员暂时和/或部分地将驾驶责任转移给车辆。 这种情况下需要与交通基础设施（例如交通标志、交通灯）、云服务器（例如访问最新的交通信息或地图数据）等进行通信，或使用微处理器和高性能计算硬件进行并行处理（例如GPU）。

此外，Car-2-X应用还需要与车辆和车外系统进行交互沟通。 这意味着该系统必须具备安全的车载通信功能、支持跨域计算平台、智能手机集成、非AUTOSAR系统集成等。 此外，还需要采取专门的措施，保证云服务的安全，例如安全云交互和应急车辆优先。 它们可支持远程和分布式服务，例如远程诊断、空中下载（OTA）更新、修复和交换处理。

AUTOSAR目前正在对AUTOSAR自适应平台进行标准化处理，使其支持客户应用的动态部署，并为需要高端计算能力的应用提供适宜的环境。 该平台的核心是基于 [POSIX](https://zh.wikipedia.org/wiki/POSIX "wikilink") 标准的操作系统。 根据IEEE1003.13（即PSE51），操作系统可以通过POSIX的子集从应用中调用。 自适应平台的一个关键特性是面向服务的通信。

自适应平台可以使用两种类型的接口：服务和应用程序编程接口（API）。 该平台由分布在服务层中的功能聚类和AUTOSAR自适应平台基础组成。

功能聚类：

  - 汇编自适应平台的功能<span lang="EN-US">2016</span>
  - 确定需求规格说明书的聚类<span lang="EN-US">2016</span>
  - 从应用和网络角度描述软件平台的行为<span lang="EN-US">2016</span>
  - 但是，不得限制实现自适应平台的架构的最终软件设计。<span lang="EN-US">2016</span>

AUTOSAR自适应平台基础中的功能聚类在每台（虚拟）机器中必须至少有一个实例，而服务则可以分布在车内网络中。

自适应平台服务包括：

\-         更新和配置管理

\-         状态管理

\-         网络管理

\-         诊断

AUTOSAR自适应平台包含规范和代码。 与经典平台相比，AUTOSAR开发的实现可缩短验证周期并说明基本概念。 该实现适用于所有AUTOSAR成员。 

## 基础(Foundation)

基础标准的目的是加强AUTOSAR平台之间的互操作性。 基础包含AUTOSAR平台之间共享的通用需求和技术规范（例如协议）以及常用方法。

## 验收测试

为了降低测试的工作量及测试成本，AUTOSAR验收测试规范于2014年应运而生。 验收测试规范实则为利用相应平台指定接口的系统测试规范。 另外也考虑了在总线上的指定行为。 可将其视为针对特定平台功能的黑盒测试用例。 标准验收测试规范有助于实现以上目标。\[16\]

## 标准化应用接口

AUTOSAR以制造商和供应商之间功能性接口的标准化以及软件各分层接口的标准化为基础，实现其技术目标\[17\]。

## 组织结构

AUTOSAR入会形式分为五种。 成员合作方式不同，身份职责也不同： <sup>\[14\]</sup>

  - 核心合作伙伴<span lang="EN-US">2016</span>
  - 高级合作伙伴<span lang="EN-US">2016</span>
  - 一般合作伙伴<span lang="EN-US">2016</span>
  - 开发合作伙伴<span lang="EN-US">2016</span>
  - 观察员<span lang="EN-US">2016</span>

核心合作伙伴有宝马、博世、大陆、戴姆勒、福特、通用汽车、标致雪铁龙、丰田和大众等9位创立成员。 <sup>\[15\]</sup>  这些公司主要负责AUTOSAR开发联盟的组织、管理和调控。 <sup>\[14\]</sup>  其中，执行董事会负责制定全局策略和整体发展路线图。 <sup>\[16\]</sup>  指导委员会负责处理非技术性日常事务、会员入会、公共关系以及合约问题。 <sup>\[17\]</sup>  指导委员会任命主席和副主席，任期为九个月。 \[18\] AUTOSAR发言人负责外联工作。\[19\]\[20\] \[21\]

高级合作伙伴和开发合作伙伴在核心合作伙伴组建的项目领导小组的协调和监督下开展工作。\[22\] \[23\] 一般成员根据AUTOSAR已发布的标准文件开展工作\[24\]。 观察员目前以学术合作和非商业项目的形式参与联盟活动\[25\]。

截至2018年2月，AUTOSAR开发联盟的成员公司已超过200家。\[26\]

## 參見

[Category:发动机技术](https://zh.wikipedia.org/wiki/Category:发动机技术 "wikilink") [Category:软件架构](https://zh.wikipedia.org/wiki/Category:软件架构 "wikilink")

1.  <http://automotive.elektrobit.com/ecu/autosar>
2.  <http://www.autosar.org/>
3.
4.
5.
6.  AUTOSAR – The worldwide automotive standard for e/e systems. In: ATZextra (October 2013), p. 7.
7.
8.
9.  <http://automotive.elektrobit.com/ecu/autosar>
10. AUTOSAR – The worldwide automotive standard for e/e systems. In: ATZextra (October 2013), p. 9-10.
11.
12.
13.
14.
15.
16.
17.
18.
19. <http://auto-presse.de/autonews.php?newsid=247101>
20.
21. AUTOSAR – The worldwide automotive standard for e/e systems. In: ATZextra (October 2013), p. 6-7.
22.
23.
24.
25.
26.