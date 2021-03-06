> 本文内容由[ASP.NET Core MVC](https://zh.wikipedia.org/wiki/ASP.NET_Core_MVC)转换而来。


**ASP.NET Core MVC** 是 [ASP.NET Core](../Page/ASP.NET_Core.md "wikilink") 內，提供給 Web 應用程式開發的框架，它可視為 [ASP.NET MVC](https://zh.wikipedia.org/wiki/ASP.NET_MVC "wikilink") 的後繼版本，其主要功能均衍生自 ASP.NET MVC，但它除了基於 ASP.NET Core 外，也將 ASP.NET MVC 與類似平台進行了整合，例如負責 View 的 ASP.NET Web Pages 以及負責 [RESTful](https://zh.wikipedia.org/wiki/REST "wikilink") API 的 ASP.NET Web API，都與 ASP.NET Core MVC 的核心合併，因此在 ASP.NET Core MVC 中將可同時並存 MVC 網頁以及 RESTful API。

## 相關組件

ASP.NET Core MVC 包含了下列組件，基於 .NET Core 的精神，只有需要用到的才需要加入參考 (於 project.json)，因此開發者可以自由選擇，而不必把所有的組件都加進來。

| 組件                                        | 功能                                                                       |
| ----------------------------------------- | ------------------------------------------------------------------------ |
| Microsoft.AspNetCore.Mvc                  | ASP.NET Core MVC 引用套件                                                    |
| Microsoft.AspNetCore.Mvc.Abstractions     | ASP.NET Core MVC 功能的抽象層                                                  |
| Microsoft.AspNetCore.Mvc.ApiExplorer      | ASP.NET Core MVC 的 API 文件支援                                              |
| Microsoft.AspNetCore.Mvc.Core             | ASP.NET Core MVC 核心組件                                                    |
| Microsoft.AspNetCore.Mvc.Cors             | 提供 Web API 所需要的 [CORS](https://zh.wikipedia.org/wiki/CORS "wikilink") 能力 |
| Microsoft.AspNetCore.Mvc.DataAnnotations  | MVC 所需的資料標示 (Data Annotation) 功能                                         |
| Microsoft.AspNetCore.Mvc.Formatters.Json  | MVC/Web API 所需的 JSON 序列化器                                                |
| Microsoft.AspNetCore.Mvc.Formatters.Xml   | MVC/Web API 所需的 XML 序列化器                                                 |
| Microsoft.AspNetCore.Mvc.Localization     | MVC 應用程式本地化支援                                                            |
| Microsoft.AspNetCore.Mvc.Razor            | MVC Razor 的核心類別庫 (若要在 MVC 中使用 Razor 就必須參考此組件)                            |
| Microsoft.AspNetCore.Mvc.Razor.Host       | MVC Razor 的執行期引擎                                                         |
| Microsoft.AspNetCore.Mvc.TagHelpers       | MVC Tag Helper 的核心類別庫                                                    |
| Microsoft.AspNetCore.Mvc.ViewFeatures     | MVC View 功能的類別庫 (Controller 類別的實作在此)                                     |
| Microsoft.AspNetCore.Mvc.WebApiCompatShim | Web API 相容套件                                                             |
| Microsoft.AspNetCore.Razor                | Razor 的核心類別庫                                                             |

## 基礎建設

ASP.NET Core MVC 採用 ASP.NET Core 作為基礎，因此享有內建的相依注入能力 (Dependency Injection)，ASP.NET Core MVC 本身也是 ASP.NET Core 的服務之一，因此必須要在 ASP.NET Core 的起始類別中註冊並使用 MVC，才可以享有 MVC 的功能。下列例子即為在一個 ASP.NET Core 的程式的起始類別 (通常被命名為 Startup) 中註冊並啟用 ASP.NET Core MVC 的程式碼\[1\]：

``` csharp numberLines
public void ConfigureServices(IServiceCollection services)
{
    // 加入 ASP.NET Core MVC 服務
    services.AddMvc();
}

public void Configure(IApplicationBuilder app, IHostingEnvironment env, ILoggerFactory loggerFactory)
{
    // ...
    // 啟用 ASP.NET Core MVC
    app.UseMvc(routes =>
    {
        routes.MapRoute(
            name: "default",
            template: "{controller=Home}/{action=Index}/{id?}");
    });
}
```

註冊 ASP.NET Core MVC 服務後，ASP.NET Core 會自動將 MVC 的執行引擎加入 ASP.NET Core 的管線式相依注入 (Pipeline-based Dependency Injection) 的服務清單內，以開始提供 MVC 的相關服務。

## 路由

ASP.NET Core MVC 強化了 ASP.NET Routing 技術，使其更具彈性，除了原有的由起始類別加入的路由外，亦全面整合了之前在 ASP.NET MVC 5.2 / Web API 2.1 起支援的屬性路由能力 (Attribute Routing)，這表示開發人員不一定需要在起始類別註冊 MVC 時定義路由，只需要在 Controller 內加入路由設定即可，但官方還是建議至少加入預設路由 (default routes)，例如：

``` csharp
app.UseMvc(routes => {
    routes.MapRoute(
       name: "default",
       template: "{controller=Home}/{action=Index}/{id?}");
});
```

## Controller

ASP.NET Core MVC 可同時支援 MVC 本身的功能以及 Web API 的功能，它們都源自相同的 Controller 基底類別，此類別已被重新實作，以支援一般的 View 以及 RESTful API 的回傳值，微軟亦重新定義了 ActionResult 類別，提出新的 IActionResult 介面，但開發人員不一定要回傳 IActionResult 介面，也可以直接回傳 .NET 內建的資料型態，Controller 會自動將它對應到 Content Result。雖然微軟建議以 IActionResult 為傳回型別，但原本的 ActionResult 型別仍然適用。

下列程式是一個標準的 ASP.NET Core MVC Controller 的實作，和 ASP.NET MVC 差異相當小。

``` csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Threading.Tasks;
using Microsoft.AspNetCore.Mvc;

namespace WebApplication18.Controllers
{
    public class HomeController : Controller
    {
        public IActionResult Index()
        {
            return View();
        }

        public IActionResult About()
        {
            ViewData["Message"] = "Your application description page.";

            return View();
        }

        public IActionResult Contact()
        {
            ViewData["Message"] = "Your contact page.";

            return View();
        }

        public IActionResult Error()
        {
            return View();
        }
    }
}
```

## Model

ASP.NET Core MVC 的 Model 與 ASP.NET MVC 上使用的概念類似，官方雖建議使用 [Entity Framework Core](../Page/Entity_Framework_Core.md "wikilink")，但卻不是強制，開發者可以依應用程式自身的需求來定義 Model，也可以將 Model 移到別的類別庫內與其他專案共用。

基於關注點分離的需要，在 MVC 應用程式內會依 View 的需求另外建立單獨的 Model，此類 Model 稱為 View Model，不過 ASP.NET Core MVC 也沒有針對這個做特別的限制。

## View

ASP.NET Core MVC 的 View 除了由 ASP.NET MVC 衍生而來的標準的 View 功能外，另外新增了數項 View 的功能，包含 View Component 以及 Tag Helper。

### View Component

View Component (檢視元件) \[2\] 與原有的 Partial View (部份檢視) 相當類似，MVC 5 也可以利用 Child Action 加上 Partial View 的機制來實作出與 View Component 相同的功能，但基於關注點分離原則，若在 Controller 中加入過多的 Child Action 反而會造成 Controller 職責過重，Controller 的程式碼也會變得肥大，因此 Core MVC 加入這個新功能，每一個 View Component 都是獨立的後端程式，以一對一的方式對應 View。

View Component 基本上可以看做是一個類似 Controller 的元件，它也可以使用像 ViewBag 或 TempData 這樣的功能，不過它是由 View 來喚起的，例如下列程式為 View Component 的範例實作：

``` csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Threading.Tasks;
using Microsoft.AspNetCore.Mvc;

namespace HelloMvc.Components
{
    [ViewComponent(Name = "AddNumber")]
    public class AddNumberComponent : ViewComponent
    {
        public async Task<IViewComponentResult> InvokeAsync(int Number1, int Number2)
        {
            int result = Number1 + Number2;
            ViewBag.N1 = Number1;
            ViewBag.N2 = Number2;
            return View(result);
        }
    }
}
```

View Component 可以由 Controller 喚起 (回傳 ViewComponentResult) 或是由 View 喚起 (使用 Razor 的 Component.InvokeAsync())，例如：

``` html
<div>@await Component.InvokeAsync("AddNumber", new { Number1 = 1, Number2 = 2})</div>
```

### Tag Helper

Tag Helper \[3\]是 ASP.NET Core MVC 加入的最具威力的 View 功能，在還沒有 Tag Helper (即 ASP.NET MVC) 的時候，當 View 所需的功能愈來愈多時，一張 View (cshtml/vbhtml) 會充斥著 Razor 程式碼或是 Partial View 的呼叫，讓整個 View 顯得相當凌亂，而 Tag Helper 所提供的功能就是直接基於 HTML Tag 本身進行處理，不但可以擴充現有的 tag，也可以自訂自己的 tag，例如 ASP.NET MVC 時期的表單，大多會用 @Html.BeginForm() 進行包裝，例如：

``` csharp
@using (Html.BeginForm("Login", "Account", new { returnurl = ViewData["ReturnUrl"] }, FormMethod.Post, new { @class = "form-horizontal" }))
{
  // ...
}
```

但使用了 Tag Helper 之後，View 上的程式碼就可以移除，變成：

``` html
<form asp-controller="Account" asp-action="Login" asp-route-returnurl="@ViewData["ReturnUrl"]" method="post" class="form-horizontal">
...
</form>
```

其中的 asp-controller、asp-action、asp-route-returnurl 即是使用 Tag Helper 擴充而得。

Tag Helper 的實作與 View Component 類似，它要求繼承自 Microsoft.AspNetCore.Razor.TagHelpers 內的 TagHelper 類別，例如：

``` csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Threading.Tasks;
using Microsoft.AspNetCore.Razor.TagHelpers;

namespace HelloMvc.TagHelpers
{
    public class EmailTagHelper : TagHelper
    {
        private const string EmailDomain = "contoso.com";

        // Can be passed via <email mail-to="..." />.
        // Pascal case gets translated into lower-kebab-case.
        public string MailTo { get; set; }

        public override void Process(TagHelperContext context, TagHelperOutput output)
        {
            output.TagName = "a";    // Replaces <email> with <a> tag

            var address = MailTo + "@" + EmailDomain;
            output.Attributes.SetAttribute("href", "mailto:" + address);
            output.Content.SetContent(address);
        }
    }
}
```

然後在 View 中引用這個 Tag Helper (可以在 _ViewImport.cshtml 內引用或是在該 View 中引用)，就可以直接使用自己定義的 Tag 了。

``` html
<div>
    <h4><email mail-to="jason">support</email></h4>
</div>
```

## 相依注入功能

受惠於 ASP.NET Core 的基礎建設，ASP.NET Core MVC 能充份享有基礎建設所支援的相依注入能力，在起始類別中加入對服務的註冊，就能夠在 Controller 與 View 中使用註冊的類別。

例如下列程式會在服務清單中加入一個自訂的類別：

``` csharp
public void ConfigureServices(IServiceCollection services)
{
    services.AddMvc();
    // 註冊服務
    services.AddTransient<IDateTimeIndicator, DefaultDateTimeIndicator>(); // DefaultDateTimeIndicator 實作了 IDateTimeIndicator 介面
}
```

若要在 Controller 中使用這個註冊的服務，可以使用下列三種方式：

  - 建構式注入 (Constructor Injection)：在 Controller 的建構式中加入該服務的參數，當 Controller 被生成時，ASP.NET Core MVC 會由服務清單中取出指定的介面物件。
  - 方法注入 (Method Injection)：在 Controller 的方法中加入 \[FromService\] 的修飾，ASP.NET Core MVC 若發現方法中有這樣的修飾時就會由服務清單中取出指定的介面物件。
  - 屬性注入 (Property Injection)：在 Controller 的屬性以 \[FromService\] 修飾，ASP.NET Core MVC 若發現屬性中有這樣的修飾時就會由服務清單中取出指定的介面物件。

例如：

``` csharp
public class SettingsController : Controller
{
    private readonly SampleWebSettings _settings;

    public SettingsController(IOptions<SampleWebSettings> settingsOptions ) // 注入服務
    {
        _settings = settingsOptions.Value;
    }

    public IActionResult Index()
    {
        ViewData["Title"] = _settings.Title;
        ViewData["Updates"] = _settings.Updates;
        return View();
    }
}
```

若要在 View 中使用，則需要用 @inject 指令指定服務，接著就可以使用此變數來操作服務。

``` html
@using HelloMvc.Services;
@inject IDateTimeIndicator indicator
<html>
    <body>
        ...
        <div>
            <ul>
                <li>@indicator.GetNowIndicator(new DateTime(2016, 5, 7, 0, 0, 0))</li>
                <li>@indicator.GetNowIndicator(new DateTime(2016, 5, 7, 0, 5, 0))</li>
                <li>@indicator.GetNowIndicator(new DateTime(2016, 5, 6, 0, 20, 0))</li>
                <li>@indicator.GetNowIndicator(new DateTime(2016, 5, 5, 0, 0, 0))</li>
            </ul>
        </div>
    </body>
</html>
```

## 參考

<references />

[Category:微軟開發工具](https://zh.wikipedia.org/wiki/Category:微軟開發工具 "wikilink") [Category:ASP.NET](https://zh.wikipedia.org/wiki/Category:ASP.NET "wikilink") [Category:.NET_Core](https://zh.wikipedia.org/wiki/Category:.NET_Core "wikilink") [Category:MVC](https://zh.wikipedia.org/wiki/Category:MVC "wikilink")

1.  [Application Startup](https://docs.asp.net/en/latest/fundamentals/startup.html)
2.  [View Components](https://docs.asp.net/en/latest/mvc/views/view-components.html)
3.  [Introduction to Tag Helpers](https://docs.asp.net/en/latest/mvc/views/tag-helpers/intro.html)