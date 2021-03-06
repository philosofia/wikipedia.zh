> 本文内容由[XAML Browser Application](https://zh.wikipedia.org/wiki/XAML_Browser_Application)转换而来。


XAML Browser Application，最开始叫xapp，后来在Sept CTP中叫wba，是美國微軟公司所提出的新技術，以[XAML](../Page/XAML.md "wikilink")作為[使用者介面](https://zh.wikipedia.org/wiki/人機界面 "wikilink")（UI）之描述，寄宿（hosted）在瀏覽器（IE web browser sandbox）中執行的程式。XBAP可以取代[ActiveX](../Page/ActiveX.md "wikilink")、Java Applet、Flash等功能，有人稱之為下一代的ActiveX（next-generation ActiveX）。XAML Browser Application的副檔名是**.xbap**。

## 環境設定

在執行XBAP之前，必須先設定：

  - .NET Framework 3.0 Runtime
  - Windows SDK for .NET Framework 3.0
  - Visual Studio 2005 extensions for .NET Framework 3.0（November 2006 CTP）

## 特點

  - XBAPS更易於與DHTML結合。
  - XBAPS一旦使用寬鬆XAML（loose XAML）或使用IFRAME，必執行於安全的沙盒（secure sandbox）。
  - XBAPS可以使用WPF（[Windows Presentation Foundation](../Page/Windows_Presentation_Foundation.md "wikilink")）的98.2%的功能。
  - XBAPS必須執行於iFrame之下。
  - XBAPS必須執行於DocumentObject應用程式之下，利用querystring溝通。
  - XBAPS目前僅支援IE6或IE7。

## 安全性

  - XBAP程式無法使用檔案系統（file system）。
  - XBAP程式無法呼叫對話視窗（dialog）。
  - XBAP程式如同DHTML，是網路直接安装執行，可能遇到安全性问题，所以XBAP程序必須具備内嵌數位簽名。<ManifestKeyFile>指定签字用的证书文件名，<ManifestCertificateThumbprint>指定證明文件摘要。
  - XBAP中只允許通過HTTP和[SOAP訪問](https://zh.wikipedia.org/wiki/SOAP "wikilink")[Web Services](https://zh.wikipedia.org/wiki/Web服務 "wikilink")。

## 規劃

XAML与HTML一样是flow layout，Grid類似HTML中的Table，使整個頁面的顯示方式變成網格式区域。微軟還推荐使用StackPanel，DockPanel等继承自Panel的規劃方式，Panel在使用上的類似HTML的{{\<}}DIV{{\>}}{{\<}}\\DIV{{\>}}。

## 導航

### NavigationService

WPF提供了一個最重要的頁面導航物件**NavigationService**，可用來調整頁面之用。NavigationService物件提供有下列功能：

  - public void Navigate(Uri source)
  - public void Refresh()
  - public void StopLoading()
  - public void GoBack()
  - public void GoForward()
  - public void AddBackEntry()
  - public void RemoveBackEntry()
  - public static NavigationService GetNavigationService(DependencyObject dependencyObject);

### structured navigation

structured navigation可用於處理頁面與頁面之間的資料共享。WPF支援PageFunction這樣的頁面標籤。

<PageFunction
    ns="http://schemas.microsoft.com/winfx/2006/xaml/presentation{{dead link|date=2017年11月 |bot=InternetArchiveBot |fix-attempted=yes }}"
    xmlns:x="https://web.archive.org/web/20101113200850/http://schemas.microsoft.com/winfx/2006/xaml/"
    xmlns:sys="clr-namespace:System;assembly=mscorlib"
    x:Class="StructuredNavigationSample.TestPageFunction"
    x:TypeArguments="sys:String"
    Title="Test for Page Function" WindowWidth="250" WindowHeight="150">
`   ......`
</PageFuntion>

## 範例

將[3D動畫置入iframe](https://zh.wikipedia.org/wiki/3D "wikilink")：

<iframe height="130"
  width="130"
  src="3d_animation.xaml" />

將XBAP置入iframe：

<html>

<head>

<body>

<iframe name="Iframe1" src="%fullpathtoyourgadgetdirectory%\TestBrowserApp.xbap" ></iframe>

</body>

</html>

## 差異

WinFX Windows Application和WinFX Web Browser Application有些微的差別，在.xaml檔案中，Browser Application中，預設起始页的[根元素](https://zh.wikipedia.org/wiki/根元素 "wikilink")（root element）为Page；Windows Application中，預設起始页的根元素为Window。另外，Window class无法在Browser Application中使用，因為IE浏览器中的WPF程序是在部分信任的沙箱（sandbox）内執行。

<Page x:Class="XAMLBrowserApplication1.Page1"
    ns="http://schemas.microsoft.com/winfx/2006/xaml/presentation{{dead link|date=2017年11月 |bot=InternetArchiveBot |fix-attempted=yes }}"
    xmlns:x="https://web.archive.org/web/20101113200850/http://schemas.microsoft.com/winfx/2006/xaml/"
    WindowTitle="Hello world" WindowWidth="560" WindowHeight="400"
    Title="Page1"
    >
` `<Grid>
` `</Grid>
</Page>

## 參見

  - [MCML](https://zh.wikipedia.org/wiki/MCML "wikilink")
  - [WPF/E](https://zh.wikipedia.org/wiki/WPF/E "wikilink")

## 外部連結

  - [XBap.org](http://www.xbap.org/)
  - [XBAP = next-generation ActiveX?](http://rrelyea.spaces.live.com/blog/cns!167AD7A5AB58D5FE!1553.entry)

[Category:Microsoft_Windows](https://zh.wikipedia.org/wiki/Category:Microsoft_Windows "wikilink")