> 本文内容由[Java](https://zh.wikipedia.org/wiki/Java)转换而来。


****是一種廣泛使用的電腦[程式設計語言](https://zh.wikipedia.org/wiki/程式設計語言 "wikilink")，擁有[跨平台](https://zh.wikipedia.org/wiki/跨平台 "wikilink")、[物件導向](https://zh.wikipedia.org/wiki/物件導向 "wikilink")、[泛型程式設計的特性](https://zh.wikipedia.org/wiki/泛型程式設計 "wikilink")，广泛应用于企业级Web应用开发和移动应用开发。

任職於[昇陽電腦](../Page/昇陽電腦.md "wikilink")的[詹姆斯·高斯林](../Page/詹姆斯·高斯林.md "wikilink")等人于1990年代初开发Java語言的雛形，最初被命名为Oak，目標設定在[家用电器](../Page/家用电器.md "wikilink")等小型系統的[程式语言](https://zh.wikipedia.org/wiki/程式语言 "wikilink")，應用在[电视机](../Page/电视机.md "wikilink")、[电话](../Page/电话.md "wikilink")、[闹钟](https://zh.wikipedia.org/wiki/闹钟 "wikilink")、[烤面包机等家用电器的控制和通訊](https://zh.wikipedia.org/wiki/烤面包机 "wikilink")。由于这些[智能化家电的市场需求没有预期的高](https://zh.wikipedia.org/wiki/智能化 "wikilink")，[太阳计算机系统](https://zh.wikipedia.org/wiki/太阳计算机系统 "wikilink")（[Sun公司](https://zh.wikipedia.org/wiki/Sun公司 "wikilink")）放弃了该项计划。随着1990年代[網際網路的发展](https://zh.wikipedia.org/wiki/網際網路 "wikilink")，[Sun公司看見Oak在](https://zh.wikipedia.org/wiki/Sun公司 "wikilink")[網際網路上应用的前景](https://zh.wikipedia.org/wiki/網際網路 "wikilink")，于是改造了Oak，於1995年5月以Java的名称正式发布。Java伴随着互联网的迅猛发展而发展，逐渐成为重要的网络编程语言。

Java编程语言的风格十分接近[C++](../Page/C++.md "wikilink")语言。继承了[C++](../Page/C++.md "wikilink")语言面向对象技术的核心，舍弃了容易引起错误的[-{zh-hans:指针; zh-hant:指標;}-](https://zh.wikipedia.org/wiki/指针_\(信息学\) "wikilink")，以[-{zh-hans:引用; zh-hant:參照;}-取代](../Page/參照.md "wikilink")；移除了C++中的-{zh-hans:[运算符重载](../Page/运算符重载.md "wikilink"); zh-hant:[運算子多载](https://zh.wikipedia.org/wiki/運算子多载 "wikilink");}-和[多重继承特性](https://zh.wikipedia.org/wiki/继承_\(计算机科学\) "wikilink")，用[接口取代](../Page/接口_\(Java\).md "wikilink")；增加[垃圾回收器功能](../Page/垃圾回收_\(計算機科學\).md "wikilink")。在Java SE 1.5版本中引入了[泛型](../Page/泛型.md "wikilink")编程、[类型安全的枚举](https://zh.wikipedia.org/wiki/类型安全 "wikilink")、不定长参数和自动装/拆箱特性。昇陽電腦对Java语言的解释是：「Java编程语言是个简单、面向对象、分布式、解释性、健壮、安全与系统无关、可移植、高性能、多线程和动态的语言」

Java不同於一般的[编译語言或](https://zh.wikipedia.org/wiki/编译語言 "wikilink")[直譯語言](https://zh.wikipedia.org/wiki/直譯語言 "wikilink")。它首先将源代码编译成[字节码](https://zh.wikipedia.org/wiki/字节码 "wikilink")，再依赖各种不同平台上的虚拟机来解释执行字节码，从而具有“[一次编写，到处运行](../Page/一次编写，到处运行.md "wikilink")”的跨平台特性。在早期JVM中，这在一定程度上降低了Java程序的运行效率。但在J2SE1.4.2发布后，Java的執行速度有了大幅提升。

与传统型態不同，Sun公司在推出Java時就将其作为开放的技术。全球的Java开发公司被要求所设计的Java软件必须相互兼容。“Java语言靠群体的力量而非公司的力量”是Sun公司的口号之一，并获得了广大软件开发商的认同。这与[微软](../Page/微软.md "wikilink")公司所倡导的注重精英和封闭式的模式完全不同，此外，[微软公司後來推出了与之竞争的](https://zh.wikipedia.org/wiki/微软公司 "wikilink")[.NET平台以及模仿Java的](https://zh.wikipedia.org/wiki/.NET_Framework "wikilink")[C\#语言](https://zh.wikipedia.org/wiki/C＃ "wikilink")。後來Sun公司被[甲骨文公司](../Page/甲骨文公司.md "wikilink")併購，Java也隨之成為甲骨文公司的產品。

現時，行動[作業系統](https://zh.wikipedia.org/wiki/作業系統 "wikilink")[Android](../Page/Android.md "wikilink")大部分的代碼採用Java[程式設計語言編程](https://zh.wikipedia.org/wiki/程式設計語言 "wikilink")。

## 历史

### 早期的Java

[James_Gosling_2008.jpg](https://zh.wikipedia.org/wiki/File:James_Gosling_2008.jpg "fig:James_Gosling_2008.jpg")\]\] [Duke_(Java_mascot)_waving.svg](https://zh.wikipedia.org/wiki/File:Duke_\(Java_mascot\)_waving.svg "fig:Duke_(Java_mascot)_waving.svg")

語言最開始只是[Sun電腦](https://zh.wikipedia.org/wiki/Sun電腦 "wikilink")（Sun MicroSystems）公司在1990年12月開始研究的一個內部項目。Sun電腦公司的一個叫做的工程師被公司自己開發的[C++](../Page/C++.md "wikilink")和[C語言編譯器搞得焦頭爛額](https://zh.wikipedia.org/wiki/C語言 "wikilink")，因為其中的[API極其難用](https://zh.wikipedia.org/wiki/應用程序接口 "wikilink")。帕特里克決定改用[NeXT](../Page/NeXT.md "wikilink")，同時他也獲得了研究公司的一個叫做**「Stealth計劃」**的項目的機會。

「Stealth計劃」後來改名為「**Green計劃**」，[詹姆斯·高斯林](../Page/詹姆斯·高斯林.md "wikilink")和麥克·舍林丹（Mike Sheridan）也加入了帕特里克的工作小組。他們和其他幾個工程師一起在[加利福尼亞州](https://zh.wikipedia.org/wiki/加利福尼亞州 "wikilink")[門羅帕克市](../Page/门洛帕克_\(加利福尼亚州\).md "wikilink")[沙丘路的一個小工作室裡面研究開發新技術](https://zh.wikipedia.org/wiki/沙丘路 "wikilink")，瞄準下一代智能家電（如[微波爐](https://zh.wikipedia.org/wiki/微波爐 "wikilink")）的程序設計，[Sun公司預料未來科技將在家用電器領域大顯身手](../Page/昇陽電腦.md "wikilink")。團隊最初考慮使用C++語言，但是很多成員包括Sun的首席科學家[比爾·喬伊](../Page/比尔·乔伊.md "wikilink")，發現C++和可用的API在某些方面存在很大問題。

工作小組使用的是[嵌入式系統](https://zh.wikipedia.org/wiki/嵌入式系統 "wikilink")，可以用的資源極其有限。很多成員發現C++太複雜以至很多開發者經常錯誤使用。他們發現C++缺少[垃圾回收系統](../Page/垃圾回收_\(計算機科學\).md "wikilink")，還有可移植的安全性、[分佈程序設計](https://zh.wikipedia.org/wiki/分佈程序設計 "wikilink")、和[多執行緒功能](https://zh.wikipedia.org/wiki/多執行緒 "wikilink")。最後，他們想要一種易於移植到各種設備上的平台。

根據可用的資金，喬伊決定開發一種集[C語言和](https://zh.wikipedia.org/wiki/C語言 "wikilink")[Mesa語言大成的新語言](https://zh.wikipedia.org/wiki/Mesa語言 "wikilink")，在一份報告上，喬伊把它叫做「未來」，他提議Sun公司的工程師應該在C++的基礎上，開發一種[物件導向的環境](https://zh.wikipedia.org/wiki/物件導向 "wikilink")。最初，高斯林試圖修改和擴展C++的功能，，但是後來他放棄了。他將要創造出一種全新的語言，被他命名為「**Oak**」（橡樹），以他的辦公室外的橡樹命名。

就像很多開發新技術的秘密工程一樣，工作小組沒日沒夜地工作到了1993年的夏天，他們能夠演示新平台的一部分了，包括Green[操作系统](../Page/操作系统.md "wikilink")，Oak的程序設計語言，類庫及其硬件。最初的嘗試是面向一種類[PDA設備](https://zh.wikipedia.org/wiki/PDA "wikilink")，被命名為**Star7**，這種設備有鮮豔的圖形界面和被稱為「Duke」的智能代理來幫助用戶。1992年12月3日，這台設備進行了展示。

同年11月，Green計劃被轉化成了「**FirstPerson有限公司**」，一個Sun公司的全資子公司，團隊也被重新安排到了[帕洛阿爾托](https://zh.wikipedia.org/wiki/帕羅奧多_\(美國加州\) "wikilink")。FirstPerson團隊對建造一種高度互動的設備感興趣，當[時代華納發佈了一個關於](https://zh.wikipedia.org/wiki/時代華納 "wikilink")[電視](https://zh.wikipedia.org/wiki/電視 "wikilink")[機頂盒的徵求提議書時](../Page/數位視訊轉換盒.md "wikilink")（Request for proposal），FirstPerson改變了他們的目標，作為對徵求意見書的響應，提出了一個機頂盒平台的提議。但是[有線電視業界覺得FirstPerson的平台給予用戶過多的控制權](https://zh.wikipedia.org/wiki/有線電視 "wikilink")，因此FirstPerson的投標敗給了[SGI](../Page/硅谷图形公司.md "wikilink")。與[3DO公司](../Page/3DO公司.md "wikilink")的另外一筆關於機頂盒的交易也沒有成功，由於他們的平台不能在電視工業產生任何效益，公司被併回Sun公司。

### Java和「Java」

由于[商标](../Page/商标.md "wikilink")搜索显示Oak已被一家显示卡制造商注册。于是同年，Oak被改名为**Java**。当使用十六进制编辑器打开由Java源代码编译出的二进制文件（.class文件）的话，最前面的32位将显示为CA FE BA BE，即词组“CAFE BABE”（咖啡屋宝贝）。

### Java和互联网

[J-0.23.0.png](https://zh.wikipedia.org/wiki/File:J-0.23.0.png "fig:J-0.23.0.png") [Java_se-cdc-clds.PNG](https://zh.wikipedia.org/wiki/File:Java_se-cdc-clds.PNG "fig:Java_se-cdc-clds.PNG")環境與CDC的關連\]\] [MHP-software_stack_english.png](https://zh.wikipedia.org/wiki/File:MHP-software_stack_english.png "fig:MHP-software_stack_english.png") [Jsxp_arch.png](https://zh.wikipedia.org/wiki/File:Jsxp_arch.png "fig:Jsxp_arch.png")網頁的概念\]\]

1994年6月，在同、[詹姆斯·高斯林](../Page/詹姆斯·高斯林.md "wikilink")、[比尔·乔伊](../Page/比尔·乔伊.md "wikilink")、、和[埃里克·施密特](../Page/埃里克·施密特.md "wikilink")经历了一场历时三天的头脑风暴后，团队决定再一次改变努力的目标，这次他们决定将该技术应用于[万维网](../Page/万维网.md "wikilink")。他们认为随着[Mosaic](../Page/Mosaic.md "wikilink")[浏览器的到来](https://zh.wikipedia.org/wiki/浏览器 "wikilink")，因特网正在向同样的高度互动的远景演变，而这一远景正是他们在有线电视网中看到的。作为原型，帕特里克·诺顿写了一个小型万维网浏览器，WebRunner，后来改名为[HotJava](../Page/HotJava.md "wikilink")\[1\]。

1994年10月，HotJava和Java平台为公司高层进行演示。1994年，Java 1.0a版本已经可以提供下載，但是Java和HotJava浏览器的第一次公开发布却是在1995年3月23日SunWorld大会上进行的。升阳公司的科学指导约翰·盖吉宣告Java技术。这个发布是与[网景公司的执行副总裁](../Page/網景.md "wikilink")[马克·安德森](../Page/马克·安德森.md "wikilink")的惊人发布一起进行的，宣布网景将在其浏览器中包含对Java的支持。1996年1月，Sun公司成立了Java业务集团，专门开发Java技术。

在流行几年之后，Java在浏览器中的地位被逐步侵蚀。它在简单交互性动画方面的用途已经完全被[Adobe公司的](https://zh.wikipedia.org/wiki/Adobe_Systems "wikilink")[Flash排挤](../Page/Adobe_Flash.md "wikilink")，2005年Java倾向只被用于[雅虎游戏那样的更为复杂的应用程序](https://zh.wikipedia.org/wiki/雅虎游戏 "wikilink")。Java同时遭受到来自微软的反对，他们决定在新版本的[Internet Explorer和](../Page/Internet_Explorer.md "wikilink")[Windows中不再附带Java平台](https://zh.wikipedia.org/wiki/Microsoft_Windows "wikilink")。

与此相反，在万维网的服务器端和手持设备上，Java变得更加流行。很多网站在後端使用[JSP](../Page/JSP.md "wikilink")和其他的Java技术。

在桌面系统上，独立的Java程序还是相对少见这是因为Java平台的运行开销较大，而许多人的电脑上没有安装Java，由于网络带宽在以前较小，下载Java曾经是个耗时的事情。但是随着计算机计算能力、网络带宽在10年中取得了很大的进步，同时虚拟机和编译器的质量得到了提高，许多应用程序得到了广泛的使用，包括：

  - [开源软件](../Page/开放源代码.md "wikilink")

<!-- end list -->

  - [NetBeans](../Page/NetBeans.md "wikilink")和[Eclipse](../Page/Eclipse.md "wikilink")等軟件開發工具
  - [Android](../Page/Android.md "wikilink")操作系统
  - [JEdit](../Page/JEdit.md "wikilink")
  - [Azureus](https://zh.wikipedia.org/wiki/Vuze_\(软件\) "wikilink") [BitTorrent客户端](https://zh.wikipedia.org/wiki/BitTorrent "wikilink")。
  - [JNode](../Page/JNode.md "wikilink")操作系统
  - [Apache軟件基金會的](https://zh.wikipedia.org/wiki/Apache軟件基金會 "wikilink")[Ant](../Page/Apache_Ant.md "wikilink")、[Derby](../Page/Apache_Derby.md "wikilink")、[Hadoop](https://zh.wikipedia.org/wiki/Hadoop "wikilink")、[Jakarta](../Page/Jakarta项目.md "wikilink")、[POI和](../Page/Apache_POI.md "wikilink")[Tomcat](../Page/Apache_Tomcat.md "wikilink")
  - [JBoss和](https://zh.wikipedia.org/wiki/JBoss "wikilink")[GlassFish應用伺服器](https://zh.wikipedia.org/wiki/GlassFish "wikilink")

<!-- end list -->

  - [商業軟體](https://zh.wikipedia.org/wiki/商業軟體 "wikilink")

<!-- end list -->

  - [EIOffice](https://zh.wikipedia.org/wiki/EIOffice "wikilink")（永中Office）
  - [Minecraft](https://zh.wikipedia.org/wiki/Minecraft "wikilink")
  - 纯Java 3D游戏[合金战士](https://zh.wikipedia.org/wiki/合金战士 "wikilink")[Chrome](https://zh.wikipedia.org/wiki/Chrome_\(游戏\) "wikilink")
  - IBM Websphere、[ColdFusion和](https://zh.wikipedia.org/wiki/ColdFusion "wikilink")[WebLogic](../Page/WebLogic.md "wikilink")
  - [IntelliJ IDEA](../Page/IntelliJ_IDEA.md "wikilink")

目前Java提供以下三个版本：

  - Java Platform, Enterprise Edition（[Java EE](https://zh.wikipedia.org/wiki/J2EE "wikilink")：[Java平台企业版](https://zh.wikipedia.org/wiki/J2EE "wikilink")）
  - Java Platform, Standard Edition（[Java SE](https://zh.wikipedia.org/wiki/J2SE "wikilink")：[Java平台标准版](https://zh.wikipedia.org/wiki/J2SE "wikilink")）
  - Java Platform, Micro Edition（[Java ME](https://zh.wikipedia.org/wiki/J2ME "wikilink")：[Java平台微型版](https://zh.wikipedia.org/wiki/J2ME "wikilink")）
  - Java Platform, Card Edition

### Java開放原始碼項目

2006年SUN在[JavaOne公佈Java](https://zh.wikipedia.org/wiki/JavaOne "wikilink") [開放原始碼項目](https://zh.wikipedia.org/wiki/開放原始碼 "wikilink")，並推出[OpenJDK](../Page/OpenJDK.md "wikilink")計畫\[2\]。[Java虛擬機](https://zh.wikipedia.org/wiki/Java虛擬機 "wikilink")、Java[編譯器](../Page/編譯器.md "wikilink")和Java類庫以GNU通用公共許可證公開。

### 版本历史

  - 1995年5月23日，Java语言诞生
  - 1996年1月，第一个[JDK](../Page/JDK.md "wikilink")-[JDK1.0诞生](https://zh.wikipedia.org/wiki/JDK1.0 "wikilink")
  - 1996年4月，10个最主要的[操作系统](../Page/操作系统.md "wikilink")供应商申明将在其产品中嵌入JAVA技术
  - 1996年9月，约8.3万个网页应用了JAVA技术来制作
  - 1997年2月18日，[JDK1.1发布](https://zh.wikipedia.org/wiki/JDK1.1 "wikilink")
  - 1997年4月2日，JavaOne会议召开，参与者逾一万人，创当时全球同类会议规模之纪录
  - 1997年9月，[JavaDeveloperConnection社区成员超过十万](https://zh.wikipedia.org/wiki/JavaDeveloperConnection "wikilink")
  - 1998年2月，[JDK1.1被下载超过](https://zh.wikipedia.org/wiki/JDK1.1 "wikilink")**2,000,000**次
  - 1998年12月8日，[JAVA2企业平台J](https://zh.wikipedia.org/wiki/JAVA2 "wikilink")2EE发布
  - 1999年6月，SUN公司发布Java的三个版本：标准版（[J2SE](https://zh.wikipedia.org/wiki/J2SE "wikilink")）、企业版（[J2EE](https://zh.wikipedia.org/wiki/J2EE "wikilink")）和微型版（[J2ME](https://zh.wikipedia.org/wiki/J2ME "wikilink")）
  - 2000年5月8日，[JDK1.3发布](https://zh.wikipedia.org/wiki/JDK1.3 "wikilink")
  - 2000年5月29日，[JDK1.4发布](https://zh.wikipedia.org/wiki/JDK1.4 "wikilink")
  - 2001年6月5日，[NOKIA宣布](../Page/诺基亚.md "wikilink")，到2003年将出售1亿部支持Java的手机
  - 2001年9月24日，[J2EE1.3发布](https://zh.wikipedia.org/wiki/J2EE1.3 "wikilink")
  - 2002年2月26日，[J2SE1.4发布](https://zh.wikipedia.org/wiki/J2SE1.4 "wikilink")，自此Java的计算能力有了大幅提升
  - 2004年9月30日18:00PM，[J2SE1.5发布](https://zh.wikipedia.org/wiki/J2SE1.5 "wikilink")，成为Java语言发展史上的又一里程碑。为了表示该版本的重要性，[J2SE1.5更名为Java](https://zh.wikipedia.org/wiki/J2SE1.5 "wikilink") SE 5.0
  - 2005年6月，[JavaOne大会召开](https://zh.wikipedia.org/wiki/JavaOne大会 "wikilink")，SUN公司公开Java SE 6。此时，Java的各种版本已经更名，以取消其中的数字“2”：J2EE更名为Java EE，J2SE更名为Java SE，J2ME更名为Java ME
  - 2006年12月，SUN公司发布JRE6.0
  - 2009年12月，SUN公司发布Java EE 6
  - 2010年11月，由於Oracle公司對於Java社群的不友善，因此Apache揚言將-{退出}-JCP\[3\]
  - 2011年7月28日，Oracle公司發佈Java SE 7
  - 2014年3月18日，Oracle公司发表Java SE 8
  - 2017年9月21日，Oracle公司发表Java SE 9
  - 2018年3月21日，Oracle公司发表Java SE 10
  - 2018年9月25日，Java SE 11发布

## 语言特性

Java之所以被开发，是要达到以下五个目的：

  - 应当使用面向对象程序设计方法学
  - 应当允许同一程序在不同的计算机平台执行
  - 应当包括内建的对计算机网络的支持
  - 应当被设计成安全地执行远端代码
  - 应当易于使用，并借鉴以前那些面向对象语言（如C++）的长处。

Java技术主要分成几个部分：Java语言、[Java執行環境](../Page/Java平臺.md "wikilink")、类库。一般情况下说Java时并不区分指的是哪个部分。

Java在1.5版本時，做了重大改變，Sun公司並1.5版本重新命名為[Java 5.0](../Page/Java_5.0.md "wikilink")。

### 面向对象

Java的特点之一就是[面向对象](../Page/面向对象程序设计.md "wikilink")，是程序设计方法的一种。“面向对象程序设计语言”的核心之一就是开发者在设计软件的时候可以使用自定义的类型和关联操作。代码和数据的实际集合体叫做“对象”。一个对象可以想象成绑定了很多“行为（代码）”和“状态（数据）”的物体。对于数据结构的改变需要和代码进行通信然后操作，反之亦然。面向对象设计让大型软件工程的计划和设计变得更容易管理，能增强工程的健康度，减少失败工程的数量。

### 跨平台性

跨平台性是Java主要的特性之一，跨平台使得用Java语言编写的程序可以在编译后不用经过任何更改，就能在任何硬件设备条件下运行。这个特性经常被称为“一次编译，到处运行”。

执行Java应用程式必须安装**Java 运行时环境**（Java Runtime Environment，JRE），JRE包括[Java虚拟机](../Page/Java虚拟机.md "wikilink")（Java Virtual Machine，JVM），以及Java平台核心类和基础Java 平台库。\[4\]通过JVM才能在电脑系统执行Java应用程序（Java Application），这与**[.Net Framework](https://zh.wikipedia.org/wiki/.Net_Framework "wikilink")**的情况一样，所以电脑上没有安装JVM，那么这些java程序将不能够执行。

实现跨平台性的方法是大多数编译器在进行Java语言程序的编码时候会生成一个用[字节码写成的](https://zh.wikipedia.org/wiki/字节码 "wikilink")“半成品”，这个“半成品”会在Java虚拟机（解释层）的帮助下运行，虚拟机会把它转换成当前所处硬件平台的原始代码。之后，Java虚拟机会打开标准库，进行数据（图片、线程和网络）的存取工作。主要注意的是，尽管已经存在一个进行代码翻译的解释层，有些时候Java的字节码代码还是会被[JIT编译器进行二次编译](https://zh.wikipedia.org/wiki/JIT "wikilink")。

有些编译器，比如[GCJ](../Page/GCJ.md "wikilink")，可以自动生成原始代码而不需要解释层。但是这些编译器所生成的代码-{只}-能应用于特定平台。并且[GCJ](../Page/GCJ.md "wikilink")目前只支持部分的Java API。

甲骨文公司对于Java的许可是“全兼容的”，这也导致了微软和升阳关于微软的程序不支持RMI和JNI接口、并且增加特性为己所用的法律争端。升阳最终赢得了官司，获得了大约两千万[美元](../Page/美元.md "wikilink")的赔偿，法院强制要求微软执行升阳公司关于Java的许可要求。作为回应，[微软](../Page/微软.md "wikilink")不再在[Windows系统中捆绑Java](https://zh.wikipedia.org/wiki/Windows "wikilink")，最新的Windows版本，[Windows Vista和Internet](../Page/Windows_Vista.md "wikilink") Explorer 7.0版本也不再提供对于Java应用程序和控件的支持。但是升阳公司和其他使用Java运行时系统的公司在Windows操作系统下对用户提供无偿的第三方插件和程序支持。

Java语言使用解释层最初是为了轻巧性。所以这些程序的运行效率比C语言和C++要低很多，用户也对此颇有微词。很多最近的调查显示Java的程序运行速度比几年前要高出许多，有些同样功能的程序的效率甚至超过了C++和C语言编写的程序。

Java语言在最开始应用的时候是没有解释层的，所有需要编译的代码都直接转换成机器的原始代码。这样做虽然使程序获得了最佳的性能，但是导致程序异常臃肿。从JIT技术开始，Java的程序都经过一次转换之后才变成机器码。很多老牌的第三方虚拟机都使用一种叫做“[动态编译](https://zh.wikipedia.org/wiki/动态编译 "wikilink")”的技术，也就是说虚拟机实时监测和分析程序的运行行为，同时选择性地对程序所需要的部分进行编译和优化。所有这些技术都改善了代码的运行速度，但是又不会让程序的体积变得失常。

程序的轻便性事实上是软件编写很难达到的一个目标，Java虽然成功地实现了“一次编译，到处运行”，但是由于平台和平台之间的差异，所编写的程序在转换代码的时候难免会出现微小的、不可察觉的错误和意外。有些程序员对此非常头疼，他们嘲笑Java的程序不是“一次编译，到处运行”，而是“一次编译，到处调试”。以Java AWT為例，早期Java AWT內提供的按鈕、文字區等均是以電腦系統所預設的樣式而顯示。這令Java程式在有些沒有提供圖案的電腦系統產生錯誤（在Microsoft Windows設有視窗管理員，在一些Linux distribution則沒有）。後來SUN公司針對Java AWT一些問題而推出Java Swing。

平台无关性让Java在服务器端软件领域非常成功。很多服务器端软件都使用Java或相关技术建立。

### 自動垃圾回收（Garbage Collection）

C++語言被用戶詬病的原因之一是大多數C++編譯器不支持[垃圾收集機制](../Page/垃圾回收_\(計算機科學\).md "wikilink")。通常使用C++編程的時候，程式設計師於程式中初始化對象時，會在主機[記憶體](https://zh.wikipedia.org/wiki/記憶體 "wikilink")[堆疊上分配一塊記憶體與位址](https://zh.wikipedia.org/wiki/堆疊 "wikilink")，當不需要此對象時，進行解構或者刪除的時候再釋放分配的記憶體位址。如果對象是在堆疊上分配的，而程序員又忘記進行刪除，那麼就會造成[記憶體洩漏](https://zh.wikipedia.org/wiki/記憶體洩漏 "wikilink")（Memory Leak）。長此以往，程序運行的時候可能會生成很多不清除的垃圾，浪費了不必要的記憶體空間。而且如果同一記憶體地址被刪除兩次的話，程序會變得不穩定，甚至崩潰。因此有經驗的C++程序員都會在刪除之後將指標重置為NULL，然後在刪除之前先判斷指標是否為NULL。

C++中也可以使用「智慧指標」（Smart Pointer）或者使用[C++託管擴展編譯器的方法來實現自動化記憶體釋放](https://zh.wikipedia.org/wiki/C++託管擴展 "wikilink")，智慧指標可以在[標準類庫中找到](https://zh.wikipedia.org/wiki/標準類庫 "wikilink")，而C++託管擴展被微軟的Visual C++ 7.0及以上版本所支持。智慧指標的優點是不需引入緩慢的垃圾收集機制，而且可以不考慮線程安全的問題，但是缺點是如果不善使用智慧指標的話，性能有可能不如垃圾收集機制，而且不斷地分配和釋放記憶體可能造成記憶體碎片，需要手動對堆進行壓縮。除此之外，由於智慧指標是一個基於模板的功能，所以沒有經驗的程序員在需要使用多態特性進行自動清理時也可能束手無策。

Java語言則不同，上述的情況被自動垃圾收集功能自動處理。對象的建立和放置都是在記憶體堆疊上面進行的。當一個物件沒有任何引用的時候，Java的自動垃圾收集機制就發揮作用，自動刪除這個物件所佔用的空間，釋放記憶體以避免記憶體洩漏。

注意程式設計師不需要修改finalize方法，自動垃圾收集也會發生作用。但是記憶體洩漏並不是就此避免了，當程序員疏忽大意地忘記解除一個物件不應該有的引用時，記憶體洩漏仍然不可避免。

不同廠商、不同版本的JVM中的記憶體垃圾回收機制並不完全一樣，通常越新版本的記憶體回收機制越快，IBM、BEA、SUN等等開發JVM的公司都曾宣稱過自己製造出了世界上最快的JVM，JVM性能的世界紀錄也在不斷的被打破並提高。

IBM有一篇有關Java記憶體回收機制比不啟用垃圾收集機制的C++記憶體處理快數倍的技術文章\[5\]，而著名的Java技術書籍《Java編程思想》（*Thinking in Java*）也有一段論述Java記憶體及性能達到甚至超過C++的章節\[6\]。

### 基本语法

编写Java程序前应注意以下几点：

  - **大小写敏感**：Java是大小写敏感的，这就意味着标识符`Hello`与`hello`是不同的。
  - **类名**：对于所有的类来说，类名的首字母应该大写。如果类名由若干单词组成，那么每个单词的首字母应该大写，例如**`MyFirstJavaClass`**。
  - **方法名**：所有的方法名都应该以小写字母开头。如果方法名含有若干单词，则后面的每个单词首字母大写，例如**`myFirstJavaMethod`**。
  - **源文件名**：源文件名必须和类名相同。当保存文件的时候，你应该使用类名作为文件名保存（切记Java是大小写敏感的），文件名的后缀为`.java`。（如果文件名和类名不相同则会导致编译错误）。
  - **主方法入口**：所有的Java程序由`public static void main(String[] args)`方法开始执行。

### Java关键字

下面列出了Java[关键字](https://zh.wikipedia.org/wiki/关键字 "wikilink")。这些关键字不能用于[常量](https://zh.wikipedia.org/wiki/常量 "wikilink")、[变量](https://zh.wikipedia.org/wiki/变量 "wikilink")、和任何[标识符的名称](https://zh.wikipedia.org/wiki/标识符 "wikilink")。

| 类别           | 关键字              | 说明         |
| ------------ | ---------------- | ---------- |
| 访问控制         | private          | 私有的        |
| protected    | 受保护的             |            |
| public       | 公共的              |            |
| 类、方法和变量修饰符   | abstract         | 声明抽象       |
| class        | 类                |            |
| extends      | 扩允,继承            |            |
| final        | 最终值,不可改变的        |            |
| implements   | 实现（接口）           |            |
| interface    | 接口               |            |
| native       | 本地，原生方法（非Java实现） |            |
| new          | 新,创建             |            |
| static       | 静态               |            |
| strictfp     | 严格,精准            |            |
| synchronized | 线程,同步            |            |
| transient    | 短暂               |            |
| volatile     | 易失               |            |
| 程序控制语句       | break            | 跳出循环       |
| case         | 定义一个值以供switch选择  |            |
| continue     | 继续               |            |
| default      | 默认               |            |
| do           | 运行               |            |
| else         | 否则               |            |
| for          | 循环               |            |
| if           | 如果               |            |
| instanceof   | 实例               |            |
| return       | 返回               |            |
| switch       | 根据值选择执行          |            |
| while        | 循环               |            |
| 错误处理         | assert           | 断言表达式是否为真  |
| catch        | 捕捉异常             |            |
| finally      | 有没有异常都执行         |            |
| throw        | 抛出一个异常对象         |            |
| throws       | 声明一个异常可能被抛出      |            |
| try          | 捕获异常             |            |
| 包相关          | import           | 引入         |
| package      | 包                |            |
| 基本类型         | boolean          | 布尔型        |
| byte         | 字节型              |            |
| char         | 字符型              |            |
| double       | 双精度浮点            |            |
| float        | 单精度浮点            |            |
| int          | 整型               |            |
| long         | 长整型              |            |
| short        | 短整型              |            |
| null         | 空                |            |
| 变量引用         | super            | 父类,超类      |
| this         | 本类               |            |
| void         | 无返回值             |            |
| 保留关键字        | goto             | 是关键字，但不能使用 |
| const        | 是关键字，但不能使用       |            |

  - 注释

[注释的作用](https://zh.wikipedia.org/wiki/注释 "wikilink")：标识程序是干什么的，以及它是如何构建的。注释帮助程序员进行相互沟通以及理解程序。注释不是程序设计语言，所以编译器编译程序时忽略它们。

### 接口和类別

Java自带了创建接口的类別，可以这样使用：

``` java
public interface Deleteable {
    void delete();
System.out.println(" ATTACH DATABASE 'DatabaseName' As 'Alias-Name'");
}
```

这段代码的意思是任何实现（implement）`Deleteable`接口的类別都必须实现`delete()`方法。每个类別对这个方法的实现可以自行定制。由此概念可以引出很多种使用方法，下面是一个类別的例子：

``` java
public class Fred implements Deleteable {
        // 必須實作Deleteable介面中的delete方法
@Override
public void delete() {
        // 實作的程式碼
    }

       // 這個類別也可以包含其他方法
public void doOtherStuff() {

    }
}
```

在另外一个类別中，可以使用这样的代码：

``` java
public void deleteAll（Deleteable [] list）{
    for（int i = 0; i < list.length; i++）{
        list[i].delete();
    }
}
```

因为队列中所有的对象都可以使用`delete()`方法。`Deleteable`队列中包含`Fred`对象的引用，而这个类別和其他`Deleteable`类別在使用`deleteAll()`方法时候不需要进行任何改变。

之所以这样做就是为了在接口的执行和其代码之间进行区别。举例来说，一个名叫`Collection`的接口可以包含任何对象所需要的引入、转换和存储数据的方法，其他的类都可以使用这个接口。但是这个接口可以是一个可重定义大小的队列、一个[链表](../Page/链表.md "wikilink")或者是其他功能的集合。

这种特性其实是一种折中的办法。Java的设计者们不想让Java有[多重继承](../Page/多重继承.md "wikilink")的特性，因为C++的多重继承显示了这种特性的困难。Java的接口功能可以提供同样的功能，但是又不会很复杂。

### 应用程序开发接口

在Java语言中，[应用程序接口](../Page/应用程序接口.md "wikilink")（API）化身成-{zh-hans:类; zh-hant:類別;}-，并且分组成为-{zh-hans:包; zh-hant:套件;}-。每个包中包含有相关的接口和类。对于不同的平台，Java提供了不同版本的包。API的设定由sun公司和其他公司通过[JCP](../Page/JCP.md "wikilink")（Java社群程序）决定。任何公司和个人都可以参与这个工程，对API进行设计。2004年，[IBM](../Page/IBM.md "wikilink")和[BEA公司准备联合对官方的Java开源软件工程进行支持](https://zh.wikipedia.org/wiki/BEA_Systems "wikilink")，但是2005年初，sun公司拒绝了这个支持。

## Hello World

下面这个程序显示“Hello, world\!”然后结束运行，注意`java.lang`套件是自動載入的，所以不需要在程式之前加入`import java.lang.*;`

``` java
public class HelloWorld {
    public static void main(String[] args) {
        System.out.println("Hello World!"); // Prints the string to the console.
    }
}
```

## 關於Java的批評

[Java_Ring.jpg](https://zh.wikipedia.org/wiki/File:Java_Ring.jpg "fig:Java_Ring.jpg")

Java試圖通過新的方式解決軟體編寫的複雜性。很多人認為Java語言做到了它承諾的一切。但是Java並不是一門完美的語言。

### 整體性問題

並不是所有的工程和環境需要企業等級的複雜性，比如一個簡單的個人網站或者獨自編程的程式師所寫的程式。這些程式師會發現Java的複雜管理對於自己要做的程式來說過於強大了。一些人覺得Java在物件導向上面做的沒有[Ruby](../Page/Ruby.md "wikilink")和[Smalltalk](../Page/Smalltalk.md "wikilink")純粹。但是最新出現的用Java實現的語言[Groovy](../Page/Groovy.md "wikilink")解決了這些問題。

作為一種已經建立的新技術，Java顯然綜合了很多語言的特性，比如C++、C語言、[Python](../Page/Python.md "wikilink")等等。一些對於Java的評論認為Java的不變性在動搖。

### 語言問題

有些程式師不喜歡原始類型（primitive type）和類別（class）的分離，尤其是那些曾經使用過[Smalltalk](../Page/Smalltalk.md "wikilink")和[Ruby](../Page/Ruby.md "wikilink")的程序员。Java的[代碼相對於其他的](https://zh.wikipedia.org/wiki/代碼 "wikilink")[代碼來說過於冗長](https://zh.wikipedia.org/wiki/代碼 "wikilink")，這與它的輕便化聲明相違背。

Java是一種[單繼承的語言](https://zh.wikipedia.org/wiki/單繼承 "wikilink")。這也導致了程式師在試圖使用[多重繼承時候的不便](https://zh.wikipedia.org/wiki/多重繼承 "wikilink")，而很多語言都可以使用這個特性。但是Java可以使用[介面類](https://zh.wikipedia.org/wiki/介面類 "wikilink")，把多重繼承可能導致的風險減少到最小。Java不支持[運算符重載](https://zh.wikipedia.org/wiki/運算符重載 "wikilink")，這是為了防止[運算符重載使得代碼的功能變得不清晰](https://zh.wikipedia.org/wiki/運算符重載 "wikilink")。但是用Java實現的語言[Groovy](../Page/Groovy.md "wikilink")可以進行[運算符重載](https://zh.wikipedia.org/wiki/運算符重載 "wikilink")。過去Java對於文本的操作和其他語言，比如[Perl](../Page/Perl.md "wikilink")和[PHP](../Page/PHP.md "wikilink")相比差的較多，但Java在1.4版本時候引入了[正则表达式](../Page/正则表达式.md "wikilink")。

至Java 1.7为止，Java语言不支持闭包（closure）和混入（mixin）特性。

Java 1.8加入lambda表达式（Lambda Expressions）\[7\]。

### 類庫問題

使用[Swing平臺編寫的帶有](../Page/Swing_\(Java\).md "wikilink")[GUI](https://zh.wikipedia.org/wiki/圖形使用者界面 "wikilink")（圖形用戶介面）的程式和其他原始程式非常不同。選用[AWT](../Page/AWT.md "wikilink")工具包編寫程式的程式師看到的都是原始介面，而且也無法獲得先進的GUI編程支援，如果使用的話，就要提供每個平臺上面所需的API，這將是一項龐大的工程。Swing則是完全用Java語言所寫的程式，避免了介面元素重複的問題，只使用所有平臺都支持的最基本的繪圖機制。但是很多用戶不知道如何在Java風格和Windows風格之間進行轉換，結果造成了Java程式的介面在很多程式中非常特殊。[蘋果電腦已經提供了優化過的Java運行時程式](https://zh.wikipedia.org/wiki/蘋果公司 "wikilink")，包含了[Mac OS X的經典](https://zh.wikipedia.org/wiki/Mac_OS_X "wikilink")[Aqua介面風格](../Page/Aqua_\(GUI\).md "wikilink")。

在IBM捐赠给Eclipse基金会的SWT界面框架中，用户会看到熟悉的本地风格界面。但这又引起了不同喜好的开发人员之间的争论。

### 性能問題

由於Java編譯器和虛擬機的不同對Java代碼的性能影響比語言本身的影響大的多，所以統一討論Java的程式的性能經常是有誤導性的。據IBM的資料，在同樣的硬體上2001年時的[IBM](../Page/IBM.md "wikilink") [JDK](../Page/JDK.md "wikilink")版本的性能是1996年的JDK版本的十倍左右。<ref>見IBM東京研究院的資料：[<http://www.is.titech.ac.jp/ppl2004/proceeding>](http://www.is.titech.ac.jp/ppl2004/proceedings/ishizaki_slides.pdf)

[s/ishizaki_slides.pdf](http://www.is.titech.ac.jp/ppl2004/proceedings/ishizaki_slides.pdf)</ref>而即使是在同一時期，不同公司的JDK和[JRE](../Page/JRE.md "wikilink")的性能也不一樣，比如SUN、IBM、[BEA等公司都有自己開發的JDK和](https://zh.wikipedia.org/wiki/BEA_Systems "wikilink")[JRE](../Page/JRE.md "wikilink")。

Java語言的一些特性不可避免的有額外的性能代價，例如陣列範圍檢查、運行時類型檢查等等。Java程式的性能還會因為不同的動態複雜性和垃圾處理機制使用的多少而各有不同。如果JVM的實現比較優化的話，那麼這些功能甚至可以增加記憶體分配的性能。這和總是使用STL或者託管C++的程式的情況類似。

儘管如此，仍然有許多人認為Java的性能低。這部分歸因於Sun公司最初的JVM實現使用未優化的解釋機制來執行位元組碼。一些新版本的JVM使用Just-In-Time（[JIT](https://zh.wikipedia.org/wiki/JIT "wikilink")）編譯器，在載入位元組碼的時候將其編譯成針對運行環境的本地代碼來實現一些本地編譯器的優化特性。Just-In-Time機制和本地編譯的性能比較仍舊是一個有爭議的話題。JIT編譯需要很多時間，對於運行時間不長或者代碼很多的大型程式並不適宜。但是不算JIT編譯階段的話，程式的運行性能在很多[JVM下可以和本地編譯的程式一爭短長](https://zh.wikipedia.org/wiki/JVM "wikilink")，甚至在一些計算比較密集的數值計算領域也是這樣。目前，Java已經使用更先進的[HotSpot技術來代替JIT技術](https://zh.wikipedia.org/wiki/HotSpot_\(java\) "wikilink")，Java的性能有了更進一步的提升。另外，在使用-server選項運行Java程式時，也可以對Java進行更深入的優化，比如在運行時將調用較多的方法內聯（inline）到程式中來提高運行速度，這就是所謂的“動態優化”，而本地編譯器是無法做到這一點的；這也是一些Java代碼比對應用C/C++等語言編寫的本地代碼運行的更快的原因之一。微軟的.NET平臺也使用JIT編譯器，所以也有類似問題。

Java的設計目的主要是安全性和可攜性，所以對於一些特性，比如對硬體架構和記憶體位址訪問的直接訪問都被去除了。如果需要間接調用這些底層功能的話，就需要使用[JNI](https://zh.wikipedia.org/wiki/JNI "wikilink")（Java本地介面）來調用本地代碼，而間接訪問意味著頻繁調用這些特性時性能損失會很大，微軟的.NET平臺也有這樣的問題。所以到目前為止，性能敏感的代碼，例如驅動程式和3D电子游戏，還是大多使用本地編譯，甚至直接以不直接支援面向对象的C語言或機器碼編寫。但最近已經有了許多用純Java編寫的3D遊戲，其效果與用C語言編寫的不相上下，例如“[合金戰士](https://zh.wikipedia.org/wiki/Chrome_\(游戏\) "wikilink")”（英文名：Chrome）。這主要是因為新版的Java 3D技術已經能像C++一樣調用硬體加速，也就是使用[顯卡來加速](https://zh.wikipedia.org/wiki/顯示卡 "wikilink")，無論是C++還是Java語言寫的3D遊戲都是使用顯卡及[GPU來處理](https://zh.wikipedia.org/wiki/GPU "wikilink")，從而使得[CPU可以專注於其他方面的工作](https://zh.wikipedia.org/wiki/中央處理器 "wikilink")。

## 用途

1.桌面GUI应用程序： Java通过抽象窗口工具包（AWT），Swing和JavaFX等多种方式提供GUI开发。虽然AWT包含许多预先构建的组件，如菜单，按钮，列表以及众多第三方组件，但Swing（一个GUI小部件工具包）还提供某些高级组件，如树，表格，滚动窗格，选项卡式面板和列表。JavaFX是一组图形和媒体包，提供了Swing互操作性，3D图形功能和自包含的部署模型，可以快速编写Java小应用程序和应用程序的脚本。\[8\]

2.移动应用程序： Java Platform，Micro Edition（Java ME或J2ME）是一个跨平台框架，用于构建可在所有Java支持的设备（包括功能手机和智能手机）上运行的应用程序。此外，最受欢迎的移动操作系统之一的Android应用程序通常使用Android软件开发工具包（SDK）或其他环境在Java中编写脚本。

3.嵌入式系统： 从微型芯片到专用计算机的嵌入式系统是执行专门任务的大型机电系统的组件。诸如SIM卡，蓝光光盘播放器，公用事业仪表和电视机等多种设备都使用嵌入式Java技术。据甲骨文公司称，100％的蓝光光盘播放器和1.25亿台电视设备都采用Java技术。

4\. Web应用程序： Java通过Servlets，Struts或JSP提供对Web应用程序的支持。编程语言提供的简单编程和更高的安全性使得大量政府应用程序可用于基于Java的健康，社会安全，教育和保险。Java也可以使用Broadleaf等开源电子商务平台开发电子商务Web应用程序。

5\. Web服务器和应用程序服务器： 今天的Java生态系统包含多个Java Web服务器和应用程序服务器。虽然Apache Tomcat，Simple，Jo \!, Rimfaxe Web服务器（RWS）和Project Jigsaw占据了Web服务器空间，但WebLogic，WebSphere和Jboss EAP在商业应用服务器领域占据重要地位\[9\]。

6.企业应用程序： Java企业版（Java EE）是一种流行的平台，为脚本和运行企业软件（包括网络应用程序和Web服务）提供API和运行时环境。甲骨文宣称Java在97％的企业计算机上运行。Java中更高的性能保证和更快的计算能力导致像Murex这样的高频交易系统被编入脚本中。它也是各种银行应用程序的中枢，它们将Java从前端用户端运行到后端服务器端。

7.科学应用： Java是许多软件开发人员用于编写涉及科学计算和数学运算的应用程序的选择。这些程序通常被认为是快速和安全的，具有更高的便携性和低维护性。像MATLAB这样的应用程序使用Java来交互用户界面和作为核心系统的一部分。

## 参见

  - [比较Java和C++](https://zh.wikipedia.org/wiki/比较Java和C++ "wikilink")
  - [比较C Sharp和Java](https://zh.wikipedia.org/wiki/比较C_Sharp和Java "wikilink")
  - [Java元数据接口](https://zh.wikipedia.org/wiki/Java元数据接口 "wikilink")
  - [Java applet](../Page/Java_applet.md "wikilink")
  - [Java平臺](../Page/Java平臺.md "wikilink")
  - [Java RMI](https://zh.wikipedia.org/wiki/Java_RMI "wikilink")

## 註釋

## 參考文獻

### 引用

### 来源

  - Jon Byous, [*Java technology: The early years*](http://java.sun.com/features/1998/05/birthday.html)。Sun Developer Network, no date \[ca. 1998\]。Retrieved April 22, 2005.
  - [James Gosling](../Page/詹姆斯·高斯林.md "wikilink")，[*A brief history of the Green project*](https://web.archive.org/web/20070127143602/http://today.java.net/jag/old/green/)。Java.net, no date \[ca. Q1/1998\]。Retrieved April 22, 2005.
  - [James Gosling](../Page/詹姆斯·高斯林.md "wikilink")，[Bill Joy](../Page/比尔·乔伊.md "wikilink")，[Guy Steele](https://zh.wikipedia.org/wiki/Guy_L._Steele,_Jr. "wikilink")，and [Gilad Bracha](https://zh.wikipedia.org/wiki/Gilad_Bracha "wikilink")，*The Java language specification*, second edition. Addison-Wesley, 2000. ISBN 0-201-31008-2.
  - [James Gosling](../Page/詹姆斯·高斯林.md "wikilink")，[Bill Joy](../Page/比尔·乔伊.md "wikilink")，[Guy Steele](https://zh.wikipedia.org/wiki/Guy_L._Steele,_Jr. "wikilink")，and [Gilad Bracha](https://zh.wikipedia.org/wiki/Gilad_Bracha "wikilink")，*The Java language specification*, third edition. Addison-Wesley, 2005. ISBN 0-321-24678-0.
  - Tim Lindholm and Frank Yellin. *The Java Virtual Machine specification*, second edition. Addison-Wesley, 1999. ISBN 0-201-43294-3.
  - [蔡學鏞](https://zh.wikipedia.org/wiki/蔡學鏞 "wikilink")：{{〈}}從編譯器與VM角度分析Java2 v5.0語言的新特色{{〉}}

## 外部链接

{{-}}

[Category:过程式编程语言](https://zh.wikipedia.org/wiki/Category:过程式编程语言 "wikilink") [Category:编程典范](https://zh.wikipedia.org/wiki/Category:编程典范 "wikilink") [Category:面向对象的程序设计](https://zh.wikipedia.org/wiki/Category:面向对象的程序设计 "wikilink") [Category:Java](https://zh.wikipedia.org/wiki/Category:Java "wikilink") [Category:JVM程式語言](https://zh.wikipedia.org/wiki/Category:JVM程式語言 "wikilink")

1.
2.  [OpenJDK](http://openjdk.java.net/)
3.  [Statement by the ASF Board on our participation in the Java Community Process](https://blogs.apache.org/foundation/entry/statement_by_the_asf_board1)
4.
5.  [Java理論與實踐：再談Urban性能傳言](http://www-128.ibm.com/developerworks/cn/java/j-jtp09275.html)
6.
7.
8.  [Applications of Java Programming Language](https://www.invensis.net/blog/it/applications-java-programming-language/)
9.  [1](https://jelastic.com/blog/java-stacks-usage-statistics-2017/)