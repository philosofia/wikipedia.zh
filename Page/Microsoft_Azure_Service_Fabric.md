> 本文内容由[Microsoft Azure Service Fabric](https://zh.wikipedia.org/wiki/Microsoft_Azure_Service_Fabric)转换而来。


**Microsoft Azure Service Fabric** 是微軟 Azure 平台上的平台服務之一，它也是基於微軟資源管理架構與基礎建設發展出的新型服務，可用來建置以[微服務](../Page/微服務.md "wikilink")為主的雲端分散式應用程式，而它也將會是 [Microsoft Azure 雲端服務](../Page/Microsoft_Azure_雲端服務.md "wikilink") 的後繼者。Azure 平台上的數個重要服務如 Azure SQL Database、Azure IoT 服務、Azure DocumentDB、Azure Event Hub 等服務都是使用 Service Fabric 作為基礎所開發。

Service Fabric 自 2015 年於 Build 2015 研討會中揭示，並於 2016/3/30 Build 2016 研討會上由 Scott Guthrie 宣佈正式進入 General Availability 階段。

## 架構

Service Fabric 是一個基於 Azure 基礎建設上的平台服務，但它和 Azure 雲端服務最大的差異是，Service Fabric 一開始就有叢集 (Cluster) 的概念，Azure 雲端服務是以虛擬機器為單位，Service Fabric 則是以叢集為單位，每一個叢集依照服務等級會有不同的虛擬機器數量，大小則是看建立叢集時的選擇。

### 運算能量

叢集所使用的虛擬機器的大小與[Microsoft Azure 虛擬機器服務相同](../Page/Microsoft_Azure_虛擬機器服務.md "wikilink")，依照地區與開放的程度可選擇 A、D、DS 或是 G 等級的虛擬機器。

Service Fabric 規定每個叢集最低的虛擬機器數為 3 台 (且會標示成測試用服務)，正式的服務必須要有 5 台\[1\]，叢集的持久性 (Durability) 被劃分成金級 (固定使用 G 級虛擬機器) 與銅級 (可選擇 A、D、DS 等虛擬機器)，可靠性 (Reliability) 則決定了最少的虛擬機器數量。

  - 白金級 (Platinum) 9 台
  - 金級 (Golden) 7 台
  - 銀級 (Silver) 5 台
  - 銅級 (Bronze) 3 台

當持久性選定後，就只能針對數量來修改，雖然可靠性訂定了下限，但上限則沒有限制，視訂用帳戶的上限來決定 (也就是若想用到 10000 台的話只要聯絡微軟技術支援開放上限就可以)。

Service Fabric 目前使用 Windows Server 作為基礎作業系統，未來可能也會導入 Linux 版本的 Service Fabric 虛擬機器。

### 節點

一個 Service Fabric 叢集可以包含最多三個節點 (Node)，節點的概念和雲端服務的角色類似，它可以個別定義虛擬機器的等級、類型與數量，配置方式也可以自訂。當叢集部署到 Azure 後，每一個節點都會生成指定數量的虛擬機器，並且依照錯誤域 (Fault Domain) 與更新域 (Upgrade Domain) 做隔離配置，而每一個節點會擁有自己的負載平衡器，所有與該節點有關係的虛擬機器網路設定都要由該負載平衡器處理，包含對外的 IP 與可用的 Port 等。

節點的部署是採用虛擬機器擴展集 (VM Scale Set) 的規則進行，每一次的 VM 橫向擴展都會賦與有規則性增長的連接埠，因此若要連到個別的虛擬機器，除了可用 Service Fabric 的 API 外，也可以由 Portal 取得該機器的 Port，再使用遠端桌面連入即可。

## 開發模型

Service Fabric 在概念上有分為有狀態 (Stateful) 以及無狀態 (Stateless) 兩種，而在 API 類型上則分為客座可執行檔 (Guest Executable)、可靠動作者 (Reliable Actor) 以及可靠服務 (Reliable Service) 三種。

客座可執行檔係指 Service Fabric 在啟動服務時啟動的是一個可執行檔，而不是由 Service Fabric API 所開發的應用程式，因此它雖然是放在 Service Fabric 內，但本身並不參與 Service Fabric 裡面的互動，通常也不會使用 Service Fabric 的 API 取得資訊 (例如服務的 Proxy 或是網路位址等)，它就只是單純的可執行檔，通常會作為前端介面，例如 [node.js](https://zh.wikipedia.org/wiki/node.js "wikilink") 網站。客座可執行檔在 Service Fabric 中是以無狀態的概念管理。

可靠動作者是以 Actor Model 的概念開發的，每個應用程式都是一個動作者 (Actor)，每個動作者是一個獨立的單執行緒執行空間，但一個 Service Fabric 內可以有很多個動作者，而且每個動作者之間是隔離的空間，而每個動作者可以被建立出多個執行個體，簡單的說，一個遊戲者 (Gamer) 可以建立出多個動作者，例如與別的遊戲者交談的 Session Actor、遊戲進行的主線 Main Actor、交換訊息的 Messaging Actor 等，而這些動作者可以被多個用戶端所建立，因此等於每個動作者的擁有者都會不同，Service Fabric 叢集內會不斷的生出許多的動作者，而每一個動作者都運行著它自己要做的工作，或是和別的 Actor 交談。

可靠服務則是提供功能的服務，視應用程式需要可劃分成有狀態 (Stateful Service) 與無狀態 (Stateless Service)，這兩者的差異是有狀態的服務可以使用可靠字典 (Reliable Dictionary) 與可靠佇列 (Reliable Queue) 來保存狀態，可靠字典與可靠佇列的可用性與可存取性是由 Service Fabric 進行管理，服務不需要介入，只要使用 Service Fabric API 就能獲取；無狀態的服務則是一般的服務，若它要保存狀態，就要依賴外部的狀態保存機制，例如 Azure Redis Cache。

## 參考

<references />

[Category:微軟](https://zh.wikipedia.org/wiki/Category:微軟 "wikilink") [Category:Microsoft_Azure](https://zh.wikipedia.org/wiki/Category:Microsoft_Azure "wikilink")

1.  [Service Fabric 叢集容量規劃考量](https://azure.microsoft.com/zh-tw/documentation/articles/service-fabric-cluster-capacity/)