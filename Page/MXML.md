> 本文内容由[MXML](https://zh.wikipedia.org/wiki/MXML)转换而来。


**MXML**是一种用于在[Adobe Flex布局用户界面组件的](https://zh.wikipedia.org/wiki/Adobe_Flex "wikilink")[XML](../Page/XML.md "wikilink")语言。语言标签中使用**mx**作为前缀。MXML区分大小写，主要用于在[Flex中的程序编写](https://zh.wikipedia.org/wiki/Flex "wikilink")。

Adobe系統，這在2005年12月收購了Macromedia公司，給出的縮寫MXML沒有官方意義。一些開發商認為這應該代表“可擴展標記語言”。這是可能的名字來自給發布於2002年和2004年，或者“Macromedia的可擴展標記語言”的Macromedia Studio產品的MX後綴。

MXML主要用於聲明應用程序的接口，也可以用於實現業務邏輯和Web應用的行為。它可以包含的ActionScript.CSS代碼。

MXML經常使用Flex伺服器，動態編譯成標準的二進制文件。然而，的Adobe Flash Builder的 IDE（原的Adobe的Flex Builder）和免費的Flex SDK也可以編譯成MXML文件，而無需使用一個Flex伺服器。

還有一個PHP PEAR包叫做XML_MXML，這是一個框架來構建的Adobe Flex應用程序。

MXML被認為是一個專有標準，由於其與Adobe技術緊密集成 並開源於Apache基金會。

## 理念

修正HTML 標記語言混亂、擴充性、彈性均不佳,效能問題(需要下載整份檔案，才能開始對檔案做搜尋)，
並且強制規範顯示格式的缺點 ,**MXML以彈性為出發點**提供所有開發商可自行開發 ,各自的標記語言顯示方式 ,再由使用者導入即可。
並且由第三方供應商的生成器，其能夠產生其他產品，例如本地或者移動應用。
也就是，【第三方顯示介面開發者】+【第三方平台轉換器】+【編輯軟體】，
各自可自行開發完全彈性，再由Web設計師導入使用，
而Web設計師也可以修改，顯示介面開發的套件，做出專屬的介面格式發布成品至各平台。
而MXML就是扮演著【第三方顯示介面開發者】開發標準的腳色,完全開源透明。

## 範例

手機頁面範例: index.mxml

``` mxml
<?xml version="1.0" encoding="utf-8"?>
<s:ViewNavigatorApplication xmlns:fx="http://ns.adobe.com/mxml/2009"
    xmlns:s="library://ns.adobe.com/flex/spark" firstView="testView" applicationDPI="160">
</s:ViewNavigatorApplication>
```

testView.mxml

``` mxml
<?xml version="1.0" encoding="utf-8"?>
<s:View xmlns:fx="http://ns.adobe.com/mxml/2009"
        xmlns:s="library://ns.adobe.com/flex/spark" title="主页视图">
    <s:Label text="Hello World!">
    </s:Label>
</s:View>
```

## 擴充結構

基本結構依循[XML](../Page/XML.md "wikilink")標準 在這之下 "\<s:" 代表 spark 也就是開發商命名空間,由adobe 開發出的套件spark的首字 我們也可以修改或變更導入我們自己的套件

[Category:XML](https://zh.wikipedia.org/wiki/Category:XML "wikilink")