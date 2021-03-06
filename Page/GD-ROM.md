**GD-ROM**（“giga disk [read-only memory](https://zh.wikipedia.org/wiki/只读存储器 "wikilink")”的简称）是一种私有的[光盘格式](https://zh.wikipedia.org/wiki/光盘 "wikilink")，由[世嘉和](https://zh.wikipedia.org/wiki/世嘉公司 "wikilink")[雅马哈共同开发](https://zh.wikipedia.org/wiki/雅马哈株式会社 "wikilink")，被用于[Dreamcast](../Page/Dreamcast.md "wikilink")及其他多个街機系统。这种光盘格式与[CD-ROM](../Page/CD-ROM.md "wikilink")十分相近。但由于凹点之间距离更小，它能储存更多数据。1.2GB的容量几乎是传统CD-ROM的两倍大。

## 光碟结构

GD-ROM盘片上有三个数据区域。第一个区域是按照CD格式储存的，通常由一个包含随意或幽默的警告信息的音轨构成，以提醒使用者这张盘片是在Dreamcast上使用的，而非普通CD播放机的。这段声音常常来自游戏角色，如游戏[永恒的阿卡迪亚](../Page/永恒的阿卡迪亚.md "wikilink")中的信息为“我们不能在CD播放器中拯救世界！请把我们放回Dreamcast以让我们去做我们该做的！ (We can't save the world from a CD player\! Put us back in the Dreamcast so we can do our job\!)”。这一CD数据区域同时也包含数据部分，使其可以在电脑上被读取。大部分GD-ROM碟片的这个区域只包含了一些文本文件，如游戏标识、版权信息及分类信息等。也有部分游戏为电脑用户准备了额外的资料，如游戏[索尼克大冒险](../Page/索尼克大冒险.md "wikilink")中包含了索尼克的人物图片。

接着是一个分割用的部分，除了“Produced by or under license from Sega Enterprises LTD Trademark Sega”这段文字之外，没有任何数据。而这段区域曾经被认为可能像[SEGA Saturn一样用于存放安全密钥来防止盗版](https://zh.wikipedia.org/wiki/SEGA_Saturn "wikilink")。最后，也是最外层的区域，以高密度的格式包含了游戏数据。

一个传统的CD驱动器永远不可能读取到第一个部分以外的内容，因为根据CD内容索引，那里没有任何内容。但可以通过调整[固件](https://zh.wikipedia.org/wiki/固件 "wikilink")，使普通的CD驱动器可以读取到第二个内容索引，以从高密度区域读取数据。此外还可以用“swap-trick”的方法，即先放入一个含有大的内容索引的普通CD，然后再在不让CD驱动器知道的情况下换成GD-ROM盘片。这种方法可以使CD驱动器读取到第一张盘片所指明的区域的数据。

从GD-ROM盘片上读取数据，最流行的办法就是将Dreamcast本身作为驱动器，然后通过一个“coder's cable”或者Dreamcast适配器从上面复制数据。另一种可选的方法是在Dreamcast上添加一个[USB](../Page/USB.md "wikilink")接口。\[1\]

世嘉现在已经停止了GD-ROM介质的生产。

## 技术資訊

Dreamcast中的GD-ROM与大部分现代光驱一样，以恒定角速度的方式工作。世嘉利用降低转速，并保持CD-ROM部件以原速读取的方式来读取GD-ROM内较高密度的数据。这种方法使得世嘉在生产Dreamcast的时候，可以使用许多便宜的现成部件。

[NetBSD](../Page/NetBSD.md "wikilink")项目已经开发出了一个可以在其系统下使用的GDRom驱动，同时这个驱动也有[Linux](../Page/Linux.md "wikilink")移植版。但由于版权原因，以及与Linux内核接口的配合不佳，另外一个新的Linux驱动已经开始开发。[Linux核心](https://zh.wikipedia.org/wiki/Linux核心 "wikilink") 2.6.25 已经可以支持Dreamcast上的GD-ROM驱动器了。\[2\]

## 参见

  - [CD-ROM](../Page/CD-ROM.md "wikilink")
  - [DDCD](https://zh.wikipedia.org/wiki/DDCD "wikilink")

## 来源

## 外部链接

  - [Sega's GD-ROM Presentation](https://web.archive.org/web/20080218151806/http://mc.pp.se/dc/gdrom.html)

[Category:Dreamcast](https://zh.wikipedia.org/wiki/Category:Dreamcast "wikilink") [Category:電腦貯存裝置](https://zh.wikipedia.org/wiki/Category:電腦貯存裝置 "wikilink") [Category:電子遊戲儲存媒體](https://zh.wikipedia.org/wiki/Category:電子遊戲儲存媒體 "wikilink")

1.
2.