> 本文内容由[DirectShow](https://zh.wikipedia.org/wiki/DirectShow)转换而来。


**DirectShow**（有时缩写如**DS**或**DShow**），开发代号*Quartz*，是一种由[微软公司开发的能够让软件开发者对媒体文件执行各种不同处理的](https://zh.wikipedia.org/wiki/微软公司 "wikilink")[应用程序设计接口](https://zh.wikipedia.org/wiki/应用程序设计接口 "wikilink")。它是微软公司对早先[Windows视频科技的一次更新](https://zh.wikipedia.org/wiki/Windows "wikilink")。基于微软公司Windows组件对象模型（[COM](https://zh.wikipedia.org/wiki/COM "wikilink")）框架，DirectShow为大部份微软公司程序设计语言提供了一个媒体的普遍接口，而且是一个可扩展的，能在使用者或开发者的命令下播放或记录媒体文件的，以Filter为基础的框架。DirectShow开发工具及凭证被加入到微软公司[SDK平台的一部份](https://zh.wikipedia.org/wiki/SDK "wikilink")。Windows Media Player这样的应用程序运用DirectShow或者它的各种衍生来播放来自文件或是互联网上的内容。DirectShow's的最大的竞争对手是[苹果计算机的](https://zh.wikipedia.org/wiki/苹果计算机 "wikilink")[QuickTime](../Page/QuickTime.md "wikilink")框架。

## 历史

ActiveMovie，开发代号Quartz，这个由Geraint Davies为微软公司设计的DirectShow的前身，在Windows 3.0时代，是作为一种对当时最流行的媒体平台QuickTime的回应而开发的。ActiveMovie最早的出现是被附加在Windows 95上面的并且需要系统安装了IE3.0。它当时的使命是作为IE的附件播放在其窗口内的媒体文件，正如当时QuickTime为Netscape以及IE提供的服务那样，它的另一个功能是作为Windows视频技术（VFW，Video For Windows）的一个替换，特别地为在VFW架构中难于处理的MPEG（移动图象专家组格式文件）文件提供辅助处理。

在1998年，大致在DirectX 5年代的时候，ActiveMovie被重新命名为DirectShow（反映了微软公司在那时正在努力加强“直接地”在一个通常的取名系统之下与硬件合作的技术）并且被包含为" DirectMedia SDK"的一部份。在DirectX的7版中，DirectShow变成了DirectX SDK主要组成部分而且如同DirectInput等其它DirectX APIs一样被给予了它自己的位置。甚至之后，DirectShow被主要用来接收来自像一个手提摄像机这样的电視输入装置的数据，而且它从文件中显示数据的能力被广泛用在Windows Media Player上面。 从2005年四月起，DirectShow被从DirectX SDK移除，必须单独下载Extra包才能得以支持，之后DirectShow的文档和示例被转移到[Windows SDK](https://zh.wikipedia.org/wiki/Windows_SDK "wikilink")，DirectShow也正式成为Windows的一个组件。然而，在编译某些DirectShow的示例时，DirectX SDK仍然是必需的。

## 设计模型

DirectShow运行的方式通常是一个开发者创建一个Filter Graph，把一些Filter - 可能订制 - 加入Filter Graph，然后播放文件，或者播放来自互联网或照相机的数据。当播放进程运行时，Filter Graph在Windows注册中寻找注册了的Filters并且为这些Filter创建本地提供的Graph。在这之后，它将所有的Filter连接在一起，并且在开发者的请求下，播放／中止创造的Graph。

为一个[mp3文件创建的Filter](https://zh.wikipedia.org/wiki/mp3 "wikilink") graph，由DirectShow自带的示例GraphEdit来播放。在这幅图中大的方块代表Filter graph，小的方块代表端口。 每个Filter表示数据处理过程的一个阶段，举例来说从一个文件或照相机读取数据，解码，转换以及绘制。filter有若干的能被连接到其他filter上的连接点的Interface。Interface可能是输出或输入。根据filter，数据被采用“拉模式”从输出端口输出，或者以“推模式”被推到另一个输入端口，并借此来传输数据。 大多数filters的创建使用了一组DirectShow SDK提供的C++类，叫做DirectShow BaseClass。这些为filters解决了许多创建，注册和连接的问题。如果要让filter graph能够自动的使用filters，它们需要在一个分开的DirectShow项目中被登记并与COM一起登记。这一个注册能被DirectShow BaseClass处理。然而，如果应用程序手工增加filters，他们不需要被全部登记。不幸地，它难以修改一个正在运行中的graph。从头停止graph而产生一个新graph通常是比较容易的。

## 功能

在DirectShow中有许多抽象的播放源文件的方法，实现这些功能也是相当简单的而且不需要一个定制过的filter。下一步相对复杂的过程是程序开发员需要开发他（她）自己的filter graph，举个例子他们可能设计一个可以接受来自互联网或是硬盘文件数据的source filter，也许有些定制的filter就是开发者想要的，接下来他们需要让DirectShow为用户完成一个filter Graph并将所有filter连接起来，在最后开发者仅仅只用让DirectShow为他们生成一个可以获取文件数据的source filter就可以了。

DirectShow预先设置支持许多通常的媒体格式，如MP3，和Windows媒体视频和一些比较常见的格式，比如简单的静态图像。自从在Windows中这些技术被许可了，对Fraunhofer来说就没有为专利权而付出花费的必要了，比如MP3执照。扩充机制允许DirectShow在将来可以支持出现的任何格式，举例来说，已经有对Ogg Vorbis文件和AC3文件的支持filters，此外还有若干其它的支持filters。

不同于为了读取媒体文件必须在循环中需要调用MoviesTask的为QuickTime设计的main C API，DirectShow以一种透明的方式处理这个问题。它在后台创建了一些线程来平缓的播放这些来自文件和互联网的数据与此同时不需要程序做很多工作。还跟QuickTime正好相反的是，在读取一段来自互联网数据而不是读取硬盘文件的时候没有特别的需要：DirectShow的filter graph摘录了来自程序的这些明细。然而，QuickTime（包括一个[ActiveX](../Page/ActiveX.md "wikilink")控制）在这方面的发展相比之下逊色很多。

## 批评

播放一个文件是一项相对简单的任务，不过对于像是从视频窗口接收特定窗口信息到创建特定filters，开发者会不断地遇到DirectShow API的黑暗面。DirectShow因其复杂性而声名狼藉与此同时很多人认为它是微软最复杂的libraries/APIs。在“Microsoft.public.win32.programmer.directx.video”新闻群组上存在一个长期的灰色笑话，讲的是每当某人想要为DirectShow开发一个新的filter时，那么“六个月后见吧”。

开发者很少直接创建DirectShow filters，他们通常使用被称为“基本类（DirectShow Base Classes）”的一组类别来处理大多数的工作。基本类的代码大小几乎是整个MFC library类大小的一半。所以即使有了基本类，DirectShow的COM物件仍然是相當的多，仍然會讓開發者在開發時倍感辛苦。DirectShow的API有时违反传统的COM规则，比如在方法中参数的用法等。因此，开发者也时常使用比DirectShow更高层次的API，如Windows Media Player SDK，它提供了较少COM介面的ActiveX控制。

DirectShow也因為僅支援非常有限的[数位版权管理](https://zh.wikipedia.org/wiki/数位版权管理 "wikilink")（DRM）功能而受到批评。相對的，Windows Media Player SDK支持較多的DRM功能。

## 参看

  - [DirectX](../Page/DirectX.md "wikilink")
  - [GraphEdit](https://zh.wikipedia.org/wiki/GraphEdit "wikilink")
  - [Video for Windows](../Page/Video_for_Windows.md "wikilink")

## 外部链接

  - [MSDN中DirectShow的官方文档](http://msdn.microsoft.com/library/default.asp?url=/library/en-us/directshow/htm/directshow.asp)
  - [MSDN](https://web.archive.org/web/20081010131256/http://msdn2.microsoft.com/en-us/library/ms783323.aspx) - 'Official DirectShow documentation from MSDN'
  - [DirectShow论坛，MSDN英文站](https://web.archive.org/web/20100303022850/http://social.msdn.microsoft.com/Forums/en/windowsdirectshowdevelopment/threads)
  - [MSDN](http://www.microsoft.com/downloads/results.aspx?productID=&freetext=directshow&DisplayLang=en) - 'DirectShow Downloads from MSDN'
  - [Home page of Geraint Davies](http://www.gdcl.co.uk) - 'Creator of DirectShow and a DirectShow [MVP](https://zh.wikipedia.org/wiki/Microsoft_Most_Valuable_Professional "wikilink") – Contains several [FAQs](https://zh.wikipedia.org/wiki/FAQ "wikilink") and examples.'
  - [The March Hare](http://tmhare.mvps.org/) - 'Prolific DirectShow MVP – Contains several FAQs'
  - [Chris P's code](http://www.chrisnet.net/code.htm) - 'Another DirectShow MVP – Some samples focused on audio.'
  - [AV Programming Forum](https://web.archive.org/web/20060313214825/http://www.avdevforum.com/av/) - 'Articles and Forum for DirectShow and Format SDK.'
  - [Standard Mpeg DirectShow SDK](https://web.archive.org/web/20070421073740/http://www.standardmpeg.com/products/encoder-sdk/) - 'DirectShow SDK for encoding to Mpeg.'
  - [DirectShow in Russian](https://web.archive.org/web/20070427033237/http://directshow.wonderu.com/) - 'DirectShow Tutorial（Russian）'

[Category:DirectX](https://zh.wikipedia.org/wiki/Category:DirectX "wikilink") [Category:Windows_API](https://zh.wikipedia.org/wiki/Category:Windows_API "wikilink") [Category:多媒体框架](https://zh.wikipedia.org/wiki/Category:多媒体框架 "wikilink")