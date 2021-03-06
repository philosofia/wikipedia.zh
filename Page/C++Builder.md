> 本文内容由[C++Builder](https://zh.wikipedia.org/wiki/C++Builder)转换而来。


**C++Builder** 是一個用於在Windows平台上撰寫[C++](../Page/C++.md "wikilink")語言應用程式的快速化程式開發（[RAD](https://zh.wikipedia.org/wiki/RAD "wikilink")，Rapid Application Development）的整合開發環境（[IDE](https://zh.wikipedia.org/wiki/IDE "wikilink")，Integrated Development Environment），原係由[Borland](../Page/Borland.md "wikilink")公司所開發銷售，現在此產品則歸屬於Embarcadero Technologies旗下的子公司Codegear。

C++Builder把由[Delphi](../Page/Delphi.md "wikilink")開發出來的IDE和[VCL](https://zh.wikipedia.org/wiki/VCL "wikilink")（Visual Component Library）與C++[編譯器](../Page/編譯器.md "wikilink")結合。此系列產品的開發週期通常是先在Delphi上作重要的改進，然後再用到C++Builder上。在Delphi上所開發的主要元件通常無須修改就可以給C++Builder使用，但C++ Builder的元件卻不一定能給Delphi使用。

C++Builder的開發環境中包含了[所見即所得](https://zh.wikipedia.org/wiki/所見即所得 "wikilink")（WYSIWYG）的圖形使用者介面（[GUI](https://zh.wikipedia.org/wiki/GUI "wikilink")）設計工具，是最早導入簡易的、真正可以用拖拉方式進行軟體開發的程式設計工具之一。

## 版本

| 發佈時間       | 版本                                                   | 發佈公司                                              | 執行環境                        |
| ---------- | ---------------------------------------------------- | ------------------------------------------------- | --------------------------- |
| 1997年      | 1                                                    | Borland International, Inc.                       | Windows                     |
| 1998年      | 3                                                    | Borland International, Inc.                       | Windows                     |
| 1999年      | 4                                                    | Inprise Corporation                               | Windows                     |
| 2000年      | 5                                                    | Inprise Corporation, Borland Software Corporation | Windows                     |
| 2002年      | 6                                                    | Borland Software Corporation                      | Windows                     |
| 2003年      | X                                                    | Borland Software Corporation                      | Windows, Linux, Solaris     |
| 2005年      | 2006 (10)                                            | Borland Software Corporation, CodeGear            | Windows                     |
| 2007年      | 2007 (11)                                            | CodeGear                                          | Windows                     |
| 2008年8月    | 2009 (12)                                            | Embarcadero Technologies                          | Windows                     |
| 2009年8月24日 | RAD Studio 2010 (14)                                 | Embarcadero Technologies                          | Windows                     |
| 2010年8月30日 | RAD Studio XE (15)                                   | Embarcadero Technologies                          | Windows                     |
| 2011年8月31日 | RAD Studio XE2 (16)                                  | Embarcadero Technologies                          | Windows, OS X               |
| 2012年9月4日  | RAD Studio XE3 (17)                                  | Embarcadero Technologies                          | Windows, OS X               |
| 2013年4月22日 | RAD Studio XE4 (18)                                  | Embarcadero Technologies                          | Windows, OS X               |
| 2013年9月11日 | RAD Studio XE5 (19)                                  | Embarcadero Technologies                          | Windows, OS X               |
| 2014-4-15  | RAD Studio XE6 (20)                                  | Embarcadero Technologies                          | Windows, OS X, iOS, Android |
| 2014-9-2   | RAD Studio XE7 (21)                                  | Embarcadero Technologies                          | Windows, OS X, iOS, Android |
| 2015-4-7   | RAD Studio XE8 (22)                                  | Embarcadero Technologies                          | Windows, OS X, iOS, Android |
| 2015-8-31  | RAD Studio 10 Seattle (23)                           | Embarcadero Technologies                          | Windows, OS X, iOS, Android |
| 2016-4-20  | RAD Studio 10.1 Berlin (24 incl. Delphi, C++Builder) | Embarcadero Technologies                          | Windows, OS X, iOS, Android |
| 2017-3-22  | RAD Studio 10.2 Tokyo (25)                           | Embarcadero Technologies                          | Windows, OS X, iOS, Android |
| 2018-7-18  | RAD Studio 10.2.3 Tokyo release 3 Build 3231(25)     | Embarcadero Technologies                          | Windows, OS X, iOS, Android |

## 兼容性

Windows操作系统中由Microsoft编译器生成的.obj与.lib文件不能直接用于C++Builder. 需要用C++Builder自带的工具软件转换：

`  coff2omf.exe -lib:st oldFormat.lib newFormat.lib`

## 设置

  - 设置编辑器的字体：Tools-\>Options-\>Editor Options-\>Display-\>Editor font

## 常用类体系

  - 字符串类，实际上是指向对象的指针。对象包含32比特的长度域、32比特的引用计数、16比特的数据长度域（即每个字符的字节数表示）、16比特代码页以及数据存储域。其中AnsiString是窄字符，String、UnicodeString、WideString都是宽字符。String即UnicodeString。UnicodeString内部采用了Windows操作系统的UTF16LE，赋值兼容于其他字符串类型。采取了堆上的动态分配，引用计数，更新前拷贝(copy-on-write)技术，长度没有限制。注意，采用了基于Delphi的基于1的下标索引，而不是C语言的基于0的下标索引。WideString兼容于COM的BSTR类型，不引用计数。
      - 其他类型与AnsiString相互转化的库函数：BoolToStr、StrToBool、IntToStr、StrToFloat、FloatToStr、FloatToStrF带四舍五入、FormatFloat带格式转为字符串、StringToColor、等等。
      - 类成员函数，通常不是作用于字串本身，而是返回新的字串：Delete删除子串、Insert插入子串、AnsiLastChar最后一个字符、SubString取子字符串、AnsiCompare比较、AnsiCompareIC比较不考虑大小写、Pos查字符串、AnsiPos、Length、SetLength（相当于left函数）、IsEmpty、LowerCase、UpperCase、TrimLeft、TrimRight、Trim、StringOfChar同字符重复输入、c_str获得内部的char\*指针、ToDouble、ToInt、ToIntDef、WideChar转换到一个宽字符数组、LastDelimiter
      - 类成员运算符：=、+=、+ 、==、\!+=、\<、\<=、\>、\>=
      - StringReplace字符串替换

## 相關

  - [Delphi](../Page/Delphi.md "wikilink")
  - [整合開發環境列表](../Page/整合開發環境列表.md "wikilink")

## 外部链接

  - [C++Builder](http://www.embarcadero.com/products/cbuilder)

[Category:集成开发环境](https://zh.wikipedia.org/wiki/Category:集成开发环境 "wikilink") [Category:C++編譯器](https://zh.wikipedia.org/wiki/Category:C++編譯器 "wikilink") [Category:图形用户界面设计器](https://zh.wikipedia.org/wiki/Category:图形用户界面设计器 "wikilink")