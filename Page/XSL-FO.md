> 本文内容由[XSL-FO](https://zh.wikipedia.org/wiki/XSL-FO)转换而来。


**XSL-FO**是**XSL Formatting Objects**的缩写，它是一种用于文档格式的[XML](../Page/XML.md "wikilink") [置标语言](../Page/置标语言.md "wikilink")。XSL-FO是[XSL的一部分](https://zh.wikipedia.org/wiki/XSL "wikilink")，而[XSL是一组定义XML数据转换与格式的](https://zh.wikipedia.org/wiki/XSL "wikilink")[W3C技术](https://zh.wikipedia.org/wiki/W3C "wikilink")。XSL的其他部分有[XSLT](../Page/XSLT.md "wikilink")与[XPath](../Page/XPath.md "wikilink")。截止到2006年12月12日，XSL-FO的最新版本是[v1.1](http://www.w3.org/TR/2006/REC-xsl11-20061205/)。

## XSL-FO基础

与其他的[HTML](../Page/HTML.md "wikilink")与[CSS组合不同](https://zh.wikipedia.org/wiki/CSS "wikilink")，XSL-FO是一种unified表示语言，它没有HTML中那样的置标语法格式，并且与CSS更改外部XML或者HMTL文档的缺省表示不同，XSL-FO将所有的文档数据保存在内部。

XSL-FO总的设计思想用户写到文档中的数据是XML语言的文档，而不是FO，所用语言可以是[XHTML](../Page/XHTML.md "wikilink")、[DocBook](../Page/DocBook.md "wikilink")以及[TEI或者其他任何的XML语言](https://zh.wikipedia.org/wiki/TEI "wikilink")。然后，用户自己写一个或者找一个[XSLT](../Page/XSLT.md "wikilink")变换，将XML转换成XSL-FO。

一旦生成了XSL-FO文档，就将它送到FO处理器这样的应用程序中。FO处理器将XSL-FO文档转换成可以阅读或者可以打印的格式。最常见的XSL-FO输出格式是[PDF或者](https://zh.wikipedia.org/wiki/PDF "wikilink")[PostScript](../Page/PostScript.md "wikilink")，有一些FO处理器只能输出成[RTF](../Page/RTF.md "wikilink")这样的格式或者只能输出到图形用户界面的页面序列及内容。

人们最初认为XSLT语言本身仅仅是为这个目的所用的，但是现在由于更加通用的XML转换的出现已经超出了这个范围。由于这个转换是一个必然的过程，因此人们也常常将XML转换为XSL-FO的XSLT当作XSL-FO文档本身。甚至是XSL-FO的教程也在FO处理用法也用XSLT命令表示。

XSLT转换过程功能非常强大，它可以自动生成内容的列表、参考链接、索引以及其他的结果。

XSL-FO文档与PDF或者PostScript文档不同，它没有充分地描述文本在不同页面上的布局，相反，它仅仅描述了页面外观以及不同内容放置的位置。根据这些，FO处理器依据FO文档中描述的边界确定文本的位置。XSL-FO规范甚至允许不同的FO处理器根据所生成的页面有不同的响应。

例如，有些FO处理器为了节约空间在换行的时候会加入连字符，有些却不会这样做。不同的处理器甚至会使用不同的连字符算法，从一些简单的算法到需要考虑前后行是否也许要连字符这样复杂的算法。这样就会在不同的页面改变页面布局，尤其是带有边框的时候更是这样。另外还有一些场合，XSL-FO规范明确允许FO处理器根据布局作出一定的选择。

虽然不同的FO处理器生成的结果并不一致，但是人们并不太关心。这是因为XSL-FO的目的是生成经过分页的可打印媒体。XSL-FO文档本身通常用于中介的媒体，通常用于生成[PDF文件或者作为最终要分发的打印文档](https://zh.wikipedia.org/wiki/PDF "wikilink")。这与HTML直接作为最终形式分发给用户有所不同。因此，如果需要生成一个打印文档，只需要选择满足需要的FO处理器，比如布局效果以及较少的空白等，而无需在不同的处理器上测试XSL-FO文档。

## XSL-FO语言的概念

XSL-FO语言的设计目的是用于分页媒体，采用的方式是类似于用于非分页媒体的HTML以及CSS。因此，页面是XSL-FO结构内在的一个概念，FO赋予了用户很大的权利以确定如何在页面上显示信息。

FO最适合用在“内容驱动”设计的场合，这是图书、文章、法律文档等排版所用的标准方法。这涉及到一行邻近的文本以及嵌入在页面边界中的不同变化信息。这与报纸与杂志中所用的“布局驱动”设计有所不同。在那些文档中，如果无法在特定的位置完整地放进去，那么就会对内容进行裁减。XLS-FO很难处理杂志布局的严格要求，实际上在很多场合，它根本不具备表示所需布局的能力。

尽管这种语言有这些设计局限，但是它仍然能够胜任很多的表现任务。它提供表格、列表、side floats等许多特性。这些特性与CSS的布局特性类似，但是其中一些特性需要用XSLT表示。

## XSL-FO文档结构

XSL-FO文档是XML文档，但是不必遵循[DTD或其模型规范](https://zh.wikipedia.org/wiki/DTD "wikilink")。相反，它们遵循XSL-FO规范中定义的语法。

XSL-FO文档包括两个必须部分。第一部分列出页面布局的细节，第二部分是带有置标的文档数据，根据不同的页面布局确定如何在不同的页面上摆放内容。

页面布局定义了页面的属性。可以定义文本的排列方向以满足不同语言的要求，定义页面的尺寸以及页面边界。更加重要的特点是，它可以定义页面的顺序从而允许偶数页与奇数页的布局不同。例如，用于打印的文档可以定义更大的边界；在需要装订的时候可以留出更大的边界。

文档数据部分是一系列的数据流组成的，每个数据流都附属于一个页面布局。数据流包括一系列的按顺序排列的数据块，每个部分一系列的文本数据、内嵌的置标元素或者是二者的组合。在文档边界上也可以加入页码、章节等类似内容。

数据块以及内嵌元素的功能非常类似于CSS，但是空白的填补与保留在FO与CSS之间有所不同。相对于页面方向的数据块及内嵌元素排列方向可以进行充分的定义，这样FO文档可以处理与英文排列方向不同的其他语言。FO规范的语言与CSS 2.1不同，使用开始与结束这样的呈方向中性的术语而不是左与右来表示方向。

XSL-FO的基本内容置标是从CSS及其层叠规则派生出来的，因此XSL-FO中的许多属性除非进行了显示重载否则就会延伸到子元素的部分。

## XSL-FO v1.0的功能

XSL-FO有许多处理文本布局的功能。除了上面介绍的一些之外，XSL-FO语言可以完成下面定义的功能。

### 多栏

一个页面可能需要多栏的布局，在这种情况下，数据块按照顺序从一栏排到下一栏。单个的数据块可以扩展到所有栏，在页面中生成文本的分隔。分隔符上面的数据连在一起，下面的也连在一起，但是上面的不能与下面的连在一起。

根据XSL-FO页面规范的特性，每个页面可能会有不同的分栏及栏宽，因此文本可以很容易地从每页3栏转到每页5栏或者每页1栏。

FO的所有特性都能在多栏页面的约束下正常工作。

### 列表

XSL-FO列表本质上就是两列并排排列的数据块。每个条目都由左侧或者一行开始方向的数据与右侧或者一行结束方向的数据块组成。从概念上来说左侧就是列表的编号或者标志。但是，也可以是术语表中列出的简单的字符串或者文本。右侧的数据就是所要的结果。这两块数据都可以在同一个数据列表条目中包含多个数据块。

通常XSL-FO列表的编号是XSLT或者其他生成XSL-FO文档的过程产生的。因此，编号列表通常在XSL-FO显式地进行编号。

### 分页控制

用户可以指定[Widow和](https://zh.wikipedia.org/wiki/Widow "wikilink")[Orphan的处理方式](../Page/寡行和孤行.md "wikilink")\[1\]。另外，用户可以指定一个文本块不被分割。例如，一个图片和图片的说明应在一起显示。FO处理器会尽力保证这些命令的实现。

<references />

### 脚注

用户可以在页面的底部创建脚注。在FO文档中，脚注就像其他文字一样，写在他被引用的地方，FO处理器会把它当作一个或多个文字块放在页面的底部。FO处理器保证，不论被引用的是什么，脚注都会和被引用的内容处在同一页中。只有在极个别的情况下，这样的处理会产生额外的空行。

### 表格

FO表格功能非常类似于HTML/CSS表格的功能。用户定义每个单元格的行，用户也可以定义每列的格式，如背景颜色等。另外，用户也可以将第一行定义为表格标题，并且可以有自己的格式。

可以精确地告诉FO处理器每列的宽度，也可以让用自动宽度匹配的方法分配宽度。

### 文本方向控制

FO有强大的文本方向控制能力。在一页中间可以设定另外一种不同的文本板块方向。这种文本板块的方向控制可以用于不同语言的方向，或者是仅仅用于排版目的。实际上这些板块可以包含从表格、列表、甚至是另外一个重新排列方向的文本板块等在内的所有数据块。

### 其他

  - 页码引用。在文本中可以引用包含特殊标记符的页面，FO处理器将在标记符出现的地方添加实际的页码。
  - 多种风格板块边框
  - 背景颜色与图像
  - 字体控制与大小，与CSS类似
  - 侧面浮动条
  - 其他内嵌元素

## XSL-FO v1.1的功能

与1.0版相比，XSL-FO 1.1版加入了许多新的功能。

### 多数据流及数据流映射

XSL-FO 1.0对于一页中文本的排列位置的要求相当严格，而1.1版大幅度地放宽了这些限制，允许文本数据流能够映射到一页中多个区域。这样就可以象报纸那样进行排版。

### 书签

许多用于XSL-FO处理器的输出格式，尤其是PDF格式都带有书签特性。这样就可以在一个独立的窗口中定义特定的字符串让用户选择。当用户选择之后，文档窗口就会立刻自动滚动到文档中的特定区域。

现在XSL-FO v1.1中增加了添加书签的能力，这样处理器就可以将书签传递给支持这种功能的格式。

### 索引

XSL-FO 1.1支持生成某些图书后面具有的索引功能，这是通过对FO文档中进行正确标记的元素进行索引所完成的。

## XSL-FO的优点

由于XSL-FO是一种XML语言，因此从任何的XML语言生成XSL-FO代码仅仅需要XSLT变换以及XSLT处理器。人们可以很容易地创作一个[TEI或者](https://zh.wikipedia.org/wiki/TEI "wikilink")[DocBook](../Page/DocBook.md "wikilink")格式的文档，然后将它转换成HTML用于网络浏览或者经过FO处理器转换成PDF用于打印。实际上，现在已经有许多用于这些目的的TEI以及DocBook XSLT转换工具。

另外，由于它是一种XML语言，尤其是由于它没有固定的语法或者文件类型定义，它可以保存所有类型的XML数据。最常见的数据有SVG图像，许多FO处理器都可以读取或者将它加入到文档中。

XSL-FO的另外一种优点是用法相当简单。这种语言大多数的功能都是基于CSS的工作，因此CSS用户对于那些基本的标记属性相当熟悉。相对于难于理解的[TeX](../Page/TeX.md "wikilink")这样的布局与排版来说，FO文档的特定部分将如何显示也显得很容易理解。

## XSL-FO的缺点

FO的主要缺点是对于它的支持不多。FO很难、或许没有一家能够具有与规范100%的兼容性。尽管规范已经出现了很多年，但是现实仍然是这样。通常这是由于缺少对于XSL-FO的需求而引起的。[TeX](../Page/TeX.md "wikilink")及其他类似产品已经在排版语言市场上占据了很长时间，大多数TeX用户都没有切换到XSL-FO的需求。

XSL-FO另外一个不太严重的缺点是将数据排列到页边的功能不够强大，控制类似数据的能力可能没有用户所想象的那样。

FO的另外一个问题是，尽管容易理解，但是如果手工生成这样的文档非常困难，并且非常繁琐。XSLT就是用来更加方便地生成XSL-FO文档的，因此没有使FO文档更加简练的推动力。这样带来的问题就是新手不仅要学习如何写FO文档的细节，而且要学习写XSLT变换。当然，如果不是从一个现有的用于标准文档格式的XSLT变换开始，这会变得很困难。

## 参见

  - [XML](../Page/XML.md "wikilink")
  - [XSL](https://zh.wikipedia.org/wiki/Extensible_Stylesheet_Language "wikilink")
  - [XSLT](https://zh.wikipedia.org/wiki/XSL_Transformations "wikilink")
  - [Cascading Style Sheets](https://zh.wikipedia.org/wiki/Cascading_Style_Sheets "wikilink")
  - [XHTML](../Page/XHTML.md "wikilink")

## 外部链接

  - [XSL-FO 1.0 Specification](http://www.w3.org/TR/xsl/)
  - [XSL-FO 1.1 Specification](http://www.w3.org/TR/xsl11/)
  - [What is XSL-FO?](http://www.xml.com/pub/a/2002/03/20/xsl-fo.html) on XML.com

{{-}}

[Category:置标语言](https://zh.wikipedia.org/wiki/Category:置标语言 "wikilink") [Category:页面描述语言](https://zh.wikipedia.org/wiki/Category:页面描述语言 "wikilink") [Category:基于XML的标准](https://zh.wikipedia.org/wiki/Category:基于XML的标准 "wikilink") [Category:W3C标准](https://zh.wikipedia.org/wiki/Category:W3C标准 "wikilink")

1.  Widow指一个段落的最后一行落到一个新页，成为新页的第一行；Orphan相反，指一个段落的第一行单独留在前一页，而本段的其他内容在后面一页。