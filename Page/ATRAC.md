> 本文内容由[ATRAC](https://zh.wikipedia.org/wiki/ATRAC)转换而来。


[Atrac3.gif](https://zh.wikipedia.org/wiki/File:Atrac3.gif "fig:Atrac3.gif")

**自適應聽覺轉換編碼**（，缩写**ATRAC**）為[Sony公司於](https://zh.wikipedia.org/wiki/Sony "wikilink")1992年所開發之音訊[有损数据压缩](../Page/有损数据压缩.md "wikilink")技術，也是相關技術名詞之總稱。除了Sony本身，其他[MiniDisc](../Page/MiniDisc.md "wikilink")製造商如[Sharp](https://zh.wikipedia.org/wiki/夏普 "wikilink")、[Panasonic等](https://zh.wikipedia.org/wiki/Panasonic "wikilink")，也有各自研發自家的ATRAC[编解码器](../Page/编解码器.md "wikilink")。

Sony在2007年9月11日發佈的Walkman,S600F/S700F系列SonicStage和ATRAC音频格式，而Sony對此決定解釋為“为了考虑到各个地区的市场特性，所作出的规格决定。”\[1\]。

[美國與其他國家之](https://zh.wikipedia.org/wiki/美國 "wikilink")[專利](https://zh.wikipedia.org/wiki/專利 "wikilink")[授權來自](../Page/授權_\(法律\).md "wikilink")[杜比實驗室](../Page/杜比實驗室.md "wikilink")。

## 關於名稱

Sony研發ATRAC初版（為避免混淆，稱作**ATRAC1**）後，又接續開發了相關的有損壓縮技術**ATRAC2**、**ATRAC3**、**ATRAC3plus**、以及無損的**ATRAC Advanced Lossless**。事實上，這五種壓縮技術除了名稱類似外，彼此之間並不盡相同。

另外，ATRAC2、ATRAC3名稱末尾的數字，經常會被誤解為ATRAC的版本號，事實上該數字是編碼技術名稱的一部分。由於Sony先前將自家生產的ATRAC1編解碼器依照版本命名為「ATRAC Version 1～ATRAC Version 4.5」，因此經常會與前述名稱混淆。ATRAC3不是ATRAC1的最新版本，ATRAC Version 3、ATRAC3、ATRAC3plus是三種全然不同的東西。

Sony於2005年秋季將這些技術名詞總稱為**ATRAC**，希望就此結束命名上的混亂局面。

## ATRAC1

### 概要

ATRAC1，通常记作ATRAC。為減輕運算處理負擔，ATRAC1編碼時先使用兩次QMF（Quadrature Mirror Filters），將輸入的音訊分割為三個子頻帶；第一次分離出高頻（11.025～22.05kHz），第二次分離剩餘的中低頻（0～5.5125kHz、5.5125～11.025kHz）。子頻帶再於MDCT（Modified Discrete Cosine Transform，變址離散餘弦變換）切割分塊，並依據人耳對音頻的敏感度而調整資料塊的分配量，也是所謂的自適應。壓縮時，ATRAC根據[聽覺心理學](https://zh.wikipedia.org/wiki/聽覺心理學 "wikilink")，忽略人耳聽覺極限之外的音訊，以及被大音量屏蔽的細小聲音，以達到資料壓縮的目的。ATRAC1沒有明定如何流量分配等細節，便於日後微調改善音質。

### 用於MiniDisc

音樂[MiniDisc](../Page/MiniDisc.md "wikilink")所採用的ATRAC1規格，分為立體聲（292kbps）及單聲道（146Kbps）兩種格式。

初代MiniDisc錄放音機所使用的ATRAC1晶片稱為ATRAC Version 1。由於早期MiniDisc讀寫錯誤率較高，故在碟片上寫入兩份同樣的資料作為備份；ATRAC Version 1實際上只用了規格一半的流量來紀錄音樂，因而音質不佳、充滿噪音。因為這件事情使得大眾對於ATRAC的音質有著不好的成見，對於ATRAC的普及化推廣具有頗大的影響，並使其在眾家解碼器之中變得惡名昭彰。但Sony、Sharp等製造商仍不斷各自改進ATRAC1晶片版本與編碼技術，至今各家編碼音質均相當優異，一般人已不易分辨ATRAC1與PCM之間的差異。

### 用於SDDS劇院系統

ATRAC格式同時也被Sony Cinema Products Corporation所開發之劇院音響系統[SDDS](../Page/SDDS.md "wikilink")（Sony Dynamic Digital Sound）所採用。SDDS可收錄5.1或7.1聲道，合計最大流量達1280Kbps，比起定位相同的杜比數位（Dolby Digital）與數位劇院系統（DTS）音質要好。但由於混音設備昂貴，因此SDDS並不如其他5.1聲道規格來的普及。

## ATRAC2

**ATRAC2**為Sony於1994年所發表，主要用於[MD Data上之音訊規格](../Page/MD_Data.md "wikilink")。壓縮比高達10:1或20:1，可於MD DATA碟片上播放／錄製長達148分鐘的立體聲音訊。ATRAC2於編碼上捨棄了傳統ATRAC1的觀念，使用了PQF（Polyphase Quadrature Filters，多級正交濾波器）代替QMF，將音訊拆為4個子頻帶，並抽出音樂中的音調單獨編碼，最後使用[霍夫曼編碼增加壓縮率](https://zh.wikipedia.org/wiki/哈夫曼树 "wikilink")。也因此ATRAC2無法相容於ATRAC1，該規格也隨著MD DATA在市場的失敗而消失。

## ATRAC3/ATRAC3plus

### 概要

1999年Sony所發表的格式。一般多認為是由於受到MP3、AAC等新式壓縮格式的衝擊，才推出的因應方案。用途較ATRAC1、ATRAC2更加廣泛。

ATRAC3以ATRAC2為部份技術基礎，並可相容ATRAC1的立體聲與單聲道模式，意圖與當時逐漸流行的[MP3](../Page/MP3.md "wikilink")格式相抗衡。ATRAC3使用QMF，將音訊分割為0～2.75625kHz、2.75625～5.5125kHz、5.5125～11.025kHz、11.025～22.05kHz等4個子頻帶，並可抽出音樂中的音調，另行較低壓縮率的編碼。ATRAC3位元率分為132kbps（LP2）、105kbps、66kbps（LP4）3種。其中66kbps使用選擇性的[Joint Stereo](https://zh.wikipedia.org/wiki/Joint_Stereo "wikilink")，以彌補流量的不足。但ATRAC3也浪費了將近10%的流量於相容ATRAC1之上。ATRAC3 LP2可錄製約162分鐘的音樂於一般MD碟片上，而LP4則可錄製約324分鐘的音樂。

隨後，Sony在2002年時發表更高壓縮率的ATRAC3plus，子頻帶切割多達16組，並會自動選擇最佳壓縮模式。這與ATRAC3、ATRAC1都不相容，不過發表後經常與ATRAC3配套使用。ATRAC3plus最初僅設計為低流量之用，只提供64kbps、48kbps兩種高壓縮流量，但自2004年起開始追加低壓縮、高音質的流量，逐漸取代ATRAC3。目前最新版的SonicStage提供48、64（Hi-LP）、96、128、160、192、256（Hi-SP）、320、352kbps等多種流量可轉換。

### 音質爭議

一般認為132kbps的ATRAC3，音質近似相近流量的[MP3](../Page/MP3.md "wikilink")。一份Sony提供的盲測報告[1](http://www.sony.net/Products/ATRAC3/tech/TESTfactory_Listening_test.pdf)（2003/02），指出132kbps ATRAC的音質甚至優於相近流量的MP3。

但在一份私人的[雙盲測試報告](https://zh.wikipedia.org/wiki/雙盲 "wikilink")[2](https://web.archive.org/web/20060831191536/http://www.rjamorim.com/test/)（2004/05）中，比較了[Ogg](../Page/Ogg.md "wikilink")、[AAC](https://zh.wikipedia.org/wiki/AAC "wikilink")、以及[LAME](../Page/LAME.md "wikilink") [VBR](https://zh.wikipedia.org/wiki/VBR "wikilink") [MP3](../Page/MP3.md "wikilink")多種格式的音質，結果卻是ATRAC3殿後。一般多批評評測者並未使用最佳品質的ATRAC3編解碼器。有人辯稱ATRAC多在電力有限的行動裝置上編製，因此難以進行負荷量較大的高音質壓縮。但事實上Sony幾乎在所有Hi-MD規格的手提播放器都使用上最高規格的TYPE S解碼器。

Sony另宣稱64kbps的ATRAC3plus音質近似CD，並有確實的第三方公證實驗室評級測試中得以證實。[3](http://www.sony.net/Products/ATRAC3/tech/TESTfactory_Listening_test.pdf)

### 用於個人電腦

ATRAC3及ATRAC3plus，可用於個人電腦之上，與較常用於視聽設備之中的ATRAC1不同。

第一款支援ATRAC3格式的電腦軟體，是Sony於1999年底發表的[OpenMG Jukebox](https://zh.wikipedia.org/wiki/OpenMG_Jukebox "wikilink")。OpenMG Jukebox是用來管理、傳輸數位隨身聽內音樂文件的軟體，可將[CD](../Page/CD.md "wikilink")音樂壓縮為ATRAC3，或將電腦內的[WAV](../Page/WAV.md "wikilink")、[MP3](../Page/MP3.md "wikilink")檔案轉換為ATRAC3格式，以便傳入隨身聽。Sony後來接續推出的[SonicStage](../Page/SonicStage.md "wikilink")和[Connect Player](https://zh.wikipedia.org/wiki/Connect_Player "wikilink")，也都具有同樣的功能。

同時，為搭配[NetMD隨身聽的發售](https://zh.wikipedia.org/wiki/NetMD "wikilink")，其他廠商也各自推出相容軟體，如日本Justsystem的[BeatJam](https://zh.wikipedia.org/wiki/BeatJam "wikilink")、[Kenwood的Mulia等](https://zh.wikipedia.org/wiki/Kenwood "wikilink")。

第一款支援ATRAC3plus的軟體，則是被預先安裝在日版[Vaio](https://zh.wikipedia.org/wiki/Vaio "wikilink")2002年秋季款內的SonicStage 1.5。當初只有64kbps、48kbps兩種低流量格式，比ATRAC3的3種壓縮量要高，相對地音質也低，因此不太受歡迎。不過，2.0版內隨即出現了256kbps，接著3.2版又追加了320kbps、192kbps、160kbps、128kbps、96kbps五種流量，最後3.3版新增了352kbps，比ATRAC3更能滿足高音質、低壓縮的廣泛需求。

ATRAC3檔案的原始副檔名為「aa3」，若經過[OpenMG進行版權保護加密後](https://zh.wikipedia.org/wiki/OpenMG "wikilink")，則會變成「omg」或「oma」。由於OpenMG Jukebox和早期的SonicStage無法關閉加密功能，因此罕以aa3副檔名呈現。即使SonicStage3.2版以及CONNECT Player均能生成不加密的音樂檔案，該副檔名仍舊與加密文件同為「oma」。

### 用於數位音樂播放器

最早採用ATRAC3為播放格式的隨身聽，是1999年底發售的Sony [Memory Stick隨身聽](https://zh.wikipedia.org/wiki/Memory_Stick "wikilink")「NW-MS7」。使用附送的OpenMG Jukebox軟體，將CD、WAV、MP3轉換為ATRAC3後，再傳入內含MagicGate版權保護晶片的Memory Stick（MGMS）。理論上ATRAC3/ATRAC3plus的規格統一，存入Memory Stick後也能用於其他廠牌的相容產品之中。但Memory Stick本身推出了太多種格式，且ATRAC3plus遲至2003年才被採用，因此早期產品彼此間的相容性不太完整。

Memory Stick隨身聽發售翌年，索尼創設新的子品牌「Network Walkman」，推出一系列內建快閃記憶體、硬碟為載體的數位隨身聽。這些網路隨身聽幾乎只支援ATRAC3格式，直到2003年發售的NW-MS70D才又支援了ATRAC3plus。Sony同時也推出一系列新CD隨身聽，能播放內含ATRAC3/ATRAC3plus的CD-R/RW（ATRAC CD）。

### 用於其他裝置

除了Sony旗下的隨身聽支援ATRAC3/ATRAC3plus外，Sony推出的[CLIE](https://zh.wikipedia.org/wiki/CLIE "wikilink") PDA、[PSP](https://zh.wikipedia.org/wiki/PSP "wikilink")、[PS3](https://zh.wikipedia.org/wiki/PS3 "wikilink")、[VAIO](../Page/VAIO.md "wikilink") Pocket、NETJUKE、PSX、在美推出的Mylo等非隨身聽品牌的產品，也多能播放ATRAC3/ATRAC3Plus。

某些[Sony Ericsson日系](https://zh.wikipedia.org/wiki/Sony_Ericsson "wikilink")[NTT DoCoMo](https://zh.wikipedia.org/wiki/NTT_DoCoMo "wikilink")、[au等系統手機](https://zh.wikipedia.org/wiki/Au_\(電訊\) "wikilink")，也能透過Memory Stick播放ATRAC3或ATRAC3plus音樂。2005年京瓷於日本推出的WillcomPHS手機「WX310k」，則是很特別地使用miniSD卡來存放MP3/ATRAC3音樂。[Sony Ericsson旗下的手機](https://zh.wikipedia.org/wiki/Sony_Ericsson "wikilink")，如W800i等，雖能使用記憶卡播放MP3等格式，但尚無機種支援ATRAC3/ATRAC3Plus格式。

### 用於MiniDisc擴充規格

MiniDisc自2000年開始，導入了可長時間錄音的規格「MDLP」，增加了ATRAC3 132kbps（LP2）、ATRAC3 66kbps（LP4）兩種模式。翌年，2001年登場的NetMD更實現了將電腦中的音樂傳輸入MD的功能，也能與Network Walkman共享ATRAC3檔案。於網路上也能直接下載、播放ATRAC3格式的音樂。

在2004年推出的擴充規格「[Hi-MD](https://zh.wikipedia.org/wiki/Hi-MD "wikilink")」上，除了MDLP所用的2種格式，還加入ATRAC3 105kbps，以及ATRAC3plus的256kbps、64kbps、48kbps。同時ATRAC3plus 256kbps和64kbps，也分別被安上了Hi-SP、Hi-LP兩種名稱。

### RealAudio8與ATRAC3

[RealNetworks](../Page/RealNetworks.md "wikilink")公司旗下的音樂格式：[RealAudio](https://zh.wikipedia.org/wiki/RealAudio "wikilink")8，採用ATRAC3作為核心編碼器，同時也導入OpenMG版權加密技術。也因此該公司的軟體與網路隨身聽、NetMD等硬體相容。

RealAudio8的流量非常自由，可選擇352kbps、264kbps、176kbps、146kbps、132kbps、105kbps、94kbps、66kbps等設定。但ATRAC3將105kbps以上視為高流量，所以把94kbps、66kbps作為一般低流量用的選項。

於個人電腦上使用時，可選擇檔案是否加密。加密後的附檔名為「rmx」，未加密則為「rmj」。這些檔案與Sony旗下軟體所生成的ATRAC3並無直接相容性。但可以透過Real Network下載plug-in對應部份NetMD產品。

RealAudio10格式則改以[AAC核心取代ATRAC](https://zh.wikipedia.org/wiki/AAC "wikilink")3。

### 其他應用

小型光碟[UMD](https://zh.wikipedia.org/wiki/UMD "wikilink")（Universal Media Disc）的音樂規格「UMD Audio」，以及影片規格「UMD Video」之中，採用ATRAC3plus作為音訊編碼。

## ATRAC Advanced Lossless

**ATRAC Advanced Lossless**在2005年9月的A\&VFesta2005中發表，是ATRAC家族中唯一的[無失真壓縮規格](../Page/无损数据压缩.md "wikilink")，簡稱AAL。

該格式可同時包含無失真壓縮、破壞性壓縮兩部份。破壞壓縮部份可使用ATRAC3、ATRAC3plus等格式，而無失真部份則是將原始音訊進行可逆性的無損壓縮。除了傳送整個AAL檔案至隨身聽外，也可以只取出較小的ATRAC3/ATRAC3plus部分。

AAL壓縮率約為30～80%，由於AAL同時內含有破壞性壓縮的音訊，因此破壞壓縮所使用的格式也會影響AAL的壓縮量。

AAL首度於2005年11月1日發表的SonicStage 3.3版所支援。可以傳送完整AAL資料給完全支援AAL的音樂播放器，也可以只傳送ATRAC3/ATRAC3plus的部份。硬體方面，SONY至2006年10月發表之NW-S700F、NW-S600才完全支援AAL。

## 參見

  - [MP3](../Page/MP3.md "wikilink")
  - [破壞性資料壓縮](https://zh.wikipedia.org/wiki/破壞性資料壓縮 "wikilink")
  - [MiniDisc](../Page/MiniDisc.md "wikilink")
  - [Memory Stick](https://zh.wikipedia.org/wiki/Memory_Stick "wikilink")

## 外部連結

  - [SONY ATRAC官方網站（英文）](http://www.sony.net/Products/ATRAC3/)
  - [ATRAC1技術介紹（英文）](http://www.minidisc.org/aes_atrac.html)
  - [ATRAC2技術介紹（英文）](http://www.minidisc.org/atrac2.html)
  - [ATRAC3 Codec下載](http://www.free-codecs.com/download/Sony_ATRAC3_Audio_Codec.htm)

## 註釋

[Category:數位音訊](https://zh.wikipedia.org/wiki/Category:數位音訊 "wikilink") [Category:文件格式](https://zh.wikipedia.org/wiki/Category:文件格式 "wikilink") [Category:音频格式](https://zh.wikipedia.org/wiki/Category:音频格式 "wikilink") [Category:聲音儲存](https://zh.wikipedia.org/wiki/Category:聲音儲存 "wikilink") [Category:音频编解码器](https://zh.wikipedia.org/wiki/Category:音频编解码器 "wikilink") [Category:有损压缩算法](https://zh.wikipedia.org/wiki/Category:有损压缩算法 "wikilink") [Category:索尼](https://zh.wikipedia.org/wiki/Category:索尼 "wikilink")

1.  各地域の市場特性を考慮して製品仕様を決めているため