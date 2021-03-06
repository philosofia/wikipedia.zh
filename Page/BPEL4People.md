> 本文内容由[BPEL4People](https://zh.wikipedia.org/wiki/BPEL4People)转换而来。


**BPEL4People**的全称是**WS-BPEL Extension for People**，是[BPEL](../Page/BPEL.md "wikilink")在人工活动方面的扩展。

## 历史

2005年7月，IBM和SAP在一个联合白皮书中提出BPEL4People。2007年6月，Active Endpoints, Adobe, BEA, IBM, Oracle和SAP共同发布了BPEL4People和WS-HumanTask规范，描述了BPEL过程中如何进行人员的交互。

## 问题定义和动机

[BPEL](../Page/BPEL.md "wikilink")语言说明了业务过程的行为特性，过程的活动是[Web服务](../Page/Web服务.md "wikilink")。人员交互并不在其范围内。虽然在分布式商业应用中广泛采用了Web服务，但是缺乏人员交互是应用于真实世界业务过程的一大差距。

为了填补这个差距，BPEL4People扩展了BPEL，从只能编排Web服务，扩展为同时支持对Web服务和基于角色的人工活动进行编排。

## 目标

在业务流程方面， BPEL4People通过以额外的独立语法和语义扩展BPEL，提供以下功能：

  - 支持基于角色的人员交互
  - 提供将人员活动指派给人员角色的方法。
  - 支持以下场景：
      - 四只眼原则
      - 任务任命
      - 任务升级
      - 执行链

*WS-HumanTask*规范引入了人工活动和通知的定义，包括它们的属性，行为特性，和一系列用于操纵人工活动的操作。同时，引入了一个协调协议，用于控制互操作方式下的人工任务服务的自治和生命周期管理。

*BPEL4People*规范引入了一个WS-BPEL的扩展，用于在WS-BPEL中引入人员交互。扩展定义了一种新的基本活动，允许由人工任务作为其实现，并允许指定过程局部的任务或使用过程定义外的任务。这一扩展基于WS-HumanTask规范。

## 参见

  - [BPEL](../Page/BPEL.md "wikilink")

## 外部链接

  - [Specification: Web Services for Human Task (WS-HumanTask), version 1.0](https://www.sdn.sap.com/irj/sdn/go/portal/prtroot/docs/library/uuid/a0c9ce4c-ee02-2a10-4b96-cb205464aa02)
  - [Specification: WS-BPEL Extension for People, (BPEL4People), version 1.0](https://www.sdn.sap.com/irj/sdn/go/portal/prtroot/docs/library/uuid/30c6f5b5-ef02-2a10-c8b5-cc1147f4d58c)
  - [BPEL4People project at SourceForge.net](http://bpel4people.sourceforge.net)
  - [WS-BPEL Extensions for People—BPEL4People](http://www.sdn.sap.com/irj/servlet/prt/portal/prtroot/docs/library/uuid/cfab6fdd-0501-0010-bc82-f5c2414080ed)
  - [Evaluation of the BPEL4People and WS-HumanTask Extensions to WS-BPEL 2.0 using the Workflow Resource Patterns](https://web.archive.org/web/20081121065856/http://is.tm.tue.nl/staff/wvdaalst/BPMcenter/reports/2007/BPM-07-10.pdf)

[分类:Web服务规范](https://zh.wikipedia.org/wiki/分类:Web服务规范 "wikilink")

[Category:基于XML的标准](https://zh.wikipedia.org/wiki/Category:基于XML的标准 "wikilink") [Category:计算机语言](https://zh.wikipedia.org/wiki/Category:计算机语言 "wikilink")