> 本文内容由[Office Document Query](https://zh.wikipedia.org/wiki/Office_Document_Query)转换而来。


**Office Document Query**（缩写：ODQ）即通用流式文档查询语言。它是一种通用于不同文档格式的查询语言。

目前世界上流行的流式文档的标准格式有：[OOXML](../Page/Office_Open_XML.md "wikilink")、[ODF](../Page/开放文档格式.md "wikilink")、[UOF](../Page/统一办公文档格式.md "wikilink")。不同格式有着不同的访问接口。Office Document Query针对流式文档，在一定程度上屏蔽文档格式和版本的差异，提供统一的访问接口。

## 产生背景

网络上存在着大量非常有价值的文档，包括学术论文、数据资料、课件、简历等，它们大多以流式办公文档形式存在。这些文档质量较高、相关性强，并且垃圾信息较少。但由于流式文档格式种类繁多，且各自的文档模型差别较大，因此，尽管有人在互操作方面做了很多贡献，但文档格式间的互操作还是困难重重。这给开发者和普通用户都带来了不少的麻烦。
目前世界上流行的流式文档的标准格式有：[OOXML](../Page/Office_Open_XML.md "wikilink")、[ODF](../Page/开放文档格式.md "wikilink")、[UOF](../Page/统一办公文档格式.md "wikilink")。不同格式有着不同的访问接口。 其存在的问题有：

  - 访问接口不统一、数据兼容困难。
  - API与文档格式相关
  - 与编程语言相关
  - 二次开发困难

Open Document Query针对流式文档:

  - 屏蔽文档格式和版本的差异，提供统一的访问接口
  - 实现应用层和数据处理的分离
  - 与编程语言无关
  - 可嵌入到协议中远程访问文档，也可访问本地的文档
  - 简化二次开发

## 文档模型及语法扁平化处理 \[1\]

  -
### 通用文档模型

  - Office Document Query通用文档模型，提取三大主流办公文档格式的文档模型的共性，从用户角度入手，保留及更改部分节点。
  - 扁平化是管理学中经典的概念。

对于ODQ而言数据是个总谱包括文档元数据、文本、式样等。如果说使用API为的是获得丰富多样的功能支持，那么使用ODQ就是为了更直接地操作数据。既然总谱是数据，那么文档模型就必须围绕数据而建。ODQ文档模型的扁平化，就是要精简文档结构层数。通过认真分析用户需求，将普通用户最关心也是最常用的文档数据比如text、style等，从底层提高到更高的层次中，并且不限制它们在文档模型中出现的次数。也就是说以往被放置于底层的文档对象，有可能同时出现在除顶层节点之外的任意节点下。

### 语法扁平化处理

Office Document Query查询语法参考数据库查询语言SQL（Structured Query Language）。Office Document Query面对处在不同位置的文档数据，提供几种简单的通用结构来覆盖全部查询操作。Office Document Query语法分为GET、UPDATE、DELETE、INSERT这四大类，分别完成查询、修改、删除和插入的任务。Office Document Query按照英语的语法规则，采用关键字of来替换多线型结构中的箭头，联通各条线，形成一条数据通路。

## 常用语法

### 语法格式

GET 属性1,\[属性2,…\] | 式样1,\[式样2,…\] | 节点1 \[all|序号|范围\] FROM 节点\[all|序号|范围\] \[of节点\[all|序号|范围\] …\] of Document \[WHERE {属性1=值1,\[属性2=值2…\]|式样1=值1,\[式样2=值2\]…} \]

### 说明

GET子句：指明要查询的内容，包括三类：节点属性、节点式样和节点对象。 FROM子句：FROM关键字后面是路径表达式。 WHERE子句：Where子句中的谓词用于对结果进行过滤，只返回满足特定标准的节点或属性，多个条件之间可以用 and、or等谓词连接。

## 书写理由

Office Document Query为流式文档的查询提供了独特的见解与方法。

## 参考文献

  - [几种基于XML的流式文档访问方式分析](https://web.archive.org/web/20150923205052/http://www.cnki.net/KCMS/detail/detail.aspx?QueryID=0&CurRec=1&recid=&filename=SJSJ201404064&dbname=CJFD2014&dbcode=CJFQ&pr=&urlid=&yx=&uid=WEEvREcwSlJHSldSdnQ0TWhVdFhzTVl6R1VaQVVXMHhUUGdWUHQ3YmZBbjRXU3F1enJLNGtIRUJiZk9id1A5dzFBPT0%3D%249A4hF_YAuvQ5obgVAqNKPCYcEjKensW4IQMovwHtwkF4VYPoHbKxJw%21%21&v=MjU2NjdmWXVkbUZDdm1WTC9PTmlmWVpMRzRIOVhNcTQ5RFlJUjhlWDFMdXhZUzdEaDFUM3FUcldNMUZyQ1VSTCs%3D)

[Category:文件格式](https://zh.wikipedia.org/wiki/Category:文件格式 "wikilink")

1.