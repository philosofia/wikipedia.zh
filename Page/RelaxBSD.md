> 本文内容由[RelaxBSD](https://zh.wikipedia.org/wiki/RelaxBSD)转换而来。


[RelaxBSD_logo.gif](https://zh.wikipedia.org/wiki/File:RelaxBSD_logo.gif "fig:RelaxBSD_logo.gif")

**RelaxBSD**是一套中国大陆用户在[FreeBSD](../Page/FreeBSD.md "wikilink")的基础上开发的，方便中文用户使用的BSD系统。目前其官方网站relaxbsd.org已经关闭，故可以判断该系统已经停止开发。

## 许可协议

RelaxBSD在[BSD许可证](../Page/BSD许可证.md "wikilink")下发布，允许任何人在保留版权和许可协议信息的前提下随意使用和发行。

## 版本历史

### 2005-06-01

RelaxBSD 1.0 Release 发布。

### 2005-06-23

RelaxBSD 1.1 Release代号为sprout。

1.1 Release主要解决1.0 Release一的一些bug，关键解决BSDInstaller（安装RelaxBSD）的问题，这样大家既可把RelaxBSD作为LiveCD直接从光盘运行，也可将RelaxBSD安装到硬盘上使用。

为了方便硬盘上还装有Linux的用户，装在硬盘上的RelaxBSD将采用Grub引导。另外如果你想将RelaxBSD 1.1 安装在你的硬盘内，请你预先在你的硬盘上划一个至少4G的主分区空间（注意：是主分区）。

### 2006-06-16

RelaxBSD 2.0-RELEASE 发布。

RelaxBSD 2.0-RELEASE核心部分基于FreeBSD 6.1-RELEASE。构建RelaxBSD的软件均由FreeBSD ports编译并有小量修改。整个系统带参数：CPUTYPE?=pentium3 CFLAGS= -O2 -pipe进行编译。可升级至更新版本的FreeBSD（FreeBSD 6.1-RELEASE及以上）。RelaxBSD 2.0-RELEASE 有如下特点：

  - 可同时支持英文、简体中文、繁体中文，针对桌面系统特别设计；
  - 用基于QT的GUI安装界面，使得安装过程非常简单。只需几步便可完成全部安装；
  - 用Grub作启动管理。能自动识别其它Windows分区，系统第一次启动后可自动加入其它grub（如Linux）的启动项；
  - 直接支持多种打印机、数码相机、扫描仪、电视卡设备；可以自动识别网卡（自动设为DHCP）、声卡、显卡；
  - 包含有[OpenOffice](https://zh.wikipedia.org/wiki/OpenOffice "wikilink")、[Gimp](https://zh.wikipedia.org/wiki/Gimp "wikilink")、nvu、[Glade2](https://zh.wikipedia.org/wiki/Glade2 "wikilink")、mplayer、xine、stardict、reciteword、kbtv、[aMule](https://zh.wikipedia.org/wiki/aMule "wikilink")、KTorrent等优秀的软件；
  - 自动挂载FAT32、NTFS、Ext2fs、ReiserFS、UFS分区。基中，FAT32、NTFS分区按选择语言编码挂载，NTFS、ReiserFS按只读方式挂载；
  - 包括OpenOffice在内的编辑软件支持cups打印；
  - 自动识别并挂载移动存储设备。

[Category:BSD](https://zh.wikipedia.org/wiki/Category:BSD "wikilink")