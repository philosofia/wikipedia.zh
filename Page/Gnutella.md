> 本文内容由[Gnutella](https://zh.wikipedia.org/wiki/Gnutella)转换而来。


**Gnutella**（，单词中的*g*不发音，或者发音为）是一种[文件共享网络](https://zh.wikipedia.org/wiki/文件共享 "wikilink")。2005年6月，gnutella约有181万台用户（计算机）\[1\]，而2006年1月增加到超过300万个节点\[2\]。截至2007年底，它是[互联网](../Page/互联网.md "wikilink")上最流行的文件共享网络，估计市场份额超过40%。\[3\]\[4\]

## 历史

Gnutella网络的第一个客户端由[Nullsoft公司的](https://zh.wikipedia.org/wiki/Nullsoft "wikilink")[贾斯汀·法兰科](https://zh.wikipedia.org/wiki/贾斯汀·法兰科 "wikilink")（Justin Frankel）与[汤姆·帕勃](https://zh.wikipedia.org/wiki/汤姆·帕勃 "wikilink")（Tom Pepper）于2000年早期最先开发。同年3月14日，该程序被放在Nullsoft的服务器上并允许公众下载。该程序的[源代码](../Page/源代码.md "wikilink")原计划稍后在[GNU通用公共许可证](../Page/GNU通用公共许可证.md "wikilink")下被发布。

与半集中式网络如[FastTrack](https://zh.wikipedia.org/wiki/FastTrack "wikilink")（[KaZaA](https://zh.wikipedia.org/wiki/KaZaA "wikilink")）以及[Napster](../Page/Napster.md "wikilink")不同，Gnutella网络是完全分布式的。其最初的流行是源于2001年早期Napster由于法律纠纷而被关闭的威胁。不断增长的用户也使得该协议的最初版本暴露了不少缺陷。2001年早期，各种不同版本的协议（最初以[专有](../Page/专有软件.md "wikilink")[闭源客户软件形式实现](https://zh.wikipedia.org/wiki/闭源软件 "wikilink")）使得Gnutella的扩展性得到了增强。与先前的协议将每一个用户节点都当作用户以及服务器不同，改进过的协议将某些用户当作"超节点"（ultrapeer），其为与之连接的所有用户路由搜索请求及回应。

这些发展使得Gnutella网络进一步吸引了更多用户。2001年晚期，一种Gnutella客户端软件[LimeWire](../Page/LimeWire.md "wikilink")成为免费开源软件。2002年2月，[Morpheus](https://zh.wikipedia.org/wiki/Morpheus_\(computer_program\) "wikilink")，一个商业文件共享开发群，放弃了原先的基于[FastTrack的端到端软件](https://zh.wikipedia.org/wiki/FastTrack "wikilink")，并发行了新的基于免费开源Gnutella客户端软件[Gnucleus的新客户端软件](https://zh.wikipedia.org/wiki/Gnucleus "wikilink")。

"Gnutella"这个词语现在被来指作被不同的客户端软件使用的一种开放网络协议，而不用来指作任何一个单独的项目或者某一个软件。由于许多不同的组织都在开发新的客户端软件，而且该协议本身也将不断演变，Gnutella这个词语的意义在将来或许也会变化。

Gnutella这个名字是*[GNU](../Page/GNU.md "wikilink")*与*[Nutella](https://zh.wikipedia.org/wiki/Nutella "wikilink")*的[混成词](https://zh.wikipedia.org/wiki/混成词 "wikilink")：人们普遍认定法兰科与帕勃在开发Gnutella项目的时候吃了许多的[Nutella](https://zh.wikipedia.org/wiki/Nutella "wikilink")，并且希望在GNU通用公共许可证下完成项目。Gnutella并未与任何[GNU](../Page/GNU.md "wikilink")项目相关联；\[5\]关于Gnutella在GNU中的相关项目，可以参见[GNUnet](https://zh.wikipedia.org/wiki/GNUnet "wikilink")。

## 工作原理

要了解Gnutella网络是怎样工作的，先设想一个大的由用户（称为“节点”）组成的环，每个节点都有Gnutella客户端软件运行。当初始启动时，客户端软件必须进行[自举](https://zh.wikipedia.org/wiki/自举 "wikilink")（Bootstrapping）并找到至少一个其它节点，有多种不同的方法可以达到这一功能，包括软件内置的一组正在工作的已经存在的地址列表，Web缓存的已知节点更新（称为[GWebCaches](http://www.shareazasecurity.be/wiki/index.php?title=GWC)）, UDP服务器缓存以及[IRC](https://zh.wikipedia.org/wiki/Internet_Relay_Chat "wikilink")。一旦连接上，客户端就会请求一张活动地址列表。

当用户想要进行搜索时，客户向每一个活动联接节点发送请求。在历史上（协议0.4版本），一个客户的活动联接节点数十分小（大约是5），所以每一个收到请求的联接节点都会再向其自身的所有联接节点转发该条请求，如此继续下去，直到该请求数据包在网络中被转发的“跳数”超过一个预先设定的数值（最大为7）。

到了0.6版之后，Gnutella网络中的节点被划分为叶节点（leaf nodes）与超节点（ultra nodes或ultrapeers）。每个叶节点仅与少数（一般为3）超节点连接，而每一个超节点与多于32个的其它超节点相连。在这种更高的出度（outdegree）下，先前提到的一条查询在网络中能达到的最大“跳数”被降低到4。

叶节点与超节点利用查询路由协议（Query Routing Protocol）来交换查询路由表（Query Routing Table (QRT)）。叶节点将它的QRT发送到每一个与之连接的超节点，超节点随后将每一个与之相连接的叶节点传来的QRT以及其本身的QRT合并，并且将其与自身的邻居节点交换。

在实际中，这种在Gnutella网络中的搜索模式是十分不可靠的。由于每一个节点都是一台普通的计算机用户，他们经常连接或者断开网络，所以整个Gnutella网络结构永远都不是完全稳定的。Gnutella网络搜索的带宽消耗也是随着连接用户的增加而指数递增的[1](http://www.darkridge.com/~jpr5/doc/gnutella.html)，经常饱和的连接会导致较慢的节点失去作用。因此，搜索请求在网络中会被经常丢弃，与整个网络相比，大多数的查询只会到达其中的很少一部分节点。

## 协议功能及扩展

Gnutella曾经是一种纯粹的基于洪泛式请求（query flooding）协议。早期的Gnutella 0.4版使用5种不同的数据包种类，即是：

  - ping：用于发现网络中的节点
  - pong：用于回覆ping消息
  - query：用于寻找某一个文件search for a file
  - query hit：用于回覆query消息
  - push：用于处于防火墙后的服务器的下载请求

以上不同消息包的定义主要是为了处理Gnutella网络中的搜索功能。文件传输功能是由[HTTP协议实现的](https://zh.wikipedia.org/wiki/HTTP "wikilink")。

Gnutella协议的开发目前由[GDF](https://zh.wikipedia.org/wiki/Gnutella_Developers_Forum "wikilink")（Gnutella开发者论坛）所领导。许多扩展协议已经或正在由不同的软件商以及GDF的自由开发人员开发。这些扩展包括智能查询路由（intelligent query routing）、[SHA-1](../Page/SHA-1.md "wikilink")校验码、query hit transmission via [UDP](https://zh.wikipedia.org/wiki/UDP "wikilink")、基于UDP的查询（querying via UDP）、基于[TCP的动态查询](https://zh.wikipedia.org/wiki/TCP "wikilink")（dynamic queries via TCP）、基于UDP的文件传输（file transfers via UDP）、[XML](../Page/XML.md "wikilink")元数据、source exchange（也被称为"the download mesh）以及parallel downloading in slices（swarming）。

在Gnutella开发网站上有试图在Gnutella 0.6版中将这些协议扩展规范完成的相关努力。由于所有的协议扩展还只是作为提议而存在于规范中，因此尽管已经过时，Gnutella 0.4版的标准至今仍是最新的完整技术规范。实际上，GDF的开发人员指出在目前的Gnutella网络中使用0.4版的消息握手机制已经十分困难，或者根本不可能，开发人员应该遵循[正在编写中的技术规范](http://gnet-specs.gnufu.net)来进行开发工作。

## Gnutella2

Gnutella2并不是Gnutella的继承者，\[6\]而是Gnutella网络协议的一个分支，其于Gnutella相比既有优点也有自己的缺点。\[7\] A sore point with many Gnutella supporters is that the "Gnutella2" name conveys an upgrade or superiority.\[8\]\[9\]

## 参见

  - [Bitzi](https://zh.wikipedia.org/wiki/Bitzi "wikilink")
  - [Gnutella crawler](https://zh.wikipedia.org/wiki/Gnutella_crawler "wikilink")
  - [Gnutella Web Cache](https://zh.wikipedia.org/wiki/Gnutella_Web_Cache "wikilink")
  - [GNUnet](https://zh.wikipedia.org/wiki/GNUnet "wikilink")
  - [WASTE](https://zh.wikipedia.org/wiki/WASTE "wikilink")
  - [JXTA](https://zh.wikipedia.org/wiki/JXTA "wikilink")

## 参考资料

## 外部链接

  - [Gnutella Protocol Development Wiki](http://gnet-specs.gnufu.net/)

<!-- end list -->

  - [Gnutella论坛](http://www.gnutellaforums.com/)
  - [GnuFU](http://gnufu.net)，"Gnutella For Users: A description of the inner workings of the Gnutella network in User-Friendly Style"
  - [Why Gnutella Scales quite well](http://basis.gnufu.net/gnufu/index.php/Why_Gnutella_scales_quite_well) - A text which corrects some of the myths around Gnutella
  - [Gnutella Client Feature Comparision](http://www.phex.org/wiki/index.php/Features#Feature_Comparision) - Client comparison of [LimeWire](../Page/LimeWire.md "wikilink")，[Phex](https://zh.wikipedia.org/wiki/Phex "wikilink")，[BearShare](https://zh.wikipedia.org/wiki/BearShare "wikilink")，[gtk-gnutella](https://zh.wikipedia.org/wiki/gtk-gnutella "wikilink")，[Gnucleus](https://zh.wikipedia.org/wiki/Gnucleus "wikilink")，[Shareaza](../Page/Shareaza.md "wikilink")。
  - [Gnutella announcement](http://slashdot.org/article.pl?sid=00/03/14/0949234) on [Slashdot](../Page/Slashdot.md "wikilink")
  - [*Regarding Gnutella* by GNU](http://www.gnu.org/philosophy/gnutella.html)
  - [Gnutella web cache (GWC) responses and engines](http://www.shareazasecurity.be/wiki/index.php?title=GWC)
  - "[A Measurement Study of Peer-to-Peer File Sharing Systems](https://web.archive.org/web/20080911021437/http://www.cs.washington.edu/homes/gribble/papers/mmcn.pdf)", by Stefan Saroiu, P. Krishna Gummadi, Steven D. Gribble. Proceedings of Multimedia Computing and Networking 2002（MMCN'02）, San Jose, CA, January 2002.
  - *[Mapping the Gnutella Network: Properties of Large-Scale Peer-to-Peer Systems and Implications for System Design](http://people.cs.uchicago.edu/~matei/papers/ic.pdf)*. M. Ripeanu; I. Foster and A. Iamnitchi, IEEE Internet Computing, 6（1）, February 2002.
  - [The 5th annual Passive & Active Measurement Workshop](https://archive.is/20111007051349/http://www.pam2004.org/programme.html)
  - *[Music Downloads: Pirates- or Customers?](http://hbswk.hbs.edu/item.jhtml?id=4206&t=innovation)*. Silverthorne, Sean. [Harvard Business School Working Knowledge](https://zh.wikipedia.org/wiki/Harvard_Business_School "wikilink")，2004.
  - *[Free riding on Gnutella revisited: the bell tolls?](http://dx.doi.org/10.1109/MDSO.2005.31)*. D. Hughes, G. Coulson, and J. Walkerdine. IEEE Distributed Systems Online, 6（6）, June 2005.

[Category:P2P](https://zh.wikipedia.org/wiki/Category:P2P "wikilink") [Category:应用层协议](https://zh.wikipedia.org/wiki/Category:应用层协议 "wikilink")

1.  [Slyck News - eDonkey2000 Nearly Double the Size of FastTrack](http://www.slyck.com/news.php?story=814), Thomas Mennecke for [Slyck.com](https://zh.wikipedia.org/wiki/Slyck.com "wikilink"), June 2, 2005.
2.  [On the Long-term Evolution of the Two-Tier Gnutella Overlay](http://www.barsoom.org/papers/gi-2006-long-term.pdf). Rasti, Stutzbach, Rejaie, 2006. See Figure 2a.
3.  [Ars Technica Study: BitTorrent sees big growth, LimeWire still \#1 P2P app](https://arstechnica.com/news.ars/post/20080421-study-bittorren-sees-big-growth-limewire-still-1-p2p-app.html) Eric Bangeman, April 21, 2008.
4.  [Ars Technica Report on P2P File Sharing Client Market Share](http://arstechnica.com/news.ars/post/20080421-study-bittorren-sees-big-growth-limewire-still-1-p2p-app.html)
5.  [Regarding Gnutella（www.gnu.org）](http://www.gnu.org/philosophy/gnutella.html)
6.  [Slyck interviews Greg Blidson of LimeWire on Gnutella2](http://www.mp3newswire.net/stories/2003/gnutella2.html)
7.  [Gnutella and Gnutella2 search methods compared](http://wortschatz.uni-leipzig.de/~fwitschel/vorlP2P/literatur/search_methods.pdf)
8.  [Comments on Gnutella2 disruption of Gnutella <small>WORD DOC</small>](http://www.bileta.ac.uk/Document%20Library/1/The%20（dis）illusions%20of%20a%20rebel-%20A%20reappraisal%20of%20the%20General%20Public.doc)
9.  [Slyck interview with Vincent Falco, creator of BearShare on Gnutella2](http://www.slyck.com/news.php?story=100)