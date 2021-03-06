> 本文内容由[Object Windows Library](https://zh.wikipedia.org/wiki/Object_Windows_Library)转换而来。


**Object Windows Library**（簡稱**OWL**），是一個[Borland C++對應於原生WinAPI的物件導向的framework設計](../Page/Borland_C++.md "wikilink")。它被使用在[Turbo Pascal](../Page/Turbo_Pascal.md "wikilink") for Windows，[Borland Pascal與](https://zh.wikipedia.org/wiki/Borland_Pascal "wikilink")[Borland C++的套件中](../Page/Borland_C++.md "wikilink")。由Borland公司在[Turbo Pascal](../Page/Turbo_Pascal.md "wikilink") for Windows時所推出，可自動完成許多由設計者自行撰寫的程式碼，他的竸爭對手是Microsoft Foundation Class Library（[MFC](https://zh.wikipedia.org/wiki/MFC "wikilink")）。其後繼者為VCL。

## 歷史

早在1990年代，Borland在C++的市場上耕耘已久，1991年推出的Borland C++ 3.0，縱橫C++編譯器市場十餘年，廣受歡迎。

1992年Borland買下[White Water的C](https://zh.wikipedia.org/wiki/White_Water "wikilink")++ Framework，改名為Object Window Library（OWL），並且推出以OWL 1.0為核心的Borland C/C++ 3.1。

1993年，Borland推出Borland C++ 2.0 for OS/2內附有OWL 2.0. OWL 2.0使用BIDS。

1994年，Borland急於推出Borland C++ 4.0 for Windows內含OWL 2.0.增加了Doc/View support, VBX controls, OLE等功能。Borland C++ 4.0不是穩定的版本，容易當掉，使微軟的Visual C++ 1.0趁機拿下大量的市場。

1995年，Borland C++ 4.5 with OWL 2.5趕在Windows 95之前推出。4.51版和 4.52版緊接著修正與Windows 95不相容之處。OWL 2.5，為了完整支援OLE，OWL 2.5同時包含了Object Component Framework（OCF）。Object Component Framework是功能強大的Framework，但與之前OWL不相容，使得舊有的使用者無法適從。最後倒向微軟的Visual C++陣營，種下了日後市場萎縮的遠因。1995年Microsoft同時推出Windows 95與Visual Studio 4.0，在某些程度上扭轉了C++ compiler以來的逆勢，奪取超過50%的市場佔有率。

1996年，Borland推出Borland C++ 5 for Windows，內含有OWL 5. 1997年8月Borland C++ 5.02的推出小小修正了OWL 5.

1999年，Borland停止銷售Borland C++ 5.02 and OWL。

雖然Borland放棄了OWL，但有一個群組仍繼續發展，[OWLNExt](http://owlnext.sourceforge.net)存放有許多OWL的原始碼。

2007年Borland/Codegear推出的Borland C++ Builder 2007內含OWLNext的CD，內有VCL/OWL可支援Vista.

## 風格

OWL支援單一／多文件介面（Single/Multiple Document Interface（SDI/MDI）），還有文件與視覺文件模式（Doc & View Document Model），拖曳（Drag\&Drop），列表（print）以及預覽列印（print-preview），還有GDI, Windows Help (Winhelp), MAPI, Internet (OwlSock/WinSock), OLE 1.0和OLE 2.0。

OWL是由類別所組成的架構，其類別名稱都是T當成前置詞，例如：TApplication, TWindow, TFrameWindow, TDialog, TBitmap等。VCL可使用相同的T前置詞，但是VCL的根類別（root class）只有一個TObject，而OWL有許多的根類別。本質上，OWL使用多重繼承。TWindow是OWL最常用的類別，它多重繼承自TFrameWindow, TDecoratedFrameWindow, TDialog, TInputDialog, TFileOpenDialog等類別，也包含了TEdit, TStatic, TButton, TGlyphButton, TComboBox等類別。

## 版本

| Product version              | OWL version  |
| ---------------------------- | ------------ |
| Borland C/C++ 3.1            | OWL 1.0      |
| Borland C/C++ 2.0 for OS/2   | OWL 2.0      |
| Borland C++ 4.0x             | OWL 2.0      |
| Borland C++ 4.5x             | OWL 2.5      |
| Borland C++ 5.0x             | OWL 5.0      |
| Borland C++ 5.0x Japanese    | OWL 5.0      |
| Borland C++ Builder 4.0      | OWL 5.0      |
| Borland C++ Builder 5.0      | OWL 5.0      |
| Borland C++ Builder 2007     | OWLNext 6.20 |
| Turbo Pascal for Windows 1.0 |              |
| Turbo Pascal for Windows 1.5 |              |
|                              |              |

## 參考書目

1.
## 外部連結

  - [Downloadable OWL source from CodeGear](http://cc.codegear.com/partners/bcb5/exclusive/object_windows_library/index.html)
  - [Download OWLNext 6.20 full install from Codegear](http://cc.codegear.com/partners/cppbuilder2007/owlnext/owlnext/index.html)

[Category:C++](https://zh.wikipedia.org/wiki/Category:C++ "wikilink")