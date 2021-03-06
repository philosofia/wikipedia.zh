> 本文内容由[DICOM](https://zh.wikipedia.org/wiki/DICOM)转换而来。


**醫療數位影像傳輸協定**（，）是一組通用的標準協定，在對於[醫學影像](../Page/醫學影像.md "wikilink")的處理、儲存、列印、傳輸上。它包含了檔案格式的定義及網路通信協定。DICOM是以[TCP/IP為基礎的應用協定](https://zh.wikipedia.org/wiki/TCP/IP协议 "wikilink")，並以TCP/IP聯繫各個系統。兩個能接受DICOM格式的醫療儀器間，可藉由DICOM格式的檔案，來接收與交換影像及病人資料。

DICOM可以整合不同廠商的醫療影像儀器、[伺服器](https://zh.wikipedia.org/wiki/伺服器 "wikilink")、[工作站](../Page/工作站.md "wikilink")、列印機和網路設備，使它們都能整合在[PACS系統中](https://zh.wikipedia.org/wiki/PACS "wikilink")。許多不同廠商的儀器、伺服器、工作站都根據DICOM的標準，來製造支援DICOM機器。DICOM已經廣泛地被醫院所採用，並且在牙醫和一般的診所中獲得小規模的運用。

## DICOM的資料格式

在所有的用途上都是使用相同的格式，包括了網路應用和檔案處理，和其他格式不同的是它統合了所有的資訊在同一個資料內，也就是說，如果有一張胸腔X光影像在你的病人個人資料內，這個影像決不可能意外地再從你的病人資料中分離。

DICOM的檔案是由標準化且自由型式的開頭再加上一連串的影像數據，單一個DICOM的物件只包含一張影像，但是此影像可能會有多個套圖，這是為了能儲存動態影像以及其他複圖形式的資料，影像資料可以經壓縮用在其他的格式上，包括了JPEG, JPEG Lossless, JPEG 2000, LZW and Run-length encoding (RLE)。

## DICOM服務

DICOM是由多種支援服務結合而成，大部分和網路上的資料傳輸有關，下面的這些處理過程和它只是小有關係。

### 儲存

DICOM的儲存服務是用在傳送影像或是將其他的持續物件（persistent objects）（例如整理過的病歷報告）傳送到PACS的工作站。

### 儲存確認

DICOM的儲存確認是一種為了確定影像儲存在特定地方（可能是硬碟或是其他的支援媒界，如燒在光碟內）的服務，此等級的用戶端（機器設備或是工作站等）用從服務供應器（儲存站或原始端）發出的資訊來確認，以確保原始端的影像可以放心地刪除了。

### 影像獲得

此項功能讓工作站可以找到影像列或是其他的PACS物件，如此便可取得影像。

### 工作列表

此項功能讓一个图像设备（a modality）可以以电子方式接收到病人的详细信息和计划对此病人进行的检查，以此避免重复输入信息以及在重复输入信息中产生错误。

### 原始端執行進程記錄（Modality Performed Procedure Step）

原始端工作列的附加服務，可以讓原始端送出有關此項檢查的其他資料，如獲得的影像數還有劑量的輸出數等等。...

### 列印

DICOM的列印服務是將影像傳送至DICOM印列機，大部分是輸出ｘ光影像，有一套標準的校正程序，以確保在不同的顯示裝置（包括數位複製）中仍保有一致性。

### 離線支援

DICOM限制DICOM上的支援設備名稱有8字元的名字（很多人都錯誤地用8.3，但那是不合法的），研發者沒有小心地注意這個限制通常都是問題產生的來源，要和舊的系統久遠保持相容性是相當重要的，DICOM也改修了檔案定位的方式，就是DICOMDIR檔案，它提供了媒體形式的導引和結論等資訊，DICOMDIR資料對每一個檔案可以存放的資訊比其他的檔案類型都大得多，有時就不需要有意義的檔案名稱。

## 歷史

早期著名的DICOM標準是3.0版，在1993年發明，原先是在用國際電子製造組織（[NEMA](../Page/美國電氣製造商協會.md "wikilink")）還有許多公眾產業上，也有不少公開的支援工具。媒體形式的交換測試、光碟媒體形式的連接過程、和由IHE組織發展的網路活動等都不斷地運作。

DICOM支持的設備有下列項目：

  - AS = [Angioscopy](https://zh.wikipedia.org/wiki/Angioscopy "wikilink") 血管鏡
  - BI = [Biomagnetic Imaging](https://zh.wikipedia.org/wiki/Biomagnetic_Imaging "wikilink") 生物磁場成像
  - CD = [Color Flow Doppler](https://zh.wikipedia.org/wiki/Color_Flow_Doppler "wikilink") 彩色血流多普勒
  - CF = [Cinefluorography](https://zh.wikipedia.org/wiki/Cinefluorography "wikilink") 熒光透視
  - CP = [Colposcopy](https://zh.wikipedia.org/wiki/Colposcopy "wikilink") 陰道鏡
  - CR = [Computed Radiography](https://zh.wikipedia.org/wiki/Computed_Radiography "wikilink") 電腦X光攝影
  - CS = [Cystoscopy](https://zh.wikipedia.org/wiki/Cystoscopy "wikilink") 膀胱鏡
  - CT = [Computed Tomography](https://zh.wikipedia.org/wiki/Computed_Tomography "wikilink") 電腦斷層攝影
  - DD = [Duplex Doppler](https://zh.wikipedia.org/wiki/Duplex_Doppler "wikilink") 雙工多普勒
  - DF = [Digital Fluoroscopy](https://zh.wikipedia.org/wiki/Digital_Fluoroscopy "wikilink") 數位熒光透視
  - DG = [Diaphanography](https://zh.wikipedia.org/wiki/Diaphanography "wikilink") 透視攝影
  - DM = [Digital Microscopy](https://zh.wikipedia.org/wiki/Digital_Microscopy "wikilink") 數字顯微鏡
  - DSA = [Digital Subtraction Angiography](https://zh.wikipedia.org/wiki/Digital_subtraction_angiography "wikilink") 數位減影心血管造影
  - DX = [Digital Radiography](https://zh.wikipedia.org/wiki/Digital_Radiography "wikilink") 數位X光攝影
  - EC = [Echocardiography](https://zh.wikipedia.org/wiki/Echocardiography "wikilink") 超聲心動圖
  - ES = [Endoscopy](../Page/內視鏡.md "wikilink") 內視鏡
  - FA = [Fluorescein Angiography](https://zh.wikipedia.org/wiki/Fluorescein_angiography "wikilink") 透視血管攝影
  - FS = [Fundoscopy](https://zh.wikipedia.org/wiki/Fundoscopy "wikilink") 眼底檢查
  - HC = [Hard Copy](https://zh.wikipedia.org/wiki/Hard_Copy "wikilink") 硬拷貝
  - LP = [Laparoscopy](https://zh.wikipedia.org/wiki/Laparoscopy "wikilink") 腹腔鏡
  - LS = [Laser Surface Scan](https://zh.wikipedia.org/wiki/Laser_Surface_Scan "wikilink") 雷射體表掃描
  - MA = [Magnetic Resonance Angiography](https://zh.wikipedia.org/wiki/Magnetic_Resonance_Angiography "wikilink") 磁共振血管攝影
  - MR = [Magnetic Resonance](../Page/核磁共振成像.md "wikilink") 核磁共振成像
  - MS = [Magnetic Resonance Spectroscopy](https://zh.wikipedia.org/wiki/Magnetic_Resonance_Spectroscopy "wikilink") 核磁共振波譜
  - NM = [Nuclear Medicine](https://zh.wikipedia.org/wiki/Nuclear_Medicine "wikilink") [核子醫學](https://zh.wikipedia.org/wiki/核子醫學 "wikilink")（简体：核医学）
  - OT = Other 其他
  - PT = [Positron Emission Tomography](https://zh.wikipedia.org/wiki/Positron_Emission_Tomography "wikilink") (PET) [正電子發射斷層顯像](https://zh.wikipedia.org/wiki/正電子發射斷層顯像 "wikilink")
  - RF = [Radio Fluoroscopy](https://zh.wikipedia.org/wiki/Fluoroscopy "wikilink") 透視攝影
  - RG = Radiographic Imaging (conventional film screen) X光成像（傳統底片）
  - RTDOSE = [Radiotherapy](https://zh.wikipedia.org/wiki/Radiotherapy "wikilink") Dose 放射治療劑量
  - RTIMAGE = Radiotherapy Image 放射治療影像
  - RTPLAN = Radiotherapy Plan 放射治療計劃
  - RTSTRUCT = Radiotherapy Structure Set 放射治療結構裝置
  - ST = Single-photon Emission Computed Tomography 單光子放射斷層攝影（单光子发射计算机断层摄影）
  - TG = [Thermography](https://zh.wikipedia.org/wiki/Thermography "wikilink") 熱影像技術
  - US = [Ultrasound](https://zh.wikipedia.org/wiki/Ultrasound "wikilink") 超聲波成像
  - VF = Videofluorography 視頻透視
  - VL = Visible Light Microscope 光學顯微鏡
  - XA = [X-Ray Angiography](https://zh.wikipedia.org/wiki/Angiogram "wikilink") X光血管攝影
  - XC = eXternal Camera 外置鏡頭
  - ECG = [Electrocardiograms](https://zh.wikipedia.org/wiki/心電圖 "wikilink") 心電圖

## 参见

  - [LOINC](https://zh.wikipedia.org/wiki/LOINC "wikilink")
  - [HL7](https://zh.wikipedia.org/wiki/HL7 "wikilink")
  - [IHE](https://zh.wikipedia.org/wiki/IHE "wikilink") (https://en.wikipedia.org/wiki/Integrating_the_Healthcare_Enterprise)
  - [HIPAA](https://zh.wikipedia.org/wiki/HIPAA "wikilink")
  - [FHIR](https://zh.wikipedia.org/wiki/FHIR "wikilink")

[Category:医学成像](https://zh.wikipedia.org/wiki/Category:医学成像 "wikilink") [Category:医学信息学](https://zh.wikipedia.org/wiki/Category:医学信息学 "wikilink")