> 本文内容由[GObject](https://zh.wikipedia.org/wiki/GObject)转换而来。


[GObject_example.png](https://zh.wikipedia.org/wiki/File:GObject_example.png "fig:GObject_example.png")

**[GLib](../Page/GLib.md "wikilink")对象系统**，或者说**GObject**，是一个在[LGPL下发布的](https://zh.wikipedia.org/wiki/LGPL "wikilink")[自由](../Page/自由软件.md "wikilink")[软件库](https://zh.wikipedia.org/wiki/软件库 "wikilink")，它提供了一个轻便的[对象系统并支持透明的多语言互通](https://zh.wikipedia.org/wiki/对象系统 "wikilink")。GObject被设计为可以直接使用在[C程序中](https://zh.wikipedia.org/wiki/C语言 "wikilink")，也[封装至其他语言](https://zh.wikipedia.org/wiki/封装 "wikilink")。

## 历史

GObject仅依赖于[GLib](../Page/GLib.md "wikilink")和[libc](https://zh.wikipedia.org/wiki/libc "wikilink")。它是[GNOME](../Page/GNOME.md "wikilink")的基石并且在[GTK+](https://zh.wikipedia.org/wiki/GTK+ "wikilink")，[Pango](../Page/Pango.md "wikilink")，[Accessibility Toolkit和大多数](https://zh.wikipedia.org/wiki/Accessibility_Toolkit "wikilink")[GNOME](../Page/GNOME.md "wikilink")的高级库和应用程序中被广泛使用。在GTK+ 2.0之前，GObject代码是GTK+的一部分。（现在GObject这个名字已经不在GTK+中了──取代它的基本类型叫做`GtkObject`。）

由于对象系统适用的范围更广，较有一般性，所以在GTK+2.0发布时，对象系统被分离了出來，改放到了另一個函数库。GtkObject在Gtk演进的过程里，大部分与GUI不相关的部份都移到了GObject里，造就了新的共用基础类型GObject的诞生。从2002年3月11日（也就是GTK+ 2.0发布的日子）开始，GObject就一直以一个分离的函数库的形式存在。GObject函数库現在被许多非GUI的程式，像命令行应用程序、服务器应用程序等，所使用。

## 与GLib的关系

雖然GObject有屬於它自己的文件[1](https://web.archive.org/web/20070703165009/http://developer.gnome.org/doc/API/2.0/gobject/) 與獨立的函式庫，但原始碼卻是在Glib的源碼樹裡，並且與GLib一起發行。因此，GObject使用與GLib一樣的版本號碼，而且一般Linux Distro的作法也是把GObject包在GLib裡（舉例來說，Debian把GObject放在libglib2.0套件家族裡）。

## 類型系統

GObject框架的基層主要依靠泛型與動態型別，稱作GType。GType系統保留所有物件的執行時期描述以讓glue code能方便地與其他語言作連結。[類型系統](../Page/類型系統.md "wikilink")可以處理任何單一繼承的類別架構以及非類別的型別，如[不透明指標](https://zh.wikipedia.org/wiki/不透明指標 "wikilink")、字串跟各種長度的整數與浮點數。

[類型系統](../Page/類型系統.md "wikilink")知道如何複製、指派和釋放屬於任何已註冊類型的值。這對像整數這種不是[參考計數](https://zh.wikipedia.org/wiki/參考計數 "wikilink")（reference-counted）的型別來說是很瑣碎的事情，但是對於其他是參考計數的複雜物件來說，是必要的。當[類型系統](../Page/類型系統.md "wikilink")複製了一個參考計數的物件，它僅僅只是增加該物件的參考計數，對複製一個複雜、不是參考計數的物件時，則是以配置記憶體的方式建立副本。

這項基本的能力被實作在GValue，GValue是一個泛型容器的型別，裡面可以用來保存註冊在[類型系統](../Page/類型系統.md "wikilink")裡的型別的值。這樣的容器在與動態型別語言溝通時，特別地有用。

### 基礎類型

沒有任何關聯類別的類型被稱作非類別的。這些型別相當於根類別，也就是基礎類型，可以被其他類型繼承。

在GLib 2.9.2 [2](https://web.archive.org/web/20081010234322/http://developer.gnome.org/doc/API/2.0/gobject/gobject-Type-Information.html) 裡，非類別的內建基礎類型有：

  - 空類型，對應到C的void (G_TYPE_NONE）;
  - 對應到C的有號、無號char、int、long和64位元整數long long （G_TYPE_CHAR, G_TYPE_UCHAR, G_TYPE_INT, G_TYPE_UINT, G_TYPE_LONG, G_TYPE_ULONG, G_TYPE_INT64, and G_TYPE_UINT64）;
  - 布林類型（G_TYPE_BOOLEAN）;
  - 列舉型別和"旗標"型別，都對應到C的列舉類型，但後者只使用在位元欄位上（G_TYPE_ENUM and G_TYPE_FLAGS）;
  - 單精度與雙精度的[IEEE浮點數](../Page/IEEE_754.md "wikilink")，對應到C的float跟double(G_TYPE_FLOAT and G_TYPE_DOUBLE）;
  - 字串類型，對應到C的char \* (G_TYPE_STRING);
  - [不透明指標](https://zh.wikipedia.org/wiki/不透明指標 "wikilink")，對應到C的void \*（G_TYPE_POINTER）。

類別內建的基礎類型有：

  - GObject實體的基底類別類型，標準類別繼承樹的根（G_TYPE_OBJECT）
  - 基底介面類型，跟基底類別類型很相似，但卻是標準介面繼承樹的根（G_TYPE_INTERFACE）
  - 包裝了結構的類型，被用來包裝簡單的值物件或外來物件在參考計數的"盒子"裡（G_TYPE_BOXED）
  - "參數規格物件的類型，用在GObject裡作為描述物件屬性的[元數據](../Page/元数据.md "wikilink")（G_TYPE_PARAM）。

可以被系統自動實體化的類型被稱作可實體化（instantiable）。這些類型的一個重要特色就是實體的第一個位元組永遠包含一個指標，指向連結到該實體類型的類別結構（虛擬表格的表單）。為此，任何可被實體化的類型應該是類別。相對地，任何非類別類型（像整數或字串）必須是不可實體化。另外，大部分類別類型是可實體化的，但某些類型，像介面類型，就不是。

### 衍生類型

從內建GObject基礎類型衍生下來的，主要有四種類型：

  - 列舉類型和"旗標"類型:一般來說，列舉類型或旗標其實都是整數，以相對口語的單字來表示特定的數值，一般都作為物件屬性的類型。GLib提供了`glib-mkenums` [3](https://web.archive.org/web/20070812004020/http://developer.gnome.org/doc/API/2.0/gobject/glib-mkenums.html) 工具來自動化產生的過程，並產生必要的代碼。
    Boxed類型:有些資料結構很簡單，並不需要是一個類別。舉例來說，我們可能有個類別，裡面需要加個`background-color`屬性，他的值應該是某個結構的實體，所以代碼看起來像是這樣：`struct color { int r,g,b; }`。要避免繼承`GObject`的話，我們可以建立一個boxed類型來呈現這樣的結構，並且提供複製和釋放的處理函式給GType。GObject提供了簡便的方法，可以讓你為GLib資料類型作包裝。
    不透明的指標類型（Opaque pointer types）:有時候，物件既不需要複製也不需要作參考計數或釋放。這樣的物件在GObject裡，可以當作是不透明指標（`G_TYPE_POINTER`）。通常被用來參考到特定種類的物件。
    類別與介面類型: GObject應用程式裡的大部分類型都是類別，直接或間接地繼承自根類別：`GObject`。是的，GObject裡也可以使用類似[Java的介面](https://zh.wikipedia.org/wiki/Java_\(程式語言\) "wikilink")（interface），雖然很少被使用到。很少使用到的原因可能是因為介面是在GLib 2.4（在2004年3月16日釋出）才被加進去。[GIMP](../Page/GIMP.md "wikilink")就有使用到GObject的介面。

## 訊息系統

GObject訊息系統由兩個互補的部份所組成：closures與信號。

  - Closures:GObject closure是callback（回呼）的一般化版本。支援現存已經用C/C++或其他語言寫好的closure（當提供繫結時）。這允許以例如Python或Java等寫好的代碼被GObject closure調用。

<!-- end list -->

  - 信號:信號（Signal）是closure被調用的主要機制。物件向類型系統註冊信號listener，在給定的信號與給定的closure間指定對應關係。當註冊的信號被發出時，對應的closure就會被調用。在GTK+裡，所有內定的GUI事件（像滑鼠移動和鍵盤動作）都會為listeners產生GObject信號以進行運作。

## 類別實作

每個GObject類別必須包含至少兩個結構：類別結構與實體結構。

  - 類別結構:類別結構相當於C++類別的vtable。第一個元素必須是父類別的類別結構。裡面包含一組函式指標，也就是類別的[虛擬方法](https://zh.wikipedia.org/wiki/虛擬函式 "wikilink")。放在這裡的變數，就像是C++類別裡的const或類別層級的成員。
    實體結構:每個物件實體都將會是這個實體結構的副本，同樣地，第一個元素，必須是實體結構的父類別（這可以確保每個實體都有個指標可以指向類別結構，所有的基礎類別也同樣如此），在歸入父類別之後，可以在結構內放其他的變數，這就相當於C++的成員變數。

C結構沒有像"public", "protected"或"private"等的存取層級修飾，一般的方法是藉著在實體結構裡提供一個指向私有資料的指標，照慣例稱作_priv。私有的結構可以宣告在公有的表頭檔案裡，然後把實體的定義寫在實作的檔案中，這樣作，對使用者來說，他並不知道私有資料是什麼，但對於實作者來說，卻可以很清楚的知道。如果私有結構也註冊在GType裡，那麼物件系統將會自動幫它配置空間。

GObject框架最主要的不利點在於太過於冗長。像是手動定義的類型轉換巨集和難解的型別註冊咒語等的大量模板代碼都是建立新類別所必要的。GObject Builder或GOB2這些工具試圖以提供樣板語法來解決這個問題。以GOB2寫的代碼必須事先處理過才能編譯。另外，Vala可以將c\# 的語法轉換成C，並編譯出獨立的二進制檔。

## 用途

C與GObject的組合被使用在許多成功的自由軟體專案上，像是GNOME桌面、GTK與GIMP影像處理軟體。

儘管許多的GObject應用程式完全以C來撰寫，但GObject系統可以很好地對應到許多語言，像C++、Java、Ruby、Python和.NET/Mono等的原生物件系統。所以在為已經使用GObject框架寫好的函式庫建立語言繫結時，通常比較不會那麼痛苦。

以C來撰寫GObject代碼時，卻是相對痛苦。學習曲線十分陡峭，有高階物件導向語言經驗的開發者可能會發現以C撰寫GObject代碼相當的乏味。舉例來說，要繼承一個類別（即使是繼承GObject）可能就需要撰寫和（或）複製上百行的代碼。雖然如此，不可否認地，GObject可以為C的代碼提供物件導向的功能。

GObject應用程式在執行時期為類別和介面所建立的元物件提供了互相操作的良好支援。可互相操作的能力被使用在語言繫結上，還有使用者介面設計應用程式（如Glade）上。Glade允許載入提供放了Widget（元件，衍生自GObject）的函式庫，並且取得類別的屬性列表、類型資訊以及文件字串。

## 與其他物件系統比較

GObject為C提供了近乎完整的物件系統，所以使用C語言配合GObject，可以做為使用其他從C分支出去的語言，像C++和Objective-C，的替代方案。（不過C++和Objective-C其實各自有很多其他特色，而不是只有差在物件系統。）　最明顯也最簡單的不同，是GObject跟Java一樣，不支援[多重繼承](https://zh.wikipedia.org/wiki/多重繼承 "wikilink")。

另一個重要的不同，GObject僅僅只是一個函式庫，而C++和Objective-C的編譯器還額外提供了新的語法或特性。

就目前的C++編譯器來說，並沒有標準的ABI可以在所有的C++編譯器運行（除了Windows，Windows上有COM可以處理），以A這個C++編譯器所編譯出來的函式庫，並不一定能被以B C++編譯器所編譯的程式呼叫。如果需要這樣的相容性，C++的方法必須要輸出為C的函式，這樣就無法享受C++帶來的好處了。這主要是因為不同的C++編譯器使用了不同的名稱特殊處理（Name mangling）以確保輸出符號的獨一性。(這是必要的，舉例來說，不同的類別可能會有一樣名稱的成員函式、被覆載許多次的函式名稱，或者出現在多個命名空間但同名的函式，但在輸出為目的檔時，這些代碼都是獨立的，如果名稱都一樣，會被視為同一份代碼，因此需要對名稱作特殊處理。）對照C來看，C不支援任何形式的覆載或名稱特殊處理，C函式庫的作者永遠只能使用明確的前置名以確保輸出名稱的全域獨一性。因此，以C撰寫的GObject基底的函式庫將不會有名稱特殊處理的問題，也不會受到編譯器的影響。

最後，"信號"（signal）可以說是更容易被發現的相異點了（在其他語言被稱作事件）。這當然是因為GObject最早被設計用在GUI工具箱上。的確，許多物件導向語言都已經有現成的信號函式庫，但GObject是被內建在物件系統裡的。因此，GObject應用程式與其他非GObject應用程式比起來，會傾向於去使用信號來實作。這使得GObject [元件](https://zh.wikipedia.org/wiki/基于组件的软件工程 "wikilink")，相較於純C++或Java寫的元件，更易於封裝，也容易被重複使用。不過該注意的是，在幾乎所有的平台都可以使用信號，但有時其實需要額外的函式庫支援，例如可用於C++的Boost.Signals2。

## 外部連結

  - [The GObject Reference Manual （and tutorial）](http://library.gnome.org/devel/gobject/stable/)
  - [GObject Tutorial Aug 2004](https://web.archive.org/web/20081029210054/http://docs.programmers.ch/index.php/HOWTO_gobject)
  - [GOB2—the GObject Builder](http://www.jirka.org/gob.html)
  - [Vala Homepage](http://live.gnome.org/Vala)

[Category:C函式庫](https://zh.wikipedia.org/wiki/Category:C函式庫 "wikilink") [Category:GNOME](https://zh.wikipedia.org/wiki/Category:GNOME "wikilink")