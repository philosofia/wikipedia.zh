> 本文内容由[Linux历史](https://zh.wikipedia.org/wiki/Linux历史)转换而来。


历史上，**Linux操作系统内核**以其不断的发展为特点。它的[源代码](../Page/源代码.md "wikilink")已经从1991年初次发布的几个[C语言文件扩展到](https://zh.wikipedia.org/wiki/C语言 "wikilink")2007年的290MB源文件；发布许可也从禁止商业化发布，变为在通用公共许可证[GPL下发布](https://zh.wikipedia.org/wiki/GPL "wikilink")。\[1\]

## 起源

[Unix操作系统在](https://zh.wikipedia.org/wiki/Unix "wikilink")20世纪60年代构思完成并实现，并在1970年首次发布。它因容易获取与[可移植性高而广泛被学术机构和工商企业采用](https://zh.wikipedia.org/wiki/可移植性 "wikilink")、复制和修改。它的设计对其他系统的作者影响很大。

在1983年，[理查德·斯托曼](../Page/理查德·斯托曼.md "wikilink")创建了一个自由软件，[类Unix](https://zh.wikipedia.org/wiki/类Unix "wikilink")，与[POSIX兼容的操作系统为目标的](https://zh.wikipedia.org/wiki/POSIX "wikilink")[GNU计划](https://zh.wikipedia.org/wiki/GNU计划 "wikilink")。作为这个计划其中的一部分，他又写了[GNU通用公共许可证](../Page/GNU通用公共许可证.md "wikilink")（GPL）。20世纪90年代初，已经有足够的软件去创建一个完整的操作系统。但因为在1987年时，理查德·斯托曼决定以[Mach](../Page/Mach.md "wikilink")微内核进行开发，认为可以借此加速操作系统的开发，但因为一直不确定卡内基梅隆大学何时要将核心源代码发布，造成项目三年进展缓慢。GNU的内核，[GNU Mach和](../Page/GNU_Mach.md "wikilink")[GNU Hurd没能够充分吸引开发者](../Page/GNU_Hurd.md "wikilink")，这导致了GNU的未能完成。

在20世纪80年代还有另外一个关于自由操作系统的项目，[伯克利软件套件](../Page/BSD.md "wikilink")。这是由[UC Berkeley从](https://zh.wikipedia.org/wiki/UC_Berkeley "wikilink")[AT\&T](../Page/AT&T.md "wikilink")的第六版Unix开发而来的。因为它包含了AT\&T所拥有的的Unix代码，所以AT\&T在20世纪90年代初对加利福尼亚大学提起了法律诉讼。这严重限制了BSD的发展与应用。\[2\]\[3\]

[MINIX](../Page/MINIX.md "wikilink")是[安德鲁·斯图尔特·塔能鲍姆](../Page/安德鲁·斯图尔特·塔能鲍姆.md "wikilink")在1987年发布一个用于教学的微内核架构的类Unix系统。虽然系统的源代码容易得到，但是对源代码的修改与再发布却受到了限制。另外，MINIX的16位的设计与当时日渐便宜及受欢迎的、个人电脑的[Intel](https://zh.wikipedia.org/wiki/Intel "wikilink") [80386架构兼容得不好](https://zh.wikipedia.org/wiki/80386 "wikilink")。

这些因素使得Torvalds开始了他的项目。他曾说过，如果那时候有可用的GNU或者386BSD内核的话，他很可能就不会去写他自己的内核了。\[4\]\[5\]

## Linux的诞生

[Linus_Torvalds.jpeg](https://zh.wikipedia.org/wiki/File:Linus_Torvalds.jpeg "fig:Linus_Torvalds.jpeg") 1991年，在[赫爾辛基](https://zh.wikipedia.org/wiki/赫爾辛基 "wikilink")，[Linus Torvalds开始那个后面成为了](https://zh.wikipedia.org/wiki/Linus_Torvalds "wikilink")[Linux内核](../Page/Linux内核.md "wikilink")的项目。最初它只是一个Torvalds用来访问大学裡的大型的Unix服务器的[虚拟终端](../Page/虚拟终端.md "wikilink")。他专门写了一个用于他当时正在用的硬件的，与操作系统无关的程序，因为他要用他那用80386处理器的新PC机的功能。开发是在[Minix上](https://zh.wikipedia.org/wiki/Minix "wikilink")，用至今仍为首选的[编译器](https://zh.wikipedia.org/wiki/编译器 "wikilink")——[GCC](../Page/GCC.md "wikilink")——来完成的。

Torvalds在他的书*[只为欢乐](../Page/只为欢乐.md "wikilink")*\[6\] 中说过，他最后才意识到自己写了一个操作系统内核。1991年8月25日，他在发布到[新闻组](../Page/新闻组.md "wikilink")“comp.os.minix.”的[Usenet](../Page/Usenet.md "wikilink")上发布了这个系统：

## 名称的由来

Linus Torvalds本要把他的发时叫做*Freax*——“fread”，“free”和“x”（暗指Unix）的合成词。在开发系统的前半年裡，他把文件以文件名“Freax”存储。Torvalds考虑过Linux这个名字，但是因为觉得它过于自我本位而放弃了使用它\[7\]。

为便于开发，在1991年9月，他把那些文件上传到了[赫尔辛基工业大学](https://zh.wikipedia.org/wiki/赫尔辛基工业大学 "wikilink")（HUT）的[FTP服务器](https://zh.wikipedia.org/wiki/FTP服务器 "wikilink")（ftp.funet.fi)。Torvalds在HUT负责管理那个服务器的同事[Ari Lemmke](https://zh.wikipedia.org/wiki/Ari_Lemmke "wikilink")，觉得“Freax”这个名字不是很好，就在不咨询Torvalds的情况下，把项目的名字改成了“Linux”\[8\]。但是之后，Torvalds也同意“Linux”这个名字了：“经过多次讨论，他承认Linux这个名字更好。在0.01版本Linux的源代码的[makefile里仍然使用](https://zh.wikipedia.org/wiki/makefile "wikilink")‘Freax'这个名字，在之后‘Linux'这个名字才被使用。所以，Linux这个名字并不是预先想好的，只是它被广泛接受了而已”。

## GNU GPL下的Linux

Torvalds先是在它自己的许可下发布Linux内核的，即限制它用于商业活动。和这个内核一起使用的软件是发布在[GPL这个](https://zh.wikipedia.org/wiki/GPL "wikilink")[自由软件](../Page/自由软件.md "wikilink")许可下，属于[GNU计划一部分的软件](https://zh.wikipedia.org/wiki/GNU计划 "wikilink")。第一次发布的Linux内核，版本0.01，包含了GNU的[Bash](../Page/Bash.md "wikilink")的二进制版本\[9\]。 在版本0.01的备注中，Torvalds列出了运行Linux所需的GNU软件\[10\]：  1992年，他建议在[GPL下发布内核](https://zh.wikipedia.org/wiki/GPL "wikilink")。他先在版本0.12中宣布了这个决定\[11\]。1992年12月中，他在GNU GPL下发布了0.99版。\[12\]。Linux和GNU的开发者一起把GNU的部件和Linux集成起来，使它成为一个可运行的自由操作系统。\[13\]Torvalds说，“把Linux发布在GPL下是我所做过的最好的事。” \[14\]

### 关于GNU/Linux命名方式的争议

“Linux”这个名称一开始只被Torvalds用于Linux内核。但是这个内核却常和其他软件一起使用，尤其是GNU计划的软件。这很快就成为最受欢迎的GNU软件。1994年六月，在GNU的期刊中，Linux被称作“自由Unix克隆版”，[Debian](../Page/Debian.md "wikilink")计划也开始把它的产品叫做“Debian GNU/Linux”。1996年5月，[Richard Stallman发布了编辑器](https://zh.wikipedia.org/wiki/Richard_Stallman "wikilink")[Emacs](../Page/Emacs.md "wikilink")的19.31版本，其中系统的名称从Linux变成了Lignux。这种拼法为的是明确指出GNU和Linux的结合。但是这不久就被“GNU/Linux”所代替了\[15\]。

对这个名称，不同人有不同的反应。GNU和Debian项目使用那个名字，但是，多数开发者仍然简单地用“Linux”来指代它们的结合。

## 官方吉祥物

[Tux.png](https://zh.wikipedia.org/wiki/File:Tux.png "fig:Tux.png")\]\] 1996年，Torvalds为Linux选定了企鹅作为它的[吉祥物](https://zh.wikipedia.org/wiki/吉祥物 "wikilink")。[Larry Ewing提供了吉祥物的初稿](https://zh.wikipedia.org/wiki/Larry_Ewing "wikilink")。现在正在使用的著名的吉祥物就是基于这份初稿的。James Hughes根据“Torvalds's Unix”为它取了名字[Tux](../Page/Tux.md "wikilink")\[16\]。

## 新的发展

### 内核

除了Torvalds，还有许多知名的如阿兰考克斯[Alan Cox和马塞洛托萨蒂](https://zh.wikipedia.org/wiki/Alan_Cox "wikilink")[Marcelo TosattiLinux内核维护者](https://zh.wikipedia.org/wiki/Marcelo_Tosatti "wikilink")。 Cox维护2.2版的内核直到2003年底，同样, Tosatti维护2.4版的内核直到2006年年中，程序员[Andrew Morton](https://zh.wikipedia.org/wiki/Andrew_Morton_\(computer_programmer\) "wikilink") 带动了于2003年12月18日发布的首个稳定版本-2.6版内核的开发和维护。而旧版本也还在持续地改进中。

Linux在多方面成功应用，其主要原因在于它是自由软件和它的软件的稳定性、安全性和可扩展性，以及因此而带有的可维护性。虽然确实存在着漏洞，例如[vmsplice() exploit](https://zh.wikipedia.org/wiki/vmsplice\(\)_exploit "wikilink")，但是这些漏洞会很快被修复。

### 社区

关于Linux的大部分工作都是由社区完成的：世界各地使用Linux的程序员都把建议的改进发给维护员。很多公司还不但参与内核的开发，还参与了一些随Linux一起发布的辅助软件的编写。

Linux的版本当中，既有像[Debian](../Page/Debian.md "wikilink")那样由自发组织发布的，又有像[openSUSE和](https://zh.wikipedia.org/wiki/openSUSE "wikilink")[Fedora](../Page/Fedora.md "wikilink")那样直接和一些公司相关的。为了交换意见，各个项目的成员常在各种会议交流会上会面。其中最大的交流会是在[德国](../Page/德国.md "wikilink")（目前是[柏林](../Page/柏林.md "wikilink")）举行的[LinuxTag](https://zh.wikipedia.org/wiki/LinuxTag "wikilink")。每年有大约10,000人聚集在一起讨论Linux以及与Linux相关的项目。

### 开源发展实验室和Linux基金会

[開源碼發展實驗室](../Page/開源碼發展實驗室.md "wikilink")（Open Source Development Lab）创立于2000年。它是一个独立的非营利性组织。它的目标是优化Linux以应用于数据中心和运营商的领域。它是Linus Torvalds和Andrew Morton工作的赞助来源。2006年年中，Morton去了Google（Google也是使用Linux内核的）；Torvalds全职为OSDL开发Linux内核。非商业性运营机制的资金主要来源于[Red Hat](https://zh.wikipedia.org/wiki/Red_Hat "wikilink")，[Novell](../Page/Novell.md "wikilink")，[三菱](https://zh.wikipedia.org/wiki/三菱 "wikilink")，[英特尔](../Page/英特尔.md "wikilink"), [IBM](../Page/IBM.md "wikilink") ，[戴尔和](https://zh.wikipedia.org/wiki/戴尔 "wikilink")[惠普](../Page/惠普.md "wikilink")等几家大公司。

2007年1月22日，OSDL和[自由標準組織合并为](https://zh.wikipedia.org/wiki/自由標準組織 "wikilink")[Linux基金会](https://zh.wikipedia.org/wiki/Linux基金会 "wikilink")，把它们的工作焦点集中在改进[GNU/Linux以与](../Page/Linux.md "wikilink")[Windows竞争](https://zh.wikipedia.org/wiki/Windows "wikilink")\[17\]。

### 相关公司

虽然是开源项目，但是还是有一些公司从中获取了利益。这些公司大多也是开源发展实验室的成员。它们在Linux的改进与开发中投入了许多资源以使其能够适应不同领域的应用。其中包括驱动程序捐赠的硬件，对开发Linux软件的人员现金的捐赠，以及对Linux程序员的雇用。例如IBM和HP，它们首先在它们的服务器上使用了Linux；又如Red Hat，它维护着它自己的版本。同样，[Trolltech通过对Qt的开发和把它GPL许可化](https://zh.wikipedia.org/wiki/Trolltech "wikilink")，以及启用一些X和KDE开发人员来支持Linux。前者更使得开发KDE成为了可能。

## 关于Linux的争论

Linux自出现以来就已经引起了反复的争议。

### “Linux已经过时”

1992年，著名的计算机科学家，[Minix和](https://zh.wikipedia.org/wiki/Minix "wikilink")[微核心的作者](https://zh.wikipedia.org/wiki/微核心 "wikilink")，[安德魯·斯圖爾特·塔能鮑姆在新闻组](https://zh.wikipedia.org/wiki/安德魯·斯圖爾特·塔能鮑姆 "wikilink")`comp.os.minix`上写了一篇题为《Linux已经过时》的文章\[18\]。这篇文章标志着对Linux内核的著名的大讨论的开始。其中对Linux的批评主要是：

  - 该内核是[單核心的](https://zh.wikipedia.org/wiki/單核心 "wikilink")，因此它是过时的；
  - 因使用Intel 386处理器而带来的不可移植性。“写一个与某特定硬件，特别是像Intel这种奇怪的硬件相关的操作系统，在根本上就是错误的。”\[19\]；
  - 没有个人严格控制源代码\[20\]；
  - Linux使用了一系列无用的特色（他认为多线程的[文件系统](../Page/文件系统.md "wikilink")只会使用系统性能低下）\[21\]。

事实证明，[塔能鮑姆认为Linux会在几年之内就会过时并被](https://zh.wikipedia.org/wiki/安德魯·斯圖爾特·塔能鮑姆 "wikilink")[GNU Hurd取替](../Page/GNU_Hurd.md "wikilink")（他认为[GNU Hurd更为现代化](../Page/GNU_Hurd.md "wikilink")）的看法是错误的。Linux已经被移植到所有主流的平台，而且它开放的开发模式引领了一种杰出的开发步伐。相反，GNU Hurd还没有拥有可作为产品服务器的稳定性水平。\[22\]。

### 反对开源文件的出版物

### 来自微软的竞争

虽然Torvalds说过微软感到的来自Linux的威胁与他无关\[23\] ，但是微软和Linux阵营在1997年到2001年间还是有着很多敌对的情况。这种情况在1998年Eric S. Raymond发表《[万圣节文件](../Page/万圣节文件.md "wikilink")》的时候变得明显起来。这裡由一位微软工程师写的关于寻求解决[自由软件](../Page/自由软件.md "wikilink")对微软的威胁的策略的文章。\[24\]

### SCO

2003年3月，[SCO Group指责IBM把UNIX的代码移植到Linux侵犯了他们的版权](../Page/SCO_Group.md "wikilink")。SCO声称它们拥有代码的版权并對IBM提起了诉讼。Red Hat又提起了反诉讼，因此SCO又提起了其他相关的诉讼。在这些诉讼进行的同时，SCO开始把Linux的许可权卖给那些不愿意冒受SCO投诉的险的用户。因为[Novell](../Page/Novell.md "wikilink")也声称拥有UNIX的版权，所以它又对SCO提起了诉讼。接着SCO便宣告破产了。\[25\]

### 名称的商标

Linux是Linus Torvalds的注册商标。

### 商标权

在1994和1995年，有多个来自不同国家的人想把Linux注册为商标，从而一些Linux公司可以从中收取特许使用金。很多Linux的开发人员和用户都不同意此举。Torvalds在[Linux国际的帮助下得到了Linux这个商标](https://zh.wikipedia.org/wiki/Linux国际 "wikilink")，然后他把这个商标转让给了[Linux国际](https://zh.wikipedia.org/wiki/Linux国际 "wikilink")。对这个商标的保护后来就由一个专门的基金会——非营利性的[Linux标识协会](https://zh.wikipedia.org/wiki/Linux标识协会 "wikilink")——来管理。2000年，Linus Torvalds指定了分配许可权的基本规则。这意味着任何要想以Linux的名义发布产品和服务的人，都要拥有许可证。而许可证要通过购买获得。

## 大事年表

  - 1983：Richard Stallman發起以创建一个自由的操作系统为目标的GNU计划。
  - 1989：Richard Stallman撰写第一版的GNU [GPL](https://zh.wikipedia.org/wiki/GPL "wikilink")。
  - 1991：Linux内核在8月25日由21岁的芬兰学生Linus Benedict Torvalds公开发布。
  - 1992：在GNU GPL下Linux内核被重新授权使用，产生第一个“Linux发行版本”。
  - 1993：超过100个开发者致力于Linux内核开发。在他们的努力下，内核逐渐适应GNU的环境，这个为Linux创造巨大的应用空间的广阔环境。[Slackware](../Page/Slackware.md "wikilink")首次发布。后来在同一年，Debian项目设立，现已成为最大的社区发布项目。
  - 1994: 3月, Torvalds认为内核的所有组件已经完全成熟，他放出了Linux的1.0版本。[XFree86](../Page/XFree86.md "wikilink")项目组提供了一个图形化用户界面（GUI）.同年[Red Hat公司和](https://zh.wikipedia.org/wiki/Red_Hat "wikilink")[SUSE](../Page/SUSE.md "wikilink")发行他们各自的Linux 1.0分发版本。
  - 1995: Linux被移植到DEC Alpha和Sun公司的SPARC平台上，而在接下来的几年里它又被广泛地移植到更多的平台上。
  - 1996: Linux内核2.0版本发布。此时内核已经支持多处理器，因而成为各大公司的绝佳选择。
  - 1998：很多大公司，诸如IBM、Compaq ，Oracle表示支持Linux系统。另外，一部分程序员开始图形化用户界面[KDE](../Page/KDE.md "wikilink")的开发。
  - 1999：一些程序员开始致力于开发图形化环境[GNOME](../Page/GNOME.md "wikilink")，它可以替代依靠[Qt工具包才能工作的KDE](https://zh.wikipedia.org/wiki/Qt_\(toolkit\) "wikilink")。在这一年里IBM宣布一项支持Linux的浩大的工程。
  - 2004: [XFree86](../Page/XFree86.md "wikilink")小组分裂，同现有的X Windows标准组织 共同成立[X.Org基金会](../Page/X.Org基金会.md "wikilink")，促使了[X Window ServerLinux版本极其快速而迅猛的发展](../Page/X.Org_Server.md "wikilink")。

## 参见

  - [自由軟件](https://zh.wikipedia.org/wiki/自由軟件 "wikilink")
  - [自由軟件历史](https://zh.wikipedia.org/wiki/自由軟件历史 "wikilink")
  - [linux内核](https://zh.wikipedia.org/wiki/linux内核 "wikilink")

## 参考

## 外部链接

  - [Google的時間表](http://www.google.com/views?q=linux+view%3Atimeline&btnGt=Search)

[Category:Linux](https://zh.wikipedia.org/wiki/Category:Linux "wikilink") [Category:免費軟件](https://zh.wikipedia.org/wiki/Category:免費軟件 "wikilink")

1.
2.  {{ cite web | url = <http://www.coe.berkeley.edu/labnotes/history_unix.html> |title=Berkeley UNIX和开源软件的诞生}}
3.  {{ cite web|url=<http://oreilly.com/catalog/opensources/book/kirkmck.html> |title=从AT\&T的BerkeleyUnix到可自由再发布的20年 |author=Marshall Kirk McKusick |deadurl=yes |archiveurl=<https://web.archive.org/web/20091001021430/http://oreilly.com/catalog/opensources/book/kirkmck.html> |archivedate=2009-10-01 }}
4.  {{ cite web | url = <http://people.fluidsignal.com/~luferbu/misc/Linus_vs_Tanenbaum.html> | title = Linus vs. Tanenbaum debate | deadurl = yes | archiveurl = <https://web.archive.org/web/20081202074816/http://people.fluidsignal.com/~luferbu/misc/Linus_vs_Tanenbaum.html> | archivedate = 2008-12-02 }}
5.  {{ cite web | url = <http://gondwanaland.com/meta/history/interview.html> |title=The Choice of a GNU Generation - An Interview With Linus Torvalds }}
6.  Torvalds, Linus and David Diamond, *Just for Fun: The Story of an Accidental Revolutionary*, 2001, ISBN 0-06-662072-4
7.
8.
9.  Torvalds, Linus: *[Notes for linux release 0.01](http://www.kernel.org/pub/linux/kernel/Historic/old-versions/RELNOTES-0.01)* kernel.org, 1991.
10. Torvalds, Linus: *[Notes for linux release 0.01](http://www.kernel.org/pub/linux/kernel/Historic/old-versions/RELNOTES-0.01)* kernel.org, 1991.
11.
12. *[z-archive of Linux version 0.99](ftp://ftp.kernel.org/pub/linux/kernel/Historic/v0.99/linux-0.99.tar.Z) *, kernel.org, December 1992
13. *[1](http://www.gnu.org/gnu/gnu-history.html)*
14. Hiroo Yamagata: [*The ragmatist of Free Software*, Linus Torvalds Interview](http://www.tlug.jp/docs/linus.html) , 05.08.1997
15. [Linux and GNU - GNU Project - Free Software Foundation (FSF)](http://www.gnu.org/gnu/linux-and-gnu.html)
16.
17.
18.
19.
20.
21. Andrew Tanenbaum, Linus Torvalds and others: *[Linux is obsolete](http://www.educ.umu.se/~bjorn/mhonarc-files/obsolete/msg00009.html) * Usenet post, 29.01.1992
22. *[The GNU Hurd Project](http://www.gnu.org/software/hurd/hurd.html#status)*
23.
24.
25.