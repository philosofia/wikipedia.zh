> 本文内容由[X.25](https://zh.wikipedia.org/wiki/X.25)转换而来。


''' X.25 '''是一个使用电话或者[ISDN设备作为网络硬件设备来架构](https://zh.wikipedia.org/wiki/ISDN "wikilink")[广域网的](https://zh.wikipedia.org/wiki/广域网 "wikilink")[ITU-T网络协议](https://zh.wikipedia.org/wiki/ITU-T "wikilink")。它的[實體层](https://zh.wikipedia.org/wiki/實體层 "wikilink")，[数据链路层](../Page/数据链路层.md "wikilink")和[网络层](../Page/网络层.md "wikilink")（1－3层）都是按照[OSI模型](../Page/OSI模型.md "wikilink")来架构的。在国际上X.25的提供者通常称X.25为分封交换网（Packet switched network），尤其是那些国营的电话公司。它们的复合网络从80年代到90年代覆盖全球，在现在仍然应用于交易系统中。

## 历史

X.25是由ITU第VII组根据一系列的数字网络计划发展出来的，象在[Donald Davies领导下的英国的国家物理实验室的研究项目](https://zh.wikipedia.org/wiki/Donald_Davies "wikilink")，[Donald Davies率先提出了](https://zh.wikipedia.org/wiki/Donald_Davies "wikilink")[分组交换](../Page/分组交换.md "wikilink")的概念。在60年代快结束的时候，一个实验性的网络开始运营了，到了1974年已经有一系列的网络都以[SERCnet的形式相互链接了](https://zh.wikipedia.org/wiki/SERCnet "wikilink")。SERCnet在之后不断成长并在1984年改名叫[JANET](https://zh.wikipedia.org/wiki/JANET "wikilink")，这个网络直到今天仍然在运行，只是变成了一个[TCP/IP网络](https://zh.wikipedia.org/wiki/TCP/IP "wikilink")。其他的对这个标准实施作出贡献的还有70年代开始的由法国，加拿大，日本以及斯坎迪纳维亚半岛的国家合作开发的ARPA计划。各种各样的升级和附加功能使得这一标准日益完善，每4年ITU都会出版一本不同封面颜色新的技术手册来描述这些变化。

## 结构

[Televideo925Terminal.jpg](https://zh.wikipedia.org/wiki/File:Televideo925Terminal.jpg "fig:Televideo925Terminal.jpg")

X.25的首要原则是在一个基于位差错校验创建一个模拟电话网络之上的全球性的分组交换网络。许多的X.25系统误码率都很高，从而达不到这一要求所以需要接入规程**LAP-B**。X.25模型实质上是建立基于面向连接的虚电路，通过DTE来提供给用户看似点对点链接的虚连接。

X.25是在一个[哑终端](../Page/哑终端.md "wikilink")的时代发展起来的，需要连接到主计算机。取代直接连接到主计算机—这需要主计算机拥有自己的调制解调器和电话线，而且还需要没有本地通话来进行长距离呼叫请求—主机可以同网络服务器建立X.25连接。这样哑终端用户可以直接进行拨号连接到网络了。本质上来说，调制解调器和端口为一端，X.25连接在另一端，这是由ITU-T X.29和X.3标准定义的。

已经和PAD建立好连接之后，哑终端的用户通知PAD一个类似于电话号码的[X.121地址的方式来表明和哪一个主机建立连接](https://zh.wikipedia.org/wiki/X.121 "wikilink")。接下来PAD发送一个X.25请求到主机，建立一个虚电路。指出X.25建立好了一个虚电路，从而形成了一个电路交换网络，尽管实际上数据仍然是通过分组交换网络传输的。如果是两个X.25通信的话，当然就可以直接呼叫对方了；不用PAD了。理论上来说，不用在乎X.25呼叫方和X.25定义方是否在同一个传输上，单是实际上一个传输同其他传输相互呼叫并不总是可行的。

## 面向连接的虚电路

[Siemens-DAG-64_front.jpg](https://zh.wikipedia.org/wiki/File:Siemens-DAG-64_front.jpg "fig:Siemens-DAG-64_front.jpg")

在X.25的历史上，它曾经用来作[永久虚拟电路](https://zh.wikipedia.org/wiki/虚拟电路 "wikilink")（permanent virtual circuits, PVCs）来使得两台主计算机精确链接。这些应用是非常常见的，例如在银行，从而使得分散地办公室连接到一台中心主机上，这样比建立实际的长距离电话连接要便宜许多。X.25的每月服务费用通常都是比较平均的。其速度随着时间的推移逐步增长，典型值为48或者96 kbit/s。 公用的X.25网络在大多数国家都是在70年代到80年代建造的，为了减少网络服务的费用，用户首先要和网络接口进行连接，称为「虚电路交换」（SVCs）或者「虚连接到公共数据网」，这些X.25应用在90年代随着因特网的出现在大多数地方都不采用了。

许多的系统都直接使用了X.25，这其中的许多都是私有化的应用，然而这已经是X.25还是世界上唯一的网络标准的时候的事了，不过[X.400电子邮件系统仍然采用X](https://zh.wikipedia.org/wiki/X.400 "wikilink").25作为传输层。OSI最基本的设想是建立一个全球性的网络标准，然而互联网工业的发展最终采用了因特网的标准。

## 逐步被取代

随着更完美的数字电话服务和差错更正功能的调制解调器的快速发展，再来讨论X.25不再有什么实际意义了。结果就是[帧中继](../Page/帧中继.md "wikilink")的出现，帧中继就是带有差错自动修正功能的X.25。在现在，虚电路的概念仍然在[异步传输模式中使用来进行拥塞控制和网络复用](https://zh.wikipedia.org/wiki/异步传输模式 "wikilink")。

## 今天的X.25

在今天，X.25仍然有遍及全球的使用，尽管这个比例已经随着一些[第二层新技术如](../Page/OSI模型.md "wikilink")[帧中继](../Page/帧中继.md "wikilink")，[ISDN](https://zh.wikipedia.org/wiki/ISDN "wikilink")，[ATM](https://zh.wikipedia.org/wiki/异步传输模式 "wikilink")，[ADSL](../Page/ADSL.md "wikilink")，[POS的推出而在迅速下降了](https://zh.wikipedia.org/wiki/Packet_over_SONET/SDH "wikilink")。现在只有在第三世界国家有一些还在可靠运营的设备，因为毕竟PDN可能是最为可靠而且便宜的连接因特网的设备了。有一个X.25的变种叫做[AX.25仍然在](https://zh.wikipedia.org/wiki/AX.25 "wikilink")[业余无线电](../Page/业余无线电.md "wikilink")的[无线封包通信](https://zh.wikipedia.org/wiki/无线封包通信 "wikilink")（无线分组交换，packet radio）领域大量使用，然而在最近一些年里已经有一些呼声建议使用[TCP/IP来取代](https://zh.wikipedia.org/wiki/TCP/IP "wikilink")[AX.25了](https://zh.wikipedia.org/wiki/AX.25 "wikilink")。RACAL Paknet在世界的许多地方仍然采用X.25协议标准用来进行安全的低速率无线传输。Paknet现在通常用来作为GPS和POS的应用。

## 其他链接

  - [思科X.25参考](http://www.cisco.com/univercd/cc/td/doc/cisintwk/ito_doc/x25.htm)
  - [Widanet Limited - X.25 Packet Radio Solution](https://web.archive.org/web/20051027113702/http://www.widanet.com/)

[Category:网络层协议](https://zh.wikipedia.org/wiki/Category:网络层协议 "wikilink") [Category:OSI协议](https://zh.wikipedia.org/wiki/Category:OSI协议 "wikilink")