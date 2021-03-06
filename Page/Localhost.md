> 本文内容由[Localhost](https://zh.wikipedia.org/wiki/Localhost)转换而来。


**localhost**是一个在[计算机网络](../Page/计算机网络.md "wikilink")中用于表示“此计算机”的[主机名](https://zh.wikipedia.org/wiki/主机名 "wikilink")。它被用于通过[本地环回网络接口](https://zh.wikipedia.org/wiki/回环网卡 "wikilink")，来访问本机运行的服务，并且将会绕过任何物理网络接口硬件。

## 本地環迴

運用本地環迴機制，便可在主機上運行網絡服務，期間不須安裝實體網絡介面卡，也無須將該服務開放予主機所在網絡。例如，在设置好本地安装的網站后，可通过`http://localhost`這一網址，来訪問本地網站。

localhost這个主機名稱一般會[解析為](../Page/域名系统.md "wikilink")[IPv4](../Page/IPv4.md "wikilink")本地环回地址`127.0.0.1`和[IPv6](../Page/IPv6.md "wikilink")本地环回地址`[::1]`。\[1\]

## 名称解析

[IPv4](../Page/IPv4.md "wikilink") 网络标准将整个 127.0.0.0/8 地址块订为[保留地址](https://zh.wikipedia.org/wiki/保留IP地址 "wikilink")，供本地环回使用，整个地址块内有超过1600万个IP地址。所以，发送到这些地址（127.0.0.1 到 127.255.255.255）的所有数据包都会返回本机。 地址 127.0.0.1 是 IPv4 环回的常用标准地址; 其余地址并不是所有的操作系统都支持（多数人也不知道有这些地址）。但是，使用127.0.0.1/8内的不同地址，就可以在本机上设置侦听相同端口的多个服务器。 [IPv6](../Page/IPv6.md "wikilink") 标准只分配了一个本地环回地址:\[::1\]。

要将本地主机名localhost解析到一个或多个 IP 地址，可通过在操作系统的 hosts 文件中添加以下代码实现：

    127.0.0.1    localhost
    ::1          localhost

本地主机名也可以由 [DNS](https://zh.wikipedia.org/wiki/DNS "wikilink") 服务器解析，但这一主机名的解析请求，应在本地处理，而非发送到远程服务器。

除了映射到环回地址（127.0.0.1 和 ::1）之外，localhost 还可以映射到其他 IPv4 环回地址，更可以将其他名称或附加名称分配给任何回环地址。不过， 在 hosts 文件或 DNS 中为localhost这个主机名设置映射地址时，假如新设置的映射地址并不在原本指定的映射地址范围内，所作映射不一定会生效，因为应用程序内部可能已对localhost进行映射操作。

在[域名](../Page/域名.md "wikilink")系统中，localhost 被留作[顶级域名](https://zh.wikipedia.org/wiki/顶级域名 "wikilink")，最初的目的，是要被留出以避免与用于回送目的的主机名混淆。IETF 标准禁止域名注册商分配 localhost 名称。\[2\]

## IETF 标准

名称 **localhost** 由 RFC 6761（特殊用途域名）保留，用于环回。\[3\]该域名在2013年2月达到了建议标准成熟度级别。该标准规定了一些特殊的考虑因素，规范其在域名解析系统中的使用：

  - localhost 的 IPv4 或 IPv6 地址查询必须始终解析为相应的环回地址，该地址在单独的标准中指定。
  - 应用可以自行解析环回地址，或者将他们交由本地解析器机制。
  - 当名称解析器收到 localhost 的地址（A 或 AAAA）查询时，它应该返回适当的环回地址，以及其他请求的记录类型的请求响应。不应将本地主机的查询转发到缓存名称服务器。
  - 为了避免使域名系统根服务器负担流量，缓存名称服务器不应请求本地主机的名称服务器记录，也不要向权威名称服务器转发解析。
  - DNS 注册商不能在顶级域 localhost 中委派域名。
  - 在上述规定的前提下，当权威名称服务器收到 'localhost' 查询请求时，应该适当处理。
  - IPv4 环回地址由 IETF 特殊用途 IPv4 地址标准（RFC 5735）在 IPv4 地址中保留空间，\[4\]可以追溯到 1986 年 11 月分配号码标准（RFC 990）。

IPv4 环回地址由 IETF 特殊用途 IPv4 地址标准（RFC 5735）在 IPv4 地址中保留空间，可以追溯到 1986 年 11 月分配号码标准（RFC 990）。

相比之下，IETF IPv6 寻址体系结构标准（RFC 4291）在IPv6地址空间内保留单个IPv6 环回地址 ::1。 该标准排除了将该地址分配给任何物理接口,以及在任何数据包中,将其用作发送到远程主机的源地址或目标地址的用途。任何这类被错误传输的数据包都不应该被路由转发，并且应该被接收它的所有路由器或主机丢弃。

## 數據包處理

任何發往環迴地址的數據包，其處理都在 [TCP/IP](https://zh.wikipedia.org/wiki/TCP/IP "wikilink") 協定疊的[链路层中實現的](../Page/数据链路层.md "wikilink")。這些數據包不會交由[網路卡](https://zh.wikipedia.org/wiki/網路卡 "wikilink")（NIC）或者裝置驅動程式處理，既不應在電腦系統以外出現，也不可經[路由器](../Page/路由器.md "wikilink")轉發。如此一來，電腦上即使沒有實體網路卡，也可進行軟體測試或者運行本機服務。

环回数据包与其他任何通过 TCP/IP 协议栈的数据包仅通过寻址到的特殊IP地址进行区分。因此，最终接收到的服务将根据指定的目的地进行响应。例如，HTTP服务可以将发往127.0.0.99:80 和 127.0.0.100:80 的数据包路由到不同的 Web 服务器，或发送到返回不同网页的单一服务器。为了简化这种测试，可以将 hosts 文件配置为为每个地址提供合适的名称。

具有环回源地址或目标地址的数据包，在非环回接口上收到则必须被删除。这种数据包有时被称为火星包。和其他虚假数据包一样，它们可能是恶意的，它们带来的问题可以通过 bogon 滤波避免。\[5\]

## 特殊情况

在 [MySQL](../Page/MySQL.md "wikilink") 数据库上，使用主机名 localhost 与地址 127.0.0.1 和 ::1 是有差异的。\[6\]\[7\]当在应用程序的客户端连接器接口中使用 localhost 作为目标时，MySQL 的 API 使用 [Unix 域套接字连接到数据库](https://zh.wikipedia.org/wiki/Unix域套接字 "wikilink")，而通过环回接口的 TCP 连接需要直接使用显式地址。

使用 127.0.0.0/8 网络地址时，一个值得注意的例外是，它们用在多协议标签交换（MPLS）跟踪路由错误检测中，它们的不可路由属性提供了一种方便的方法来避免向最终用户传送错误数据包。

## 另见

  - [专用网络](../Page/专用网络.md "wikilink")
  - [保留IP位址](https://zh.wikipedia.org/wiki/保留IP位址 "wikilink")

## 参见

[Category:OSI协议](https://zh.wikipedia.org/wiki/Category:OSI协议 "wikilink") [Category:链路协议](https://zh.wikipedia.org/wiki/Category:链路协议 "wikilink") [Category:计算机科学](https://zh.wikipedia.org/wiki/Category:计算机科学 "wikilink")

1.
2.
3.
4.
5.
6.
7.