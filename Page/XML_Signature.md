**XML Signature**（也称作*XMLDsig*，*XML-DSig*，*XML-Sig*）是一个定义[数字签名的](../Page/數位簽章.md "wikilink")[XML](../Page/XML.md "wikilink")语法的[W3C推荐标准](../Page/W3C推荐标准.md "wikilink")。从功能上或，XML Signature与[PKCS](https://zh.wikipedia.org/wiki/公開金鑰密碼編譯標準 "wikilink")\#7有很多共同点，但是XML签名具有更好的可扩展性，并为签名XML文档做了调整。XML Signature在许多[Web技术](../Page/万维网.md "wikilink")，如[SOAP](https://zh.wikipedia.org/wiki/SOAP "wikilink"), [SAML等中使用](https://zh.wikipedia.org/wiki/SAML "wikilink")。

XML signature可以用来签名任何类型的数据（称作资源），最常见的是XML文档，但是任何可以通过[URL访问的资源都可以被签名](../Page/统一资源定位符.md "wikilink")。如果XML签名用于对包含该签名的XML文档之外的资源签名，则称为**detached** signature如果XML签名用于对包含它的XML文档的某个部分进行签名，则称为**enveloped** signature;如果XML签名包含被签名的数据，则称为**enveloping** signature。

## 结构

一个XML签名包含一个`Signature`元素，其名字空间为`http://www.w3.org/2000/09/xmldsig#`。基本结构如下所示：

``` xml
<Signature>
  <SignedInfo>
    <SignatureMethod />
    <CanonicalizationMethod />
    <Reference>
       <Transforms>
       <DigestMethod>
       <DigestValue>
    </Reference>
    <Reference />等
  </SignedInfo>
  <SignatureValue />
  <KeyInfo />
  <Object />
</Signature>
```

  - SignedInfo元素包含或引用签名后的数据，并指出使用了那种算法。
      - SignatureMethod和CanonicalizationMethod元素被SignatureValue元素所使用，并包含在SignedInfo元素中以防止篡改。
      - 一个或多个`Reference`元素通过URI引用的方式说明被签名的资源；以及在签名前对资源进行的任何转换。转换可以是一个XPath表达式，从文档树中选择一个子集\[1\]。
          - DigestMethod元素指定散列算法。
          - DigestValue元素包含转换后资源经过散列算法的结果。
  - SignatureValue元素包含一个经过[Base64](../Page/Base64.md "wikilink")编码的签名结果 - 签名是按照SignedInfo元素中的SignatureMethod元素中指明的参数进行的，签名前要先根据CanonicalizationMethod元素中指定的算法进行规范化。
  - KeyInfo元素（可选）允许签名者为接收者提供验签该签名的密钥，通常是以一个或多个[X.509](../Page/X.509.md "wikilink")数字证书的形式。如果没有出现KeyInfo元素，接收方必须从上下文中识别出验签的密钥。
  - Object元素（可选）包含被签名的数据，如果是*enveloping signature*（签名的数据在Signature元素内）的情况。

## 验证及安全考虑

当验证一个XML签名时，需要遵守一个称作核心验证（**Core Validation**）的程序：

1.  **引用验证：**每一个引用的摘要都通过获取相应的资源，并且按照指定的转换方法和摘要方法进行转换和摘要，然后将结果与DigestValue元素中的内容进行比较，如果不匹配，验证失败。
2.  **签名验证：**SignedInfo元素使用CanonicalizationMethod元素中指定的XML标准化方法进行处理，密钥或取自KeyInfo元素或通过其他方法取得，然后通过SignatureMethod指定的签名方法进行验签。

这一程序确定该资源是否是真的由宣称的当事人签名的。然而由于XML标准化和转换方法的可扩展性，验证方必须同时确认实际被签名或摘要的正式在原始数据中出现的内容，换句话说，确信签名或摘要所使用的算法没有改变被签名的数据的意思。

## XML规范化

XML签名的产生要比通常的数字签名的产生复杂一点，这有由于一个给定的XML文档（在XML开发人员通用的说法是"[XML信息集](../Page/XML信息集.md "wikilink")"）可能包含合法的序列化的表达方式以外的内容。例如，在XML元素中的白空格从句法上说是没有意义的，因此<Elem >和<Elem>没有区别。

由于数字签名是由[非对称密钥加密算法](../Page/公开密钥加密.md "wikilink")（通常是[RSA加密演算法](../Page/RSA加密演算法.md "wikilink")）对序列化的XML文档进行[散列](https://zh.wikipedia.org/wiki/密码散列算法 "wikilink")（通常是[SHA1](../Page/SHA家族.md "wikilink")）的结果进行加密。一个字节的差别会导致数字签名的不同。

此外，如果XML文档是在计算机间传输，不同操作系统的[換行](../Page/換行.md "wikilink")符可能不同，从CR到LF再到CR LF等。 对XML文档进行摘要和验证的程序可能随后以不同的方式呈现XML。例如，在元素定义的属性定义间添加额外的空格，或是使用相对的（而不是绝对的）URL，或者改变XML命名空间定义的顺序。标准化的XML对于引用远端文档的XML数字签名尤其重要，远端服务器可能会随时间改变XML呈现的方式。

为了避免这些问题，并保证逻辑上相同的XML文档会产生相同的数字签名，在对XML文档进行签名（在对SignedInfo进行签名时，规范化是强制的）时使用了一种XML规范化的转换（Canonicalization，通常缩写为**C14n**）这些算法保证逻辑上相同的文档产生完全相同的序列化的表达方式。

缺省的规范化算法处理命名空间生命的方式带来了另一个问题；通常来说一个被签名的XML文档需要嵌入另一个文档；在这种情形下，原来的规范化算法产生的结果与单独的文档规范化的结果不同。由于这个原因，一个被称为*Exclusive Canonicalization*的规范化算法产生了，该算法在序列化一个元素的[XML命名空间](../Page/XML命名空间.md "wikilink")声明时独立于该元素所嵌入的XML文档。

## 好处

与其他形式的数字签名，如[Pretty Good Privacy和](../Page/PGP.md "wikilink")[Cryptographic Message Syntax相比](https://zh.wikipedia.org/wiki/Cryptographic_Message_Syntax "wikilink")，XML Signature更加灵活，这是因为它操作的不是[二进制数据](https://zh.wikipedia.org/wiki/二进制文件 "wikilink")，而是[XML信息集](../Page/XML信息集.md "wikilink")，允许操作数据的子集，可以以不同形式将签名与被签名的信息结合，以及可以执行转换。另一个核心概念是标准化，也就是说仅对“精华”进行签名，而排除了无意义的区别，如白空格和换行符。

## 缺点

通常，批评都对准XML安全的体系结构\[2\]，以及在签名和加密XML数据前对XML进行规范化的适宜性，这是因为XML规范化的复杂性，内在的处理需求，以及性能不高的特性\[3\] \[4\] \[5\].争论在于执行XML标准化会导致额外的等待时间，这对事务的，性能敏感的[SOA应用来说简直难以克服](https://zh.wikipedia.org/wiki/面向服务的架构 "wikilink")。

这些问题正在[XML安全工作组](http://www.w3.org/2008/xmlsec/)进行解决。 \[6\] \[7\]

另一个问题是没有合适的策略，XML在SOAP中的使用和WS-Security可能导致容易受到攻击。\[8\]

## 参见

  - [Canonical XML](../Page/Canonical_XML.md "wikilink")
  - [XML Encryption](https://zh.wikipedia.org/wiki/XML_Encryption "wikilink")
  - [XAdES](https://zh.wikipedia.org/wiki/XAdES "wikilink"), extensions to XML-DSig for use with advanced electronic signature

## 参考文献

<references/>

## 外部链接

  - [XML-Signature Syntax and Processing (W3C)](http://www.w3.org/TR/xmldsig-core/)
  - [Canonical XML](http://www.w3.org/TR/2001/REC-xml-c14n-20010315)
  - [Exclusive XML Canonicalization](http://www.w3.org/TR/xml-exc-c14n/)
  - [Additional XML Security Uniform Resource Identifiers (URIs)](http://www.ietf.org/rfc/rfc4051.txt)

[Category:密码学](https://zh.wikipedia.org/wiki/Category:密码学 "wikilink") [Category:基于XML的标准](https://zh.wikipedia.org/wiki/Category:基于XML的标准 "wikilink")

1.  <http://www.w3.org/TR/xmldsig-filter2/> XML-Signature XPath Filter 2.0
2.  <http://www.cs.auckland.ac.nz/~pgut001/pubs/xmlsec.txt> Why XML Security is Broken
3.  <http://grids.ucs.indiana.edu/ptliupages/publications/WSSPerf.pdf> Performance of Web Services Security
4.  <http://www.extreme.indiana.edu/xgws/papers/sec-perf.pdf> Performance Comparison of Security Mechanisms for Grid Services
5.  <http://www.javaworld.com/javaworld/jw-01-2007/jw-01-vtd.html> Why XML canonicalization is bad for Web Services Security
6.  <http://www.w3.org/2007/xmlsec/ws/report.html> W3C Workshop on Next Steps for XML Signature and XML Encryption, 2007
7.  <http://www.w3.org/TR/xmlsec-reqs2/> XML Security 2.0 Requirements and Design Considerations
8.  <http://domino.research.ibm.com/library/cyberdig.nsf/papers/73053F26BFE5D1D385257067004CFD80/$File/rc23691.pdf>