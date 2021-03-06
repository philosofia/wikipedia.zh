> 本文内容由[Microsoft Azure SQL Database](https://zh.wikipedia.org/wiki/Microsoft_Azure_SQL_Database)转换而来。


**Microsoft Azure SQL Database** (舊稱 SQL Azure, SQL Server Data Services 或 SQL Services) 是由微軟[SQL Server 2008為主](https://zh.wikipedia.org/wiki/SQL_Server "wikilink")，建構在[Microsoft Azure雲端作業系統之上](../Page/Microsoft_Azure.md "wikilink")，執行[雲端運算](../Page/雲端運算.md "wikilink") (Cloud Computing)的[關聯式資料庫服務](https://zh.wikipedia.org/wiki/關聯式資料庫 "wikilink") (Database as a Service)，是一種雲端儲存(Cloud Storage)的實作，提供網路型的應用程式資料儲存的服務。

2017年5月，微軟於 Build 2017 大會時宣布對 [MySQL](../Page/MySQL.md "wikilink") 與 [PostgreSQL](../Page/PostgreSQL.md "wikilink") 的 SQL Database 服務。

[SQL_Azure_Architecture.png](https://zh.wikipedia.org/wiki/File:SQL_Azure_Architecture.png "fig:SQL_Azure_Architecture.png") [SQL_Azure_HA.png](https://zh.wikipedia.org/wiki/File:SQL_Azure_HA.png "fig:SQL_Azure_HA.png")

## 基礎架構

Windows Azure SQL Databsae 的基底是SQL Server (通常以最新版為主)，不過它是一個特殊設計的SQL Server，並且以Windows Azure為基座平台，配合Windows Azure的特性，Windows Azure SQL Databsae也是一種分散在許多實體基礎架構(Physical Infrastucture)與其內部許多虛擬伺服器(Virtual Servers)的一種雲端儲存服務，外部應用程式或服務可以不用在乎資料庫實際儲存在哪裡，就可以利用Windows Azure SQL Databsae顯露的SQL Fabric殼層服務以接受外部連結，並且在內部使用連線繞送 (connection routing) 的方式，讓連線可以對應到正確的伺服器，而且資料庫是在雲端中由多個伺服器來提供服務，每一次連線所提供服務的伺服器可能會不同，因此也可以保證雲端儲存的高度可用性(High availability)。

Windows Azure SQL Databsae 架構在資料中心可分為三個部份\[1\]：

1\. 服務提供層 (Service Layer)：

服務提供層是 Windows Azure SQL Database 顯露在用戶端前面的服務介面 (Facade 模式)，負責接取所有向 Windows Azure SQL Databsae 提交要求的 TDS over SSL 連線與指令，當連線進入 Windows Azure SQL Databsae 時，Windows Azure SQL Databsae Load Balancer 會分派連線到不同的 Windows Azure SQL Databsae Gateway 中。**Windows Azure SQL Databsae Gateway**係負責處理 TDS 連線，管理連接層安全性 (connection-level security) 以及解析指令是否有內含潛在威脅的指令，再交由連線管理員 (Connection Manager) 將連線分派到位於平台提供層內不同的 Windows Azure SQL Databsae 資料庫伺服器中進行處理，Windows Azure SQL Databsae Gateway 也會管理對 SQL Azure 的連線，以避免可能會封鎖住伺服器的連線 (例如過長的查詢或過長的資料庫交易等)。

2\. 平台提供層 (Platform Layer)：

平台提供層則是以 Windows Azure Computes 的虛擬機器叢集 (Cluster)，每台虛擬機器都安裝有 SQL Server 以及管理一定數量的資料庫，通常一份資料庫會分散到三至五台的 SQL Server VM 中，而每台 SQL Server VM 也安裝了 **SQL Fabric** 中控軟體，並透過 SQL Fabric 與 Windows Azure SQL Databsae Gateway 的管控下，所有對單一資料庫的連線都不一定會持續連入同一台 SQL Server VM 中。SQL Server VM 內也安裝了 SQL Azure Management Service，它會負責對每個資料庫間的資料複寫工作，以保障 Windows Azure SQL Databsae 的基本高可用性要求。每台 SQL Server VM 內的 SQL Fabric 和 Management Service 都會彼此交換健康與監控資訊等，以保持整體服務的健康與可監控性。

3\. 基礎建設層 (Infrastructure Layer)：

基礎建設層由 Windows Azure Computes 以及其高度可擴充性的運算與網路基礎架構來組成，以支援 Windows Azure SQL Databsae 所需的高可用性以及高擴充性等雲端特色。

## 供應模型

Windows Azure SQL Databsae 服務對外的供應模型 (Provisioning Model) \[2\] 的設計以平緩企業進入雲端的學習曲線為主要考量，因此 Windows Azure SQL Databsae 對外提供的是一台邏輯伺服器 (Logical Server)，此伺服器是由 SQL Gateway 所顯露，每一個 Windows Azure 的帳戶都可以建立一台 SQL Database Server，就像在本地的 SQL Server 執行個體一樣，但這個執行個體是在雲端上執行且具有高可用性等特徵的資料庫伺服器。

每台 SQL Database Server 都具有下列內容：

1.  **DNS 名稱**，用戶端應用程式要使用這個 DNS 名稱連入資料庫，格式為 \[serverid\].database.windows.net。
2.  **master 資料庫**，此資料庫會存放登入資訊 (logins)，伺服器角色以及管理伺服器所必要的動態管理檢視表 (Dynamic Management View)。
3.  **Windows Azure SQL Databsae 防火牆**，用來管理連入 SQL Database Server 的連線來源。
4.  **使用者資料庫**，每個資料庫都有不同的計費標準\[3\]，大小由 100MB 到 150GB 不等。一台 SQL Database Server 可以有多個使用者資料庫。

用戶端只要可以支援 TDS (Tabular Data Stream) over SSL，即可連線與存取 SQL Database Server 的資料庫資源，這表示像[ODBC](../Page/ODBC.md "wikilink")、[ADO.NET](../Page/ADO.NET.md "wikilink")或[JDBC的](https://zh.wikipedia.org/wiki/JDBC "wikilink") SQL Server 最新版驅動程式或SQL Native Client Library都可以連接到SQL Database Server。

## Transact-SQL的支援

作為SQL Server版本Transact-SQL的子集，不是所有的功能在Windows Azure SQL Databsae上都有被支援，由於實體伺服器架構以及安全性的問題，許多分散式的查詢法以及常用的資料庫複製法都沒有辦法被Windows Azure SQL Databsae支援，而在SQL Server 2005開始加入的[SQL CLR能力也無法在Windows](../Page/SQL_CLR.md "wikilink") Azure SQL Databsae上支援（因為它必須要掛載在Windows Azure SQL Databsae實體伺服器上，但用戶端通常無法知道當下連到的伺服器是否為有安裝SQL CLR組件的那一台）。

受支援的Transact-SQL特性\[4\]：

  - 常數。
  - [資料限制](https://zh.wikipedia.org/wiki/資料限制 "wikilink")。
  - [資料游標](../Page/指標_\(資料庫\).md "wikilink")。
  - [資料庫索引管理與索引重建](https://zh.wikipedia.org/wiki/資料庫索引 "wikilink")。
  - 本地[資料庫暫存表格](https://zh.wikipedia.org/wiki/資料庫暫存表格 "wikilink")。
  - 保留字。
  - [預存程序](../Page/存储程序.md "wikilink")。
  - [資料庫統計管理](https://zh.wikipedia.org/wiki/資料庫統計 "wikilink")。
  - [資料庫交易](https://zh.wikipedia.org/wiki/資料庫交易 "wikilink")
  - [觸發程序](https://zh.wikipedia.org/wiki/觸發器_\(資料庫\) "wikilink")。
  - [資料庫表](https://zh.wikipedia.org/wiki/資料庫表 "wikilink")、[資料表聯結以及表格變數](https://zh.wikipedia.org/wiki/資料表聯結 "wikilink")。
  - Transact-SQL語言元素，像是對資料庫、表格、使用者與登入等的建立、修改與刪除。
  - [使用者定義函數](https://zh.wikipedia.org/wiki/使用者定義函數 "wikilink")。
  - [檢視表](https://zh.wikipedia.org/wiki/視圖 "wikilink")。

未受支援的Transact-SQL特性：

  - [SQL CLR](../Page/SQL_CLR.md "wikilink")。
  - 資料庫檔案配置。
  - 資料庫映射。
  - 分散式查詢。
  - 分散式交易。
  - 檔案群組管理。
  - 全域暫存表格。
  - 稀疏資料與索引。
  - SQL Server組態選項。
  - SQL Server Service Broker
  - 系統表格。
  - 追踪旗標。

## 安全性

Windows Azure SQL Databsae 的安全性有兩個部份，一個是管理傳輸層次安全性的防火牆，一個是管理存取控制的基本安全功能。

### 防火牆

每個 SQL Database Server 都會有自己的防火牆 (Firewall) 設定，管理人員可以自由設定下列不同的用戶端來源模型：

  - 只允許雲端應用程式存取 SQL Azure Server，網段設為 0.0.0.0-0.0.0.0
  - 單一或多重網址 (address)。
  - 單一或多重網段 (segment)。

SQL Database Server 的防火牆設定會儲存在 SQL Gateway 中，作為管控用戶端連線之用。

### 基本安全功能

SQL Database Server會有兩種安全群組\[5\]：

  - 伺服器角色：有`dbmanager`以及`loginmanager`兩種。
      - `dbmanager`：賦與使用者可以建立資料庫（即CREATE DATABASE指令）的權利。
      - `loginmanager`：賦與使用者可以建立登入帳戶（即CREATE LOGIN指令）的權利。
  - 資料庫角色：與安裝在本機或伺服器上版本的SQL Server相同。

SQL Database Server目前只支援使用SQL驗證（SQL Authentication）的安全驗證方式，以往的Windows驗證在Windows Azure SQL Database上不支援。而在SQL Database Server建立時，除了master資料庫以外，還會再多建立一個具有SQL Server的sa帳戶相等權力的帳戶，供使用者操作SQL Database Server用，此帳戶稱為伺服器級主帳戶（server-level principal），基於資料庫的安全，管理人員必須要在 SQL Database Server 中再建立一個或多個登入帳戶後，再授權給資料庫，用戶端應用程式不宜使用伺服器級主帳戶來存取 SQL Azure Server 與資料庫。

### 限制

Windows Azure SQL Database 基於架構上的設計與天生的限制，SQL Database Server的帳戶與安全控制會有下列限制\[6\]：

  - 只有伺服器級主帳戶才具有變更密碼的能力，`loginmanager`群組的成員帳戶不具變更密碼的權限，同時如果要存取master資料庫，則該使用者帳戶必須要被對應到master資料庫，同時伺服器級主帳戶是不可以變更或刪除的，同時只要是被設為伺服器級主帳戶的使用者，就算沒有給予`dbmanager`或`loginmanager`，仍然可以建立資料庫並管理使用者。
  - 只要是登入伺服器，一律以master為預設資料庫，US-English為預設的登入語系。
  - 若要執行`CREATE/ALTER/DROP LOGIN`或`CREATE/DROP DATABASE`，必須要先連至master資料庫。
  - 當要在[ADO.NET](../Page/ADO.NET.md "wikilink")執行前述指令時，不可以使用參數化命令，而且前述命令於每個SQL批次也只能有一個（且是唯一的一個）。
  - 當要執行`CREATE USER`配合`FOR/FROM LOGIN`選項時，它也必須是SQL批次中唯一的一個。
  - 當要執行`ALTER USER`配合`WITH LOGIN`選項時，它也必須是SQL批次中唯一的一個。
  - 只有伺服器級主帳戶以及被賦與`dbmanager`角色的成員才有執行`CREATE DATABASE`與`DROP DATABASE`的權力。
  - 只有伺服器級主帳戶以及被賦與`loginmanager`角色的成員才有執行`CREATE LOGIN`、`ALTER LOGIN`與`DROP DATABASE`的權力。
  - 若想存取master資料庫，則該帳戶必須要對應到master資料庫。

## 工具與開發支援

Windows Azure SQL Database 基於資料庫雲端化並降低學習曲線的主要訴求之下，開發工具與管理工具基本上會與 SQL Server 完全相同，但也有基於 SQL Database 所發展的工具。

### 開發工具

開發人員可利用Visual Studio 2010 的伺服器管理員也可以連接到 SQL Database Server 並管理資料庫與資料結構。SQL Server 2008 (非R2) 則可透過輸入連線字串的方式連接 SQL Database Server，或是使用命令列工具 sqlcmd.exe 連到 SQL Database Server。在 Windows Azure SQL Database 管理介面中可獲得連線字串的範例。

SQL Database Server 可接受 TDS over SSL 的通訊與指令，因此開發人員可利用 ADO, ADO.NET, [Entity Framework](https://zh.wikipedia.org/wiki/ADO.NET_Entity_Framework "wikilink"), [LINQ to SQL](https://zh.wikipedia.org/wiki/LINQ "wikilink") 或其他可產生 TDS over SSL 的用戶端函式庫 (ex: SQL Native Client, JDBC, SQL Server Driver for PHP 等) 來存取 SQL Database Server 與資料庫。

### 管理工具

SQL Server Management Studio 可直接管理 Windows Azure SQL Database ，但目前只有 SQL Server 2008 R2 可完全相容於 Windows Azure SQL Database 的管理，而 SQL Server 2008 的 SSMS 僅支援 Transact-SQL 指令層次的管理，SQL Server 2005 以及更早版本的 SQL Server 管理工具則無法支援。除了 Management Studio 以外，微軟也在 Windows Azure Portal 中設計了 SQL Azure Database Manager (原先的 SQL Azure Web Administrator)，讓管理人員得以直接利用 Windows Azure Portal 來管理資料庫內的物件 (如資料表，預存程序，檢視表等物件)。

### 服務管理 API

Windows Azure SQL Database 在2011年五月份的更新中，加入了一組服務管理的 API，稱為 SQL Azure Server API，它允許開發人員使用與 Windows Azure 服務管理 API 相似的方式存取 Windows Azure SQL Database 上的管理資訊，並且可直接下指令給 SQL Database Server 來執行一些管理工作。

## 其他服務

### OData Services

這是在 Windows Azure SQL Database 開發初期時提供的 REST API 群，在 SQL Azure 團隊決定使用 TDS 協定開放 SQL Azure 資料庫後即暫停開發，在 Windows Azure SQL Database 服務正式發布後，這個 REST API 群即恢復開發，此 REST API 可符合 [OData](https://zh.wikipedia.org/wiki/OData "wikilink") 協定規格，目前已經停止開發，由 ASP.NET MVC OData 支援或 WCF Web API OData 支援功能取代。

### SQL Reporting

這是 Windows Azure SQL Database 上的 Reporting Services，可以讓企業與開發人員直接利用 SQL Azure 資料庫來產制 Business Intelligence 的解決方案，SQL Reporting Services 可支援 SQL Server Reporting Services 的大部份功能，並且沿用 Business Intelligence Development Studio 作為報表開發的工具。

### SQL Data Sync

SQL Data Sync 是微軟開發作為雲端 (Cloud) 與本地端 (On-premise) 資料同步化的服務，以[Microsoft Sync Framework為基礎的同步工具](https://zh.wikipedia.org/wiki/Microsoft_Sync_Framework "wikilink")，可以在雲端與企業內部或用戶端 (手持式裝置或是電腦) 進行資料的同步工作。

## 参考文献

## 外部連結

[SQL Azure MSDN Online Documentation](http://msdn.microsoft.com/en-us/library/ee336279.aspx)
[SQL Server Data Services Official Site](http://www.microsoft.com/sql/dataservices/default.mspx)

[Category:資料庫](https://zh.wikipedia.org/wiki/Category:資料庫 "wikilink") [Category:Microsoft_Azure](https://zh.wikipedia.org/wiki/Category:Microsoft_Azure "wikilink") [Category:微軟](https://zh.wikipedia.org/wiki/Category:微軟 "wikilink")

1.
2.
3.  [SQL Database Pricing Information](http://www.microsoft.com/en-us/sqlazure/purchase.aspx)
4.  [Overview of Transact-SQL](http://msdn.microsoft.com/en-us/library/ee336250.aspx)
5.  [Managing Logins and Users in SQL Database](http://msdn.microsoft.com/en-us/library/ee336235.aspx)
6.  [Guidelines and Limitations](http://msdn.microsoft.com/en-us/library/ee336245.aspx)