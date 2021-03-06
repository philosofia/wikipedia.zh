> 本文内容由[XML Schema](https://zh.wikipedia.org/wiki/XML_Schema)转换而来。


**XSD (XML Schema Definition)**是[W3C于](https://zh.wikipedia.org/wiki/World_Wide_Web_Consortium "wikilink")2001年5月发布的推荐标准，指出如何形式描述XML文档的元素。XSD是許多[XML Schema 语言中的一支](../Page/XML_Schema_语言.md "wikilink")。XSD是首先分離於XML本身的schema語言，故取得W3C的推薦地位。

像所有[XML Schema 语言一樣](../Page/XML_Schema_语言.md "wikilink")，XSD用來描述一組规则──一个XML文件必須遵守这些規则，才能根據該schema『合法（Valid）』。

然而，与其他[XML Schema 语言不同](../Page/XML_Schema_语言.md "wikilink")，XSD意圖設計为在确认一个文档的有效性时，将会产生满足特定[数据类型的一个信息集合](https://zh.wikipedia.org/wiki/数据类型 "wikilink")。这种后验证的[XML信息集](../Page/XML信息集.md "wikilink")可用来開發XML文件處理軟件。

## XSD名称的来源

因為有其他XML schema 語言存在，故在引用這W3C建議的語言時，使用XML Schema或W3C XML Schema，Schema永遠字首大寫。

“XML Schema”在2001年5月成为W3C推荐标准。由于“XML Schema”作为一种W3C的推荐标准的名字与广义的[XML Schema 语言存在名称上的混淆](../Page/XML_Schema_语言.md "wikilink")，用户社区的一部分人采用了“WXS”来称呼它， 用户社区的另一部分人采用“**XSD**”（**X**ML **S**chema **D**efinition[首字母縮略字](../Page/首字母縮略字.md "wikilink")）来称呼它。W3C发布的1.1标准采用了“**XSD**”作为官方称呼。

## 歷史

在官方文档的參考附錄里，XSD标准承認受到\[文件类型描述|DTD\]\]和其他早期XML schema 语言的影响，如、、、以及。XSD從中吸收了一些特性，然而也在這些特性中有所折衷。這些早期schema 語言中的XDR與SOX在XML Schema發布後仍繼續使用了一段时间。不少[微軟的產品支援XDR直到](https://zh.wikipedia.org/wiki/微軟 "wikilink")2006年十二月[MSXML](../Page/MSXML.md "wikilink") 6.0的發佈（MSXML 6.0拋棄了XDR改用XSD）[1](http://msdn.microsoft.com/en-us/library/ms761410) 。支援它自己的SOX schema 語言直到該公司於2004年末破產。2004年十二月，[Novell Inc.購買了該公司](../Page/Novell.md "wikilink"),，包括那些與SOX相關的專利，據報導是盡力防止被某些不相關的、以打專利相關官司為生的公司剝削圖利[2](http://www.iht.com/articles/2005/05/02/business/novell.php) 。

著名的XSD建议的内容但在XML自己的DTD中不可用的特性是命名空间感知（namespace awareness）与数据类型。

2012年4月， XSD 1.1成为W3C推荐标准。[April 2012](http://www.w3.org/News/2012#entry-9412)

## Schema与schema文档

技术上说**schema**是元数据的一个抽象集合，包含一套**schema component**: 主要是元素与属性的声明、复杂与简单数据类型的定义。这些schema component通常是在处理一批**schema document**时被创建。schema文档包含着schema component的源语言定义。在日常使用中，一个schema文档常被称作一个schema。

Schema文档通过命名空间组织起来：所有的被命名的schema component属于一个目标命名空间；这个目标命名空间是schema文档作为整体的一个属性。schema文档可以包含进来（include）使用同一命名空间的其它schema文档，也可以导入（import）使用不同命名空间的schema文档。

当一个实例文档针对一个schema来验证有效性时（这一过程称为*assessment*），用来验证有效性的schema可以作为参数提供给验证器，也可以在实例文档中作为两种特殊属性之一直接提供：

  - `xsi:schemaLocation`
  - `xsi:noNamespaceSchemaLocation`.这种机制要求客户启动验证以充分相信这个文档，知道文档对正确的schema是有效的。

"xsi"是命名空间"[http://www.w3.org/2001/XMLSchema-instance"的传统前缀](http://www.w3.org/2001/XMLSchema-instance%22的传统前缀)。

XML Schema Documents通常有[文件扩展名](../Page/文件扩展名.md "wikilink")".xsd". XSD还没有专门的[互联网媒体类型](../Page/互联网媒体类型.md "wikilink")，因此按照 RFC 3023使用"application/xml"或"text/xml" .

## Schema component

主要的schema component有:

  - **元素声明**（Element declaration）, 定义了元素的性质。包括：元素名字、目标命名空间；一个非常重要的性质是元素的类型，它限制了元素包含哪些属性与子元素。在XSD 1.1标准中，可以根据属性的值来有条件定义元素类型。一个元素可以属于一个替换群（substitution group），如果元素E在元素H的替换群中，那么schema许可H出现的地方E都可以出现。元素可以有完整性（integrity）约束：唯一性（uniqueness）约束确定特定值在该元素为根的子树中是独一无二的；引用（referential）约束确定值必须匹配一些其它元素的标识符。元素声明可以是全局的或局部的，允许同一个名字被用于一个实例文档的不同部分的不相关的元素。
  - **属性声明**（Attribute declaration）,定义了属性的性质。包括：属性名字、目标命名空间，属性类型限制了属性可以取哪些值，也可以指出属性的缺省值或固定值（fixed value，即属性只能取这个值）。
  - **简单与复杂数据类型**（Simple and complex type）.详见下节
  - **模型群**（model group）与**属性群**（attribute group）定义。这实际上是宏（macro）：被命名的元素的群与属性的群，可在许多数据类型定义中被重用。
  - **属性使用**（attribute use）表示复杂数据类型与属性声明的关系，指出属性是必需的还是可选的，在什么时候使用这种数据类型。
  - **元素粒子**（element particle）类似于表示复杂类型与元素的关系，指出元素在上下文中出现的最大与最小次数。类似于元素粒子，内容模型可以包括**模型群粒子**，在语法上相当于非终结符：定义了允许的元素序列的选择与重复的单位。此外，**通配符粒子**表示了一套元素或元素序列。

其它更专门的schema component包括annotations, assertions, notations, 以及包含了schema整体信息的**schema component**.

## 数据类型

简单数据类型（simple type）包含了可以出现在元素或属性的文本值。这是XSD与DTD的最大区别。

XSD提供了一套19个基本数据类型：

  - `anyURI`
  - `base64Binary`
  - `boolean`
  - `date`
  - `dateTime`
  - `decimal`
  - `double`
  - `duration`
  - `float`
  - `hexBinary`
  - `gDay`
  - `gMonth`
  - `gMonthDay`
  - `gYear`
  - `gYearMonth`
  - `NOTATION`
  - `QName`
  - `string`
  - `time`).

可以从这些基本数据类型通过三种机制构建三种数据类型：

  - restriction (减少值集的范围),
  - list (允许一个值的序列),
  - union (允许从几个数据类型中选择值).

XSD规范定义了25个导出数据类型。用户可以在schema中进一步定义自己的导出类型。

Restriction机制包括指出最大最小值、[正则表达式](../Page/正则表达式.md "wikilink")、限制字符串的长度、限制十进制数的位数等。XSD 1.1又增加了assertions, 即通过一个\[XPath 2.0\]\]表达式给出任意约束的能力。

复杂数据类型描述了一个元素的许可内容。包括这个元素、属性、子元素的许可内容。复杂类型定义由一套属性使用与一个内容模型组成。内容模型可以是：

  - 只有元素的内容（element-only content）, 不允许有文本（但可以有空白符或者子元素可以有文本）;
  - 简单内容（simple content）, 允许有文本，不允许有子元素;
  - 空内容（empty content）, 文本与子元素都不被允许;
  - 混合内容（mixed content）, 文本与子元素都可以有.

复杂数据类型可以从别的复杂类型导出：

  - restriction方法，不允许基类型允许的一些元素、属性或者值
  - extension方法，允许额外的属性或元素出现。

XSD 1.1又增加了assertion方法来约束复杂类型, 即通过一个\[XPath 2.0\]\]表达式必须求值为真

## Schema 既验信息集（Post-Schema-Validation Infoset）

基于 Schema 的验证完成后，可以按照 Schema 所隐含的数据模型来表达文档的结构与内容。XML Schema 数据模型包括：

  - 词汇（元素与属性名称集）
  - 内容模型（关联与结构）
  - 数据类型

这些信息的集合即为 Schema 既验信息集（Post-Schema-Validation Infoset （PSVI））。对于有效的 XML，PSVI 给它赋以特定的“类型”，从而便于以对象方式来处理整个文档，并应用面向对象程序设计（OOP）范式。

## XML Schema的次要用途

XML Schema的主要用途是形式描述XML文档，然而最终的schema除了简单验证文档外还有许多其他用途。

### 代码生成

Schema可用于生成代码，这称作{\[tsl|en|XML Data Binding}}。这些代码允许XML文档的内容作为编程环境中的对象。

### XML文件结构文档的生成

Schema可用于产生人可读的文档来描述一个XML文件的结构。这在作者利用了标记元素（annotation element）时非常有用。

## 批评

虽然XML Schema取得了广泛的成功应用，但也受到了大量严厉的批评，远超出其他W3C推荐标准。下述研究者很好地总结了这些批评：James Clark,\[1\] Anders Møller与Michael Schwartzbach,\[2\] Rick Jelliffe\[3\]，David Webber.\[4\]

一般问题:

  - 推荐标准数百页，语句非常技术化，对于非专业的用户来说过于复杂难读。很多人发现[W3Cs XML Schema Primer](http://www.w3.org/TR/xmlschema-0/)更易于理解.
  - XSD缺少形式化数学规范，这使得关于schema的自动推理很困难，例如证明一个修改过的schema是[向后兼容的](https://zh.wikipedia.org/wiki/向后兼容 "wikilink")。
  - 语言中有很多例外，如元素的限制（restriction）不同于属性的限制。

表达能力的实践限制:

  - XSD对无序内容提供了极少支持
  - XSD不能要求提供*root element* (因而要求额外的信息来验证即使最简单的文档).
  - 在描述*mixed content*, 没有任何方式约束字符内容(甚至没办法指定一个有效字符集).
  - *内容与属性声明不能依赖于元素或属性上下文* (这也是DTD的一个大问题).
  - *不是100%自描述* (上一点就是个例子), 即使有这样的初始设计需求.
  - *默认*不能被独立于声明被指定(这使其不能给出一族schema尽在默认值上不同);*元素默认*只能是字符数据(不包含markup).

技术问题:

  - 虽然从技术上遵从命名空间，但看起来并不追随命名空间的精神原则。(例如 "unqualified locals").
  - XSD 1.0不提供机制，使得一个属性的值或者存在依赖于另一个属性的值或存在(被称为*co-occurrence constraints*). XSD 1.1解决了这个问题.
  - XSD数据类型的范围非常随意.\[5\]
  - 验证与扩增(augmentation，增加类型信息与默认值)应该保持分离。

## 示范

一个Schema的简易示例，描述某个指定的国家，是这样的：

<xs:schema
  xmlns:xs="<nowiki>http://www.w3.org/2001/XMLSchema</nowiki>">
`   `<xs:element name="country" type="Country">
`     `<xs:complexType name="Country">
`      `<xs:sequence>
`       `<xs:element name="name" type="xs:string"/>
`       `<xs:element name="population" type="xs:decimal"/>
`      `</xs:sequence>
`     `</xs:complexType>
`   `</xs:element>
</xs:schema>

一份遵从这个视图的XML文件：

<country
  xmlns:xsi="<nowiki>http://www.w3.org/2001/XMLSchema-instance</nowiki>"
  xsi:noNamespaceSchemaLocation="country.xsd">
`  `<name>`France`</name>
`  `<population>`59.7`</population>
</country>

## 參見

  - [RELAX NG](https://zh.wikipedia.org/wiki/RELAX_NG "wikilink") - 另一種XML綱要語言（ISO國際標準）通常用在XML Schema資料型別上
  - [XML信息集](../Page/XML信息集.md "wikilink")

## 外部連結

  - [W3C香港辦事處的權威翻譯](https://web.archive.org/web/20070311115809/http://www.w3c.org.hk/glossary/?letter=X&search=letter)

  - [XML及SGML名詞英漢翻譯表（台灣）](http://xml.ascc.net/zh/utf-8/gloss.html)

  - W3C XML Schema規格：[入門](http://www.w3.org/TR/xmlschema-0/)，[結構](http://www.w3.org/TR/xmlschema-1/)，[資料集](http://www.w3.org/TR/xmlschema-2/)，and [其他](http://www.w3.org/XML/Schema)

  - [W3Schools XML Schema教學](https://web.archive.org/web/20060428025512/http://www.w3schools.com/schema/default.asp)

  - [W3School XML Schema教学](http://www.w3school.com.cn/schema/index.asp)

[Category:W3C標準](https://zh.wikipedia.org/wiki/Category:W3C標準 "wikilink") [Category:XML](https://zh.wikipedia.org/wiki/Category:XML "wikilink")

1.  [James Clark](https://zh.wikipedia.org/wiki/James_Clark_\(XML_expert\) "wikilink") summary of *XML Schema* criticisms, and promotion of [RELAX NG](https://zh.wikipedia.org/wiki/RELAX_NG "wikilink") as an alternative, <https://web.archive.org/web/20150316212413/http://www.imc.org/ietf-xml-use/mail-archive/msg00217.html>
2.  Anders Møller and Michael I. Schwartzbach presents "Problems with XML Schema", <http://cs.au.dk/~amoeller/XML/schemas/xmlschema-problems.html>
3.  [Rick Jelliffe](https://zh.wikipedia.org/wiki/Rick_Jelliffe "wikilink") critique in May 2009, <http://broadcast.oreilly.com/2009/05/w3c-please-put-xsd-11-on-hold.html>
4.  [David Webber](https://zh.wikipedia.org/wiki/David_Webber "wikilink") OASIS comparison and insights white paper from August 2008, <http://www.oasis-open.org/committees/download.php/29164/White%20Paper%20on%20CAM%20and%20XSD.pdf>
5.  This point is amplified by Uche Ogbuji [More on XML class warfare - O'Reilly ONLamp Blog](http://archive.oreilly.com/pub/post/more_on_xml_class_warfare.html)