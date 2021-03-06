**Gerber**是一种二维矢量图像文件格式。\[1\] 它是[印刷线路板行业软件中用于描述印刷线路板图像的标准格式](https://zh.wikipedia.org/wiki/印刷线路板 "wikilink")，例如：线路层，阻焊层，字符层，钻孔层等。\[2\]\[3\]\[4\]

Gerber格式最初是由Gerber系统公司开发。因[Ucamco](../Page/Ucamco.md "wikilink")公司其前身Barco公司收购了Gerber系统公司，Gerber格式现由Ucamco公司所有。\[5\]\[6\] Ucamco公司不断地更新Gerber规格说明书的版本。\[7\]\[8\]\[9\]

目前最新的Gerber文件格式规格是于2014年2月发布的J1版本，该版本增加了传达PCB元信息例如文件所代表层类型的属性。\[10\]最新的规格说明书可在 [Ucamco网站下载页面](http://www.ucamco.com/cn/guest/downloads)免费下载。\[11\]

Gerber格式有两个版本：

  - 扩展Gerber格式，或称RS-274X格式，目前被广泛使用。
  - 标准Gerber格式，或称RS-274D格式，已被弃用并被RS-274X格式所取代。\[12\]\[13\]

标准的文件扩展名是.GBR。\[14\]

## 使用

Gerber格式的应用之一是将PCB的设计数据从设计转换到生产。PCB通常由线路板设计人员使用专业的[电子设计自动化](https://zh.wikipedia.org/wiki/电子设计自动化 "wikilink")（EDA）或者[计算机辅助设计](../Page/计算机辅助设计.md "wikilink")（CAD）软件进行设计， \[15\]然后输出成Gerber格式文件。Gerber文件被送到PCB工厂，并被输入到[電腦輔助製造](https://zh.wikipedia.org/wiki/電腦輔助製造 "wikilink") CAM系统对设计信息进行转换，为PCB生产的每一道[工艺流程提供数据](https://zh.wikipedia.org/wiki/印刷電路板#製造印刷電路板 "wikilink")。Gerber文件亦被用作传输钻孔信息，然而因为历史原因，钻孔资料通常使用Excellon 格式。\[16\] \[17\]\[18\]

另一个应用是传输单个图像，CAM系统可输出Gerber文件为绘图机提供数据。

### 交换PCB设计信息

PCB设计是通过若干Gerber格式文件和其它格式文件进行描述。通常这些文件会被压缩成单个文档送到PCB工厂。 一个Gerber文件定义单个线路层图像或绿油层图像。但它并不标明该文件所代表的PCB层别。人们指明该文件功能属性所用的一个简单方法就是将其属性在文件名中清楚说明。然而一些设计人员使用模糊的文件名并记录在任意文本格式中。这意味着制造厂商必须通过浏览数据包中所有文档的内容查找所需的文件功能属性。有些情况下，设计人员甚至会滥用文件扩展名去标明层的功能属性，例如用.BOT而不是标准的扩展名表示底层。这时生产厂商必须打开文件以查明文件的格式。\[19\]

有时候设计人员使用笔画填充而不是用单个外形去定义pad。这种技术被称作笔画填充。笔画填充可以画出所需的图形但是会导致pad的形状和位置信息丢失。PCB制造厂商进行电测的时候需要pad的位置信息。当PCB制造厂商收到的Gerber文件是通过笔画填充时，他们需要花费大量的时间把pad从笔画填充恢复过来，这是一项非常耗时且易于出错的工作。\[20\]\[21\]\[22\]

钻孔资料可被视作一个图形。因此Gerber文件可以定义钻孔数据。然而因为历史原因，IPC-NC-349 或 Excellon格式更经常被用作钻孔格式，尽管使用不同另外的格式会经常导致对位不准的问题。

一个Gerber文件不包含网表数据。网表通常使用IPC标准IPC-D-356进行定义。\[23\]

设计人员通常会使用非正规的文本文档或图纸提供层的功能属性，板材叠层，部件以及元信息。\[24\] Ucamco建议使用IPC-2581子集提供该类非图形信息。\[25\]\[26\]

Ucamco于2013年12月发布了扩展Gerber格式的规格草案，增加了转移元信息的属性。Ucamco在将其正式加入规格说明书前，请求PCB界对此给予反馈意见。\[27\]

## RS-274X 扩展Gerber格式

RS-274X Gerber格式，又称扩展Gerber格式或X-Gerber，是一种二维矢量图形描述格式\[28\]

RS-274X是一种可读的[ASCII](../Page/ASCII.md "wikilink") 格式。\[29\]它由一系列的命令和坐标组成。组成图像的元素是在特定位置画好外形的线和flash。正性和负性图形对象可以合并使用。 以下是扩展Gerber文件格式的一个例子：

G04 Gerber X2 样板资料1的简单版本

`%TF.FileFunction,Copper,L4*%`
`%TF.Part,Single*%`
`%FSLAX35Y35*%`
`%MOMM*%`
`%TA.AperFunction,Conductor,NotC*%`
`%ADD10C,0.15000*%`
`%TA.AperFunction,ViaPad*%`
`%ADD11C,0.75000*%`
`%TA.AperFunction,ComponentPad*%`
`%ADD12C,1.60000*%`
`%ADD13C,1.70000*%`
`%SRX1Y1I0.00000J0.00000*%`
`G01*`
`G75*`
`%LPD*%`
`D10*`
`X7664999Y3689998D02*`
`X8394995D01*`
`X8439999Y3734999D01*`
`X9369999D01*`
`D11*`
`X7664999Y3689998D03*`
`X8359999Y1874998D03*`
`X9882998Y3650498D03*`
`D12*`
`X4602988Y7841488D03*`
`D13*`
`X10729976Y2062988D03*`
`X10983976D03*`
`X11237976D03*`
`M02*`

RS-274X文档包含了线路板各层图像的完整描述，具有线路板图形成像需要的所有元素，不需要外部文件。RS-274X格式可定义任意形状的Apterture。正极和负极的物件可以合并使用。铜皮或铜块不需要定义为填充图形。\[30\]\[31\]

RS-274X格式是描述线路板各层的完整，强大且清晰的标准格式。它可以被自动输入和处理。这使其非常适合快速安全的数据转换以及可靠的自动化工作流程。 此格式规格已经发布。\[32\]

## RS-274-D 标准Gerber格式

标准Gerber格式已被扩展Gerber格式所取代。RS-274-D 标准Gerber格式是电子工业协会（EIA）RS-274-D格式规格的子集，\[33\] 是用于控制多领域数控机床的数据格式。Gerber RS-274-D用于控制矢量光绘机，该机器是二维数控机床。

Gerber RS-274-D是包含了控制码及X,Y坐标的ASCII格式。\[34\] 以下是RS-274-D 格式的例子：

`D11*`
`X1785250Y2173980D02*`
`X1796650Y2177730D01*`
`X1785250Y2181480D01*`
`X1796650Y2184580D01*`
`D12*`
`X3421095Y1407208D03*`
`X1785250Y2173980D03*`
`M02*`

RS-274-D标准Gerber格式是在20世纪60，70年代设计出来，用于控制数控机床，例如矢量光绘机。矢量光绘机如今已经被镭射光绘机所取代。标准Gerber格式非常适合于矢量光绘机但是受当时的技术所限制。它适用于手工操作流程，不适合PCB设计及制造之间的全自动化数据转换。 Gerber RS-274-D本身不能描述图像信息。它不包含坐标单位及Aperture信息。（Aperture是物件的形状说明，类似于PDF文档的字体）光绘机操作人员需手工设定坐标单位。坐标单位保存在被称作Aperture文件或Wheel文件的自由格式文本文档中，供操作人员阅读。Wheel文件没有统一的标准格式。设计人员和光绘机操作人员必须根据实际情况对格式使用达成一致。因此标准Gerber格式是一个数控标准而不是一个图形定义标准。\[35\]\[36\]

标准Gerber格式只支持简单的图像操作。作为变通方法，设计人员通过使用大量的矢量填充外形的方法去创建图形。此方法被称作图形填充。尽管这种方法创建了所需的图形，但是因为原始外形信息的丢失，这种文件在PCB CAM系统中非常难以处理。\[37\]

RS-274-D格式已被弃用。\[38\]

## 历史

  - 1980年8月27日，作为EIA RS-274-D子集的Gerber格式第一版发布；Gerber Systems Corporation发表了绘图数据参考书\[39\]作为驱动其光绘机产品的规格。
  - 1986年，Gerber格式被扩展并加入对尺寸可变Aperture的支持，以绘制给定范围内任意尺寸的长方形和锥形线。该功能在实际应用中已不再使用。
  - 20世纪80年代，Gerber格式为其他光绘机生产商和PCB制造中的CAM系统所采用。这时，Gerber格式已成为行业标准格式。
  - 1991年4月26日，随着光栅扫描技术的实现，Gerber格式被扩展为支持多边形和大量参数，允许用户可动态地定义不同形状、尺寸的Aperture，铜皮及多边形，而不再需要使用“填充块”。这大量的扩展参数最初是20世纪90年代由Gerber公司在AT\&T的推动下设计开发的。\[40\]
  - 1994年8月16日，Gerber公司发表了最后版本的《Gerber格式指南》。
  - 1998年4月，Gerber系统公司被比利时Barco公司所合并。Barco公司的PCB部门即是如今的Ucamco（前身为Barco ETS）。
  - 1998年9月21日，Barco公司发表《RS-274X格式用户指南》。
  - 2010年2月，Gerber格式规格更新到版本F。
  - 2010年12月，Gerber格式规格更新到版本G。\[41\]
  - 2012年1月，Gerber格式规格更新到版本H。\[42\]
  - 2013年2月，Gerber格式规格更新到版本I1。<ref name="rev I1">

</ref>

  - 2013年4月，Gerber格式规格更新到版本I2。<ref name="rev I2">

</ref>

  - 2013年6月，Gerber格式规格更新到版本I3。
  - 2013年6月，关于扩展Gerber格式以增加属性的建议发布。\[43\]
  - 2013年11月，Gerber格式规格更新到I4版本。<ref name="rev I4">

</ref>

## 相关格式

多年来人们多次尝试用其它格式代替Gerber格式，以加入除层图像以外的其它信息，例如网络(netlist)和电子元件信息。\[44\]但可能因为这些格式过于复杂，它们都未被电子制造业所广泛接受。现在Gerber格式仍是应用最广泛的数据转换格式。\[45\]

  - [IPC](https://zh.wikipedia.org/wiki/IPC_\(electronics\) "wikilink")-D-350 C 《印刷线路板数字格式描述》发表于1989年。此规格于1992年被标准化成IEC 61182-1文档，后来在2001年被取消。此格式很少被使用。
  - [DXF](../Page/DXF.md "wikilink") 偶尔被使用。因为通常使用画线进行构图，PCB物件（线和盘）信息会丢失，从而使其在CAM中应用非常困难。
  - [PDF](https://zh.wikipedia.org/wiki/PDF "wikilink") 格式很少被使用。因为PCB物件（线和盘）信息会丢失而使其难以在实际中应用。
  - DPF 格式，来自Ucamco的一种CAM格式，目前最新版本为v7，偶尔被使用。
  - 电子设计交换格式, [EDIF](https://zh.wikipedia.org/wiki/EDIF "wikilink") ,很少被使用。
  - [ODB++格式](https://zh.wikipedia.org/wiki/ODB++ "wikilink")，来自Mentor Graphics公司的一种CAM格式。偶尔被使用，是流行的非Gerber格式。\[46\]
  - GenCAM: [IPC](https://zh.wikipedia.org/wiki/IPC_\(electronics\) "wikilink")-2511A《产品制造描述数据实施的通用要求和转换方法论》2000年版本，很少被使用。
  - GenCAM: [IPC](https://zh.wikipedia.org/wiki/IPC_\(electronics\) "wikilink")-2511B 《产品制造描述数据实施的通用要求和XML图表转换方法论》 2002年版本，很少被使用。
  - Offspring: [IPC](https://zh.wikipedia.org/wiki/IPC_\(electronics\) "wikilink")-2581《印刷线路板装配产品制造描述数据通用要求和转换方法论》 2004版本。很少被使用，但近年来受到更多的关注。\[47\]
  - STEP AP210: [ISO 10303](https://zh.wikipedia.org/wiki/ISO_10303 "wikilink")-210, 《电子装配互连和封装设计 》第一版本2001， 第二版本2008。
  - Fujiko: JPCA-EB02,\[48\]基于日本福冈大学Tomokage教授的研究的日本新标准，很少被使用。

## 参考文献

## 外部链接

[在線查看 Gerber圖型](https://gerber-viewer.ucamco.com)

[Gerber X2 视频](https://www.ucamco.com/cn/gerber/demo-1)

[Gerber文件格式规格及与文件格式相关的各种文档](http://www.ucamco.com/cn/guest/downloads)

[分類:圖形文件格式](https://zh.wikipedia.org/wiki/分類:圖形文件格式 "wikilink")

[Category:电子制造](https://zh.wikipedia.org/wiki/Category:电子制造 "wikilink")

1.
2.
3.
4.
5.
6.
7.
8.
9.
10.
11.
12.
13.
14.
15.
16.
17.
18.
19.
20.
21.
22.
23.
24. IPC-2524 PWB Fabrication Data Quality Rating System, February 1999.
25.
26.
27.
28.
29.
30.
31.
32.
33.
34.
35.
36.
37.
38.
39.
40.
41.
42.
43.
44.
45.
46.
47. [IPC-2581 Panel: A Spirited Discussion on PCB Data Transfer Formats](http://www.cadence.com/Community/blogs/ii/archive/2011/10/02/ipc-2581-panel-a-spirited-discussion-on-pcb-data-transfer-formats.aspx), Richard Goering, Cadence Design Systems blog, October 2, 2011
48.