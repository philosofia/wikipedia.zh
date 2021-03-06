> 本文内容由[Microsoft Azure 虛擬網路服務](https://zh.wikipedia.org/wiki/Microsoft_Azure_虛擬網路服務)转换而来。


**Microsoft Azure 虛擬網路服務** 是 Microsoft Azure 所提供的網路通訊服務，並運行於 Azure 資料中心內，供應運算資源所需要的網路通訊能力以及必需的資源，例如 IP 位址。

虛擬網路服務是一種[軟體定義網路](../Page/軟體定義網路.md "wikilink")的實作，它完全使用軟體設定自動建置，無須人力介入。

Azure 平台內可使用虛擬網路的服務有：[虛擬機器](https://zh.wikipedia.org/wiki/Microsoft_Azure_Virtual_Machine "wikilink")、[雲端服務](https://zh.wikipedia.org/wiki/Microsoft_Azure_Cloud_Service "wikilink") 與 [應用服務內的 Web App](https://zh.wikipedia.org/wiki/Microsoft_Azure_App_Service "wikilink")。

## 網路組態

Azure 虛擬網路利用軟體的方式操作 Azure 資料中心內的網路建設，它本身就是一個大型的軟體定義網路解決方案，網路管理人員可在 Azure 虛擬網路內自由劃分需要的[子網路與IP位址空間](https://zh.wikipedia.org/wiki/子網路 "wikilink")。Azure 虛擬網路提供了三種基本位址空間供選擇 (都是 IP 位址中已定義的私人網路範圍)：

  - 10.0.0.0
  - 172.16.0.0
  - 192.168.0.0

網路管理人員可利用 [CIDR](https://zh.wikipedia.org/wiki/無類別域間路由 "wikilink") 的網路劃分法來定義主位址空間 (例如 10.0.0.0/8 或 10.0.0.0/16)，並在位址空間內劃分出子網路 (例如 10.0.1.0/24, 10.0.2.0/24) 供虛擬機器配給 IP 之用，每個子網路都有自己的 DHCP 伺服器，當虛擬機器加入到子網路時，就會自動分派 IP 位址給它，一個子網路可用的位址為該子網路劃分出的位址數量-3，Azure會保留每個子網路的前三個 IP (.1\~.3) 供 Azure 服務使用 \[1\]，因此可用位址均是由 .4 開始。

雖然子網路可以動態分配 IP 位址給虛擬機器，不過網路管理人員或服務也可以自訂要使用的 IP 位址。

## IP 位址

虛擬網路中的 IP 位址，視可聯外與否而區分，但是在新的資源管理模式 (Resource Management) 問世後，IP 位址被簡化成內部 IP 與公用 IP 兩種 \[2\]。

### 公用 IP

公用 IP (Public IP) 負責對 Internet 的連線，虛擬網路內的資源若要能連到 Internet，就必須設置一個或多個公用 IP，公用 IP 的配給方式由 Azure 管理，網路管理人員可利用 Portal 或是 PowerShell 指令等方式向 Azure 索取 IP 位址，不過 IP 位址會視可重覆使用的類型分成動態 (dynamic) 與靜態 (static)，動態係指當運算資源上線時才會分派 IP 位址，適合用在一般性的對外運算資源，但由於 IP 不固定，無法適用於常態性的 Internet 服務 (如 DNS 或 SSL)，若需要 IP 固定，則要使用靜態公用 IP，它自配發開始就固定 (視為永久上線狀態)，直到它被刪除為止。

公用 IP 位址在舊的服務管理模式下，和服務有緊密的結合，因此會有下列幾種類型：

  - 執行個體層級公用 IP (Instance-Level Public IP, ILPIP)，繫結在虛擬機器的公用 IP，為動態的公用 IP，。
  - 保留 IP (Reserved IP, VIP)，繫結在雲端服務上的 IP，為靜態的公用 IP，但不能繫結在虛擬機器，虛擬機器要使用通訊埠對應才能使用保留 IP 連線 \[3\]。

在資源管理模式下屬於獨立資源，它可以與網路卡、負載平衡器、網路閘道器 (Network Gateway) 與應用程式閘道器 (Application Gateway) 四種資源繫結 (Binding)，當 IP 不需繫結時可單獨存在，動態模式的公用 IP 在未繫結時不會配發 IP，靜態 IP 則有繫結的資源限制 (它不可以和網路閘道器或應用程式閘道器繫結)。

### 內部 IP

內部 IP (Private IP) 則是虛擬網路內運算資源之間通訊的基礎，每個配置到虛擬網路內的運算資源都會配給內部 IP，通常是由 DHCP 依子網路的位址空間進行配發，但網路管理人員也可以使用靜態的內部 IP (Static VNet IP)，當運算資源註冊了靜態內部 IP 時，除非運算資源被刪除或是解除靜態內部 IP 的繫結，否則不論運算資源啟動與否，該靜態內部 IP 都會存在且固定。靜態內部 IP 可配置在網路卡、負載平衡器與應用程式閘道器 (Application Gateway)。然而靜態內部 IP 與公用 IP 不同，它不會獨立存在，而是依附於子網路的設定內，因此各網路資源都要使用靜態內部 IP 要個別設定無法共用。

## DNS

Azure 虛擬網路內預設使用由 Azure 提供的名稱解析服務 (Name Resolution Services)，當虛擬機器配置到虛擬網路內時，其 DNS 設定會指向 Azure 的名稱解析服務，負責 Azure 本身相關服務的名稱對應，在早期以雲端服務為主的運算服務，若沒有它，則無法解析如 cloudapp.net 的名稱對應，不過在資源管理員模式導入後，它不再是必備的條件，只是若公用的 IP 位址設定了 DNS 名稱時，仍然會以 Azure 的 DNS 來處理名稱解析 \[4\]。

網路管理人員若需要自己的名稱解析方案 (如在虛擬網路內佈建 [Active Directory](../Page/Active_Directory.md "wikilink") 網域控制站) 時，仍然可以在虛擬網路內架設 [DNS](https://zh.wikipedia.org/wiki/DNS "wikilink") 伺服器，以供應自訂的名稱解析解決方案。

2015 年時，Azure 推出了自己的網域名稱代管服務 (DNS Hosting Service)，對外使用 Azure DNS 的名稱，但為避免與原有的 Azure 名稱解析服務 (其原本在文件內的名稱也是 Azure DNS)，目前在 Azure 官方技術文件上看到的 Azure DNS 都是指網域名稱代管服務，而原本的 Azure DNS 則改為名稱解析服務 (Azure-provided name resolution)。

## 負載平衡器

Azure 的網路服務中提供了兩種類型的負載平衡器，以處理面對大量運算時的工作負載分流機制，一種是 Azure 管理的負載平衡器 (Azure Load Balancer)，這也是早期以雲端服務為主的負載平衡器，由 Azure 管理，對外只能使用連接埠區分並用存取控制表來控制存取權限；另一種是內部負載平衡器 (Internal Load Balancer)，由網路管理人員自行管理，供虛擬網路內的負載分流工作。在資源管理員模式內，不論是何種負載平衡器，都視為一個獨立元件，只差在負載平衡器對外的 IP 位址的設定類型不同而已。

### 類型

面對 Internet 的負載平衡器 (Internet-facing Load Balancer) 在早期以雲端服務為主的管理模式下，它統一分派 \*.cloudapp.net 的網址，負責 Internet 連入 Azure 服務的流量調節，但它並不決定開放的通訊埠、通訊埠對應 (Port Mapping) 與存取控制，這些設定是由掛到同一個雲端服務下的運算資源來決定 (如虛擬機器)，運算資源都有兩種通訊設定，一種是給運算資源本身的，另一種是給負載平衡器的，這導致網路管理員在設定通訊埠上的困難與不便 (等於同一個 Policy 要設兩邊，而且每一個運算資源都要設)。在資源管理員模式下，負載平衡器上的通訊埠對應被改稱為連入網路位址轉換 (Inbound NAT)，網路管理人員可以決定負載平衡器的位址連入到哪一個運算資源，同樣的，內部到外部也有一個來源網路位址轉換 (Source NAT)，由負載平衡器自動管理，以加速資料經負載平衡器回傳的速度。此類負載平衡器的來源是公用 IP，且不論是動態或靜態皆可。

內部負載平衡器則是配置在虛擬網路內，其來源由虛擬網路內的子網路決定 (也可設定固定的靜態內部 IP)，其通訊埠對應機制與面對 Internet 的負載平衡器相同，但它的運用更多元，除了可輔助面對 Internet 的負載平衡器實作出多層次的應用負載平衡 (如對外是 Web Application 的負載平衡，對內則是 Database 的負載平衡)，也可以讓企業的地端網路透過 VPN 直接存取內部負載平衡器以分散內部的流量。

### 分流演算法

Azure 的負載平衡器採用[分散式雜湊表](../Page/分散式雜湊表.md "wikilink")處理來源連入的分流工作，依照負載平衡器對來源與(或)目標的參數進行雜湊演算，產生要分派的目標伺服器資訊。

負載平衡器早期只支援 5-tuple 的演算法，分配連入的來源到不同的資源，在 2014 年時，微軟宣布加入新的演算法\[5\]，以支援如遠端桌面服務 (Remote Desktop Service) 這類需要持久且固定的用戶端-伺服器端機器的對應，因此目前負載平衡器支援三種分流演算法 (Distribution Modes)：

  - 2-tuple 演算法 (Source IP Affinity 演算法)：使用來源IP與目標IP為參考資料。
  - 3-tuple 演算法 (Source IP Affinity 演算法)：使用來源IP、目標IP與通訊協定為參考資料。
  - 5-tuple 演算法 (預設的演算法): 使用來源IP、來源通訊埠、目標IP、目標通訊埠與通訊協定為參考資料。

## 存取控制

Azure 虛擬網路早期並沒有存取控制機制，全部依賴雲端服務內的虛擬機器的存取控制表 (ACL)，但設定上相當不便 (有幾台機器就要設幾次)，因此在資源管理模式下，Azure 提供了網路安全群組 (Network Security Group) 供網路管理人員組態網路存取控制之用，網路安全群組也是一個獨立元件。

網路安全群組支援流入 (inbound) 與流出 (outbound) 的 ACL 機制 (稱為 ACL 規則)，ACL 使用五種資料進行雜湊 \[6\]，分別是通訊協定、來源 IP 位址範圍、來源連接埠範圍、目的地 IP 位址範圍和目的連接埠範圍，並且在雜湊對應成功時以其設定的優先權 (Priority) 排序 (數字愈小優先權愈高)，最後再評估其存取權限 (Allow/Deny) 決定是否允許存取。網路管理員可以針對自己的網路安全需求配置許多個 ACL 規則並組合應用。

ACL 可以套用到特定的位址範圍 (例如一個 IP 或一組 IP)，或是由 Azure 定義的位址類型：

  - Internet: 來自 Internet 的 IP。
  - Azure Load Balancer: 來自於 Azure 基礎建設的負載平衡器，它會以 Azure Datacenter 的 IP 範圍為主，亦即套用於所有的 Azure 服務的 IP。
  - Virtual Network: 來自於虛擬網路的 IP。

網路安全群組可套用於網路卡 (只有資源管理模式支援)、虛擬機器 (只有傳統模式支援，且只能使用指令) 以及子網路組態，負載平衡器則是透過網路卡來支援網路安全群組的設定。

## VPN

Azure 虛擬網路為了與外界互連，因此提供了[VPN的連線能力](https://zh.wikipedia.org/wiki/VPN "wikilink")，早期虛擬網路只支援站對站(Site-to-Site VPN, S2S VPN)，且要求使用 [IKEv](https://zh.wikipedia.org/wiki/IKE "wikilink")1 的原則模式 (Policy-based Mode)，但 2014 年起導入了 IKEv2 的路由模式 (Route-based Mode) 後，VPN的應用範圍大幅提升，目前可支援站對站、點對站 (Point-To-Site, P2S VPN)、虛擬網路間對接 (VNet-to-VNet VPN)、多站式對接 (Multi-site VPN) 以及與 [Microsoft Azure ExpressRoute](https://zh.wikipedia.org/wiki/Microsoft_Azure_ExpressRoute "wikilink") 對接的 VPN。

VPN 需要使用網路閘道器 (Network Gateway)\[7\]，這會決定 VPN 使用的模式是 Policy-based 或是 Route-based，並且依流量不同分成 Basic、Standard 與 Premium 三種計費模式。閘道器要求虛擬網路內必須配置一個子網路，名稱固定為 "GatewaySubnet"，位址空間限制在 /26\~/29 之間，要用多大則視要對接的閘道數有多少決定，因為大型虛擬網路可能要和不同的網路對接，而每一個網路使用的可能不是同一個閘道。

各類 VPN 的支援如下表。

<table>
<thead>
<tr class="header">
<th></th>
<th><p>Policy-based Basic</p></th>
<th><p>Route-based Basic</p></th>
<th><p>Route-based Standard</p></th>
<th><p>Route-based Premium</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>站對站 VPN</p></td>
<td><p>Policy-based VPN 組態</p></td>
<td><p>Route-based VPN 組態</p></td>
<td><p>Route-based VPN 組態</p></td>
<td><p>Route-based VPN 組態</p></td>
</tr>
<tr class="even">
<td><p>點對站 VPN</p></td>
<td><p>不支援</p></td>
<td><p>支援，且可與站對站VPN共存</p></td>
<td><p>支援，且可與站對站VPN共存</p></td>
<td><p>支援，且可與站對站VPN共存</p></td>
</tr>
<tr class="odd">
<td><p>驗證方法</p></td>
<td><p>預先共享金鑰</p></td>
<td><p>S2S: 預先共享金鑰<br />
P2S: 以憑證為主</p></td>
<td><p>S2S: 預先共享金鑰<br />
P2S: 以憑證為主</p></td>
<td><p>S2S: 預先共享金鑰<br />
P2S: 以憑證為主</p></td>
</tr>
<tr class="even">
<td><p>最大站對站連接數</p></td>
<td><p>1</p></td>
<td><p>10</p></td>
<td><p>10</p></td>
<td><p>30</p></td>
</tr>
<tr class="odd">
<td><p>最大點對站連接數</p></td>
<td><p>不支援</p></td>
<td><p>128</p></td>
<td><p>128</p></td>
<td><p>128</p></td>
</tr>
<tr class="even">
<td><p>主動式路由支援 (BGP)</p></td>
<td><p>不支援</p></td>
<td><p>不支援</p></td>
<td><p>不支援</p></td>
<td><p>不支援</p></td>
</tr>
</tbody>
</table>

## 參考

<references />

[Category:微軟](https://zh.wikipedia.org/wiki/Category:微軟 "wikilink") [Category:Microsoft_Azure](https://zh.wikipedia.org/wiki/Category:Microsoft_Azure "wikilink")

1.  [Virtual Network FAQ](https://azure.microsoft.com/en-us/documentation/articles/virtual-networks-faq/)
2.  [IP Addresses in Azure](https://azure.microsoft.com/en-us/documentation/articles/virtual-network-ip-addresses-overview-arm/)
3.  [保留的 IP 概觀](https://azure.microsoft.com/zh-tw/documentation/articles/virtual-networks-reserved-public-ip/)
4.  [Name Resolution for VMs and Role Instances](https://azure.microsoft.com/en-us/documentation/articles/virtual-networks-name-resolution-for-vms-and-role-instances/)
5.  [Azure Load Balancer new distribution mode](https://azure.microsoft.com/zh-tw/blog/azure-load-balancer-new-distribution-mode/)
6.  [What is a Network Security Group (NSG)](https://azure.microsoft.com/en-us/documentation/articles/virtual-networks-nsg/)
7.  [About VPN gateways](https://azure.microsoft.com/en-us/documentation/articles/vpn-gateway-about-vpngateways/)