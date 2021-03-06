> 本文内容由[Nagios](https://zh.wikipedia.org/wiki/Nagios)转换而来。


**Nagios**（IPA: /ˈnɑːɡioʊs/）是电脑系统和网络监控程序，用於检测主机和服务，当异常发生和解除时能提醒用户；是基于[GPLv2开发的开源软件](https://zh.wikipedia.org/wiki/GPLv2 "wikilink")，可免费获得及使用。

Nagios原名**NetSaint**，由Ethan Galstad开发并维护至今。NAGIOS是簡稱，全写「Nagios Ain't Gonna Insist On Sainthood」，Sainthood 意思是「圣者」，而「Agios」是「saint」的希腊文。Nagios 在[Linux](../Page/Linux.md "wikilink")運作，但也能用於[Unix](https://zh.wikipedia.org/wiki/Unix "wikilink")。

## 主要功能

[ScalableGridEngineNagios2.png](https://zh.wikipedia.org/wiki/File:ScalableGridEngineNagios2.png "fig:ScalableGridEngineNagios2.png")

  - 网络服务监控（SMTP、POP3、HTTP、NNTP、ICMP、SNMP、FTP、SSH）
  - 主机资源监控（CPU load、disk usage、system logs），也包括Windows主机（使用NSClient++ plugin）
  - 可以指定自己编写的Plugin通过网络收集数据来监控任何情况（温度、警告……）
  - 可以通过配置Nagios远程执行插件远程执行脚本
  - 远程监控支持SSH或SSL加通道方式进行监控
  - 简单的plugin设计允许用户很容易的开发自己需要的检查服务,支持很多开发语言（shell scripts、C++、Perl、ruby、Python、PHP、C\#等）
  - 包含很多图形化数据Plugins（Nagiosgraph、Nagiosgrapher、PNP4Nagios等）
  - 可并行服务检查
  - 能够定义网络主机的层次, 允许逐级检查, 就是从父主机开始向下检查
  - 当服务或主机出现问题时发出通告，可通过email, pager, sms 或任意用户自定义的plugin进行通知
  - 能够自定义事件处理机制重新激活出问题的服务或主机
  - 自动日志循环
  - 支持冗余监控
  - 包括Web界面可以查看当前网络状态，通知，问题历史，日志文件等

## 参考

  - first release of NetSaint from the [1](https://web.archive.org/web/20060501150621/http://www.netsaint.org/changelog.php): changelog
  - [2](http://www.nagios.org/development/history/nagios-3x.php): Nagios 3.x Version History
  - Galstad, Ethan (2003-05-03). official FAQ "Nagios: FAQs : What does Nagios mean?" (in EN). Nagios: Frequently Asked Questions. Nagios Enterprises, LLC. Retrieved 2009-03-06. "The official meaning is that N.A.G.I.O.S. is a recursive acronym which stands for "Nagios Ain't Gonna Insist On Sainthood"."
  - "2005-02-22 - Ethan Galstad" (in EN). Fosdem 2005. 2005-02-22. Retrieved 2009-03-06. "Although we were able to eventually reach an amicable agreement on my future use of the name "NetSaint", I felt it was prudent to change the name in order to prevent any future mishaps."

## 書籍

  - Barth, Wolfgang; (2006) *[Nagios: System And Network Monitoring](https://web.archive.org/web/20080531191735/http://www.nostarch.com/frameset.php?startat=nagios)* - No Starch Press ISBN 1-59327-070-4
  - Barth, Wolfgang; (2008) "[Nagios: System And Network Monitoring, 2nd edition](http://www.nostarch.com/nagios_2e.htm)'' - No Starch Press ISBN 1-59327-179-4
  - Turnbull, James; (2006) *[Pro Nagios 2.0](http://www.apress.com/book/bookDisplay.html?bID=10096)* - San Francisco: Apress ISBN 1-59059-609-9
  - Josephsen, David; (2007) *[Building a Monitoring Infrastructure with Nagios](http://www.pearson.ch/Informatik/PrenticeHall/1471/9780132236935/Building_a_Monitoring_Infrastructure.aspx)* - Prentice Hall ISBN 0-13-223693-1
  - Dondich, Taylor; (2006) *[Network Monitoring with Nagios](http://www.oreilly.com/catalog/networknagios/index.html)* - O'Reilly ISBN 0-596-52819-1
  - Schubert, Max et al.; (2008) *[Nagios 3 Enterprise Network Monitoring](http://www.nagios3book.com/)* - Syngress ISBN 978-1-59749-267-6
  - Kocjan, Wojciech; (2008) "[Learning Nagios 3.0](https://web.archive.org/web/20090813073735/http://www.packtpub.com/guide-for-learning-nagios-3)" - Packt Publishing ISBN 1847195180

## 相关链接

  - [Nagios.org](http://www.nagios.org), 官方网站
  - [Nagios Plugins](http://www.nagiosplugins.org/) 插件首面
  - [Nagios Exchange](http://exchange.nagios.org) overview of plugins, addons, mailing lists for Nagios
  - [Nagios Commnunity](https://web.archive.org/web/20140512220909/http://community.nagios.org/audio/nagiospronunciation.mp3) 作者 Ethan 示範發音 Nagios

## 支持站点

  - [Nagios support forums](https://archive.is/20090708010557/http://support.nagios.org/)
  - [New community and wiki of Nagios.org](http://community.nagios.org/)
  - [Nagios Enterprises](http://www.nagios.com) Nagios商业支持网站

[Category:網路管理](https://zh.wikipedia.org/wiki/Category:網路管理 "wikilink") [Category:自由網路軟體](https://zh.wikipedia.org/wiki/Category:自由網路軟體 "wikilink") [Category:系統監控工具](https://zh.wikipedia.org/wiki/Category:系統監控工具 "wikilink")