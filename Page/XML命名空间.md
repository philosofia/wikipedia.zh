**XML命名空间**（**XML namespace**，也译作**XML名称空间**、**XML名字空间**）用于在一个XML文档中提供名字唯一的元素和属性。XML命名空间在[W3C推荐规范](https://zh.wikipedia.org/wiki/W3C "wikilink")[《Namespaces in XML》](http://www.w3.org/TR/REC-xml-names/)中定义。XML命名空间于1999年1月14日成为W3C的推荐规范。

W3C将XML命名空间定义为以[国际化资源标识符](https://zh.wikipedia.org/wiki/国际化资源标识符 "wikilink")（，[IRI](https://zh.wikipedia.org/wiki/IRI "wikilink")）引用为标识的元素名和属性名的集合。

## 使用命名空间的动机

一个XML文档可能包括来自多个XML词汇表的元素或属性，如果每一个词汇表指派一个[命名空间](../Page/命名空间.md "wikilink")，那么相同名字的元素或属性之间的名称冲突就可以解决。举一个简单的例子来说，在一个订单的XML文档中需要引用到客户和所购买的产品，**customer**元素和**product**元素可能都有一个叫做**id**的子元素。这时候要引用**id**元素会造成名称冲突，但是如果将两个**id**元素放到不同的命名空间中就会解决这个问题。

## 声明和引用命名空间

命名空间使用元素的属性来声明，比如：

    <nowiki>xmlns:xhtml="http://www.w3.org/1999/xhtml"</nowiki>

其中：

  - `xmlns`是使用专门用来声明命名空间的保留字，
  - xhtml是命名空间的前缀
  - <http://www.w3.org/1999/xhtml> 是命名空间的唯一标识符，是一个[IRI引用](https://zh.wikipedia.org/wiki/国际化资源标识符 "wikilink")，但通常是一个[统一资源标志符](../Page/统一资源标志符.md "wikilink")（URI）引用。

命名空间的声明就是将一个前缀与一个URI关联起来。

声明命名空间时，可以为命名空间定义前缀（见前例）。为命名空间定义前缀，而不直接使用命名空间的URI是因为URI为了唯一通常会很长，直接使用URI不但造成书写和阅读的不便，还会扰乱XML的语法。声明命名空间时，也可以不定义前缀。如：

    <nowiki>ns="http://www.w3.org/1999/xhtml"</nowiki>

未定义前缀的命名空间將被用作缺省的命名空间。

命名空间的URI仅仅是唯一的标识符，推荐规范不要求，也不建议通过其获取信息。XML解析器处理命名空间URI时，也仅仅将其作为字符串。例如，地址为<http://www.w3.org/1999/xhtml> 的文档并不包含任何代码，它仅仅为人类阅读者描述了[XHTML](../Page/XHTML.md "wikilink")命名空间。之所以采用URI（如"http://www.w3.org/1999/xhtml"）来标识命名空间是因与使用简单的字符串（如xhtml）相比，URI大大降低了命名空间重名的可能性。

XML文档中的元素名和属性名可以使用限定名或非限定名，限定名由命名空间的前缀和局部名组合而成，例如"xhtml:hr"。非限定名只有局部名，没有前缀。非限定名被认为属于缺省命名空间，如果缺省命名空间没有定义，则属于**无命名空间**。

在一个元素中声明的命名空间，在所有子元素中也有效，一种通常的做法是在XML文档的根元素声明所有命名空间。在子元素中声明的命名空间的前缀可以覆盖父元素中声明的前缀。W3C推荐规范Namespaces in XML 1.1允许取消命名空间的声明，如：

    <nowiki>xmlns:xhtml=""</nowiki>

## 命名空间的名称

虽然术语**命名空间的URI**被广泛使用，W3C推荐规范称之为**命名空间的名称**。规范并未强制规定命名空间的名称必须使用URI（即当解析器发现命名空间不是一个合法的[URI时应该拒绝该文档](../Page/统一资源标志符.md "wikilink")），实际上许多XML的解析器允许使用任何字符串。在推荐规范的1.1版，命名空间的名称变成了[国际化资源标识符](https://zh.wikipedia.org/wiki/国际化资源标识符 "wikilink")（IRI），IRI允许使用非ASCII码的字符，实际上，非ASCII码字符已经被几乎所有的XML软件所接受。但是**命名空间的URI**一词还在持续使用，在W3C和其他地方的许多规范中也有使用。

随着命名空间推荐规范的发布，在如何处理相对的URI问题上产生了激烈的争论，一方认为相对的URI应当简单地当作字符串处理，而另一方认为应该根据文档的基准URI将其转换为绝对的URI。\[1\]。W3C对这一争论的裁定是不赞成使用相对的URI的。\[2\].

命名空间的URI与HTTP协议没有任何正式的关系，然而HTTP协议形式的URL（例如*<http://www.w3.org/1999/xhtml>*）还是被广泛的用作命名空间的URI。规范并未说明如果这样的URL被**解引用**(dereference，也就是说，如果软件试图从该位置获取一个文档）会发生什么。在这个问题上存在着不同的看法，有些人认为应该在该位置放置一个[RDDL文档](https://zh.wikipedia.org/wiki/RDDL "wikilink")\[3\]。但是总的来说，用户应该假定命名空间的URI只是一个简单的名称，而非万维网上文档的地址。

## 命名空间宣言

当一个元素带有属性ns=""，该元素的默认命名空间和它的后代将恢复为“无命名空间”：那就是在任何命名空间里头都不被视为前缀名称。

## 参考文献

## 外部链接

  - [Namespaces in XML 1.0 (Second Edition)](http://www.w3.org/TR/REC-xml-names/)

  - [Namespaces in XML 1.1 (Second Edition)](http://www.w3.org/TR/2006/REC-xml-names11-20060816/)

  - [XML模式：了解命名空间](http://www.oracle.com/technetwork/cn/articles/srivastava-namespaces-098626-zhs.html)

  - [计划使用XML名称空间，第1部分](http://www.ibm.com/developerworks/cn/xml/x-nmspace/part1/)，[第2部分](http://www.ibm.com/developerworks/cn/xml/x-nmspace/part2/)

## 参见

  - [命名空间](../Page/命名空间.md "wikilink")
  - [XML](../Page/XML.md "wikilink")

{{-}}

[ja:Extensible Markup Language\#XML名前空間](https://zh.wikipedia.org/wiki/ja:Extensible_Markup_Language#XML名前空間 "wikilink")

[Category:XML](https://zh.wikipedia.org/wiki/Category:XML "wikilink")

1.
2.
3.