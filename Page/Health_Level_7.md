> 本文内容由[Health Level 7](https://zh.wikipedia.org/wiki/Health_Level_7)转换而来。


**HL7**指的是一組用於在各種醫療服務提供者所使用之軟體應用程式之間，傳輸臨床和管理數據的國際標準。這些標準側重於應用層，即OSI模型中的“第7層”。 HL7標準由國際標準組織[Health Level Seven International](https://www.hl7.org)製作，並被美國國家標準協會和國際標準化組織等其他標準發布機構採用。醫院和其他醫療保健提供者組織通常具有許多不同的資訊系統，用於計費記錄到患者追蹤等所有內容。這些所有的系統在接收新訊息時，或者當他們希望檢索訊息時，應該彼此通信（或“接口”），但並非所有系統都這樣做。 HL7 International規定了許多靈活的標準、指南和方法，各種醫療保健系統可以通過這些標準、指南和方法相互通訊。此類指南或數據標準是一組規則，允許以統一和一致的方式共享和處理信息。這些數據標準旨在使醫療保健組織能夠輕鬆共享臨床訊息。從理論上講，這種交換訊息的能力應該有助於最大限度地減少醫療保健在地理上被隔離和高度變化的趨勢\[1\]。 HL7 International認為以下標準是其主要標準\[2\]：

  - 2.x版消息傳遞標準：健康和醫療事務的互操作性規範
  - 第3版消息傳遞標準：健康和醫療事務的互操作性規範
  - 臨床文件架構（CDA）：基於HL7第3版的臨床文件交換模型
  - 連續性照護文件（CCD）：基於CDA的美國醫學摘要交換規範
  - 結構化產品標籤（SPL）：基於HL7第3版的藥物隨附的已發布信息
  - 臨床背景對象工作組（CCOW）：用於應用程式可視化集成的互操作性規範

其他HL7標準/方法包括：

  - [快捷式醫療服務互操作資源](https://zh.wikipedia.org/wiki/快捷式醫療服務互操作資源 "wikilink")：資源交換的標準
  - [Arden Syntax](https://en.wikipedia.org/wiki/Arden_syntax)：用於表示醫療條件的語法和作為醫療邏輯模塊（[Medical Logic Module](https://en.wikipedia.org/wiki/Medical_logic_module), MLM）的建議
  - 索賠附件：標準醫療保健附件，以增加另一項醫療保健交易
  - [電子健康紀錄](../Page/電子健康紀錄.md "wikilink")/[個人健康紀錄](../Page/個人健康紀錄.md "wikilink")系統的功能規範：在此類軟體應用程式中尋求或可用的健康和醫療功能的標準化描述
  - [GELLO](https://en.wikipedia.org/wiki/Gello_Expression_Language)：用於臨床決策支持的標準表達語言

## 主要標準

以下是HL7 International認為最常用和實施的標準\[3\]。

### 版本2

HL7版本2標準（也稱為Pipehat）旨在支持醫院工作流程。它最初創建於1989年\[4\]。HL7第2版定義了一系列電子訊息，以支持行政、後勤、財務和臨床流程。自1987年以來，該標準定期更新，產生版本2.1,2.2,2.3,2.3.1,2.4,2.5,2.5.1,2.6,2.7,2.7.1,2.8,2.8.1和2.8.2。v2.x標準是向後相容的（例如，支援2.6版的應用程式能夠理解基於版本2.3的資訊）。 HL7 v2.x消息使用基於段（行）和單字符分隔符的非XML編碼語法。段具有由分隔符所分隔的複合字段\[5\]。複合字段可以具有由子複合字段分隔符分隔的子複合字段（組件），並且子複合字段可以具有由子子複合字段分隔符分隔的子子複合字段（子組件）。默認分隔符是段分隔符的換行符，字段分隔符的豎線條或豎線（|），組件分隔符的插入符號（^），子組件分隔符的＆符號（＆）和＃標籤/井號（＃）是默認截斷分隔符。波浪號（〜）是默認的重複分隔符。每個段以3個字符的字符串開頭，用於標識段類型。訊息的每個部分包含一個特定類別的訊息。每條訊息都有MSH作為其第一個段，其中包含一個標識訊息類型的字段。訊息類型確定訊息中的預期段類型\[6\]。特定訊息類型中使用的段類型由HL7標準中使用的段語法表示法指定。以下是標準訊息的範例。MSH是標題段，PID是患者標識，PV1是患者訪問訊息等，PID段中的第二個字段是患者姓名，順序，姓，名，第二名（或其首字母），後綴等。根據HL7 V2.x標準版本，該段中有更多字段可用於其他患者訊息。

HL7 v2.x允許電子病人管理系統（PAS）、電子實踐管理（EPM）系統、檢驗資訊系統（LIS）、膳食、藥劑部和計費系統以及電子病歷（EMR）或[電子健康紀錄](../Page/電子健康紀錄.md "wikilink")（EHR）之間的[互操作性](../Page/互操作性.md "wikilink")。目前，HL7 v2.x資訊傳遞標準得到了美國所有主要醫療資訊系統供應商的支援\[7\]。

### 版本3

HL7版本3標準旨在支持所有醫療保健工作流程。版本3的開發始於1995年左右，導致2005年的初始標準出版物。與版本2相反，v3標準基於正式方法（HDF）和面向對象原則。

**RIM - ISO/HL7 21731** 參考資訊模型（Reference Information Model）\[8\] 是HL7版本3開發過程的基石，也是HL7 V3開發方法的重要組成部分。RIM表達特定臨床或管理上下文中所需的數據內容，並提供HL7資訊字段中攜帶的訊息之間存在的語義和詞彙連接的明確表示\[9\]。

**HL7 Development Framework - [ISO](https://zh.wikipedia.org/wiki/International_Organization_for_Standardization "wikilink")/HL7 27931** HL7第3版開發框架（HDF）仍不斷發展中，旨在開發促進醫療保健系統之間互操作性的規範。HL7 RIM，詞彙規範和模型驅動的分析和設計過程相結合，使HL7第3版成為開發基於共識的醫療信息系統互操作性標準的一種方法。HDF是HL7 V3開發方法的最新版本。HDF不僅記錄資訊傳遞，還記錄與所有HL7標準規範的開發相關的過程，工具，參與者，規則和工件。最終，HDF將包含所有HL7標準規範，包括分析電子健康記錄體系結構和要求所產生的任何新標準。HL7規範借鑒了各種來源的代碼和詞彙。V3詞彙表工作確保實現HL7規範的系統對他們正在使用的代碼源和代碼值域有明確的理解。

**V3 Messaging** HL7版本3消息傳遞標准定義了一系列安全文本消息（稱為“interactions”）以支持所有醫療保健工作流程。HL7 v3消息基於XML編碼語法，如以下範例 \[10\]：

``` xml
<POLB_IN224200 ITSVersion="XML_1.0" ns="urn:hl7-org:v3"
 xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
  <id root="2.16.840.1.113883.19.1122.7" extension="CNTRL-3456"/>
  <creationTime value="200202150930-0400"/>
  <!-- The version of the datatypes/RIM/vocabulary used is that of May 2006 -->
  <versionCode code="2006-05"/>
  <!-- interaction id= Observation Event Complete, w/o Receiver Responsibilities -->
  <interactionId root="2.16.840.1.113883.1.6" extension="POLB_IN224200"/>
  <processingCode code="P"/>
  <processingModeCode nullFlavor="OTH"/>
  <acceptAckCode code="ER"/>
  <receiver typeCode="RCV">
    <device classCode="DEV" determinerCode="INSTANCE">
      <id extension="GHH LAB" root="2.16.840.1.113883.19.1122.1"/>
      <asLocatedEntity classCode="LOCE">
        <location classCode="PLC" determinerCode="INSTANCE">
          <id root="2.16.840.1.113883.19.1122.2" extension="ELAB-3"/>
        </location>
      </asLocatedEntity>
    </device>
  </receiver>
  <sender typeCode="SND">
    <device classCode="DEV" determinerCode="INSTANCE">
      <id root="2.16.840.1.113883.19.1122.1" extension="GHH OE"/>
      <asLocatedEntity classCode="LOCE">
        <location classCode="PLC" determinerCode="INSTANCE">
          <id root="2.16.840.1.113883.19.1122.2" extension="BLDG24"/>
        </location>
      </asLocatedEntity>
    </device>
  </sender>
  <!-- Trigger Event Control Act & Domain Content -->
</POLB_IN224200>
```

### 臨床文檔架構

HL7臨床文檔架構（CDA）是一種基於XML的標記標準，旨在指定用於交換的臨床文檔的編碼，結構和語義。該標準與ISO共同出版，ISO / HL7 27932\[11\]。

### 臨床文件的交換模型

臨床文件的交換模型（CCD）是基於健康互操作性規範和醫療交易臨床文件架構（CDA）的美國醫學摘要交換規範。

### 結構化產品標籤

結構化產品標籤（SPL）描述了基於HL7第3版的藥物隨附的已發布信息。

### 臨床背景對象工作組

臨床背景對象工作組（CCOW）是一種標準協議，旨在使不同的應用程式能夠在用戶界面層即時地共享用戶上下文和患者上下文。CCOW實施通常需要CCOW Vault系統來管理應用程序之間的用戶安全性。

## 其它標準與方法

### 快捷式醫療服務互操作資源

快捷式醫療服務互操作資源是[健康資訊交換第七層協會](https://www.hl7.org)的標準草案，旨在比版本2.x或版本3更容易實現，更開放，更具可擴展性。它利用基於Web的現代API技術套件，包括基於HTTP的RESTful 用於用戶界面集成的協議，HTML和層疊樣式表，用於數據表示的JSON或XML選擇，用於授權的OAuth和用於查詢結果的ATOM\[12\]。

### 服務互操作性框架

此框架提供了所有HL7工件之間的一致性，並實現了企業架構開發和實現的標準化方法，以及衡量一致性的方法。此框架是一種思考生成規範的方法，這些規範明確地描述了實現可計算的語義工作互操作性所需的管理、一致性、合法性和行為語義。預期的資訊傳輸技術可以使用訊息傳遞、文檔交換或服務。此框架是合理化其他標準的互操作性所需的框架，是一種實現互操作性的體系結構，但它不是企業體系結構管理的整體解決方案設計。

### Arden 語法

Arden語法是用於編碼醫學知識的語言。HL7 International採用並監督從Arden語法2.0開始的標準。這些醫療邏輯模塊（MLM）用於臨床環境，因為它們可以包含足夠的知識來做出單一的醫療決策。它們可以產生警報、診斷和解釋，以及質量保證功能和管理支持。醫療邏輯模塊必須在滿足最低系統要求且安裝了正確程式的電腦上運行，使醫療邏輯模塊可以為需要的時間和地點提供建議。

### MLLP

HL7消息傳遞的很大一部分由最小下層協議（MLLP）傳輸，也稱為低層協議（LLP）\[13\]。因為TCP/IP是連續的字節流，為了通過TCP/IP進行傳輸，會在郵件中添加標題和尾部字符，以識別郵件的開頭和結尾。混合下層協議（HLLP）是MLLP的變體，包括校驗和以幫助驗證消息完整性。在其他軟體供應商，例如Microsoft\[14\]、Oracle \[15\]和[Cleo](https://zh.wikipedia.org/wiki/Cleo（company） "wikilink")\[16\]都支持MLLP。

### 功能性電子健康紀錄和個人健康紀錄規格

[電子健康紀錄](../Page/電子健康紀錄.md "wikilink")的功能規範。

## 訊息細節

### OBR Segment

OBR Segment包含有關檢查、診斷研究/觀察的信息\[17\]。這在醫令訊息（Order Message, ORM）\[18\]或檢查結果（Observation Result, ORU）兩者間是必備的訊息\[19\]。

## 参考文獻

## 外部鏈結

  - [Health Level Seven International](https://www.hl7.org)
  - [HL7 Global](https://web.archive.org/web/20100408170144/http://www.hl7.org/)
  - [HL7 Introduction](http://www.ehealthtraining.com.au/HL7-FAQ.htm)
  - [HL7 Tools](http://www.ehealthtraining.com.au/HL7-Tools.htm)
  - [臺灣健康資訊交換第七層協會](http://www.HL7.org.tw)

## 參見

  - [快捷式醫療服務互操作資源](https://zh.wikipedia.org/wiki/快捷式醫療服務互操作資源 "wikilink")
  - [電子健康紀錄](../Page/電子健康紀錄.md "wikilink")
  - [個人健康紀錄](../Page/個人健康紀錄.md "wikilink")
  - [DICOM](../Page/DICOM.md "wikilink")
  - [LOINC](https://zh.wikipedia.org/wiki/LOINC "wikilink")
  - [openEHR Foundation](https://zh.wikipedia.org/wiki/openEHR "wikilink")
  - [SNOMED CT](../Page/SNOMED_CT.md "wikilink")
  - [OpenEHR](../Page/OpenEHR.md "wikilink")

{{-}}

[Category:醫療資訊學](https://zh.wikipedia.org/wiki/Category:醫療資訊學 "wikilink") [Category:國際專業性組織](https://zh.wikipedia.org/wiki/Category:國際專業性組織 "wikilink")

1.
2.
3.
4.
5.
6.
7.
8.
9.
10.
11.
12.
13.
14.
15.
16.
17.
18.
19.