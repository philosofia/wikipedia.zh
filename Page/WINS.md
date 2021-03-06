> 本文内容由[WINS](https://zh.wikipedia.org/wiki/WINS)转换而来。


**Windows網際網路名稱服務**（，縮寫**WINS**），是由[微軟公司所發展出來的一種](../Page/微软.md "wikilink")[網路名稱轉換服務](https://zh.wikipedia.org/wiki/網路 "wikilink")，與[DNS類似](../Page/域名系统.md "wikilink")，WINS可以將[NetBIOS](../Page/NetBIOS.md "wikilink")電腦名稱轉換為對應的[IP位址](https://zh.wikipedia.org/wiki/IP位址 "wikilink")。

## 概述

WINS的主要功能如下：

  - 可讓[伺服器電腦變成](https://zh.wikipedia.org/wiki/伺服器 "wikilink") NetBIOS 的名稱伺服器，並且在網路上登錄並解析 WINS 的用戶端電腦名稱，則在[TCP/IP上的](https://zh.wikipedia.org/wiki/TCP/IP "wikilink") NetBIOS 標準協定中加以說明。
  - WINS 主要是一種動態的複寫[資料庫服務](https://zh.wikipedia.org/wiki/資料庫 "wikilink")，在主機上所使用的 NetBIOS 名稱並解析成網路上使用的 IP 位址
  - 其目的用來解決在[路由](../Page/路由.md "wikilink")環境中解析 NetBIOS 名稱的問題，WINS 是 NetBIOS 名稱解析最好的解決方式。
  - WINS 在 Microsoft [Windows Server](../Page/Windows_Server.md "wikilink") 系列中提供這項元件服務的安裝來實行。
  - 與[DNS服務執行的功能類似](https://zh.wikipedia.org/wiki/DNS "wikilink")，不過DNS是將全稱域名(FQDN)（例如 www.abc.com）轉換為IP位址 。

## 解析過程

雖然 WINS 的作用是解析 NetBIOS 名稱，但為了有效地解析名稱，用戶端需能夠動態地新增、移除或更新它們在 WINS 中的名稱。特別是 WINS 網路上的用戶端名稱要如何登錄、更新、釋放及解析。

較舊版的 [Microsoft Windows](https://zh.wikipedia.org/wiki/Microsoft_Windows "wikilink") 作業系統，會使用 NetBIOS 名稱來識別及尋找網路上登錄或解析名稱時，所需要的電腦及其他共用或分組的資源。在 Microsoft 作業系統的舊版中建立網路服務，NetBIOS 名稱是必要需求。雖然 NetBIOS 命名通訊協定可與 [TCP/IP](https://zh.wikipedia.org/wiki/TCP/IP "wikilink") 之外的網路通訊協定搭配使用，但 WINS 是專為支援「經由 TCP/IP 的 NetBIOS」([NetBT](https://zh.wikipedia.org/wiki/NetBT "wikilink")) 而設計的。

WINS 簡化了 TCP/IP 型網路中的 NetBIOS 命名空間的管理。

下列說明 WINS 用戶端及伺服器相關的一系列典型事件。

WINS 的範例：

1.  WINS 用戶端（主機 A）=\> 在WINS 登記 自己的主機名稱及IP
2.  WINS 用戶端（主機 B）=\> 去尋問 A 主機所在位址（IP）
3.  WINS-伺服器回應給（B主機）A 的 IP 位址 (192.168.100.20) 回覆。

此範例中，會發生下列情況：

  - 一般情況下在本機若找不到所對應的NetBIOS名稱與[IP位址時](https://zh.wikipedia.org/wiki/IP位址 "wikilink")，會發佈廣播[封包來通知鄰近的](https://zh.wikipedia.org/wiki/封包 "wikilink")[主機](https://zh.wikipedia.org/wiki/主機 "wikilink")，並且回報該尋問的IP。這個動作如果太過頻繁，會造成內部網路之間封包的碰撞，因此使用WINS 即可減少這類的問題。每次用戶端啟動並加入網路時，都會自動進行 WINS 登錄，所以動態位址設定變更時，WINS 資料庫會自動更新。例如，[DHCP](https://zh.wikipedia.org/wiki/DHCP "wikilink") 伺服器將一個新增或變更的IP 位址發佈到擁有 WINS 功能的用戶端電腦上時，此用戶端的 WINS 資訊就會更新。
  - 這不需要使用者或網路系統管理員手動進行變更，讓使用者可以直接利用電腦名稱來存取網路資源，而不用記憶IP 位址。一般用在Windows的網路環境內使用，並可也減少DNS的負擔。WINS SERVER 並不會做廣播，而是WINS Client向WINS SERVER註冊而WINS SERVER記錄下來這段動作為 WINS CLIENT 用廣播方式找WINS SERVER來註冊，WINS SERVER接受註冊之後，再把自己的位置IP傳給CLIENT端。

WINS [通訊協定根據為](https://zh.wikipedia.org/wiki/通訊協定 "wikilink") RFC 1001 及 1002 中指定的 NetBIOS 名稱服務所定義的通訊協定，並與其相容，所以它可以與這些 RFC 的其他執行方式一起使用。在 WINS 中複寫 NetBIOS 名稱資料是 Microsoft 私有技術，並且不能與其他 NetBIOS 名稱伺服器一起使用。如[Samba](../Page/Samba.md "wikilink") Server。

## WINS 的運作方式

當執行 [Microsoft](https://zh.wikipedia.org/wiki/Microsoft "wikilink") [作業系統的電腦已設定](https://zh.wikipedia.org/wiki/作業系統 "wikilink") WINS [伺服器位址](https://zh.wikipedia.org/wiki/伺服器 "wikilink")（手動或透過 DHCP）來進行其名稱解析時，則預設會使用交互式節點（h-node）作為 NetBIOS 名稱登錄的節點類型，除非已設定另一種 NetBIOS 節點類型。若是 NetBIOS 名稱查詢及解析，它也會使用 h-node 操作，但會稍有不同。

若是 NetBIOS 名稱解析，WINS 用戶端通常會執行下列一般操作步驟來解析名稱：

1.  用戶端會檢查受查詢的名稱是否是它所擁有的本機 NetBIOS 電腦名稱，若查詢遠端名稱的在本機 NetBIOS名稱[快取](https://zh.wikipedia.org/wiki/快取 "wikilink")。遠端用戶端的任何已解析的名稱都放置在此快取中，並在其中保留 10 分鐘。
2.  用戶端將 NetBIOS 查詢轉寄到其已設定的主要 WINS 伺服器中。如果主要 WINS 伺服器無法使用或是沒有名稱的資料項目而無法回答此查詢，用戶端就會依照所列出及設定的順序嘗試連絡其他已設定的 WINS 伺服器。
3.  用戶端將 NetBIOS 查詢廣播到本機子網路中。
4.  如果設定使用 Lmhost 檔案，用戶端就會檢查該 Lmhost 檔案以對應此查詢。
5.  用戶端會嘗試到本機的 Hosts 檔案尋找
6.  接著到DNS的[Cache中的查詢](https://zh.wikipedia.org/wiki/Cache "wikilink")
7.  最後再到 DNS 伺服器

如果欲解析的電腦名稱字元數超過15個字元，或是電腦名稱之中有句點存在，則會自動改用DNS主機名稱解析方法。步驟2和3動作決定，使用何種 Node Type。

## DNS 與 WINS 的整合

DNS的Clinet向DNS查詢時，DNS找不到相關的資料就去問WINS，讓Client端以為DNS知道該名稱的位址。

另外有可能遇到Client的電腦不會去DNS註冊資料，則有兩種情況需要做整合：

1.  舊版Windows（95、98）是不會跑去DNS登記的，也不能支援DNS的動態更新
2.  Stand Alone的電腦無法向DNS註冊，原因是DNS可能有設定安全性驗證，只能接受加入[網域的電腦](https://zh.wikipedia.org/wiki/網域 "wikilink")

因此WINS需要幫忙回答這些Client端的電腦所在的位址。

## WINS 與DNS的差異

WINS的作用跟DNS的作用有相似的地方，都在做名稱解析，但也有不同之處：

| 特性／服務                                                          | WINS                                                     | DNS                                                    |
| -------------------------------------------------------------- | -------------------------------------------------------- | ------------------------------------------------------ |
| 使用的[網路協定](https://zh.wikipedia.org/wiki/網路協定 "wikilink")       | NETBIOS、TCP/IP                                           | TCP/IP                                                 |
| 常見的[網路環境](https://zh.wikipedia.org/wiki/網路環境 "wikilink")       | 較常適用於[LAN](https://zh.wikipedia.org/wiki/LAN "wikilink") | 較常跨[WAN](https://zh.wikipedia.org/wiki/WAN "wikilink") |
| 解析名稱類型                                                         | 解NetBIOS名稱（網芳名稱轉換IP）                                     | 解FQDN名稱（網域名稱轉換IP）                                      |
| Windows系統[路徑指定方式](https://zh.wikipedia.org/wiki/路徑 "wikilink") | UNC路徑 \\\\Server1                                        | FQDN路徑Server1.domain.com                               |
| 與同類型伺服之間的關係                                                    | 無階層式                                                     | 階層式導向                                                  |
| Client端[關機前動作](https://zh.wikipedia.org/wiki/關機 "wikilink")    | 將名稱釋放（Release）                                           | 不會釋放                                                   |

事實上[Windows NT系統上既有的WINS就是設計用來支援](../Page/Windows_NT.md "wikilink")[DHCP的運作的](https://zh.wikipedia.org/wiki/DHCP "wikilink")，且已成為Microsoft 企業網路整體架構中的一個重要的部份。WINS的作用與DNS類似，都是用來提供多種管理名稱的系統服務，例如：將名稱轉換成IP地址，但是WINS只負責管理NetBIOS所使用的命名空間，而此命名空間與一般DNS所管理的階層式領域名稱並不相同。

此外WINS還能夠與DHCP配合在一起使用，也就是說可以先用DHCP指定系統所需要的IP地址，然後再自動地在WINS伺服中註冊一個機動的NetBIOS名稱。由於WINS的架構並非階層式的，因此若某一個NetBIOS名稱未在WINS伺服中註冊，就可以將之視為在網路上根本不存在。由此可知：在所有採用NetBIOS over TCP的網路上WINS可以算是一項必備的工具，其詳細的規格請參閱RFC 1001與RFC 1002。

## 尖峰處理方式

WINS 伺服器立即可以處理大量的（傳送）伺服器[負載](https://zh.wikipedia.org/wiki/負載 "wikilink")。在同時使用大量的 WINS 用戶端並嘗試在 WINS 中登錄其本端名稱時（如電源中斷），會發生傳送處理。當電源供應稍後恢復時，許多使用者啟動及同時在網路上登錄名稱，此時產生了高度的 WINS 流量。具有傳送模式支援，WINS 伺服器可以在處理及實際輸入更新到 WINS 伺服器資料庫之前，先回應這些用戶端要求。

在傳送處理中，其他用戶端的要求是 WINS 伺服器立即回答回應。回應也包含到用戶端的各種存留時間（[TTL](https://zh.wikipedia.org/wiki/TTL "wikilink")），這可幫助調節用戶端登錄負載及分配超時要求的處理。這會減慢新的 WINS 用戶端重新整理及重試率且調節傳送的 WINS 用戶端流量。

## 使用 WINS 的好處

為管理 TCP/IP 型網路，WINS 提供了下列好處：

1.  支援電腦名稱登錄及解析的動態名稱至IP位址的[資料庫](https://zh.wikipedia.org/wiki/資料庫 "wikilink")，進而有效降低NETBIOS的廣播風暴。
2.  名稱及IP位址的資料集中管理減輕對管理 Lmhost 檔案的需求。
3.  藉由許可用戶端查詢 WINS 伺服器以直接尋找遠端系統，可以降低子網路上的 NetBIOS 造成的廣播流量。
4.  支援網路上早期的 Microsoft Windows 及 NetBIOS [用戶端](https://zh.wikipedia.org/wiki/用戶端 "wikilink")，即使到今天，只要網路上還有舊版本的 Windows 或使用 NetBIOS 的應用程式在，WINS 就有存在的必要允許此類型用戶端在每個子網路上，不需本機網域控制站的存在即可瀏覽遠端 Windows 網域的清單。
5.  當執行 WINS 對應整合時，可藉由啟用 DNS 用戶端尋找 NetBIOS 資源，以支援 DNS 用戶端

## 參考資料

  - Well-Know Port：

<!-- end list -->

  -
    137/tcp Netbios-ns NETBIOS Name Service
    138/tcp Netbios-dgm NETBIOS Datagram Service
    139/tcp Netbios-ssn NETBIOS Session Service
    1512/tcp (WINS) Microsoft's Windows Internet Name Service
    1512/udp(WINS) Microsoft's Windows Internet Name Service
    [RFC1001](http://tools.ietf.org/html/rfc1001)、 [RFC1002](http://tools.ietf.org/html/rfc1002)

<!-- end list -->

  - [NetBIOS over TCP/IP](https://web.archive.org/web/20080119212617/http://www.microsoft.com/technet/network/evaluate/technol/tcpipfund/tcpipfund_ch11.mspx)
  - [Port Assignments for Commonly-Used Services](https://web.archive.org/web/20090129073607/http://www.microsoft.com/technet/prodtechnol/windows2000serv/reskit/cnet/cnfc_por_simw.mspx?mfr=true)
  - [Windows Server 2003 Windows Internet Name Service (WINS)](https://web.archive.org/web/20081028185520/http://technet2.microsoft.com/windowsserver/en/technologies/wins.mspx)
  - \[<http://technet.microsoft.com/en-us/library/cc784707(v=ws.10>).aspx WINS defined\]

[Category:Microsoft_Windows](https://zh.wikipedia.org/wiki/Category:Microsoft_Windows "wikilink")