> 本文内容由[Apache Axis2](https://zh.wikipedia.org/wiki/Apache_Axis2)转换而来。


**Apache Axis2**是一個[Web服務的核心支援引擎](https://zh.wikipedia.org/wiki/Web服務 "wikilink")。AXIS2對舊有的AXIS重新設計及重寫，並提供兩種語言[Java](../Page/Java.md "wikilink")及[C的開發版本](https://zh.wikipedia.org/wiki/C語言 "wikilink")。

事實上AXIS2 不只為WEB應用程式提供Web服務的介面，而且它也可以作為一個單獨的伺服器看待，而且很簡單就能跟[Apache Tomcat整合](../Page/Apache_Tomcat.md "wikilink")，目前AXIS2的最新版本是1.6.2。

## AXIS2項目

Apache AXIS2是一個 [SOAP](https://zh.wikipedia.org/wiki/SOAP "wikilink")（"Simple Object Access Protocol 簡單物件存取恊定"）的實作並已經提交 [W3C](https://zh.wikipedia.org/wiki/W3C "wikilink")。

來自 W3C 的規格：

"SOAP是一個輕量級協議使一個有結構好的訊息（well-formated）在分佈式環境裡裡互相交換，它是基於XML協議 包括三部份的： 1 定義一個信封框架描述信封內的是什麼消息和怎麼處理它。 2 一套編碼規則使應用程式能夠定義datatypes以表達訊息。 3 以及如何恊調及說明遠端程式調用和作出回應。"

這個AXIS2項目是基於Apache SOAP計劃。

## 為什麼要AXIS2

新的架構是在2004年8月的首腦會議在斯里蘭卡首都科倫坡提出的。新結構的 axis2 是建築在axis1.x 比較axis1, Axis2以更加靈活，高效和更好的配置。一些好的觀念亦從axis 1.X 被儲存在新的結構中。阿帕奇 axis2 不僅支援 SOAP1.1和 SOAP1.2，而且它也對於REST風格的Web服務也有綜合性的支援，相同的業務邏輯實作可以同步利用WS\*式的介面以及REST介面。

阿帕奇axis2較舊的版本是更有效率，更加模組化和更多的XML類型。它是經過精心設計，支援輕鬆添加插件"模組module"，以提升現有的功能特徵，例如安全性和可靠性，模組現有或正在發展的包括：

\- WS 可靠訊息服務由 Apache sandesha2 支援 - WS-Coordination and WS-AtomicTransaction由 Apache Kandula2 支援 - WS-Security 由 Apache Rampart 支援 - WS-Addressing 已包括作axis2 在為核心模組

Axis2有許多新的特點，以加強對行業規範的實施，主要點如下：

  - 速度：Axis2使用自己的對象模型和stax（串流API的XML）的來解析，比較早版本的Apache AXIS2以達到更明顯的速度。
  - 低記憶體：Axis2設計保持了低記憶體。
  - AXIOM: Axis2 訊息處理有自己的輕量對象模型AXIOM,，具有可擴展性，高性能及開發方便的優點。
  - 熱部署：Axis2能夠在已建立和運轉時有能力部署Web服務。 換言之，新的服務可以添加到系統無需關閉伺服器，乾脆把所需的 WebService的檔案放入服務目錄，版本和部署模型將自動部署服務以供使用。
  - 異步Web服務：Axis2現在支援異步Web服務和異步Web服務調用並使用非阻塞的客戶端。
  - MEP支援：Axis2 現在是簡便與靈活的支援消息交換模式（MEP），內置支援WSDL的2.0定義的基本MEP。
  - 靈活性-Axis2構築給開發人的發展完全自由地插入延伸到引擎定製頭處理，系統管理，以及任何你可以想像的東西。
  - 穩定：Axis2界定一套出版介面其變化對比AXIS可說改變相對比較慢。
  - 面向組件的部署-你可以很容易界定重用網路處理器，實施的共同模式處理您的請求，或發給你的夥伴。
  - WSDL的支援：axis2支援WebService描述語言（版本1.1和2.0），讓您輕鬆地建立STUB來連結遠端服務，並自動向其他機器說明你的服務部署。
  - 新增：Web Services 的多個技術已被納入， 包括 WSS4J 的保安技術(Apache Rampart),Sandesha 的可靠訊息服務，Kandula一個WEB服務的協調集成，WEB服務自動傳送。
  - 組合和擴展：模組用來加強AXIS2延展性，但模組不可以熱部署，因為模組改變AXIS2整體行為及制度。

## 相關技術

  - [Apache Axis](../Page/Apache_Axis.md "wikilink")
  - [Web服務](https://zh.wikipedia.org/wiki/Web服務 "wikilink")
  - [Java Web 服務開發架構](https://zh.wikipedia.org/wiki/Java_Web_服務開發架構 "wikilink") - web services framework
  - [XML 網路服務介面](https://zh.wikipedia.org/wiki/XML_網路服務介面 "wikilink") - RPC/web services framework
  - [Web 服務引用架構](https://zh.wikipedia.org/wiki/Web_服務引用架構 "wikilink") - Java API for invoking Web services

## 外部連結

  - [Apache AXIS 主頁](http://ws.apache.org/axis/) Apache軟體基金會
  - [Apache Axis2/Java](http://ws.apache.org/axis2/) Apache軟體基金會
  - [Apache Axis2/C](http://ws.apache.org/axis2/c) Apache軟體基金會

[Category:Apache软件基金会](https://zh.wikipedia.org/wiki/Category:Apache软件基金会 "wikilink") [Category:Java企业平台](https://zh.wikipedia.org/wiki/Category:Java企业平台 "wikilink") [Category:Web服务规范](https://zh.wikipedia.org/wiki/Category:Web服务规范 "wikilink") [Category:Web服务](https://zh.wikipedia.org/wiki/Category:Web服务 "wikilink")