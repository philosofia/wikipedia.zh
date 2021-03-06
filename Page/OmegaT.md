**OmegaT**是一个使用[Java](../Page/Java.md "wikilink")编程语言编写的[计算机辅助翻译工具](https://zh.wikipedia.org/wiki/计算机辅助翻译 "wikilink")。它是[自由软件](../Page/自由软件.md "wikilink")，最初的开发由Keith Godfrey在2000年进行，目前的开发工作由Didier Briel带领的团队进行。**OmegaT**名称在德国是注册商标。

OmegaT适用于专业译员。它的功能包括使用[正则表达式](../Page/正则表达式.md "wikilink")的可自定义分段，带有模糊匹配和匹配传播的[翻譯記憶](../Page/翻譯記憶.md "wikilink")，术语库匹配，词典匹配和参考资料搜索以及使用[Hunspell](../Page/Hunspell.md "wikilink")拼写词典的内联拼写检查功能。

OmegaT可运行于[Linux](../Page/Linux.md "wikilink")、[Mac OS X和](https://zh.wikipedia.org/wiki/Mac_OS_X "wikilink")[Microsoft Windows](https://zh.wikipedia.org/wiki/Microsoft_Windows "wikilink") 98 SE或更高版本，\[1\]并且需要Java 1.5。它的界面和文档被翻译成27种语言。在2010年对458名专业译员的调查\[2\]表明，OmegaT的用户数达到[Wordfast](../Page/Wordfast.md "wikilink")、DejaVu和[MemoQ](../Page/MemoQ.md "wikilink")的1/3，且达到了市场领导者[塔多思](../Page/塔多思.md "wikilink")的1/8。在[Bing翻译的合作伙伴中](https://zh.wikipedia.org/wiki/Bing翻译 "wikilink")，OmegaT是其中唯一一个免费的专业级辅助翻译工具\[3\] 。

## 历史

OmegaT最初由Keith Godfrey开发于2000年。当时使用C++进行编写。

在2001年二月\[4\]首次公开发布的版本使用Java写成。在这个版本中使用专有翻译记忆库格式。它能翻译无格式的[纯文本文件](https://zh.wikipedia.org/wiki/Plain_text "wikilink")、HTML以及执行块级别的分割规则（即分割成段落而不是句子）。

## 开发和软件的发布

OmegaT的开发托管在SourceForge。开发团队由Didier Briel领导。和许多开源项目一样，新版本的OmegaT会频繁发布，通常每个新版本含有2-3个错误修改和功能升级。这个指的是“标准”版本，其中总是含有完整的用户手册和包含一些还未写入用户手册的功能的“最新”版本。\[5\]可以从Sourceforge的代码版本库的更新源进行更新。\[6\]

## OmegaT的工作原理

对于每个翻译任务，OmegaT会创建包含指定文件的项目文件夹的集合。用户把未翻译文档复制到其中的/source/子文件夹，而在翻译结束后，已翻译的文档会出现在/target/子文件夹中。OmegaT会在编辑窗格的片段中显示已分段的源文档的可翻译内容供用户翻译。

在开始翻译前，用户还可以复制以前的翻译记忆到/tm/子文件夹，复制术语库到/glossary/文件夹以及复制StarDict词典到/dictionary/文件夹，在翻译时OmegaT会自动查阅它们。

进行翻译时，OmegaT会自动检查以前的翻译以寻找类似的句子，找到后会显示在模糊匹配窗格中。译员可以使用快捷键把模糊匹配插入到编辑窗格。OmegaT还会查阅用户预先添加到项目文件夹的术语库和词典。如果启用了机器翻译，例如谷歌翻译，那么它会显示在单独的机器翻译窗格。

翻译结束后，OmegaT会创建已翻译的文件，并导出项目当前的翻译到TMX文件中，这样这些文件可以在以后翻译时重用或者和其他使用OmegaT或其他CAT工具的译员进行交换。

## OmegaT的功能

OmegaT拥有主流CAT工具具有的许多功能。包括创建，导入和导出翻译记忆，使用翻译记忆进行模糊匹配，查询术语表、索引定位和一致性搜索。

OmegaT还拥有其他CAT工具不具有的功能，包括：

  - OmegaT可以同时翻译不同文件格式的多个文件，且查阅多个翻译记忆、术语表和词典（只受计算机可用内存的限制）。
  - 通过支持的文件类型，OmegaT允许用户自定义文件扩展名和文件编码。对于一些文档类型，用户还可以有选择地翻译哪些元素（例如对于OpenOffice.org Writer文件，可选择是否翻译书签；对于Microsoft Office 2007/2010 文件，可选择是否翻译脚注；而对于HTML，可选择是否翻译图像的ALT文本）。用户还可以选择如何处理第三方翻译记忆中的非标准元素。
  - OmegaT的片段分割规则基于正则表达式。可以配置片段分割规则基于语言或文件格式，而连续的片段分割规则继承彼此的值。
  - 在编辑窗口，用户可以直接跳到下一个未翻译片段或在历史中前进以及后退。用户可以撤销和重做，复制和粘贴，以及用与高级文本编辑器相同的方式切换大小写状态。用户可以选择查看已翻译片段的源文本。编辑窗格还含有使用Hunspell词典的内联拼写检查功能以及使用鼠标进行交互地拼写检查。
  - 用户可以使用键盘快捷键或鼠标插入模糊匹配。OmegaT使用彩色显示模糊匹配的相似度。OmegaT还可以显示翻译了任意指定片段的日期、时间和用户名。匹配的术语可以用鼠标插入。用户可以选择把源文本复制到目标文本区域或自动插入最接近的模糊匹配。
  - 在搜索窗口，用户可以选择搜索当前文件的源文本，目标文本，其他翻译记忆和参考文件。搜索可以是区分大小写的，还可以使用正则表达式。双击搜索结果可以直接跳转到编辑窗口中的相应片段。
  - 翻译完成后，OmegaT可以执行标签检验以确保没有意外的标签错误。OmegaT可以在项目开始前统计项目文件和翻译记忆的状态，以及在翻译期间显示翻译任务的进度。
  - OmegaT可以从[Apertium](../Page/Apertium.md "wikilink")、[Belazar以及](https://zh.wikipedia.org/wiki/Belazar "wikilink")[Google翻译](../Page/Google翻译.md "wikilink")获取机器翻译并显示在单独的窗口中。
  - 在OmegaT用户界面中可以对各个窗口向周围移动、最大化、平铺、标签化和最小化。当OmegaT启动时会显示“快速入门指南”的简短向导。

## 支持的文档格式

OmegaT支持直接翻译多种文件类型。OmegaT根据文件扩展名来确定文件类型。可以自定义文件扩展名关联的处理方式和首选的编码来覆盖默认设置。

OmegaT把格式转换成标签来处理含格式的文档，类似于其他商业的CAT工具。

### 直接支持的格式

OmegaT可以直接翻译下列格式:

<table>
<thead>
<tr class="header">
<th><p>文件格式</p></th>
<th><p>文件扩展名模式</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>文档格式</p></td>
<td></td>
</tr>
<tr class="even">
<td><p>使用任意 Java 可处理的编码（包括<a href="https://zh.wikipedia.org/wiki/Unicode" title="wikilink">Unicode</a>）的文本<br />
所有纯文本派生格式，如 <a href="../Page/DokuWiki.md" title="wikilink">DokuWiki</a>, <a href="../Page/MediaWiki.md" title="wikilink">MediaWiki</a> 和 <a href="https://zh.wikipedia.org/wiki/Markdown" title="wikilink">Markdown</a></p></td>
<td><p>.txt, .txt1, .txt2, .utf8, .md</p></td>
</tr>
<tr class="odd">
<td><p><a href="../Page/HTML.md" title="wikilink">HTML</a>/<a href="../Page/XHTML.md" title="wikilink">XHTML</a></p></td>
<td><p>.html, .htm, .xhtml, .xht</p></td>
</tr>
<tr class="even">
<td><p><a href="../Page/开放文档格式.md" title="wikilink">OpenDocument</a> (ODF)，[7]用于<a href="https://zh.wikipedia.org/wiki/LibreOffice" title="wikilink">LibreOffice</a>、<a href="https://zh.wikipedia.org/wiki/Oracle_Open_Office" title="wikilink">StarOffice</a>、<a href="https://zh.wikipedia.org/wiki/OpenOffice" title="wikilink">OpenOffice</a></p></td>
<td><p>.sx?, .st?, .od?, .ot?</p></td>
</tr>
<tr class="odd">
<td><p>Microsoft <a href="https://zh.wikipedia.org/wiki/OOXML" title="wikilink">OOXML</a></p></td>
<td><p>.doc?, .xls?, .ppt?</p></td>
</tr>
<tr class="even">
<td><p>帮助和手册页</p></td>
<td><p>.xml, .hmxp</p></td>
</tr>
<tr class="odd">
<td><p>HTML 帮助编译器</p></td>
<td><p>.hhc, .hhk</p></td>
</tr>
<tr class="even">
<td><p>LaTeX</p></td>
<td><p>.tex, .latex</p></td>
</tr>
<tr class="odd">
<td><p>QuarkXPress CopyFlow Gold</p></td>
<td><p>.tag, .xtg</p></td>
</tr>
<tr class="even">
<td><p><a href="../Page/DocBook.md" title="wikilink">DocBook</a></p></td>
<td><p>.xml, .dbk</p></td>
</tr>
<tr class="odd">
<td><p>本地化资源格式</p></td>
<td></td>
</tr>
<tr class="even">
<td><p>Android 资源</p></td>
<td><p>.xml</p></td>
</tr>
<tr class="odd">
<td><p>Java properties</p></td>
<td><p>.properties</p></td>
</tr>
<tr class="even">
<td><p>Typo3 LocManager</p></td>
<td><p>.xml</p></td>
</tr>
<tr class="odd">
<td><p>Mozilla DTD</p></td>
<td><p>.dtd</p></td>
</tr>
<tr class="even">
<td><p>Windows 资源</p></td>
<td><p>.rc</p></td>
</tr>
<tr class="odd">
<td><p>WiX 本地化</p></td>
<td><p>.wxl</p></td>
</tr>
<tr class="even">
<td><p>ResX</p></td>
<td><p>.resx</p></td>
</tr>
<tr class="odd">
<td><p>有<code>Key=Value</code>结构的文件</p></td>
<td><p>.ini, .lng</p></td>
</tr>
<tr class="even">
<td><p>多语言本地化格式</p></td>
<td></td>
</tr>
<tr class="odd">
<td><p><a href="../Page/XLIFF.md" title="wikilink">XLIFF</a></p></td>
<td><p>.xlf, .sdlxliff</p></td>
</tr>
<tr class="even">
<td><p><a href="../Page/Gettext.md" title="wikilink">Portable Object</a> (PO)</p></td>
<td><p>.po, .pot</p></td>
</tr>
<tr class="odd">
<td><p>其他格式</p></td>
<td></td>
</tr>
<tr class="even">
<td><p>SubRip 字幕</p></td>
<td><p>.srt</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://zh.wikipedia.org/wiki/SVG" title="wikilink">SVG</a> 矢量图</p></td>
<td><p>.svg</p></td>
</tr>
<tr class="even">
<td></td>
<td></td>
</tr>
</tbody>
</table>

值得注意的是，OmegaT 还提供 [MediaWiki](../Page/MediaWiki.md "wikilink") 导入功能。

### 间接支持的格式

有两种方式让OmegaT处理不支持的格式：

  - 把这种格式的文件扩展名注册到首选的文件过滤器 （通常是带格式的纯文本）
      - 在这之后可以使用分段设定正则表达式来优化结果
  - 把这种格式转换为直接支持的格式

#### 对于XLIFF的支持

[Okapi Framework中的Rainbow程序可以把某些文件格式转换成OmegaT支持的XLIFF格式](../Page/Okapi_Framework.md "wikilink")。Rainbow还可以从这类文档中创建完整的OmegaT项目文件夹，便于OmegaT的处理。\[8\]

#### 对于Gettext PO的支持

一些文件格式可以转换为能在OmegaT中翻译的Gettext Portable Object (PO) 文件。Debian Linux 中的po4a程序可以把类似[LaTeX](https://zh.wikipedia.org/wiki/LaTeX "wikilink")、[TeX](../Page/TeX.md "wikilink")以及[POD的格式转换为Gettext](https://zh.wikipedia.org/wiki/Plain_Old_Documentation "wikilink") PO。\[9\][Translate Toolkit可以把Mozilla](../Page/Translate_Toolkit.md "wikilink") .properties 和dtd文件、CSV 文件、某些Qt .ts文件以及某些XLIFF文件转换为Gettext PO。

#### 对于Office Open XML和ODF的支持

从版本97到2003的Microsoft Word、Excel以及PowerPoint文档可以转换为Office Open XML (Microsoft Office 2007/2010)或ODF (OpenOffice.org)格式。这种转换过程并不是无损的，可能导致某些格式的丢失。

#### 对于Trados® .ttx文件的支持

Trados® .ttx可以使用[Okapi TTX Filter](http://www.opentag.com/okapi/wiki/index.php?title=TTX_Filter)进行处理。

## 支持的翻译记忆和术语库格式

### TMX格式的翻译记忆

OmegaT的内部翻译记忆格式对用户不可见，但每次它自动保存翻译项目时，会自动把所有新增和更新的翻译单元都导出并添加到三个外部的TMX翻译记忆：一个原生的OmegaT TMX、一个级别1的TMX以及一个级别2的TMX。

  - 原生的TMX是为了用于OmegaT中的项目。
  - 级别1的TMX文件保留了文本信息，可以用在支持TMX级别1和2的CAT工具中。
  - 级别2的文件保留了文本信息和相应的内联标签信息，可用在支持TMX级别2的CAT工具中。

导出的级别2文件包含了封装在TMX标签中的OmegaT内部标签，这样的TMX文件可以在支持TMX级别2的CAT工具中生成匹配。在Trados和SDLX中测试通过。

OmegaT支持导入最高1.4b版本级别1和级别2的TMX文件。在OmegaT中导入级别2的文件会生成相同级别的匹配，因为OmegaT会把外部的TMX标签转换为TMX级别2的标签。对于由Transit创建的TMX文件测试又通过了。

### 术语库

对于术语库，OmegaT主要使用tab分隔的UTF-8编码且扩展名为.txt的纯文本文件。术语库文件的结构非常简单：首列包含源语言词语，第二列包含对应的目标语言词语，第三列（可省略）与词语相关的上下文注释等。文本编辑器中可以很容易创建这样的术语库。

还支持使用标准CSV格式的类似结构的文件，对于TBX文件同样如此。

## 社区用户的参与

### OmegaT项目

The OmegaT Project is a sort of “computer literacy” group that focus on translators' needs. Users are encouraged to contribute tools written by themselves in response to translators' needs which are not yet addressed by the main OmegaT program itself.\[10\]

### OmegaT的本地化

OmegaT的用户界面和文档已经被翻译为大约30种语言。志愿翻译人员可以翻译用户界面，“快速入门指南”简短向导或完整的用户手册（或者所有的三个部分）。所有的语言文件和用户手册的翻译都包含在标准的OmegaT发布程序中。

### 用户创建的程序

OmegaT用户社区的特色是对于OmegaT的不足之处经常提示用户创建实现那些功能的宏、脚本和程序，尽管有时某些功能后来会成为OmegaT自身的一部分。当OmegaT只能进行段落分割时，有用户创建了OpenOffice.org宏进行根据句子进行分割。当在OmegaT中自动平衡多个TM仍需合并TM时，有用户创建了TMX合并脚本。当OmegaT没有提供拼写检查支持时，有多个用户创建脚本或找到解决方案作为OmegaT的一部分用来在翻译过程中提供拼写检查功能。\[11\]

当前提供了某些功能且尚未内置于OmegaT的工具包括一个用于Trados TagEditor文件的转换程序，两个简单的对齐器，一个不工作的术语添加工具以及一个把标签视为占位符的工具。\[12\]

## 基于OmegaT构建的其他软件

### Autshumato translation suite

Autshumato套件包含CAT工具，双语对齐器，PDF提取器，TMX编辑器和基于抓取数据的公共TM。最终的版本将包含术语管理器和机器翻译程序。其中的CAT工具是以OmegaT为基础构建的，且需要OpenOffice.org才能运行。它的开发资金由南非政府的艺术和文化部门提供。\[13\]

### Benten

Benten是基于XLIFF的Eclipse。它使用OmegaT代码来处理翻译记忆匹配过程。它的部分开发资金由日本政府提供。\[14\]

### Boltran

Boltran是模仿OmegaT项目工作流程的基于网络的独立CAT工具。它基于开源的OmegaT构建，因此能翻译任何OmegaT可以翻译的内容，且含有与OmegaT几乎等同的术语管理和模糊匹配能力。目前，唯一公开的Boltran服务器是开发者的网站，但在理论上任何人都可以建立公开或私有的Boltran服务器。\[15\]

### OmegaT+

OmegaT+ 是在 2005 年从 OmegaT 的 1.4.5 版本派生而来的 CAT 工具。其工作方式类似于 OmegaT，同时开发了一些自己的功能，且使用了与 OmegaT 不兼容的项目格式\[16\]。在许多时候，这个名称容易让不了解的人误以为是 OmegaT 的增强版本，而**实际上 OmegaT+ 只是 OmegaT 1.4.5 的增强版本**，且从 2005 年至今 OmegaT 中已增加了大量功能增强和新特性。

## 用户评价

  - [OmegaT，一款免费又给力的翻译集成工具](https://archive.is/20140422143835/http://knewalker.com/?p=666)
  - [OmegaT这款开源的计算机辅助翻译软件如何？](http://www.zhihu.com/question/22738692/answer/22469887)

## 另请参阅

  - [翻譯記憶](../Page/翻譯記憶.md "wikilink")
  - [计算机辅助翻译](../Page/電腦輔助翻譯.md "wikilink")
  - [Office Open XML software](https://zh.wikipedia.org/wiki/Office_Open_XML_software "wikilink")
  - [可支援開放文件軟體列表](../Page/可支援開放文件軟體列表.md "wikilink")

## 参考

## 外部链接

  - [官方网站](http://omegat.org/)——其中英文页面内容通常较新

  - [SourceForge项目页面](http://sourceforge.net/projects/omegat)

  - [OmegaT 使用简介](http://www.iplaysoft.com/omegat.html)

  - [OmegaT 使用简介](http://www.openfoundry.org/index.php?option=com_content&task=view&id=1559&Itemid=144)

  - [Velior's blog about OmegaT](http://www.velior.ru/blog/en/tag/omegat/)——包含了众多 OmegaT 技巧、教程和辅助脚本等

### 用户组

  - [omegat@yahoogroups.com](http://groups.yahoo.com/group/omegat)——多语言用户邮件列表（无需订阅即可搜索存档）

[Category:电脑辅助翻译](https://zh.wikipedia.org/wiki/Category:电脑辅助翻译 "wikilink") [Category:翻譯軟體](https://zh.wikipedia.org/wiki/Category:翻譯軟體 "wikilink") [Category:用Java編程的自由軟體](https://zh.wikipedia.org/wiki/Category:用Java編程的自由軟體 "wikilink") [Category:軟體在地化工具](https://zh.wikipedia.org/wiki/Category:軟體在地化工具 "wikilink")

1.
2.  <http://www.translationtribulations.com/2010/07/results-of-june-translation-tools.html>
3.   Microsoft Translator Partners
4.
5.  [1](https://sourceforge.net/projects/omegat/files/) OmegaT's "standard" and "latest" versions
6.  [2](http://omegat.svn.sourceforge.net/viewvc/omegat/trunk/) The latest source files are always available from the Sourceforge code repository
7.  [Open Document Format for Office Applications](http://www.iso.org/iso/en/CatalogueDetailPage.CatalogueDetail?CSNUMBER=43485&scopelist=PROGRAMME) – ISO/IEC 26300:2006 format
8.  [Okapi Framework](http://okapi.sourceforge.net/Release/Shared/Help/tutorial_02.htm) – Text Extraction utility can create an OmegaT project folder tree
9.  [po4a](http://po4a.alioth.debian.org/)  – A conversion utility to and from the [Portable Object](../Page/Gettext.md "wikilink") format, perl application packaged under Debian
10. [OmegaT Getting Involved](http://www.omegat.org/en/involved.html)  – Translators are encouraged to write their own supplementary tools
11. <http://tech.groups.yahoo.com/group/OmegaT/files/>
12. <http://www.omegat.org/en/resources.html>
13. [Autshumato](http://autshumato.sourceforge.net/)
14. [Benten](http://sourceforge.jp/projects/benten/)
15. [Boltran](http://www.boltran.com/home.seam)
16. [OmegaT+](http://omegatplus.sourceforge.net/)