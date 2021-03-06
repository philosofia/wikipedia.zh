> 本文内容由[Active Directory](https://zh.wikipedia.org/wiki/Active_Directory)转换而来。


**Active -{}-Directory**（简称**AD**。中国大陸譯名為「活動目錄」，台灣为維持英文不譯）是[微軟](https://zh.wikipedia.org/wiki/微軟 "wikilink")[Windows Server中](../Page/Windows_Server.md "wikilink")，負責架構中大型[網路環境的集中式](https://zh.wikipedia.org/wiki/網路 "wikilink")[目錄管理服務](https://zh.wikipedia.org/wiki/目錄服務 "wikilink")（Directory Services），在[Windows 2000 Server開始內建於Windows](https://zh.wikipedia.org/wiki/Windows_2000_Server "wikilink") Server產品中，它處理在組織中的網路物件，物件可以是使用者，群組，電腦，網域控制站，郵件，設定檔，組織單元，樹系等等，只要是在Active Directory結構定義檔（schema）中定義的物件，就可以儲存在Active Directory資料檔中，並利用[Active Directory Service Interface來存取](../Page/Active_Directory_Service_Interface.md "wikilink")，實際上，許多Active Directory的管理工具都是利用這個介面來呼叫並使用Active Directory的資料。

Active Directory也被做為微軟部份[伺服器](https://zh.wikipedia.org/wiki/伺服器 "wikilink")[軟體與](https://zh.wikipedia.org/wiki/軟體 "wikilink")[網域構連的資料結構](https://zh.wikipedia.org/wiki/Windows_Server_Domain "wikilink")，例如[Microsoft Exchange Server 2003-2007](../Page/Microsoft_Exchange_Server.md "wikilink")，均使用AD來儲存其個人[信箱資料](https://zh.wikipedia.org/wiki/电子信箱 "wikilink")（透過建立新的Active Directory Schema），並將AD列為建置Exchange Server的必要條件。

Active Directory最早在1996年出現，並在Windows 2000中首次問世，[研發代號為](https://zh.wikipedia.org/wiki/代号 "wikilink")**Cascade**，並歷經Windows 2000、[Windows Server 2003的演化](../Page/Windows_Server_2003.md "wikilink")，目前AD已成為成熟的目錄服務元件，在[Windows Server 2008中](../Page/Windows_Server_2008.md "wikilink")，AD更擴充其角色至五種服務（包含憑證、聯合、權限控管與輕量級服務等）。

## 目錄結構

Active Directory(AD)以[樹狀的資料結構來組成網路服務的資訊](../Page/树_\(图论\).md "wikilink")，在簡單的網路環境中（例如小公司），通常網域都只有一個，在中型或大型的網路中，網域可能會有很多個，或是和其他公司或組織的AD相互連結（此連結稱為信任關係，於後面說明）。

### 物件

Active Directory的最小儲存單元為物件（object），每個物件均有自己的schema屬性，可以儲存不同的資料，像是使用者、群組、電腦、信箱或其他的基本物件等。

一個AD網域底下的基本物件，有：

  - Domain Controllers，儲存網域所屬的網域控制站（簡稱DC、域控）。
  - Computers，儲存加入網域的電腦物件。
  - Builtin，儲存內建的帳戶群組。
  - Users，儲存AD中的使用者物件。

若公司需要以不同的組織結構來管理公司的帳戶，則可以在AD中建立一個或多個組織單元（Organization Unit，簡稱OU），組織單元是一個具有收納能力的Active Directory物件（其在ADSI中是IADsContainer介面），可以在OU之中存放AD的物件，包括使用者，群組，電腦等，讓組織結構在AD中可以被真實的反映出來，而且也方便AD中的另一個功能——群組原則（Group Policy）的套用與集中管理。

### 樹系與多網域

[ActiveDirectory_DomainTree.png](https://zh.wikipedia.org/wiki/File:ActiveDirectory_DomainTree.png "fig:ActiveDirectory_DomainTree.png") [ActiveDirectory_DomainTree_WithSubDomain.png](https://zh.wikipedia.org/wiki/File:ActiveDirectory_DomainTree_WithSubDomain.png "fig:ActiveDirectory_DomainTree_WithSubDomain.png")

若組織的網路環境相當龐大與複雜時，網域可能會有許多個，在AD之中，網域可以有一個或多個，而一個大型公司可能會利用分公司或是辦公室的方式來組織網域物件，如此一來，在AD中會有數個網域，若需要在網域中共享資料或是做委派管理與組態設定時，便需要建立彼此間的組織關係，微軟將AD中多網域相互的關係階層化，稱為網域樹（domain tree），網域樹結構以[DNS識別方式來區分](https://zh.wikipedia.org/wiki/DNS "wikilink")，例如一間公司可能有業務部門，工程部門與管理部門，那麼若要以部門來建立網域時，則可以如此建立（如右圖）：

  - acme.com.tw：根網域。
  - sales.acme.com.tw：業務部門。
  - engineering.acme.com.tw：工程部門。
  - admin.acme.com.tw：管理部門。

如此便可在AD中反映出組織的結構，同樣的，網域內還是可以再建立不同的網域，例如在工程部門中若需要分為軟體部門與硬體部門時，還可以在工程部門的網域中建立：

  - software.engineering.acme.com.tw：軟體部門的網域。
  - hardware.engineering.acme.com.tw：硬體部門的網域。

而軟體部門和硬體部門的設定，會自動的繼承工程部門網域中的群組原則設定，而在軟體部門的組態，則不會影響到硬體部門（可經過設定來套用）。

### 森林

[ActiveDirectory_Forest.png](https://zh.wikipedia.org/wiki/File:ActiveDirectory_Forest.png "fig:ActiveDirectory_Forest.png")

在多個網域的環境下，可能在不同的網域之間會需要交換與共享資料，像是組態設定、使用者帳戶與群組原則設定等，在這個時候需要有一個角色來做為不同網域間的資訊交換角色，同時又必須要符合AD樹狀結構的規範，因此微軟在多網域之間建立了一個中介用的角色，稱為森林（Forest），一個組織中最多只能有一個Forest，在Forest下則是各自的網域樹系，而在Forest下的網域或網域樹系間，可以共享資訊。

## 實體結構

Active Directory背後，則是一個植基於Windows Server網路基礎結構（infrastructure）的網路服務與通訊方式所組成，這些網路服務和通訊方式讓Active Directory具有高度的擴充性與向後相容性等，網路管理人員必須要妥適的設定與監控這些網路服務與通訊方式，以讓Active Directory能夠正常且順利的運作。

在以往的[Windows NT網域環境中](../Page/Windows_NT.md "wikilink")，網域的實體結構分為三種角色，即主要網域控制站（Primary Domain Controller, PDC）、備份網域控制站（Backup Domain Controller, BDC）以及成員伺服器（Member Server）三種，網域的資料都儲存在PDC和BDC中，並且在PDC和BDC間交換資料，但PDC和BDC的部署方式並不方便（一個網域只能有一個PDC），在不同的地理環境中也不能設置PDC，而且所有網域的查詢都會被導向PDC，如此很容易造成網域登入和存取的塞車情況，這個問題在Active Directory中已獲得改善，即不再有BDC（只有DC和Member Server兩種角色），在網域中的任何一台網域控制站都可以負責處理來自用戶端的網域查詢，如此在分散部署上會具有相當的彈性。

### Global Catalog

在AD的實體結構中，最重要的角色非Global Catalog\[1\]（全域目錄，簡稱GC）莫屬，它儲存了最完整的Active Directory的結構資料，也是以目錄為主（directory-enabled）的應用程式對AD的查詢的主要標的，而通常在不同的地理位置（例如在中國大陸、台灣、美國和英國各有分公司，且各有網域）時，GC扮演了重要的快取結構角色，若台灣的員工出差到英國分公司，並試圖登入網域時，Windows會先搜尋最近的Global Catalog Server（由DNS設定提供），若找不到時，才會連結到其他地區的GC，但若分公司的網路很慢時，這種跨地理位置的AD資料存取會直接影響到登入的時間，因此謹慎的GC的佈署對AD的推行是很重要的。

### Operation Masters

[營運主機](https://zh.wikipedia.org/wiki/營運主機 "wikilink")（Operation Masters，又稱為Flexible Single Master Operation，即[FSMO](https://zh.wikipedia.org/wiki/FSMO "wikilink")）\[2\]是被設定為擔任提供特定角色資訊的網域控制站，在每一個Active Directory網域中，至少會存在三種營運主機的角色。

  - Primary Domain Controller Emulator Master：設定作為這個角色的網域控制站，可以被目前仍存在網域中的Windows NT Backup Domain Controller（備份網域控制站）當做Primary Domain Controller （主要網域控制站）來呼叫使用，同時它也是樹系中提供Windows Time Service時間同步的主機。
  - RID Master：在網域控制站中會儲存AD物件的relative ID（關聯識別碼），可分散以RID為主的查詢的流量。
  - Infrastructure Master：負責處理對目前網域的物件參考，以及對應其他網域的物件參考，並可負責處理針對AD物件的變更（例如刪除與更名）。

另外還有兩種角色，是具有額外功能，但不強制部署在網域的：

  - Schema Master：負責處理網域中所有針對物件結構的變更。
  - Domain Naming Master：負責處理網域中的目錄分割以及應用目錄分割的工作。

### Site

Active Directory站台（site），是指一個實體的網路位置，在一個站台中可能會有很多個網域控制站，AD網域資料的複製，就是以站台為主，實際處理複製作業的工具稱為KCC（Knowledge Consistency Checker，知識一致性檢查器），它會在特定時間對站台設定中的網域進行資料的同步化，複製活動則分為對內複製（intra-site replication）與對外複製（或站間複製，inter-site replication），對內複製是同一個網域間的控制站交換資訊，對外複製則是在網路管理人員的設定下，透過指定的通訊方法（IP或SMTP）以及拓樸進行複製。

預設情況下，站台的通訊方式是使用IP（即RPC over IP）來通訊，這個方式是最快的，且可以利用[TCP/IP來執行遠端呼叫以及處理](https://zh.wikipedia.org/wiki/TCP/IP "wikilink")，但若是非網域資料（架構、設定和通用類別目錄更新，亦即沒有AD物件）的複製，則可以利用[SMTP通訊方法](https://zh.wikipedia.org/wiki/SMTP "wikilink")，但這個方法需要另外建立企業級的憑證服務才可以使用，目的是確保SMTP的資料可以被確認與保全。

在中大型的網路環境中，適當的分散網路流量以及設計網路拓樸是很重要的事，KCC會利用設定好的網路通訊成本（cost）來選擇要用哪一條網路來進行複製，例如可能公司和辦公室間有一條[T1](../Page/T1.md "wikilink")和[ISDN](https://zh.wikipedia.org/wiki/ISDN "wikilink") 64Kbps的線路，而T1的成本設為500（因為會有很大流量），而ISDN只有100時，KCC會選擇ISDN做複製，這樣代表網路管理員可以自己決定要使用哪一條網路來進行複製，KCC的複製演算法會判斷哪一個網路最適合複製AD的資料。除了成本以外，AD也支援了橋接站台（site bridge）的結構，站台橋接能力讓複製的成本得以分散，並可讓同一台GC的複製流量分散，也適合在不同地理區域之間的AD資訊複製與散發工作。。

### DNS

Active Directory極度依賴[DNS](https://zh.wikipedia.org/wiki/DNS "wikilink")，因為DNS可以讓AD表現出階層化的樹狀結構，同時也可以和開放的目錄標準接軌，因此在建置網域時，DNS服務（或另有架設DNS Server）一定要存在於網路或該網域控制站中，AD以SRV記錄（SRV Record）來識別網域控制站，以提供網域處理的服務，而和Windows NT網域不同的是，Windows NT使用的是[NetBIOS](../Page/NetBIOS.md "wikilink")通訊協定，但AD使用的則是[TCP/IP](https://zh.wikipedia.org/wiki/TCP/IP "wikilink")，但AD仍然提供可以在Windows NT帳戶格式（DOMAIN\\User）和AD帳戶格式（user@domain）的格式互轉。

### 實體儲存

Active Directory使用強化過的[Microsoft Jet Database Engine](../Page/Microsoft_Jet_Database_Engine.md "wikilink")（基於Microsoft Jet Blue計畫），即[Extensible Storage Engine](https://zh.wikipedia.org/wiki/Extensible_Storage_Engine "wikilink")（ESE98），可儲存16TB的資料量，理論上可容納十億個網域物件，檔案名稱為NTDS.dit，它儲存在%system_root%\\NTDS目錄中（這個目錄所在的磁碟也必須要是[NTFS](../Page/NTFS.md "wikilink")格式），內含了物件資料表以及連結資料表，在Windows Server 2003中加入了一個描述安全資訊的新資料表。

而在AD更新資料時的記錄，都被儲存在edb\*.log，預設的名稱為edb.log，其他的檔案使用"edb" +數字 + ".log"來記錄，另搭配了edb.chk作為檢查點記錄檔，以及Res1.log和Res2.log作為系統的保留檔案。

AD實體儲存的元件有\[3\]：

  - 上層介面（interface）：作為目錄服務用戶端或目錄服務中的其他伺服器的連接介面，像是LDAP、REPL、MAPI與SAM等。
  - 目錄服務代理人（Directory Service Agent）：實作於NTDSA.DLL，負責接收與處理來自用戶端的要求或其他伺服器的要求（例如KCC的要求）。
  - 資料庫存取層：內含於ntdsa.dll中，負責直接存取資料庫。
  - 延伸儲存引擎（Extensible Storage Engine）：負責處理資料庫與其名稱（DN）的記錄對應。
  - 資料庫檔案：即NTDS.dit，以及負責處理未認可交易的記錄檔。

網域控制站會定時（預設為12小時）對NTDS.dit做重組（defragment），並清除資料檔中的垃圾，在重組前會檢查磁碟空間是否有大於資料庫檔案1.5倍的空間可用。若資料庫所在的目錄沒有足夠的可用空間，就要把資料庫移往其他地方去。然而，由於Windows 2000與Windows Server 2003在[磁碟區陰影複製服務](../Page/磁碟區陰影複製服務.md "wikilink")（VSS）的機制有所不同，使這移動過程有可能失敗。對於Windows 2000，log files與數據庫可以分別存放在不同的磁碟上，但Windows Server 2003則必須放在同一個磁碟上。要移動資料庫，必須重新啟動伺服器，並進入Active Directory Restore Mode裡，利用[ntdsutil工具進行移動](https://zh.wikipedia.org/wiki/ntdsutil "wikilink")。

### 唯讀網域控制站

在[Windows Server 2008中](../Page/Windows_Server_2008.md "wikilink")，加入了一個新的網域控制站角色，稱為唯讀型網域控制站（Read-Only Domain Controller，簡稱RODC），RODC可以作為組織的分部、分公司、辦公室或是臨時單位等，將網域控制站放在該處時會有安全性疑慮或風險時使用，顧名思義，RODC不會寫入任何資料到Active Directory，與其他網域的複寫也是有限度的，並且只會以系統管理員定義的Password Replication Policy（密碼複製原則）控制下的帳戶才會快取密碼等功能。

若要在AD中加入唯讀網域控制站，則網域的功能層級必須要在Windows Server 2003以上。

## 安全性

Active Directory的安全性可分為物件的安全性識別、階層的安全性以及森林之間的信任關係等。

### 安全性識別

AD以[Kerberos](../Page/Kerberos.md "wikilink") V5作為其安全驗證的主要架構，並且每個AD物件都擁有一個獨一無二的安全性識別碼（Security Identifier，SID），其格式範例為S-1-5-21-7623811015-3361044348-030300820-1013，每組代碼均有其意義，這組識別碼儲存在AD的objectSid屬性中。

### 階層的安全性

在AD中，不同階層的OU可以定義不同的安全性資訊，以及不同的使用者權限，而不同的網域階層之間也可以定義不同的使用者權限，管理員也可以利用安全性管理範本（Secutiy Template）來定義不同的安全性資訊，或者使用群組原則（Group Policy）來定義，在大型網路之中，使用群組原則會比安全性範本要來的方便，將兩者合併使用更可達到事半功倍之效（例如和Microsoft Base Security Analyzer的整合）。

在父階層定義的安全性，可以被繼承至子階層。

### 信任關係

在大型的網路環境中，可能組織間有夥伴關係，或者是專案間的合作，而需要在兩個Forest間共享或授權存取時，可以利用信任關係（trust relationship）來建立Forest間的信任，以授權在彼此樹系間的存取權，在Windows Server 2003以後版本的AD環境可支援四種信任關係：

  - **捷徑式信任（shortcut trust）**，此為加速驗證流程所設計的信任法，在多層次的網域中，使用者只要連接到最近的網域即可登入，無需要將訊息轉到授權的根服器。
  - **外部式信任（external trust）**，此為跨森林的授權方法。
  - **領域式信任（realm trust）**，作為與非Kerberos驗證的LDAP目錄服務與Windows網域的信任模式。
  - **森林式信任（forest trust）**，此為強化型的外部式信任法，可以經由一個中介的森林信任來取得信任關係，例如acme.com.tw信任aspvendor.com，而contoso.com.tw也信任aspvendor.com，則acme.com.tw可以取得和contoso.com.tw的信任關係。

信任關係的設定可以分為單向（one-way）和雙向（two-way）兩種，單向信任表示被信任的一方可以存取信任的一方的資源，而雙向信任則是可以存取各自的資源。

信任關係的傳遞可分為可遞移（transitive）與不可遞移（non-transitive）兩種，可遞移表示建立信任關係的網域在同一樹系內的其他網域也可以使用在建立信任關係網域中的信任資訊，不可遞移則表示只有建立信任關係的網域（不論是否有階層）才可以使用信任資訊。

## 名稱系統

Active Directory的命名預設是以[LDAP](https://zh.wikipedia.org/wiki/LDAP "wikilink")（輕量級目錄存取協定）版本的[X.500協定為主](https://zh.wikipedia.org/wiki/X.500 "wikilink")（由ADSI LDAP Directory Service Provider），對於AD這種如此規模的目錄服務而言，LDAP這種具有階層識別能力的協定，非常適合作為目錄服務的存取協定，但AD亦可以支援NT時代的UNC格式（由ADSI Windows NT Directory Service Provider提供），在UNC與LDAP名稱間的轉換則由ADSI的`IADsNameTranslate`介面來提供。

### 識別名

每個AD物件均有一個以LDAP組成的名稱，稱為識別名（Distinguished name，簡稱DN），這個識別名是作為使用LDAP查詢AD目錄中識別物件的名稱，其格式類似下列：

``` text
LDAP://cn=John Smith, ou=Software Engineering, dc=engineering, dc=acme, dc=com, dc=tw
LDAP://cn=COMP1024, ou=Computers, dc=acme, dc=com, dc=tw
```

在LDAP字串中經常使用的代字有：

  - **DC**：domainComponent
  - **CN**：commonName
  - **OU**：organizationalUnitName
  - **O**：organizationName
  - **STREET**：streetAddress
  - **L**：localityName
  - **ST**：stateOrProvinceName
  - **C**：countryName
  - **UID**：userid

當用戶端在下達LDAP查詢字串時，若無法符合AD物件的LDAP DN，則會找不到資料，LDAP代字亦可使用於搜尋（IADsDSObject與ADsDSObject(），參見[Active Directory Service Interface條目](../Page/Active_Directory_Service_Interface.md "wikilink")）。

### 一般名稱

每個AD中的物件都會有一個一般的名稱，又稱為別名（Canonical Name），在Schema中的屬性為cn（Common Name），但組織單元（OU）基本上是例外，它自己有一個代字ou作為識別符。

### 關聯識別名稱

為了要在容器與物件間作識別，在Schema中設定了一個Relative Distinguished name（簡稱RDN），儲存在rDnAttId屬性中，可在搜尋AD時可以快速的對應容器內的物件。

### GUID

每一個物件都有一個唯一的GUID物件識別碼，儲存在objectGUID屬性中，其編碼方式與[GUID相同](https://zh.wikipedia.org/wiki/GUID "wikilink")。

### 其他名稱

  - Windows NT使用者名稱系統：即SAM（Security Account Manager）的名稱系統，儲存在使用者的`sAMAccountName`屬性中。
  - 使用者主體名稱：即User Principal Name，在AD中使用者是以`user@domain`的方式呈現，這個值儲存在`userPrincipalName`屬性。

## 功能層次

Active Directory於是一個開放式的目錄服務，而且為了要能夠容納不同版本的Windows作業系統以及其網域，因此特別在AD中使用了一種版本控制的機制，稱為功能層次（functional level），功能層次定義了目前在網域環境中可以使用的最大版本層次，同時這個修改是單向無法復原的修改。若網域中有不同版本作業系統的網域控制站，則為了最大的相容性，功能層次的設定應要以最低版本為主，例如一個網域中有Windows Server 2003和Windows 2000時，則網域的功能層次應該設為Windows 2000混合模式（Mixed Mode），若設為Windows Server 2003原生模式（Native Mode）時，Windows 2000的網域控制站會失效。但由於新版本的AD設定通常都會比前版的要強（尤其是安全性的改進），因此若網域中沒有前版本的作業系統，則應將功能層次設定到最新版本，以開放AD的所有功能。

另外，若要在網域中安裝新版本的作業系統（例如在Windows Server 2003網域中要安裝Windows Server 2008）作為網域控制站時，必須要先將Active Directory中的Schema資訊做擴充以相容於較新版本的作業系統，因此微軟在安裝光碟中都會提供一個Active Directory準備工具 (adprep.exe），它可以讓系統管理員以簡單的方式升級Active Directory中的資料結構，包含樹系以及網域的資料結構（使用參數設定），以相容於新版本作業系統。

  - `adprep /forestprep`：升級樹系的資料結構。
  - `adprep /domainprep`：升級網域的資料結構。
  - `adprep /rodcprep`：準備網域以提供RODC（唯讀網域控制站）的功能（Windows Server 2008以後版本才支援）。

對於Windows NT的BDC，則不是透過功能層次的設定，而是用Operation Master的PDC Emulator來保持相容性。

## 物件結構

由於微軟在設計Active Directory是使用開放型的目錄服務為方針，且目錄服務的最基本特性之一就是要能「廣納百川」，除了基本的網路服務資料外，還需要能夠和其他異質型服務連接與整合，因此微軟在AD之中實作了一個物件的儲存單位，稱為「物件結構」（schema），物件結構可以視為AD物件的[元數據](https://zh.wikipedia.org/wiki/元數據 "wikilink")（metadata）。每一個物件（不論是單元或是容器物件）都有各自的schema，用以儲存識別該物件的不同資料，schema是由class和attribute所組成，attribute是最小的儲存單元，class則是包含attribute的集合體。

儲存在attribute中的資料有很多種格式，微軟將這些格式定義成27種Schema資料型態，像是指示帳戶過期日的`Account-Expires`屬性，其值是interval資料型態（代表時間週期，為一個64位元整數值），又如指示帳戶SAM名稱的`sAMAccountName`屬性，其值是String（Unicode）值（支援Unicode的字串值），又如儲存使用者的照片的`Picture`屬性，其值是Object(Repl-Link，代表是位元組資料，且可以複製到其他網域控制站）。

微軟也開放了可延伸schema的方法\[4\]，開發人員可以利用這一套方法來延伸Active Directory Schema中的資料，但一旦寫入AD後，即不可刪除（因為物件識別碼不可更動），但是可以停用，延伸AD Schema最好的例子就是Microsoft Exchange Server。

## 服務

Active Directory本身除基本的網路目錄服務外，微軟也應用這個基礎架構設計了不同的服務，並且在Windows Server 2003不同的版次中加入，以提升Active Directory的應用範圍。

### 聯合服務

由於AD本身具有可分散式的身份驗證與授權能力，且在2003年時Web正吹起了單一簽入（single-sign on）的架構研究風，微軟也開始利用AD來設計一個可支援多個網站（或應用程式）的單一簽入功能，其實作品即為Active Directory Federation Services（AD聯合服務，簡稱ADFS），它顯露了幾個主要成員\[5\]：

  - Federation Service：負責在ADFS的SSO架構中處理驗證的伺服器。
  - Federation Service Proxy：在外部網路或是WS-I服務中，扮演Federation Service的代理角色，並支援WS-Federation規格的驗證設定。
  - Claim-aware client：由ADFS開放的Claim-aware（宣告感知）元件的Web用戶端，或是[ASP.NET](../Page/ASP.NET.md "wikilink")應用程式，可直接支援ADFS的SSO架構。
  - Windows Token-based Agent：以Windows驗證為主的Web應用程式，ADFS可支援AD權仗與Windows NT權仗的模擬與交換。

此服務在Windows Server 2003 R2版本中首次出現，並在Windows Server 2008中升級為Active Directory Federation Service角色。

### 輕量級服務

輕量級服務（Lightweight Directory Service）\[6\]在Windows Server 2003中被稱為Active Directory Application Mode（ADAM），它是一個不需要與AD基礎架構整合就可以獨立運作的目錄服務，適合用來表現企業的階層化概念與物件的管理，而且開發人員只要把使用ADSI的經驗搬過來即可使用，不必另外學習ADAM的操作方法，它也可以做為ADFS的外部驗證提供者。輕量級目錄可以在同一台電腦中安裝多個執行個體，因此也很適合用ADAM來實作Directory-Enabled的應用程式，尤其是與組織結構相關的（例如人事或人力資源系統），ADAM本身也可以延伸schema，開發人員可以將ADAM視為另一種型式的資料庫，也可以由AD中複製資料到ADAM，不過ADAM不會對AD進行站台複製，開發人員需要自行撰寫程式來複製資料。

輕量級服務在Windows Server 2008中改名為Active Directory Lightweight Directory Service（簡稱AD LDS），並提升為AD的應用角色之一。

### 憑證服務

憑證服務（Certificate Service）\[7\]是在Windows Server 2008中首次納入Active Directory體系的服務，它原本是在Windows 2000與Windows Server 2003的憑證伺服器（Certificate Server），用來建立企業中的[公開金鑰基礎建設](../Page/公開金鑰基礎建設.md "wikilink")，在Windows Server 2008中，憑證和AD物件有了更強更緊密的整合，所以有了Active Directory Certificate Service（AD CS）的角色，這個角色還可以和權限管理的Right Management Service（RMS）整合在一起，提供對文件或應用程式層次的權利管理。

### 權利管理服務

權利管理服務（Right Management Service）\[8\]也是在Windows Server 2008中首次納入Active Directory體系的服務，最早的時候，它是在[Microsoft Office 2003開始提出的資訊權利管理](../Page/Microsoft_Office.md "wikilink")（Information Right Management）功能，可利用它來控制Office文件散布時的權限，例如列印以及儲存檔案等，接著微軟發表了Right Management Server以及RMS SDK，供Windows Server 2003平台使用，而在Windows Server 2008中即將它整合到Active Directory中，變成AD服務的一部份。

## 整合Unix到Active Directory中

Active Directory互通的多樣性層次得以透過符合標準的LDAP用戶端在大多數的[類Unix作業系統記錄](https://zh.wikipedia.org/wiki/類Unix作業系統 "wikilink")，但這些系統通常缺乏與Windows元件像是群組原則與單向信任關聯的許多屬性的自動直譯，目前也有許多第三方軟體廠商提供了將Unix平台（包含[UNIX](../Page/UNIX.md "wikilink")、[Linux](../Page/Linux.md "wikilink")、[Mac OS X與數個](https://zh.wikipedia.org/wiki/Mac_OS_X "wikilink")[Java](../Page/Java.md "wikilink")與Unix-based應用程式）整合Active Directory方法，這些供應商的一部份，包含Thursby Software System（ADmitMac）, Quest Software（Vintela Authentication Services）, Centrify（DirectControl），與Likewise Software（Likewise Open and Likewise Enterprise）。Microsoft也在這個市場中擁有為UNIX產品所設計的免費Microsoft Windows服務（即Windows Service for Unix）。

這些額外的物件結構在Windows Server 2003 R2版本中被釋出，包含完全對應到RFC 2307的一般用途的屬性。這些RFC 2307、nss_ldap與pam_ldap的參考實作均提供自PADL.com，包含直接使用這屬性以及填充資訊的支援。預設群組成員（group membership）的Active Directory Schema與被提議的RFC 2307bis延伸功能一起編譯。RFC 2307bis使用LDAP成員屬性儲存Unix的群組成員資料，與基礎RFC 2307，以儲存群組成員為以逗號分隔的使用者識別碼清單有所不同。Windows Server 2003 R2包含了一個[MMC](https://zh.wikipedia.org/wiki/Microsoft_Management_Console "wikilink") snap-in以建立與編輯這些屬性。

一個替代選項是使用其他的目錄服務，像是[Fedora](../Page/Fedora.md "wikilink") Directory Server（之前的Netscape Directory Server）或是[Sun的Java](https://zh.wikipedia.org/wiki/Sun "wikilink") System Directory Server，它可以執行與Active Directory雙向同步化，進而在需要使用FDS驗證的Unix與Linux平台與需要使用Windows驗證的Windows用戶端之間，提供一個與Active Directory之間**轉向**（deflected）的整合。另一個選項是使用[OpenLDAP](../Page/OpenLDAP.md "wikilink")以及它的透通覆蓋（translucent overlay）功能得以延伸項目於使用額外屬性儲存在本地資料庫的任何遠端LDAP伺服器上。在本地資料庫中指示的用戶端將會看到包含在遠端和地的屬性，當遠端資料庫仍保持完整不變的情況下。

[Samba 4](../Page/Samba.md "wikilink")，在2012年12月11日发布的 Samba 4\[9\]中包含了一個Active Directory相容伺服器。

## 参考文献

## 外部链接

1.  [Windows Server 2003 Technical Library:Active Directory Collection](http://technet.microsoft.com/en-us/library/cc780036.aspx)

2.  [Infrastructure Planning and Design:Active Directory Domain Services](http://technet.microsoft.com/en-us/library/cc268216.aspx)

3.  [Windows Server 2008 Active Directory](https://web.archive.org/web/20081226154209/http://www.microsoft.com/taiwan/windowsserver2008/prodinfo/active-directory.aspx)

4.  [微软活动目录产品官方网页](http://www.microsoft.com/windowsserver2003/technologies/directory/activedirectory/default.mspx)

5.  [WINS](../Page/WINS.md "wikilink")（Windows Internet Naming Service）

6.  [分布式管理任务课题组](http://www.dmtf.org)

7.  [Linux系统上的活动目录](https://web.archive.org/web/20060221034826/http://www.pcquest.com/content/linux/2005/105010303.asp)

## 参见

  - [活动目录服务接口](https://zh.wikipedia.org/wiki/活动目录服务接口 "wikilink")
  - [Windows开放服务架构](https://zh.wikipedia.org/wiki/Windows开放服务架构 "wikilink")
  - [微软目录同步服务](https://zh.wikipedia.org/wiki/微软目录同步服务 "wikilink")
  - [群組原則](https://zh.wikipedia.org/wiki/群組原則 "wikilink")

{{-}}

[Category:活动目录](https://zh.wikipedia.org/wiki/Category:活动目录 "wikilink") [Category:認證方法](https://zh.wikipedia.org/wiki/Category:認證方法 "wikilink") [Category:微软服务器技术](https://zh.wikipedia.org/wiki/Category:微软服务器技术 "wikilink") [Category:Windows组件](https://zh.wikipedia.org/wiki/Category:Windows组件 "wikilink")

1.  [Global Catalogs](http://technet.microsoft.com/en-us/library/cc728188.aspx)
2.  [Operation Masters](http://technet.microsoft.com/en-us/library/cc779716.aspx)
3.  [Directory Data Store](http://technet.microsoft.com/en-us/library/cc772829.aspxActive)
4.  \[<http://msdn.microsoft.com/en-us/library/ms676900（VS.85>）.aspx Extending the schema\]
5.  [Directory Federation Services概觀](http://technet.microsoft.com/zh-tw/library/cc772593.aspxActive)
6.  [Directory輕量型目錄服務概觀](http://technet.microsoft.com/zh-tw/library/cc754361.aspxActive)
7.  [Directory憑證服務概觀](http://technet.microsoft.com/zh-tw/library/cc731564.aspxActive)
8.  [Directory Rights Management Services概觀](http://technet.microsoft.com/zh-tw/library/cc771627.aspxActive)
9.  [Samba4.0 Release](https://www.samba.org/samba/history/samba-4.0.0.html)