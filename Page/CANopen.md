> 本文内容由[CANopen](https://zh.wikipedia.org/wiki/CANopen)转换而来。


**CANopen**是一種架構在[控制器區域網路](https://zh.wikipedia.org/wiki/控制器區域網路 "wikilink")（Controller Area Network, CAN）上的高層[通訊協定](https://zh.wikipedia.org/wiki/通訊協定 "wikilink")，包括通訊子協定及設備子協定常在[嵌入式系統中使用](https://zh.wikipedia.org/wiki/嵌入式系統 "wikilink")，也是工業控制常用到的一種[現場總線](../Page/現場總線.md "wikilink")。

CANopen實作了[OSI模型](../Page/OSI模型.md "wikilink")中的[網路層以上](https://zh.wikipedia.org/wiki/網路層 "wikilink")（包括網路層）的協定。CANopen標準包括定址方案、數個小的通訊子協定及由設備子協定所定義的[應用層](https://zh.wikipedia.org/wiki/應用層 "wikilink")。CANopen支援網路管理、設備監控及節點間的通訊，其中包括一個簡易的[傳輸層](https://zh.wikipedia.org/wiki/傳輸層 "wikilink")，可處理資料的分段傳送及其組合。一般而言[資料鏈結層及](https://zh.wikipedia.org/wiki/資料鏈結層 "wikilink")[實體層會用CAN來實作](https://zh.wikipedia.org/wiki/實體層 "wikilink")。除了CANopen外，也有其他的通訊協定（如[POWERLINK及](https://zh.wikipedia.org/wiki/POWERLINK "wikilink")[EtherCAT](../Page/EtherCAT.md "wikilink")）實作CANopen的設備子協定。

基本的CANopen設備及通訊子協定定義在CAN in Automation (CiA) draft standard 301.\[1\]。針對個別設備的子協定以CiA 301為基礎再進行擴充。如針對I/O模組的CiA401\[2\]及針對運動控制的CiA402\[3\]。

## 設備模型

以下是所有CANopen設備都要具備的功能：

  - **通訊單元**處理和網路上其他模組通訊所需要的通訊協定。
  - 設備的啟動及重置由**狀態機（state machine）**控制。狀態機需包括以下的幾個狀態：Initialization, Pre-operational, Operational及Stopped。當接收到網路管理（NMT）通訊物件，狀態機會轉換到對應的狀態。
  - **物件字典（Object Dictionary）**是一個有16位元索引（Index）的變數陣列。每個變數可以（但非必須）有8位元的子索引（Subindex）。變數可用來調整設備的組態，也可以對應設備量測的資料或設備的輸出。
  - 當狀態機設定為operational　之後，設備的**應用（application）**部份就會實現設備預期的機能。此部份可以由物件字典中的變數調整其設定，而資料由通訊層傳收或接收。

### 物件字典

CANopen設備都需要具備物件字典，用來設定設備組態及進行非即時的通訊。物件字典的entry定義如下：

  - **索引（Index）**：物件16位元的位址。
  - **物件名稱（Object name）**：一個代表物件的symbolic type，可以是陣列、紀錄或只是一個變數。
  - **名稱（Name）**：描述此entry的字串。
  - **形態（Type）**：變數的資料形態。
  - **屬性（Attribute）**：提供此entry是否可讀／可寫的資料，有下列四種：可讀/寫、唯讀、唯寫、唯讀常數。
  - **必須（Mandatory）/可選（Optional）**欄位定義屬於特定設備規範下的設備，是否必須實現某些物件。

在CANopen標準中定義了物件字典中的基本資料型態，包括邏輯值、整數及浮點數。也定義了複合物件：如陣列、記錄及字串。複合物件用一個8位元的數值作為其子索引（subindex）。記錄或陣列中子索引0的位置記錄此資料結構的元素個數，資料型態為UNSIGNED8。

例如在CiA301標準中，設備通訊的參數放在索引範圍0x1000 - 0x1FFF（通訊行規區）。此區域的前幾項如下：

| 索引     | 物件名稱 | 名稱                       | 形態         | 屬性 | M/O |
| ------ | ---- | ------------------------ | ---------- | -- | --- |
| 0x1000 | VAR  | device type              | UNSIGNED32 | 唯讀 | M   |
| 0x1001 | VAR  | error register           | UNSIGNED8  | 唯讀 | M   |
| ...    |      |                          |            |    |     |
| 0x1008 | VAR  | manufacturer device name | Vis-String | 常數 | O   |
| ...    |      |                          |            |    |     |

若配合適當的工具，可以用編輯電子資料表（electronic data sheet, EDS)檔案的方式規劃一個設備，並且將變數的數值上傳到設備中。EDS檔案的格式通常會是[INI檔](https://zh.wikipedia.org/wiki/INI檔 "wikilink")。

## 通訊

### 通訊物件

CANopen的物理層CANbus每次傳送的資料量不大，其中包括11位元的ID、遠端傳輸請求（RTR）位元及大小不超過8位元組的資料。CANopen將CANbus 11位元的ID分為4位元的功能碼及7位元的CANopen節點ID。7位元的ID共有128種不同的組合，其中ID 0不使用，因此一個CANopen網路上最多允許127台設備。CANbus在CAN 2.0 B規格中允許29位元的ID，因此若配合CAN 2.0 B使用，CANopen網路上可以超過127台設備，不過在實際運用中，大多數的CANopen網路上設備數量均低於此數值。

CANopen將CANbus的11位元ID稱為通訊物件ID（COB-ID）。當傳輸資料出現碰撞時，CANbus的仲裁機制會使COB-ID最小的訊息繼續傳送，不用等待或重傳。COB-ID的前4個位元是CANopen的功能碼，因此數值小的功能碼表示對應的功能重要，允許的延遲時間較短。

以下是一個標準的CANopen頁框：

|     | COB-ID | RTR | 資料長度 | 資料  |
| --- | ------ | --- | ---- | --- |
| 功能碼 | 節點ID   |     |      |     |
| 長度  | 4位元    | 7位元 | 1位元  | 4位元 |

在CANopen標準中，部份COB-ID被保留作網路管理及SDO通訊用。而在設備初始化後，有些功能碼和COB-ID會對映到標準的功能，不過後續仍可以規劃為其他用途。

### 通訊模型

CANopen設備間的通訊可分為以下三種通訊模型。

  - 在**主從**（**master/slave模型**）中，一個CANopen設備為master，負責傳送或接收其他設備（稱為slave）的資料。NMT協定就使用了master/slave模型。

<!-- end list -->

  - **客户端/服务器**（**client/server**）**模型**定義在SDO協定中，SDO client將物件字典的索引及子索引傳送給SDO server，因此會產生一個或數個需求資料（物件字典中，索引及子索引對應的內容）的SDO封包。

<!-- end list -->

  - **生產者／消費者**（**producer/consumer**）**模型**用在Heartbeat and Node Guarding協定。由一個生產者送出資料給消費者，同一個生產者的資料可能給一個以上的消費者。又可分為二種：
      - push-model：生產者會自動送出資料給消費者。
      - pull-model：消費者需送出請求訊息，生產者才會送出資料。

### 协议

#### NMT协议

**NMT**（**網路管理**, **Network management**）协议是用来发布（設備內部）狀態機的狀態變更命令（如啟動設備或停止設備）、以及监测遠端設備启动及故障情形。

NMT master使用的**模組控制協定**可變更設備的狀態。其COB-ID為0，其功能碼及節點ID均為0，因此網路上的所有節點均會處理這個訊息。在此訊息的資料部份會有此訊息實際針對節點的ID，此ID也可為0，表示所有節點都要變更為指定的狀態。

**心跳協定**（**Heartbeat protocol**）是用[心跳機制來監控網路中的節點及確認其正常工作](https://zh.wikipedia.org/wiki/心跳機制 "wikilink")。心跳訊息的生產者（一般是slave設備）週期性的送出功能碼1110、ID為本身節點ID的訊息，訊息的資料部份有一個表示節點狀態的位元。而心跳訊息的消費者負責接收上述資料，若在指定時間（於設備的物件字典中定義）內，消費者均未收到訊息，可採取相關行動（例如顯示錯誤或重置該設備）。

其格式為：

`      COBID + DATA (status of node)  `

CANopen設備需要在bootup時自動從Initializing狀態切換至Pre-operational狀態，設備會在切換完成後送出一個心跳訊息，這就是心跳協定。

有一種pull model的NMT協定，稱作節點監控（Node guarding）協定，也可以作從機的監控。

#### 服務資料物件（SDO）協定

**服務資料物件**（**SDO**）可用來存取遠端節點的物件字典，讀取或設定其中的資料。提供物件字典的節點稱為SDO server，存取物件字典的節點稱為SDO client。SDO通訊一定由SDO client開始，並提供初始化相關的參數。

在CANopen的術語中，**上傳**是指由SDO server中讀取資料，而**下載**是指設定SDO server的資料。

由於物件字典中的資料長度可能超過8個位元組，無法只用一個CAN頁框傳輸，SDO也支援長訊息的分割（segmentation）和合併（desegmentation）。這樣的物件有二種：**SDO下載/上傳**（**SDO download/upload**）及**SDO區塊下載/上傳**（SDO Block download/upload）。CANopen協定較新版本支援SDO區塊傳輸，可以允許傳輸大量的資料，且傳輸的overhead可以較低。

負責處理SDO資料傳輸的COB ID可在物件字典中設定。在物件字典的索引0x1200至0x127F可設定SDO server的COB ID，最多可設定到127個。而SDO client可以在物件字典的索引0x1280至0x12FF中設定。不過**預定義連結**（**pre-defined connection set**）定義在開機後（Pre-operational狀態）可用來設定設備組態的SDO。接收用的COB ID為0x600 +節點ID，而傳送用的COB為0x580 +節點ID。

以下用SDO下載來說明SDO的協定，SDO client在要啟始下載時，會送出CAN訊息，其ID為接收端SDO channel的COB ID，而CAN頁框的資料欄位內容如下：

| CAN頁框的資料欄位 |
| ---------- |
| 位元組1       |
| 3位元        |
| ccs=1      |

  - **ccs**是SDO傳輸時client指令的識別碼，可分為以下幾種：
      - 0：SDO區域下載
      - 1：啟始下載
      - 2：啟始上傳
      - 3：SDO區域上傳
      - 4：中斷SDO傳輸
  - **n**為此訊息中實際資料的長度，只有在e和s設定時有效
  - **e**若設為1，表示是快速傳輸（expedited transfer），目前訊息即包括了所有要傳輸的資料。若設為0，表示要傳輸的資料無法用一個訊息傳送，會分割為數個訊息。
  - **s**若設為1，且**e**也設為1，表示資料長度記錄在**n**。若**e**設為0，表示實際完整資料的長度會放在此訊息中的資料欄位中。
  - **索引**是要存取資料的物件字典索引。
  - **子索引**是要存取變數的子索引。
  - **資料**在快速傳輸（e=1）時是要上傳的資料，若s=1且e=0，則是實際資料的長度。

#### \-{zh-hans:进程数据对象; zh-tw:程序資料物件}-（PDO）協定

**-{zh-hans:进程数据对象; zh-tw:程序資料物件}-**（**PDO**）協定可用來在許多節點之間交換即時的資料。可透過一個PDO，傳送最多8位元組（64位元）資料給一設備，或由一設備接收最多8位元組（64位元）的資料。一個PDO可以由物件字典中幾個不同索引的資料組成，規劃方式則是透過物件字典中對應PDO mapping及PDO參數的索引。

PDO分為兩種：傳送用的TPDO及接收用的RPDO。一個節點的TPDO是將資料由此節點傳輸到其他節點，而RPDO則是接收由其他節點傳輸的資料。一個節點分別有4個TPDO及4個RPDO。

PDO可以用同步或非同步的方式傳送：同步的PDO是由SYNC訊息觸發，而非同步的PDO是由節點內部的條件或其他外部條件觸發。例如若一個節點規劃為允許接受其他節點產生的TPDO請求，則可以由其他節點送出一個沒有資料但有設定RTR位元的TPDO（TPDO請求），使該節點送出需求的資料。　

藉由RPDO也可以使兩個或兩個以上的設備同時啟動。只要將其RPDO對應到相同的TPDO即可。

#### 同步（SYNC）協定

同步協定使用生產者/消費者模型。同步生產者（Sync-Producer）會定時產生同步信號供同步消費者（Sync-Consumer）使用。當同步消費者收到信號，即可以進行已規劃好的同步工作。\[4\]

同步信號會定時產生，若有PDO是由同步信號引發，透過PDO傳送時間及同步信號傳送週期之間的調整，可以使感測器定期的取様，而致動器也可以根據最新的輸入信號產生對應的輸出。

在物件字典中，同步物件的索引為0x1005，可透過編輯此物件啟動同步協定。

#### 時間標記物件（TIME）協定

一般而言，時間標記物件的內容是從1984年1月1日午夜之後到現在之間經過的時間，單位為[毫秒](https://zh.wikipedia.org/wiki/毫秒 "wikilink")。為一個48位元（6位元組）的數值。

不過有些應用會要求時間要非常精確，這種情形會需要精準的同步，尤其是在大型網路，通訊速度受限時更是如此。此時需要將各設備的時鐘同步，精準度要到毫秒的等級。這個要求可透過高解析度的同步信號達成，在同步信號中也包括了另一種時間標記，可供各設備調整時鐘用。

同步信號中的時間標記型態為unsigned32，單位為1毫秒，因此時間標記會在每72分鐘歸零重新計數。

#### 緊急物件（EMCY）協定

### 初始化

以下是在master初始化2個壓力感測器（ID分別為1和2）中，通訊的資料。

| CAN ID | 資料長度 | 資料          | 說明                                                                                        |
| ------ | ---- | ----------- | ----------------------------------------------------------------------------------------- |
| 0x0    | 2    | 1 0         | master將系統設定為operational mode                                                              |
| 0x80   | 0    |             | Master送出SYNC訊息，使設備送出資料                                                                    |
| 0x181  | 4    | CD 82 01 00 | ID 1的節點（CID-0x180），讀到的壓力為0x0182CD (99021) [帕](https://zh.wikipedia.org/wiki/帕 "wikilink") |
| 0x182  | 4    | E5 83 01 00 | ID 2的節點（CID-0x181），讀到的壓力為0x0183E5 (99301) [帕](https://zh.wikipedia.org/wiki/帕 "wikilink") |

## CANopen專有名詞

  - PDO程序資料物件 - 對應實際物理量的輸入及輸出。資料的單位可能是RPM, V, Hz, mAmp...。
  - SDO服務資料物件 - 一般來說是組態設定的資料，如節點位置、節點ID、通訊速度、位移、增益等……。
  - COB-ID - CAN物件編號
  - CAN ID - CAN Identifier.是在每個CAN訊息前面的訊息識別碼，共11位元。
  - EDS - 電子資料檔（Electronic data sheet）是INI格式的檔案。
  - DCF - 設備組態檔案（Device configuration file），是加強版的EDS，可以設定節點ID及通訊速度。

## 參照

  - [控制器區域網路](https://zh.wikipedia.org/wiki/控制器區域網路 "wikilink")（CAN）
  - [DeviceNet](../Page/DeviceNet.md "wikilink")（另一種使用CAN的工業通訊定）

## 參考資料

<references/>

## 外部連結

  - [CAN in Automation的CANopen簡介](http://www.can-cia.org/can-knowledge/canopen/canopen/)
  - [CANopen簡介（www.esacademy.com）](http://www.esacademy.com/myacademy/classes/CANopenIntro/CANopenIntro_files/frame.htm?category=&)
  - [CANopen的教學網頁（softing.com）](http://www.softing.com/home/en/industrial-automation/products/can-bus/more-can-open/communication/reference-model.php)
  - [CANopen開發資料（canopendesign.com）](https://web.archive.org/web/20070930121500/http://www.canopendesign.com/)
  - [CAN-wiki中CANopen的頁面](http://www.can-wiki.info/CanOpen)
  - [CANopen: An Introduction](http://www.industrialcontroldesignline.com/showArticle.jhtml?articleID=192200423)
  - [關於About CANopen（canopensolutions.com）](http://www.canopenslutions.com/english/about_canopen/about_canopen.shtml)
  - [CANopen-Lift社群的WIKI](http://en.canopen-lift.org/)
  - [Introduction to CANopen基礎介紹（www.canopen-solutions.com）](http://www.canopen-solutions.com/canopen_fundamentals_en.html)
  - [CanFestival - 一個開放源碼多平台CANopen的計劃](http://www.canfestival.org/)

[Category:网络协议](https://zh.wikipedia.org/wiki/Category:网络协议 "wikilink") [Category:自动控制](https://zh.wikipedia.org/wiki/Category:自动控制 "wikilink") [Category:工業自動化](https://zh.wikipedia.org/wiki/Category:工業自動化 "wikilink")

1.  CiA Draft Standard 301，在[CAN in Automation](http://www.can-cia.org)網站上
2.  CiA Draft Standard 401
3.  CiA Draft Standard 402
4.