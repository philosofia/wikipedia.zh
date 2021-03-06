> 本文内容由[ASP.NET](https://zh.wikipedia.org/wiki/ASP.NET)转换而来。


**ASP.NET**是由[微軟在](https://zh.wikipedia.org/wiki/微軟 "wikilink")[.NET Framework框架中所提供](https://zh.wikipedia.org/wiki/.NET_Framework "wikilink")，開發[Web應用程式的類別庫](../Page/网络应用程序.md "wikilink")，封裝在`System.Web.dll`檔案中，顯露出`System.Web`命名空間，並提供ASP.NET網頁處理、擴充以及HTTP通道的應用程式與通訊處理等工作，以及[Web Service的基礎架構](https://zh.wikipedia.org/wiki/Web_Service "wikilink")。ASP.NET是[ASP技術的後繼者](../Page/Active_Server_Pages.md "wikilink")，但它的發展性要比ASP技術要強大許多。

ASP.NET可以運行在安裝了.NET Framework的[IIS伺服器上](https://zh.wikipedia.org/wiki/Internet_Information_Server "wikilink")，若要在非微軟的平台上執行，則需要使用[Mono](../Page/Mono.md "wikilink")平台\[1\]，ASP.NET在2.0版本已經定型，在[.NET Framework](https://zh.wikipedia.org/wiki/.NET_Framework "wikilink") 3.5上則加上了許多功能，像是[ASP.NET AJAX](../Page/ASP.NET_AJAX.md "wikilink")、[ASP.NET MVC Framework](../Page/ASP.NET_MVC_Framework.md "wikilink")、[ASP.NET Dynamic Data與](https://zh.wikipedia.org/wiki/ASP.NET_Dynamic_Data "wikilink")[Microsoft Silverlight的伺服器控制項等](https://zh.wikipedia.org/wiki/Microsoft_Silverlight "wikilink")。

很多人都把 ASP.NET 當做是一種[程式語言](https://zh.wikipedia.org/wiki/程式語言 "wikilink")，但它實際上只是一個由 .NET Framework 提供的一種開發平台 (development platform)，並非程式語言。也可认为ASP.NET是.NET组件，任何.NET语言，例如[C\#](../Page/C♯.md "wikilink")，可以引用该组件，创建网页或Web服务。

為了因應雲端化所誘發的多作業平台整合與開發能力，微軟特別開發一個新一代的 ASP.NET，稱為 ASP.NET vNext，並於 2014 年命名為 ASP.NET 5，但隨後於 2016 年將它更名為 [ASP.NET Core](../Page/ASP.NET_Core.md "wikilink")，由於架構上的差異頗大，因此未來 ASP.NET 與 ASP.NET Core 將是分別發展與維護，Windows 平台的 ASP.NET 4.6 以上版本仍維持 Windows Only，但 ASP.NET Core 則是具有跨平台 (Windows, Mac OSX 與 Linux) 的能力。

## 發展緣起

[MIX_Keynote-Scott_Guthrie_09_MS_05_2007.jpg](https://zh.wikipedia.org/wiki/File:MIX_Keynote-Scott_Guthrie_09_MS_05_2007.jpg "fig:MIX_Keynote-Scott_Guthrie_09_MS_05_2007.jpg")

ASP.NET的前身ASP技術，是在IIS 2.0上首次推出（[Windows NT](../Page/Windows_NT.md "wikilink") 3.51），當時與 [ADO](../Page/ADO.md "wikilink") 1.0 一起推出，在IIS 3.0（Windows NT 4.0）發揚光大，成為伺服器端應用程式的熱門開發工具，微軟還特別為它量身打造了[Visual InterDev開發工具](https://zh.wikipedia.org/wiki/Visual_InterDev "wikilink")，在1994年到2000年之間，ASP技術已經成為微軟推展[Windows NT 4.0平台的關鍵技術之一](../Page/Windows_NT_4.0.md "wikilink")，數以萬計的ASP網站也是這個時候開始如雨後春筍般的出現在網路上。由於它的簡單以及高度客制化的能力，也是它能迅速竄起的原因之一。

不過ASP的缺點也逐漸的浮現出來：

  - 義大利麵型的程式開發方法，讓維護的難度提高很多，尤其是大型的ASP應用程式。
  - 直譯式的[VBScript](../Page/VBScript.md "wikilink")或[JScript](../Page/JScript.md "wikilink")語言，讓效能有些許的受限。
  - 延展性因為其基礎架構擴充性不足而受限，雖然有[COM元件可用](https://zh.wikipedia.org/wiki/COM "wikilink")，但開發一些特殊功能（像檔案上傳）時，沒有來自內建的支援，需要尋求第三方軟體商開發的元件。

1997年時，微軟開始針對ASP的缺點（尤其是義大利麵型的程式開發方法）準備開始一個新專案來開發，當時ASP.NET的主要領導人剛從[杜克大學畢業](https://zh.wikipedia.org/wiki/杜克大學 "wikilink")，他和IIS團隊的[Mark Anders經理一起合作兩個月](https://zh.wikipedia.org/wiki/Mark_Anders "wikilink")，開發出了下一代ASP技術的原型，這個原型在1997年的聖誕節時被發展出來，並給予一個名稱：**XSP**\[2\]，這個原型產品使用的是[Java](../Page/Java.md "wikilink")語言。不過它馬上就被納入當時還在開發中的[CLR平台](https://zh.wikipedia.org/wiki/CLR "wikilink")，Scott Guthrie事後也認為將這個技術移植到當時的CLR平台，確實有很大的風險（huge risk），但當時的XSP團隊卻是以CLR開發應用的第一個團隊。

為了將XSP移植到CLR中，XSP團隊將XSP的核心程式全部以[C\#語言重新撰寫](../Page/C♯.md "wikilink")（在內部的專案代號是 "Project Cool"，但是當時對公開場合是保密的），並且改名為**ASP+**，作為ASP技術的後繼者，並且也會提供一個簡單的移轉方法給ASP開發人員。ASP+首次的Beta版本以及應用在[PDC](../Page/专业开发者大会.md "wikilink") 2000中亮相，由[Bill Gates发表Keynote](https://zh.wikipedia.org/wiki/Bill_Gates "wikilink")（即關鍵技術的概覽），由[富士通](../Page/富士通.md "wikilink")公司展示使用[COBOL](../Page/COBOL.md "wikilink")語言撰寫ASP+應用程式，並且宣布它可以使用[Visual Basic.NET](https://zh.wikipedia.org/wiki/Visual_Basic.NET "wikilink")、[C\#](https://zh.wikipedia.org/wiki/C_Sharp "wikilink")、[Perl](../Page/Perl.md "wikilink")與[Python](../Page/Python.md "wikilink")語言（後兩者由ActiveState公司開發的互通工具支援）來開發。

在2000年第二季時，微軟正式推動.NET策略，ASP+也順理成章的改名為**ASP.NET**，經過四年的開發，第一個版本的ASP.NET在2002年1月5日亮相（和[.NET Framework](https://zh.wikipedia.org/wiki/.NET_Framework "wikilink") 1.0），Scott Guthrie也成為ASP.NET的產品經理（到現在已經開發了數個微軟產品，像[ASP.NET AJAX和](../Page/ASP.NET_AJAX.md "wikilink")[Microsoft Silverlight](https://zh.wikipedia.org/wiki/Microsoft_Silverlight "wikilink")）。

## ASP.NET處理架構

ASP.NET 運行的架構分為幾個階段：

  - 在 IIS 與 Web 伺服器中的訊息流動階段。
  - 在 ASP.NET 網頁中的訊息分派。
  - 在 ASP.NET 網頁中的訊息處理。

### Web伺服器的訊息流動階段

[ASPNET_IIS_Execute.png](https://zh.wikipedia.org/wiki/File:ASPNET_IIS_Execute.png "fig:ASPNET_IIS_Execute.png")

當裝載(hosting) ASP.NET 的 Web 伺服器接收到 HTTP 请求時，HTTP 聆聽程式 (HTTP Listener，实际上是内核态的HTTP.SYS) 會將请求轉交給 URL 指定的網站應用程式池中的工作者进程 (Worker Process)\[3\]，ASP.NET 的工作者进程接收到这个请求之后，装载专用于处理ASP.NET页面的一个ISAPI扩展“aspnet_isapi.dll”，并将HTTP请求传给它。若是 IIS 5.0 時則是 aspnet_wp.exe。

aspnet_isapi.dll负责加载ASP.NET应用程序的运行环境CLR（IIS 7集成模式下，CLR是预加载的），每个ASP.NET应用程序都运行于自己的应用程序域（AppDomain）中。每个应用程序域都对应着一个ApplicationManager类的实例（通过AppManagerAppDomainFactory创建），负责管理运行在域中的ASP.NET应用程序（启动和停止一个ASP.NET应用程序、创建对象等）。ApplicationManager还会创建一个HostingEnvironment对象，提供了ASP.NET应用程序的一些管理信息（如ASP.NET应用程序的标识、虚拟目录与对应的物理目录等）。

应用程序域创建完成之后，创建 System.Web.Hosting 命名空間中的基于ISAPIRuntime的一个对象，调用其ProcessRequest()方法。在此方法中，根据传入的HTTP请求信息屏蔽了版本差异化后封装实例化了一个HttpWorkerRequest的对象并初始化一个HttpRuntime对象。调用HttpRuntime的ProcessRequestInternal方法。ProcessRequestInternal方法实例化一个HttpContext对象（其构造函数内部又实例化了在ASP.NET编程中非常重要的HttpRequest和HttpResponse对象）、通过HttpApplicationFactory获取HttpApplication对象实例。再调用HttpApplication对象的BeginProcessRequest方法启动整个HTTP请求的处理过程（即**HTTP管线模式**）。

System.Web.UI.Page类提供了“Requset”和“Response”属性来引用这两个对象，因此在ASP.NET网页中可以直接访问这两个对象。同样，System.Web.UI.Page类的Context属性引用HttpContext对象。

HttpRuntime类的ProcessRequest()方法除了创建HttpContext对象之外，还完成了另一个很重要的工作——向HttpApplicationFactory类的一个实例（它管理一个HttpApplication对象池）申请分配一个HttpApplication对象用于管理整个“HTTP请求处理管线（HTTP Pipeline）”中的各种事件的激发。在HttpApplication对象的InitModules()方法中创建HTTP模块（HTTP Module），通常在HTTP模块对象（实现IHttpModule接口）的Init()方法中响应HttpApplication对象所激发的特定事件。开发者可以创建基于IHttpHandler接口的对象，在Web.Config中插入特定的内容可以将自定义的HTTP模块加入到HTTP请求的处理流程中。 在IIS6和IIS7经典模式下，是用 Event+事件名称做key将所有事件的保存在HttpApplication的Events属性对象里，然后在BuildSteps里统一按照顺序组装。在IIS7集成模式下，是通过HttpModule名称+RequestNotification枚举值作为key将所有的事件保存在HttpApplication的ModuleContainers属性对象里，这个属性的类型是PipelineModuleStepContainer\[\]。

“HTTP请求处理管线（HTTP Pipeline）”的处理过程为：

1.  预处理阶段：由多个HTTP模块参与，通过事件来驱动，主要是对HttpContext对象的各种属性进行修改。
2.  处理阶段：由System.Web.UI.Page类接手HttpContext对象。Page类实现了IHttpHandler接口，因此有ProcessRequest()方法并被自动调用。ProcessRequest()方法的执行结果刷新了HttpContext对象的内容。
3.  后处理阶段：HttpApplication对象继续激发后继的事件。如果有特定的HTTP模块响应这些事件，则它们会被自动调用。在管线末端，信息傳回到 ISAPIRuntime，以及 aspnet_isapi.dll，最後交由 HTTP Listener 回傳給用戶端。当HTTP请求处理完毕，相关的对象被释放，但创建的应用程序域，以及HttpApplication等对象仍然存活，以响应下一次HTTP请求。

具体的处理管线：

1.  BeginRequest: 开始处理请求。当ASP.NET运行时接收到新的HTTP请求的时候引发这个事件
2.  AuthenticateRequest授权验证请求，获取用户授权信息。当ASP.NET 运行时准备验证用户身份的时候引发这个事件
3.  PostAuthenticateRequest：验证身份成功。通过HttpContext.User获取
4.  AunthorizeRequest 用户权限授权。当ASP.NET运行时准备授权用户访问资源的时候引发这个事件
5.  PostAuthorizeRequest:获得授权
6.  ResolveRequestCache:获取页面缓存结果，如果存在直接返回结果
7.  PostResolveRequestCache 缓存检查结束
8.  MapRequestHandler：IIS7集成模式才支持
9.  查找并创建HttpHandler：根据URL路径或扩展名和匹配规则查找创建，赋值给HttpContext.Handler属性（仅限于IIS6与IIS7经典模式）
10. PostMapRequestHandler 成功创建IHttpHanlder对象
11. AcquireRequestState 获取请求状态，一般用于获取Session：先判断当前页面对象是否实现了IRequiresSessionState接口，如果实现了，则从浏览器发来的请求报文体中获得SessionID,并到服务器的Session池中获得对应的Session对象，最后赋值给HttpContext的Session属性
12. PostAcquireRequestState 成功获得Session
13. PreRequestHandlerExecute:准备执行HttpHandler处理程序。
14. 执行HttpHandler处理程序（仅限于IIS6与IIS7经典模式）：调用HttpHandler的ProcessRequest方法（同步）或BeginProcessRequest方法（异步）。
15. PostRequestHandlerExecute 执行HttpHandler处理程序结束。
16. ReleaseRequestState 准备释放请求状态（Session）
17. PostReleaseRequestState 成功释放请求状态（Session）
18. Filter：将内容写入Filter（仅限于IIS6与IIS7经典模式）
19. UpdateRequestCache 更新缓存
20. Filter：将内容写入Filter（仅限于IIS7集成模式）
21. PostUpdateRequestCache 已更新缓存
22. LogRequest 为当前请求执行日志记录（仅限于IIS7集成模式）
23. PostLogRequest 已完成日志（仅限于IIS7集成模式）
24. EndRequest 完成。把响应内容发送到客户端之前引发这个事件。
25. Noop：扩展使用（仅限于IIS6与IIS7经典模式）
26. PreSendRequestHeaders：根据发送的Headers动态设置一些参数（仅限于IIS7集成模式）
27. PreSendRequestContent：可对输出内容做压缩（仅限于IIS7集成模式）

在 ASP.NET 內部的 HTTP 處理器有：

  - ISAPIRuntime：由 aspnet_isapi.dll 呼叫，初始化 HttpWorkerRequest 物件（會由IIS的版本決定要初始化的版本）。
  - HttpRuntime：提供请求佇列 (Request Queue)、呼叫 HttpWorkerRequest 中的 ProcessRequest() 方法，以及後續的處理工作。
  - HttpWorkerRequest：產生 HttpApplication、HttpRequest、HttpResponse 等基礎物件的 HTTP 请求物件，並將要求轉送到要處理的物件（並呼叫它的 ProcessRequest() 方法）。
  - IHttpHandler 與 IHttpAsyncHandler：負責處理 HTTP 请求的單元，由 ProcessRequest() 來分派與執行请求。

### ASP.NET網頁中的事件程序

當 HttpWorkerRequest 呼叫 **ASP.NET 網頁**（System.Web.UI 命名空間的 Page 類別）的 Page.ProcessRequest() 方法時，它會依序的引發 Page 內的各個事件，並同時呼叫在 Page 中所有控制項的相關事件，其引發順序為\[4\]：

启动阶段：设置页面基本属性，如 Request 和 Response。在此阶段，页面还将确定请求是回发请求还是新请求，并设置 IsPostBack 属性。

1.  PreInit 事件：執行預先初始化的工作，在ASP.NET 2.0中，若要動態調整主版頁面 (Master Page)、佈景主題 (Theme) 時，要在這個事件中調整。设置页面一些最基本的特性，如加载个性化信息和主题、运行时Culture。
2.  Init 事件：執行初始化工作。根据页面的服务器标签及其属性设置，生成各个服务器控件的实例和给这些服务器控件的实例的属性进行赋值，并存入ViewState，但因为本阶段的赋值行为优先于ViewState的TrackViewState被调用，所以这些视图的值都将不会存入最终呈现的视图状态隐藏字段中。
3.  InitCompleted 事件：在完成初始化工作後引發。调用ViewState的TrackViewState方法，开启对视图状态更改的跟踪。
4.  Preload 事件：載入表单传值）。页面方法调用LoadViewState、LoadControlState、ProcessPostData，服务器控件对应调用LoadViewState和实现IPostBackDataHandler接口的LoadPostData方法
5.  Load 事件：執行載入的工作，大多數的網頁都擁有 Page_Load 事件處理常式，使用者控制項 (user control) 中也有 Page_Load 事件常式，都會在此時呼叫。
      -
        控制項的 PostBack 變更通知：當網頁偵測到是 PostBack 要求時，會引發 PostBack 訊息通知的事件。
        控制項的 PostBack 相關事件：當網頁偵測到是 PostBack 要求時，會引發 PostBack 訊息指定的控制項的事件。
6.  LoadCompleted 事件：執行載入完成後的工作。
7.  PreRender 事件：處理在產生 HTML 結果前的工作。
8.  SaveStateCompleted 事件：處理頁面狀態（ViewState 與 ControlState）儲存完成後的事件。
9.  Render 事件：處理產生 HTML 的工作。
10. Unload 事件：處理結束網頁處理時的工作。

如果 HttpWorkerRequest 呼叫的是實作 IHttpHandler 介面的 **HTTP 處理常式** 時，它只會呼叫 IHttpHandler.ProcessRequest() 方法，由它來處理程式的輸出，不像 Page.ProcessRequest() 會處理事件順序，因此 HTTP Handler 很適合輕量級的資料處理，像是輸出檔案資料流或是圖片資料流等。

### ASP.NET的事件模型

ASP.NET 的原始設計構想，就是要讓開發人員能夠像 VB 開發工具那樣，可以使用[事件驅動式程式開發模式](https://zh.wikipedia.org/wiki/事件驅動 "wikilink") (Event-Driven Programming Model) 的方法來開發網頁與應用程式，若要以ASP技術來做到這件事的話，就必須要使用大量的輔助資訊，像是查詢字串或是表單欄位資料來識別與判斷物件的來源、事件流向以及呼叫的函式等等，需要撰寫的程式碼量相當的多，但 ASP.NET 很巧妙利用表單欄位和JavaScript指令碼把事件的傳遞模型隱藏起來了。

ASP.NET 的事件模型是由 <code>

<form runat="server">

</form>

</code> 以及數個 Hidden Field 組合而成，基於 HTTP 模型的限制，所有的網頁程式在執行結果輸出到用戶端後，程式就會結束執行，為了維護在 ASP.NET 網頁與控制項的狀態資料，因此在輸出 ASP.NET 控制項時，ASP.NET 會將部份狀態資料儲存到網頁的 Hidden Field 中，這類型的狀態資料稱為 **ViewState**（ID 為 `__VIEWSTATE`），在伺服器端即會被解譯出狀態與事件資料。在大多數的內建 Web 控制項中都有使用到這個機制，因此在使用大量 ASP.NET Web 控制項的網頁中，會有許多的 ViewState 會存放在網頁中並隨著 HTTP 資料流輸出到用戶端，ViewState 在輸出時，會被加密為一組亂碼字串，其金鑰值定義在電腦中，並且每一個物件都會被序列化 (serialize) 成字串（因此若是自訂物件要放到 ViewState 時，則應要讓它支援序列化），再輸出到 `__VIEWSTATE` 欄位中，在每次的網頁來回時都會被傳輸，較大的 ViewState 會讓網頁大小膨脹，不利於快速的網路傳輸，不過 ASP.NET 本身有提供將 ViewState 關閉的功能，因此如果控制項不需要狀態保存時，可將它關閉以減少輸出的大小。

為確保控制項的事件能夠確實被引發，讓事件驅動能夠被執行，因此控制項事件引發命令時需要的參數，是交由 JavaScript 指令碼在用戶端引發時，填入另一個 Hidden Field（ID 為 `__EVENTTARGET` 以及 `__EVENTARGUMENT`），並且引發表單的送出指示 (submit)，傳送到伺服端後，伺服端的 HttpApplication 中的工具函式會解析 `__EVENTTARGET` 和 `__EVENTARGUMENT` 欄位中的資訊，並且交由控制項所實作的 RaisePostBackEvent() 來引發事件，並由 .NET Framework 內部的事件處理機制接手處理（呼叫控制項設定的事件處理常式）。

### ASP.NET的來回模式

[DotNet3.0.svg](https://zh.wikipedia.org/wiki/File:DotNet3.0.svg "fig:DotNet3.0.svg") 在 ASP.NET 運行的時候，經常會有網頁的來回動作 (round-trip)，在 ASP.NET 中稱為 **PostBack**，在傳統的 ASP 技術上，判斷網頁的來回是需要由開發人員自行撰寫，到了 ASP.NET 時，開發人員可以用 Page.IsPostBack 機能來判斷是否為第一次執行（當 ASP.NET 發現 HTTP POST 要求的資料是空值時），它可以保證 ASP.NET 的控制項事件只會執行一次，但是它有個缺點（基於 HTTP POST 本身的缺陷），就是若使用者使用瀏覽器的重新整理功能（按 F5 或重新整理的按鈕）刷新網頁時，最後一次執行的事件會再被執行一次，若要避免這個狀況，必須要強迫瀏覽器清空快取才可以。

ASP.NET 2.0 中有新增三個來回模式：

  - Cross Page Postback：允許跨不同的網頁執行 PostBack，伺服端可使用 Page.IsCrossPostBack 來判斷是否是跨網頁型的來回。
  - Async Page Mode：允許網頁使用非同步的方式執行，伺服端可用 Page.IsAsync 來判斷。
  - Callback：ASP.NET 2.0 新增的由網頁回呼用戶端指令的功能，伺服端可用 Page.IsCallback 來判斷是否要求是來自 Callback。

來回模式不僅是 ASP.NET 運作時的核心，它也是 ASP.NET 應用程式的一個主要缺點，尤其是在設計複雜度高的頁面時，在網頁中隱藏的 ViewState 的大小會相當大，而在每次的來回動作中，都會傳送 ViewState 在內的表單資訊，大量的 ViewState 會使得傳送的時間拉長，而且每次來回動作都會讓整個網頁被刷新，而出現閃爍的情況（就算在本地端也一樣），但在[AJAX](../Page/AJAX.md "wikilink")技術尚未成熟時，只能夠忍受這種因底層限制所帶來的問題，在[ASP.NET AJAX技術發展出來後](../Page/ASP.NET_AJAX.md "wikilink")，透過**UpdatePanel**成功的緩解了這個問題（但 ViewState 傳送的問題仍然未根本的解決，必須要使用像 Page Method 這樣的方式才能徹底的解決）。

### 繪製技術

熟悉 ASP 技術的人都知道，程式碼都是混在 HTML 標籤之間，以輸出預期需要的 HTML 指令，這個技術在 ASP.NET 中，由各控制項的**繪製** (Render) 機制包裝起來了，繪製機制裝載了 HtmlTextWriter 物件，由它來產生 HTML 指令，它會輸出至 HttpContext 的 Response 輸出資料流中（即 ASP 技術的 Response.Write()），下列程式碼為繪製技術的示例：

``` csharp
[System.Security.Permissions.PermissionSet(System.Security.Permissions.SecurityAction.Demand, Name="FullTrust")]
protected override void Render(HtmlTextWriter output)
{
    if ( (HasControls()) && (Controls[0] is LiteralControl) )
    {
        output.Write("<H2>Your Message: " + ((LiteralControl) Controls[0]).Text + "</H2>");
    }
}
```

為了讓控制項的輸出有階層性，ASP.NET 開發了一個可以階層化輸出控制項 HTML 指令的方式，稱為**控制項樹 (Control Tree)**，藉由控制項樹，可以讓各個控制項的輸出可以階層化，不論是否是收納型控制項，還是一般型的控制項，都可以按照控制項的順序來輸出。

## 狀態管理

狀態管理 (state management) 在[Web應用程式中](../Page/网络应用程序.md "wikilink")，一向是很重要的課題，良好的狀態管理可以幫助開發人員發展出具有狀態持續能力的應用程式（像是[工作流程型應用程式或是](https://zh.wikipedia.org/wiki/工作流程 "wikilink")[電子商務應用程式](https://zh.wikipedia.org/wiki/電子商務 "wikilink")），但狀態管理功能會視應用程式的部署狀態以及資訊的共用程度來選擇，在 ASP.NET 中，分為伺服器端狀態管理以及用戶端狀態管理，用戶端狀態管理為**ViewState**以及[Cookie](../Page/Cookie.md "wikilink")s，伺服端狀態管理則是**Session**與**Application**物件。它們的差異點在於：

  - ViewState 是加密的資料流，和 HTML 一起輸出到用戶端。
  - Cookies 是加密（也可不加密）的小型資料，和 HTML 不同，它可以快取在用戶端瀏覽器中。
  - Session 是伺服器端的狀態保存機制，每個用戶端均有獨立的空間（以瀏覽器執行個體來賦與唯一的SessionID值）。
  - Application 是伺服器端的狀態保存機制，但應用程式所有的用戶端共用同一份狀態資料。

### 應用程式層級物件

Application 物件會在應用程式的 Application_OnStart 事件中初始化，並使用名稱來識別資料（它是一個 NameObjectCollectionBase 集合的實作品），它會儲存在應用程式的範圍內，所有的連線（使用者）都可以使用，屬於共用型的儲存體，適合儲存所有使用者都可使用的資料，在多人使用的情況下，可以適當的使用 Lock/Unlock 的機制來確保應用程式狀態的更新。

``` csharp
Application.Lock();
Application["PageRequestCount"] =
    ((int)Application["PageRequestCount"])+1;
Application.UnLock();
```

### 連線層級物件

連線層級的物件是 Session，以瀏覽器的執行個體為識別單位，資料依瀏覽器的執行個體來儲存，在瀏覽器的執行個體第一次連到應用程式時，ASP.NET會設定一個Session ID，並且使用它來識別 Session，每一個 Session 都是 ICollection 與 IEnumerate 的實作，用 key 來識別資料值，並且具有時間的限制 (timeout)，若超出時限時伺服器會自動清理掉，預設的 Session 時限為 20 分鐘。Session ID 的演算法是由 RNGCryptoServiceProvider（密碼編譯亂數產生器提供者）產生，並編碼成一個 Session ID 字串（例如 anf4vuup3xiq0arjlqla2l55 這樣的字串）儲存在伺服器中，用以識別不同的 Session 個體。

為因應不同的用戶端，ASP.NET 設計了不同的 Session ID 存放機制，像是舊式的瀏覽器或是行動用戶端這種不支援本地儲存[cookie的裝置時](https://zh.wikipedia.org/wiki/cookie "wikilink")，ASP.NET 可以直接在 URL 中加上 Session ID 的識別，像是 `http://www.example.org/(anf4vuup3xiq0arjlqla2l55)/profile.aspx` 這樣的 URL，可以由開發人員自行設定，或是使用 AutoDetect 設定來讓 ASP.NET 自行判斷要使用的 Session ID 存放方式。

Session ID 的產生方法可以由程式開發人員自訂，藉由覆寫 SessionIDManager 的 CreateSessionID() 方法來自訂。

``` csharp
using System;
using System.Configuration;
using System.Web.Configuration;
using System.Web;
using System.Web.SessionState;


namespace Samples.AspNet.Session
{

  public class GuidSessionIDManager : SessionIDManager
  {

    public override string CreateSessionID(HttpContext context)
    {
      return Guid.NewGuid().ToString();
    }


    public override bool Validate(string id)
    {
      try
      {
        Guid testGuid = new Guid(id);

        if (id == testGuid.ToString())
          return true;
      }
      catch
      {
      }

      return false;
    }
  }
}
```

### 跨機器狀態管理

狀態管理在單一伺服器上，可以儲存在伺服器的記憶體中，但若是在大型網站中，使用許多的 Web 伺服器來實行[負載平衡](https://zh.wikipedia.org/wiki/負載平衡 "wikilink")（Load Balancing）處理時，會有狀態儲存在哪個位置的問題，因此需要有一個可以在每個 Web 伺服器之間做狀態儲存的媒介，像是獨立的伺服器或是資料庫等等。在 ASP.NET 中支援了四種狀態儲存的媒介\[5\]：

  - **InProc**：儲存與 ASP.NET 相同的執行行程中 (in-procedure state)，適合單一伺服器的狀態儲存。
  - **StateServer**：儲存在 ASP.NET 狀態伺服器 (state server) 中，適合跨伺服器的狀態儲存，但因為它使用的通訊埠，因此在使用上需要注意防火牆的問題。
  - **SQLServer**：儲存在獨立的 [SQL Server](https://zh.wikipedia.org/wiki/SQL_Server "wikilink") 資料庫中，適合跨伺服器的狀態儲存。
  - **Custom**：以自行實作的狀態提供者 (state provider)。

## 部件

ASP.NET 是開發 Web 應用程式的基礎架構 (framework)，除了它內部的運作方法外，對外也顯露了許多的開發支援，讓開發人員可以利用它來發展出許多強大的 Web 應用程式解決方案。

### 基礎部件

#### 網頁

ASP.NET 最基礎的底層為網頁 (Page)，網頁由 `System.Web.UI.Page` 類別來提供基礎支援，包含了頁面的事件以及物件繪製的引發點（Page 類別本身是一個 HTTP Handler 的實作品）。ASP.NET 網頁在微軟的官方名稱中，稱為 **Web Form**，除了是要和[Windows Forms作分別以外](../Page/Windows_Forms.md "wikilink")，同時也明白的刻劃出了它的主要功能：「讓開發人員能夠像開發 Windows Forms 一樣的方法來發展 Web 網頁」。因此 ASP.NET Page 所要提供的功能就需要類似 Windows Forms 的表單，每個 Web Form 都要有一個 <code>

<form runat="server">

</form>

</code> 區塊，所有的 ASP.NET 伺服器控制項都要放在這個區域中，這樣才可以讓 ViewState 等伺服器控制能夠順暢的運作。

在網頁中也可以使用程式碼，以類似於[ASP時代的撰寫方式來開發](https://zh.wikipedia.org/wiki/ASP "wikilink")，此種開發方式稱為 **inline code**，在 ASP.NET 的程式開發模式中，inline code ，要放在 <code>

<script runat="server">

</script>

</code> 區域中，如下列的範例程式：

``` csharp
<%@ Page Language="C#" %>

<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN"
"http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">

<script runat="server">

    protected void Page_Load(object sender, EventArgs e)
    {
        Label1.Text = DateTime.Now.ToLongDateString();
    }

</script>

<html ns="http://www.w3.org/1999/xhtml">
<head runat="server">
    <title>Sample page</title>
</head>
<body>
    <form id="form1" runat="server">
    <div>
        The current time is: <asp:Label runat="server" id="Label1" />
    </div>
    </form>

</body>
</html>
```

另一種模式則是將程式碼和網頁分離，這種模式稱為**程式碼後置 (Code-Behind)**，這個方法可以將程式碼獨立到一個檔案中，網頁可以保持較乾淨的狀態，讓維護網頁程式的複雜度降低很多，在網頁的提示指令 (directive) 中，可以設定程式碼後置的參數，像是 Inherit、CodeFile、Class 等參數。

``` asp
<%@ Page Language="C#" CodeFile="SampleCodeBehind.aspx.cs" Inherits="Website.SampleCodeBehind"
AutoEventWireup="true" %>
```

而一個典型的程式碼後置例子為：

``` csharp
using System;

namespace Website
{
    public partial class SampleCodeBehind : System.Web.UI.Page
    {
        protected override void Page_Load(EventArgs e)
        {
            base.OnLoad(e);
        }
    }
}
```

使用程式碼後置模式的設定時，可以讓 ASP.NET 執行引擎在載入網頁時，由程式碼後置參數取得對應的類別資訊，藉以使用 Reflection 的方式來執行後置的程式碼。

ASP.NET 可以支援[HTML](../Page/HTML.md "wikilink")和[XHTML](../Page/XHTML.md "wikilink")兩種網頁內容，但在[Visual Studio.NET中](https://zh.wikipedia.org/wiki/Visual_Studio "wikilink")，預設是使用 HTML，但在[Visual Studio 2005以後的版本](https://zh.wikipedia.org/wiki/Visual_Studio "wikilink")，則一律都改用XHTML格式。

#### 控制項

ASP.NET 的內建控制項分為兩種：

  - **HTML 控制項 (HTML control)**：直接在 HTML 標記中加上 runat="server"，即可對應到 ASP.NET 指定的 HTML 伺服器控制項類別，像是：
      - **HtmlAnchor**：表示 HTML 的 <a>。
      - **HtmlButton**：表示 HTML 的 <input type="button">。
      - **HtmlImage**：表示 HTML 的 <img>。
      - **HtmlGenericControl**：表示沒有對應到伺服器控制項的物件，都會被對應到這個類別。

<!-- end list -->

  - **Web 控制項 (Web control)**：由 ASP.NET 提供，比 HTML 控制項提供更多的功能，但操作與設定會比 HTML 控制項要複雜許多，像是：
      - **LinkButton**：一種外型為連結 (<a>) 的按鈕。
      - **CheckBoxList**：建立 CheckBox 的清單的控制項。
      - **GridView**：將資料繫結並產生 HTML 表格的控制項。
      - **RequiredFieldValidator**：檢查欄位是否有輸入資料的控制項。

除了內建的控制項之外，ASP.NET 也提供了可以自訂的控制項架構，並且支援兩種控制項開發方法：

  - **使用者控制項 (User control)**，以 .ascx 為副檔名，可以讓開發人員用最輕鬆的方式來開發控制項，優點是開發速度很快，但缺點是無法轉散布，且無法加入參考。
  - **自訂控制項 (Custom control)**，可轉散布型的控制項，是經過編譯後的程式碼 (DLL)，可單獨轉散布，並且可在其他的專案加入參考取用，自訂控制項有三種開發模式：
      - **基礎控制項 (General Control)**：由 System.Web.UI.Control 類別繼承而來，或是由現有的 Web 控制項繼承而來，像是由 Button 控制項繼承。
      - **複合控制項 (Composite Control)**：由 System.Web.UI.WebControls.CompositeControl 繼承而來，可以用複合的方式來開發控制項。
      - **樣板控制項 (Template Control)**：可以在控制項中使用樣板 (template)，並套用資料到樣板中，支援資料繫結的運算式。

#### 指令碼

ASP.NET 的 Web 控制項有時會包裝一些用戶端指令碼 (client-side scripting)，在控制項被繪製時輸出到用戶端，這些指令碼多數被包裝在 DLL 的資源檔中，並由 ScriptResource.axd 處理常式來輸出，開發人員也可以利用 ClientScriptManager（Page.ClientScript 屬性）中的方法來添加指令碼到網頁程式中，常用的方法有：

  - **ClientScriptManager.RegisterClientScriptBlock()**：註冊用戶端指令碼區塊 (script block)。
  - **ClientScriptManager.RegisterStartupScript()**：註冊在起始時執行的指令碼。
  - **ClientScriptManager.RegisterOnSubmitStatement()**：註冊在處理表單發送時要執行的指令碼。
  - **ClientScriptManager.RegisterClientScriptInclude()**：註冊由外部檔案 (.js) 提供的指令碼來源。

#### 基本物件

以往在 ASP 中常被使用的五大基本物件，在 ASP.NET 中仍然持續被支援，但它們都換了一個身份來提供：

  - Application：包裝了 HttpApplication 物件，在程式中使用 Application 指令取得的物件，都是來自於 HttpContext.Current.Application 屬性回傳而得。
  - Request：包裝了 HttpRequest 物件，在程式中使用 Request 指令取得的物件，都是來自於 HttpContext.Current.Request 屬性回傳而得。
  - Response：包裝了 HttpResponse 物件，在程式中使用 Response 指令取得的物件，都是來自於 HttpContext.Current.Response 屬性回傳而得。
  - Session：包裝了 HttpSessionState 物件，在程式中使用 Session 指令取得的物件，都是來自於 HttpContext.Current.Session 屬性回傳而得。
  - Server：包裝了 HttpServerUtility 物件，在程式中使用 Server 指令取得的物件，都是來自於 HttpContext.Current.Server 屬性回傳而得。

### 導覽部件

**導覽部件 (navigation controls)**\[6\] 是在 ASP.NET 2.0 中才出現的功能，包含：

  - **選單 (Menu)**：提供內建的滑鼠偵測方式，實作階層式的選單功能。
  - **網站地圖 (Sitemap)**：提供可層次化目前瀏覽位置的功能，可支援由 Web.sitemap 中的資料，或是來自資料庫或 XML 資料檔中的資料來源。
  - **樹狀檢視 (TreeView)**：提供階層化的資料瀏覽，類似於檔案總管的介面。

### 應用程式服務

應用程式服務 (application services) 是在 ASP.NET 2.0 中才開始提供，它以 Provider-based Pattern 為主，實作出數個網站的常用服務，包含會員服務 (Membership Service)\[7\]、角色服務 (role service)\[8\]與設定檔服務 (profile service)\[9\] 等。

會員服務由 Membership 以及其資料提供者 MembershipProvider 構成，應用程式使用 Membership 所顯露的方法來操作，它會將要求轉送給指定的 MembershipProvider 實作來處理，ASP.NET 目前支援來自於資料庫的 SqlMembershipProvider（支援 SQL Server）以及來自於[Active Directory的](../Page/Active_Directory.md "wikilink") ActiveDirectoryMembershipProvider，開發人員也可以自行由 MembershipProvider 繼承來實作自訂的會員服務資料提供者。

角色服務與會員服務類似，由 Role 以及其資料提供者 RoleProvider 構成，應用程式使用 Role 所顯露的方法操作，由 RoleProvider 實作提供資料服務，目前內建的 RoleProvider 有來自 Active Directory 或 XML 檔案的 AuthorizationStoreRoleProvider，由 SQL Server 供應資料的 SqlRoleProvider，以及支援 Windows 角色的 WindowsTokenRoleProvider 三種，開發人員可自行實作 RoleProvider 的方法以發展出自訂的角色服務提供者。

設定檔服務是一個特殊的服務，它結合了 .NET Framework 的 CodeDOM 開發模式，以及 System.Web.Profile 命名空間的 ProfileBase、ProfileInfo 與 ProfileManager 等類別，組合出完整的設定檔支援，其資料來源也是以 Provider-based Pattern 為主，由 ProfileProvider 提供，ASP.NET 內建由 SQL Server 資料庫建立的 SqlProfileProvider，其欄位係由開發人員在 ASP.NET 組態檔中自行定義，再由 ASP.NET 動態產生強型別的欄位屬性。

設定檔服務也是作為 ASP.NET 2.0 的**網頁組件 (Web Part Framework)** 所需要的設定檔儲存支援\[10\]，Web Part Framework 可以讓開發人員可以開發出具備個人化能力 (Personalization) 的網頁配置方案，讓使用者可以用自行新增與拖放的方式來設計自己的網頁佈置，所需要的設定儲存即由設定檔服務處理。

另一個需要和應用程式服務配合使用的功能為 **Web 事件架構 (Web Event Framework)**\[11\]，它需要由應用程式服務提供資料結構，它也有 Provider-based Pattern，並可以支援數種的事件資料提供者。

### 延展性支援

除了 ASP.NET 網頁以外，.NET Framework 還提供了兩種可以由開發人員自行發展處理模型的模組，一種是**HTTP Handler**，另一種則是**HTTP Module**\[12\]。

HTTP Handler（副檔名為 .ashx）由 System.Web.IHttpHandler 介面定義了必要的方法（可支援非同步的 HTTP Handler 稱為 HTTP Async Handler，由 System.Web.IHttpAsyncHandler 介面定義），其中最重要的方法是 ProcessRequest() 方法，開發人員必須要實作這個方法，才能夠讓 HTTP Handler 有作用，它也可以透過 ASP.NET 的組態設定，讓 HTTP Handler 可以處理特定的副檔名，它可以被視為 .NET Framework 中的 ISAPI Extensions 實作方法。

HTTP Module 則是由 System.Web.IHttpModule 介面定義，它可以在整個網頁生命週期中被呼叫多次，並實際處理由 HttpApplication 所引發的事件，開發人員需要實作 IHttpModule.Init() 方法，以及處理 HttpApplication 事件需要的程式碼。它可被視為 .NET Framework 中的 ISAPI Filter 實作方法。

## 一致性與多樣性介面的支援　

ASP.NET 在一開始的時候是缺乏[範本引擎](https://zh.wikipedia.org/wiki/範本引擎 "wikilink") (template engine) 的，其主因是.NET Framework本身是物件導向，且需要用繼承的方式才能夠延伸功能，大多數的開發人員都是由 System.Web.UI.Page 繼承並定義出新的基礎類別，並撰寫要繪製 HTML 的方法，以及在他們的應用程式中修改以繼承該類別，然而這個方法可能會被用在網站的很多地方，因而會大大的提升混合程式碼與標記的複雜度，這個方法也只能在執行期才能夠以視覺化的方式測試，無法在設計時期視覺化，其他的開發人員總是使用原有的 ASP 方法（即`<!-- #include -->` 指令）來把每個網頁需要的部份包到網頁中，防止在每個網頁中都要撰寫相同的導覽程式碼。

在 ASP.NET 2.0 中，推出了**母板頁面 (master page)**的概念\[13\]，它可以讓開發人員先行定義外觀版型 (\*.master)，再使用它來套用實際執行的網頁，網頁與主版頁面之間以 ContentPlaceHolder 的 ID 做連結，以套用正確的內容到保留區（即由 ContentPlaceHolder 包住的區域）中，開發人員也可以定義在保留區沒有套用時需要顯示的預設內容。在 ASP.NET 3.5 中更進一步的支援設計時期的巢狀主版頁面 (nested master pages)，以及把網頁的 HEAD 區塊納入 ContentPlaceHolder 的範圍。

與主版頁面相關的，還有**主題(Theme)**以及**面板(skin)**技術\[14\]，這兩個技術允許開發人員或設計人員自行定義網頁的樣式設定以及套用的樣式支援，每個主題中可以包含數個面板檔，這些面板檔決定了控制項要輸出時套用的樣式，開發人員則可以利用主題來決定不同的外觀要使用的樣式。

ASP.NET 也允許在應用程式中動態的變更主版頁面與主題，但必須要在頁面的 PreInit 事件常式設定。

``` csharp
void Page_PreInit(Object sender, EventArgs e)
{
    Page.MasterPageFile = "~/NewMaster.master";
    Page.Theme = "MyTheme";
}
```

## 編譯模型

ASP.NET 在 1.x 時，使用的是組件為主的編譯方式，一個網頁只會產生一個組件，這個方式最大的優點，就是可以自由定義命名空間，且在部署應用程式時會比較方便，但由於 ASP.NET 1.x 所處的時代，如果網站是有許多程式碼的情況下（即 DLL 檔很大），載入的速度會變慢，且佔用記憶體的量會很多，當時的記憶體價格也尚未降到現在的水準。因此在 ASP.NET 2.0 開始，另外提供了一個**預先編譯**(Pre-compilation) 的編譯模型，這個編譯方法會將每個網頁都各自編譯成一個組件，其檔案名稱會是 App_\[亂數字串\].dll 命名，在編譯時期由 ASP.NET Pre-compilation 工具（aspnet_compiler.exe）給定，優點是可以不必載入過量的程式碼到記憶體中，但缺點則是無法自訂命名空間，而且在更新時必須要更新所有的 DLL 檔以及網頁等，否則會造成名稱不一致，讓 DLL 無法被載入的問題。

早期 ASP.NET 2.0 僅提供預先編譯模式，讓它的缺點很快的被暴露出來，因此微軟也為 ASP.NET 2.0 開發了沿用 ASP.NET 1.x 的編譯模型的工具：Web Application Project，在 Visual Studio 2008 中開始內建，至此，ASP.NET 支援兩種編譯模式的架構抵定。

## 安全性支援

ASP.NET 的安全性支援分為**驗證 (Authentication)**與**授權 (Authorization)**兩個部份。

### 驗證

ASP.NET 的驗證方式有三種\[15\]：

  - **Windows 驗證**：由 IIS 目前執行的帳戶，或者是使用者模擬 (user impersonate) 帳戶的方式進行驗證。
  - **表單驗證**：由表單的資料提供驗證，開發人員自訂驗證邏輯，並交由 ASP.NET 表單驗證工具寫入驗證憑證，以進行授權。
  - **Passport 驗證**：在 ASP.NET 1.x 中，連接[Windows Live ID](https://zh.wikipedia.org/wiki/Windows_Live_ID "wikilink")（當時的舊稱為Microsoft Passport）服務以進行驗證。

### 授權

ASP.NET 的授權方式有兩種\[16\]：

  - **檔案授權**：由 ASP.NET 檢查檔案的 [存取控制表](https://zh.wikipedia.org/wiki/存取控制表 "wikilink") (ACL) 來授權存取權限。
  - **URL授權**：由開發人員設定的 URL 來給予權限。

一個 URL 授權的設定範例如下：

``` xml
<authorization>
  <allow users="Kim"/>
  <allow roles="Admins"/>
  <deny users="John"/>
  <deny users="?"/>
</authorization>
```

## Web Service支援

ASP.NET 1.0 開始支援 [Web Service](https://zh.wikipedia.org/wiki/Web_Service "wikilink") 的開發，是微軟在原生平台上支援 Web Service 發展的第一個實作品，但它卻不是微軟的第一個 Web Service 開發工具實作品\[17\]，.NET Framework 中提供了一個 WSDL.exe，可以連接 Web Service 下載[WSDL](../Page/WSDL.md "wikilink")定義檔，並產生一個 Proxy Class 的原始碼，供用戶端應用程式使用，若是使用 Visual Studio 開發的話，這個動作會由「加入 Web 參考」的動作在背後處理掉。

ASP.NET Web Service 的發展只是平台的基礎，微軟在 Web Service 的開發上提供持續的支援，尤其是在 [WS-I](https://zh.wikipedia.org/wiki/WS-I "wikilink") (Web Service Interoperability) 組織成立後，為符合 WS-I 的 Web Service 標準，微軟開發了強化 Web Service 的增強套件 Web Service Enhancement (WSE)，最新版本為 3.0 版（搭配 ASP.NET 2.0），可支援許多 WS-I 的標準。

由於 [Windows Communication Foundation](https://zh.wikipedia.org/wiki/Windows_Communication_Foundation "wikilink") 的推出，微軟將 Web Service 的發展重心移到 WCF 上，原有的 ASP.NET Web Service 即給定了一個名稱：**ASMX Web Service**。

## 擴充功能

ASP.NET 在 2.0 版時，功能已大致底定，成為 Web 應用程式的基礎架構，微軟開始在 ASP.NET 2.0 上開發擴充的功能，包括 AJAX 的支援、[MVC](../Page/MVC.md "wikilink")架構的支援以及更容易開發出資料庫應用的架構。

### ASP.NET AJAX

ASP.NET AJAX 是微軟發展的 AJAX Framework，讓 ASP.NET 的開發人員得以用很簡單的方式就可以開發出支援 AJAX (AJAX-enabled) 的應用程式，包含用戶端指令碼的支援，以及伺服器端的連結等等。

### ASP.NET MVC Framework

ASP.NET MVC Framework 是微軟基於 MVC (Model-View-Controller) 架構所開發的架構，讓應用程式各個模型可以在 MVC 架構下運行。

  - **View**：負責顯示資料以及使用者介面，在 ASP.NET MVC 架構下，View 可以支援 REST 樣式的 URL。
  - **Model**：負責定義資料的儲存，此部份可以由 [LINQ](https://zh.wikipedia.org/wiki/LINQ "wikilink") to SQL 與 [ADO.NET Entity Framework](https://zh.wikipedia.org/wiki/ADO.NET_Entity_Framework "wikilink") 來代替。
  - **Controller**：負責處理 View 和 Model 之間的聯繫。

ASP.NET MVC Framework 也支援[以測試驅動的開發模式](../Page/测试驱动开发.md "wikilink") (Test-Driven Development)。

### ASP.NET Dynamic Data Framework

ASP.NET Dynamic Data Framework 是微軟在 ASP.NET 3.5 中開發的一組類別庫，封裝在 System.Web.DynamicData 命名空間中，並且配合 ASP.NET Routing Model（網頁繞送功能）讓開發人員可以很簡單的開發出基於 [LINQ](https://zh.wikipedia.org/wiki/LINQ "wikilink") to SQL 或是 [ADO.NET Entity Framework](https://zh.wikipedia.org/wiki/ADO.NET_Entity_Framework "wikilink") 資料模型的資料庫應用程式。

### ASP.NET Routing

ASP.NET Routing Model（官方譯名為 ASP.NET 路由）是一個基於[REST規格下的](https://zh.wikipedia.org/wiki/REST "wikilink") URL 對應機制，開發人員可以在伺服器端設定 URL 的格式，使用者可以用由開發人員定義的 URL 格式瀏覽網頁，ASP.NET 會自動將 URL 轉換成為內部的 URL 格式，雖然它和 [URL Rewriting](https://zh.wikipedia.org/wiki/URL_Rewriting "wikilink") 很像，但微軟認為 ASP.NET Routing 不是 URL Rewriting\[18\]。

### Silverlight

Silverlight 是微軟的新一代[RIA技術](https://zh.wikipedia.org/wiki/RIA "wikilink")，ASP.NET 3.5 Service Pack 1 (SP1) 中加入了對 Silverlight 2.0 的 ASP.NET 伺服器端支援，包含：

  - **Silverlight控制項**：讓伺服器端可以產生支援 Silverlight 的物件標記，以及自訂參數等。
  - **Media控制項**：讓伺服器端輸出以 Silverlight 為主的串流影音 (streaming media) 播放器。

## 開發工具

目前已有數個工具可支援 ASP.NET 應用程式的開發。

  - [Visual Web Developer 2008 Express Edition](https://zh.wikipedia.org/wiki/Visual_Studio_Express "wikilink")（免費）或 [Visual Studio 2008](https://zh.wikipedia.org/wiki/Visual_Studio "wikilink") (ASP.NET 2.0/3.5)\[19\]
  - [Visual Web Developer 2005 Express Edition](https://zh.wikipedia.org/wiki/Visual_Studio_Express "wikilink")（免費）或 [Visual Studio 2005](https://zh.wikipedia.org/wiki/Visual_Studio "wikilink") (ASP.NET 2.0)
  - [Visual Studio .NET](https://zh.wikipedia.org/wiki/Visual_Studio_.NET "wikilink") (ASP.NET 1.x)
  - [Delphi 2006](../Page/Delphi.md "wikilink")
  - [Macromedia HomeSite](https://zh.wikipedia.org/wiki/Macromedia_HomeSite "wikilink") 5.5 (For ASP Tags)
  - [Microsoft Expression Web](https://zh.wikipedia.org/wiki/Microsoft_Expression_Web "wikilink")，[Microsoft Expression Studio](../Page/Microsoft_Expression_Studio.md "wikilink") 工具集的一部份
  - [Microsoft SharePoint Designer](../Page/Microsoft_SharePoint_Designer.md "wikilink")
  - [MonoDevelop](../Page/MonoDevelop.md "wikilink")（免費／[開放原始碼](https://zh.wikipedia.org/wiki/開放原始碼 "wikilink")）
  - [SharpDevelop](../Page/SharpDevelop.md "wikilink")（免費／[開放原始碼](https://zh.wikipedia.org/wiki/開放原始碼 "wikilink")）
  - [Eiffel for ASP.NET](https://web.archive.org/web/20061017130147/https://www.eiffel.com/downloads/asp.net.html)（免費）
  - WebMatrix 3（免費）
  - Adobe Dreamweaver CC。

## 版本

在一台计算机上，查看[Windows注册表的](https://zh.wikipedia.org/wiki/Windows_Registry "wikilink")

`   HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\NET Framework Setup\NDP\v4\Full`

其Version节点显示的就是所安装的ASP.NET的版本号。

<table>
<thead>
<tr class="header">
<th><p>日期</p></th>
<th><p>版本</p></th>
<th><p>說明</p></th>
<th><p>新功能</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>2002年1月16日</p></td>
<td><p>1.0</p></td>
<td><p>與<a href="https://zh.wikipedia.org/wiki/Visual_Studio_.NET" title="wikilink">Visual Studio .NET一起發行的第一個版本</a></p></td>
<td><ul>
<li><a href="https://zh.wikipedia.org/wiki/物件導向" title="wikilink">物件導向的Web應用程開發</a>，支援<a href="https://zh.wikipedia.org/wiki/繼承" title="wikilink">繼承</a>、<a href="https://zh.wikipedia.org/wiki/多型" title="wikilink">多型與其他標準</a><a href="https://zh.wikipedia.org/wiki/物件導向程式設計" title="wikilink">物件導向程式設計的功能</a>。</li>
<li>開發人員不再需要使用 Server.CreateObject(...)，讓早期繫結與型別安全變得可能。</li>
<li>以<a href="https://zh.wikipedia.org/wiki/Microsoft_Windows" title="wikilink">Microsoft Windows程式設計為基礎</a>，開發人員能夠使用在Web Server上使用的DLL類別庫來建立許多能夠做到比只簡單的輸出 HTML 更多的魯棒性 (robust) 應用程式（例如<a href="https://zh.wikipedia.org/wiki/例外處理" title="wikilink">例外處理功能</a>）。</li>
</ul></td>
</tr>
<tr class="even">
<td><p>2003年4月24日</p></td>
<td><p>1.1</p></td>
<td><p>與<a href="../Page/Windows_Server_2003.md" title="wikilink">Windows Server 2003和</a><a href="https://zh.wikipedia.org/wiki/Visual_Studio_.NET_2003" title="wikilink">Visual Studio .NET 2003一起發表</a>。</p></td>
<td><ul>
<li>行動裝置控制項。</li>
<li>自動化輸入驗證。</li>
</ul></td>
</tr>
<tr class="odd">
<td><p>2005年11月7日</p></td>
<td><p>2.0</p></td>
<td><p>研發代號為<a href="https://zh.wikipedia.org/wiki/Whidbey" title="wikilink">Whidbey</a>，和<a href="https://zh.wikipedia.org/wiki/Visual_Studio_2005" title="wikilink">Visual Studio 2005</a>、<a href="../Page/Microsoft_Visual_Studio_Express.md" title="wikilink">Visual Web Developer Express與</a><a href="https://zh.wikipedia.org/wiki/Microsoft_SQL_Server" title="wikilink">SQL Server 2005一起發表</a>。</p></td>
<td><ul>
<li>新的資料控制項（GridView、FormView、DetailsView）</li>
<li>新的宣告式資料存取技術（SqlDataSource、ObjectDataSource 與 XmlDataSource 控制項）</li>
<li>導覽控制項（SiteMap、Menu、TreeView）</li>
<li>主版頁面 (Master Page)</li>
<li>登入控制項</li>
<li>主題</li>
<li>表皮 (skin)</li>
<li>Web 部件 (Web Part)</li>
<li>個人化服務 (Profile)</li>
<li>全功能的預先編譯能力</li>
<li>全新的當地語系化技術</li>
<li>支援<a href="../Page/64位元.md" title="wikilink">64位元</a>平台</li>
<li>提供者類別模式</li>
</ul></td>
</tr>
<tr class="even">
<td><p>2007年11月19日</p></td>
<td><p>3.5</p></td>
<td><p>與<a href="https://zh.wikipedia.org/wiki/Visual_Studio_2008" title="wikilink">Visual Studio 2008和</a><a href="../Page/Windows_Server_2008.md" title="wikilink">Windows Server 2008一起發表</a></p></td>
<td><ul>
<li>新資料控制項（ListView、DataPager）</li>
<li><a href="../Page/ASP.NET_AJAX.md" title="wikilink">ASP.NET AJAX</a> 內含到.NET Framework，成為.NET Framework的一部份。</li>
<li>提供支援 <a href="https://zh.wikipedia.org/wiki/Language_Integrated_Query" title="wikilink">LINQ</a> 的 LinqDataSource 控制項。</li>
</ul></td>
</tr>
<tr class="odd">
<td><p>2008年8月11日</p></td>
<td><p>3.5 Service Pack 1<ref>{{cite web</p></td>
<td><p>url=<a href="http://www.asp.net/downloads/3.5-SP1/readme/">http://www.asp.net/downloads/3.5-SP1/readme/</a></p></td>
<td><p>title=ASP.NET in .NET 3.5 Service Pack 1</p></td>
</tr>
<tr class="even">
<td><p>2010年4月12日</p></td>
<td><p>4.0</p></td>
<td><p>與<a href="https://zh.wikipedia.org/wiki/Visual_Studio" title="wikilink">Visual Studio 2010一起發表</a></p></td>
<td><ul>
<li>配合<a href="https://zh.wikipedia.org/wiki/.NET_Framework" title="wikilink">.NET Framework 4.0讓Web應用程式具有如並列運算函式庫</a>(Parallel Library)等新功能。</li>
<li><a href="https://zh.wikipedia.org/wiki/ASP.NET_MVC" title="wikilink">ASP.NET MVC 2.0</a></li>
<li><a href="https://zh.wikipedia.org/wiki/jQuery" title="wikilink">jQuery完全整合與</a><a href="../Page/ASP.NET_AJAX.md" title="wikilink">ASP.NET AJAX</a> Client Library 強化，以及 AJAX CDN 的支援。</li>
<li>ASP.NET 的 Render Compatibility (3.5以前版本或4.0版)，可控制許多 ASP.NET Web 控制項的繪製行為，以配合標準 HTML 與 jQuery 的處理。</li>
<li><a href="https://zh.wikipedia.org/wiki/SEO" title="wikilink">SEO的支援</a>。</li>
<li>自訂快取提供者 (Extensible Output Cache)。</li>
<li>QueryExtender 的支援。</li>
<li>CSS 控制行為的變更。</li>
<li>自訂的 Client ID 輸出。</li>
<li>ViewState 的控制。</li>
<li>配合 Visual Studio 2010 的 Web Deploy 工具。</li>
<li>Entity Framework 4.0 的支援。</li>
<li>Dynamic Data Framework 與 Chart Control 內建至核心中。</li>
</ul></td>
</tr>
<tr class="odd">
<td><p>2012年8月15日</p></td>
<td><p>4.5</p></td>
<td><p>與<a href="https://zh.wikipedia.org/wiki/Visual_Studio" title="wikilink">Visual Studio 2012一起發表</a></p></td>
<td></td>
</tr>
<tr class="even">
<td><p>2013年10月17日</p></td>
<td></td>
<td><p><a href="https://zh.wikipedia.org/wiki/Visual_Studio_2013" title="wikilink">Visual Studio 2013</a>[20]发布用于<a href="https://zh.wikipedia.org/wiki/Windows_Server_2012_R2" title="wikilink">Windows Server 2012 R2与</a><a href="../Page/Windows_8.1.md" title="wikilink">Windows 8.1</a></p></td>
<td><ul>
<li><a href="https://zh.wikipedia.org/wiki/Bootstrap_(front-end_framework)" title="wikilink">Bootstrap</a> 3.0</li>
<li>Web API 2: <a href="https://zh.wikipedia.org/wiki/OAuth" title="wikilink">OAuth</a> 2.0, <a href="https://zh.wikipedia.org/wiki/Open_Data_Protocol" title="wikilink">OData改进</a>, <a href="https://zh.wikipedia.org/wiki/Cross-origin_resource_sharing" title="wikilink">CORS</a></li>
<li><a href="https://zh.wikipedia.org/wiki/ASP.NET_MVC" title="wikilink">MVC</a> 5: Attribute routing, authentication filters，filter overrides</li>
<li><a href="../Page/Entity_Framework.md" title="wikilink">EF</a> 6</li>
<li><a href="../Page/SignalR.md" title="wikilink">SignalR</a></li>
<li><a href="https://zh.wikipedia.org/wiki/Open_Web_Interface_for_.NET" title="wikilink">OWIN</a></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>2014年5月5日[21]</p></td>
<td></td>
<td></td>
<td><ul>
<li>更高可靠性的HTTP header检查与修改方法</li>
<li>新的方式调度背景异步worker任务</li>
</ul></td>
</tr>
<tr class="even">
<td><p>2015年7月29日[22]</p></td>
<td></td>
<td><p>发布于[23]<a href="https://zh.wikipedia.org/wiki/Visual_Studio_2015" title="wikilink">Visual Studio 2015</a>[24]与<a href="../Page/Entity_Framework.md" title="wikilink">EF</a> 7预览版用于<a href="../Page/Windows_Server_2016.md" title="wikilink">Windows Server 2016与</a><a href="../Page/Windows_10.md" title="wikilink">Windows 10</a></p></td>
<td><ul>
<li><a href="https://zh.wikipedia.org/wiki/HTTP/2" title="wikilink">HTTP/2支持运行于</a> Windows 10</li>
<li>更多的异步任务返回API</li>
</ul></td>
</tr>
<tr class="odd">
<td><p>2015年11月30日[25]</p></td>
<td></td>
<td></td>
<td></td>
</tr>
<tr class="even">
<td><p>2016年8月2日[26]</p></td>
<td></td>
<td></td>
<td><ul>
<li>改进的异步支持(输出cache与session providers)</li>
</ul></td>
</tr>
<tr class="odd">
<td><p>2017年4月11日[27]</p></td>
<td></td>
<td><p>包含在Windows 10 Creators Update[28]</p></td>
<td><ul>
<li>操作系统支持TLS协议</li>
</ul></td>
</tr>
<tr class="even">
<td><p>2017年10月17日[29]</p></td>
<td></td>
<td><p>包含在Windows 10 Fall Creators Update.[30]</p></td>
<td><ul>
<li>改进可访问性</li>
<li>Value tuple 类型序列化</li>
<li>SHA-2 支持</li>
</ul></td>
</tr>
<tr class="odd">
<td><p>2018年5月1日[31]</p></td>
<td></td>
<td></td>
<td></td>
</tr>
<tr class="even">
<td><p>2019年4月18日[32]</p></td>
<td></td>
<td><p>包含在 Windows 10 May 2019 Update</p></td>
<td><p>修复了ASP.NET的10个bugs</p></td>
</tr>
<tr class="odd">
<td><p>2015年11月18日</p></td>
<td></td>
<td><p>这一版本后来从ASP.NET分开，改称<a href="../Page/ASP.NET_Core.md" title="wikilink">ASP.NET Core</a> 1.0.[33]</p></td>
<td><p>一个全新项目有不同的开发原则与目标。</p></td>
</tr>
<tr class="even">
<td></td>
<td></td>
<td></td>
<td></td>
</tr>
</tbody>
</table>

## 參見

  - [ASP.NET Core](../Page/ASP.NET_Core.md "wikilink")
  - [.NET Framework](https://zh.wikipedia.org/wiki/.NET_Framework "wikilink")
  - [Visual Studio](https://zh.wikipedia.org/wiki/Visual_Studio "wikilink")
  - [Microsoft Silverlight](https://zh.wikipedia.org/wiki/Microsoft_Silverlight "wikilink")
  - [ASP](../Page/Active_Server_Pages.md "wikilink")
  - [ADO.NET](../Page/ADO.NET.md "wikilink")
  - [Web Service](https://zh.wikipedia.org/wiki/Web_Service "wikilink")
  - [PHP](../Page/PHP.md "wikilink")
  - [JSP](../Page/JSP.md "wikilink")

## 參考資料

<div class="references-small">

<references />

</div>

## 外部連結

  - [ASP.NET Overview](http://msdn.microsoft.com/zh-tw/library/4w3ex9c2.aspx)

  - [ASP.NET Official Site](http://www.asp.net/)

  - [ASP.NET Developer Center on MSDN](http://msdn.microsoft.com/en-us/asp.net/default.aspx)

  - [ASP.NET Web Blogs](http://weblogs.asp.net/)

[Category:.NET](https://zh.wikipedia.org/wiki/Category:.NET "wikilink") [Category:.NET编程语言](https://zh.wikipedia.org/wiki/Category:.NET编程语言 "wikilink") [Category:微軟API](https://zh.wikipedia.org/wiki/Category:微軟API "wikilink") [Category:ASP.NET](https://zh.wikipedia.org/wiki/Category:ASP.NET "wikilink")

1.  [MONO Project](http://www.mono-project.com/Main_Page)
2.  [Architecture Journal Profile: Scott Guthrie](http://msdn.microsoft.com/en-us/library/bb266332.aspx)
3.  若是 IIS 5.x 時，則是轉交給網站的執行緒，IIS 6.0 以後的版本才有 Worker Process 的工作模型
4.  [ASP.NET Page Lifecycle Overview](http://msdn.microsoft.com/en-us/library/ms178472.aspx)
5.  [工作階段狀態模式](http://msdn.microsoft.com/zh-tw/library/ms178586.aspx)
6.  [ASP.NET 網站巡覽](http://msdn.microsoft.com/zh-tw/library/ms227558.aspx)
7.  [使用成員資格管理使用者](http://msdn.microsoft.com/zh-tw/library/tw292whz.aspx)
8.  [使用角色管理授權](http://msdn.microsoft.com/zh-tw/library/9ab2fxh0.aspx)
9.  [ASP.NET 設定檔屬性概觀](http://msdn.microsoft.com/zh-tw/library/2y3fs9xs.aspx)
10. [Web 組件個人化概觀](http://msdn.microsoft.com/zh-tw/library/z36h8be9.aspx)
11. [ASP.NET 健康監視事件概觀](http://msdn.microsoft.com/zh-tw/library/bb398933.aspx)
12. [HTTP 處理常式和 HTTP 模組概觀](http://msdn.microsoft.com/zh-tw/library/bb398986.aspx)
13. [ASP.NET 主版頁面](http://msdn.microsoft.com/zh-tw/library/18sc7456.aspx)
14. [ASP.NET 佈景主題和面板概觀](http://msdn.microsoft.com/zh-tw/library/ykzx33wh.aspx)
15. [ASP.NET 驗證](http://msdn.microsoft.com/zh-tw/library/eeyk640h.aspx)
16. [ASP.NET 授權](http://msdn.microsoft.com/zh-tw/library/wce3kxhd.aspx)
17. 早期還有一個在 ASP 上發展 Web Service 的工具，稱為 SOAP Toolkit。
18. [ASP.NET 路由](http://msdn.microsoft.com/zh-tw/library/cc668201.aspx)
19.
20.
21.
22.
23.
24.
25.
26.
27.
28.
29.
30.
31. [Microsoft .NET Framework 4.7.2 正式版发布 2018年05月01日 cnBeta.COM](https://www.cnbeta.com/articles/soft/721649.htm)
32. [Announcing the .NET Framework 4.8](https://devblogs.microsoft.com/dotnet/announcing-the-net-framework-4-8/)
33.