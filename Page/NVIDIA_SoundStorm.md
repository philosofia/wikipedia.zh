> 本文内容由[NVIDIA SoundStorm](https://zh.wikipedia.org/wiki/NVIDIA_SoundStorm)转换而来。


**SoundStorm**曾是一个高級的5.1音效技術認證。它是由[NVIDIA發明](https://zh.wikipedia.org/wiki/NVIDIA "wikilink")，用於[nForce2平台](https://zh.wikipedia.org/wiki/nForce2 "wikilink")，並以nForce音效处理單元（nForce audio processing unit，APU）作為基楚。

## 認證

為了得到SoundStorm認證，主板廠商必須令主板包含nForce APU和指定的輸出介面，介面通常不是直接焊在主板上，而是另加接線或子卡。主板亦須要通過[Dolby Digital音效實驗室的測試](https://zh.wikipedia.org/wiki/Dolby_Digital "wikilink")，確保音質符合一定程度。

SoundStorm認證保證了很多廠商的產品符合高品質的音效輸出。正因如此，SoundStorm達到了一個目的：為硬體狂熱者提供一個高品質而又價錢適中的音效產品。還有，它是當時唯一一張能提供真正杜比5.1數位音效輸出的音效卡（Dolby Digital Live技術），這對HTPC是非常重要的。

## 硬體

很多人以為有一顆晶片負責SoundStorm技術，其實那是一個謬誤。真正的「晶片」其實就在MCP-D和MCP-T南橋裏頭，各自屬於[nForce和](https://zh.wikipedia.org/wiki/nForce "wikilink")[nForce2晶片組](https://zh.wikipedia.org/wiki/nForce2 "wikilink")。一系列的固定功能和多用途處理元件，合共提供每秒四十億個的運算動作。一個可編程的數位訊號處理器提供特別的音效效果，它是以Motorola 56300處理器為基本。但DirectX只對它提供有限的支援，反而XBOX對開發者提供更多功能。APU的DSP是由指令推動。指令是由一間名為Sensaura的3D音效中介軟體公司提供。Sensaura的中介軟體亦被大多數音效卡的Windows驅動程式使用，甚至比Creative提供的還要多。與一般的音效卡不同，SoundStorm的Sensaura指令在硬體層面支援，而並非軟體層面，所以它的CPU資源佔用率非常低。它與即時杜比5.1數位音效解碼相容。一般音效卡的資源佔用率比SoundStorm高10-20%，而[Creative的](https://zh.wikipedia.org/wiki/創新科技 "wikilink")[Audigy音效卡性能則與SoundStorm相若](https://zh.wikipedia.org/wiki/Audigy "wikilink")。但Audigy的成本比較高，而且需要另外購買音效卡。

## 驅動程式

SoundStorm解決方案是使用一個一般用途的DSP，當系統啟動時，**指令**會由驅動程式上傳到音效卡，這樣新功能就能輕易增加。這亦表示開發第三者驅動程式是一件不可能的事，因為不能使用DSP指令。Linux的SoundStorm驅動程式只不過是直接與音效轉碼器（例如[RealTek](https://zh.wikipedia.org/wiki/RealTek "wikilink") ALC650）溝通，完全繞過APU，而所有的音效編碼則文由軟體負責。

另外要注意的是nForce 2 APU只是一個純數位的元件，所以主機板廠商需另加音效轉碼晶片（例如RealTek ALC650）作音效輸出，包括數位類比轉換（DAC）。隨著SoundStorm的消失，RealTek ALC650編碼晶片已成為一個標準整合型音效輸出解決方案，由於主機處理器擺脫了音效處理功能，就其本身而論，驅動程式的品質就顯得非常重要。除了確保低CPU資源佔用率外，還要保證沒有音效問題。

## Xbox

SoundStorm的發展原先由[微软](../Page/微软.md "wikilink")資助，希望用於[Xbox](../Page/Xbox.md "wikilink")遊戲機核心。

## 中斷研發

由於成本過高，nVidia決定不再將SoundStorm整合於晶片組中。它依然存在於[nForce 2晶片組中](https://zh.wikipedia.org/wiki/nForce_2 "wikilink")，後在[nForce 3中被剔除](https://zh.wikipedia.org/wiki/nForce_3 "wikilink")。

此外，由於缺乏一個正式的認證程序，這樣很難鼓勵主機板廠商使用高質素的音效元件，作音響高度傳真性的輸出。從技術層面看，沒有通過認證的主機板一樣能處理**未經處理的聲音**，例如[MP3](../Page/MP3.md "wikilink")和CD。

一些廠商曾經推出能實時處理杜比數碼音效和[DTS](../Page/DTS.md "wikilink")的音效卡。

## 外部連結

  - [NVIDIA: SoundStorm](http://www.nvidia.com/object/feature_soundstorm.html)
  - [由NVIDIA推出的數碼音效系統（整合型音效）](http://www.3dss.com/reviews/nForce/nForce.html)
  - [Sensaura（已被Creative收購）](https://web.archive.org/web/20050713234506/http://www.sensaura.com/)

[Category:英伟达](https://zh.wikipedia.org/wiki/Category:英伟达 "wikilink") [Category:音效卡](https://zh.wikipedia.org/wiki/Category:音效卡 "wikilink") [Category:主板](https://zh.wikipedia.org/wiki/Category:主板 "wikilink")