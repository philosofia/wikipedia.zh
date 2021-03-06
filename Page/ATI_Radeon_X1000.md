> 本文内容由[ATI Radeon X1000](https://zh.wikipedia.org/wiki/ATI_Radeon_X1000)转换而来。


**Radeon X1 Series**（代号R520為X1800），是[ATi的一款顯示卡](https://zh.wikipedia.org/wiki/ATi "wikilink")，以台積電0.09微米Low-k製程生產，支援DirectX 9.0c。经过重新设计的Radeon X1 Series与前代Radeon X Series核心完全不相类似。Radeon X1 Series亦支援ShaderModel 3.0、HDR等技術，与对手[nVIDIA的同代产品平起平坐](https://zh.wikipedia.org/wiki/nVIDIA "wikilink")。

## 系列列表

  - 高階Radeon X1800（R520核心）- 核心有3億2千萬顆電晶體，比nVidia G70還多，數量是X850（R420核心）的兩倍。256-bit記憶體頻寬
      - X1800 XT - 16條Pixel Shader流水線及8個Vertex Shader引擎的架構，原对手為GeForce 7800 GTX
      - X1800 XL - 架構与X1800 XT一样，只是时脈較低，原对手為GeForce 7800 GT
  - 中階Radeon X1600（RV530核心）,128-bit記憶體頻寬
      - Radeon X1600 XT - 12條Pixel Shader流水線，原对手為GeForce 6600 GT，但 nVidia 在 GeForce 7 Series 全面推出前為 GeForce 6 Series 變陣，利用6800GS迎頭痛擊X1600XT，結果6800GS大勝，X1600XT被逼降價，而ATI被迫紧急启用性能强大的老将Radeon X800GTO 16管 DDRIII才挽回颓势。
      - Radeon X1600 Pro - 架構与X1600 XT一样，只是时脈較低，其後為改變定位，先後更名為X1300XT及X1650
      - Radeon X1650 GT -架构类似X1950，是X16XX系列中最具杀伤力的产品，性能明显优于Geforce 7600GT。
  - 低階Radeon X1300（RV515核心）,128-bit記憶體頻寬
      - Radeon X1300 Pro - 4條Pixel Shader流水線，原对手為GeForce 6600 和 GeForce 6200，但也在 nVidia GeForce 6 系列變陣中被 6600 DDR2 擊敗
      - Radeon X1300 - 架構与X1300 Pro一样，只是时脈較低

全系列均支援[CrossFire](https://zh.wikipedia.org/wiki/CrossFire "wikilink")

## 繪圖核心

R520核心是全新的繪圖引擎，稱為**Ultra-Threaded Pixel Shader Engine**。它比以前的繪圖核心更有效率。加上以高時脈運作，所以X1800 XT在只擁有16條像素流水線的情況下，效能能与超越擁有24條像素流水線的GeForce 7800 GTX。

### Pixel Shader方面：

支援Pixel Shader 3.0。新的繪圖引擎能把一個很長的Pixel指令，分拆為很多較短的指令，然後再分給各個Pixel Shader Unit運算，由於指令被分拆成很多的小段，各个Unit的運算时間相若。不像以往指令比較長，各小段的複雜程度有分別，造成一些Unit比較快完成運算，而等待另一个Unit的運算結果，造成閒置和浪費。新的繪圖引擎能同時處理512個指令，並支援4\*4=16像素的Pixel Block，提高了Dynamic Branching的效率。这个引擎如果發現了有Unit處於閒置，會立即指示新的指令，不會造成浪費。如果閒置的原因是等待其他Unit的運算結果，它會被凍結此Unit，釋出ALUs來執行其他指令。

### Vertex Shader方面：

新的繪圖核心支援Vertex Shader 3.0，可執行1個128Bit Floating Point Data或是四個32Bit的組合，每個Vertex Shader單元能在每時脈能生成兩個Vertices。

### 記憶體控制器方面：

全新的記憶體控制器稱為**512-Bit Ring Bus Memory Controller**，能減少記憶體的延遲率，增加Hyper-Z的效能。在高解像度和開啟AA及AF特效下，效能會有明顯改善。

傳統顯示卡縱使有高記憶體頻寬，效能亦不能大大提升，原因是核心很多时並不需要太高的頻寬。有如小水流在大水管內流动，很多空間被浪費掉了。

  - 資料儲存

雖然ATi R520的記憶體頻寬是256Bit，但內部架構卻是512Bit。它其實是由兩個256Bit環型管道、四個Ring Stop及8組32Bit的Memory Client所組成。每一個Ring Stop會負責2顆32Bit的記憶體顆粒，而資料的儲存是會通過Ring Stop直至到達指定記憶體。由於兩個環的走向是相對的，多數通過一個Ring Stop就能到達指定記憶體。

  - 記憶體讀取

R520的記憶體讀取架構是，當某單元需要從記憶體讀取資料时，該單元會向記憶體控制器作出讀取要求，但資料不會回傳到記憶體控制器，而是通过Ring Bus傳到該單元。由於不用回傳資料，效率提高了。

ATi亦改良了對外的記憶體頻寬，R520和ATi Radeon X850都是256Bit記憶體頻寬。但X850是由4組64Bit通道組成，而R520則是由8組32Bit通道組成。當核心從記憶體提取8个32Bit的資料时，一个周期即能完全讀取。但上一代的X850同样提取8个32Bit的資料时，由於只有4組通道，需要兩个周期才能完全讀取。

### 新的Anti-Aliasing模式

新的AA模式稱為**Adaptive AA**。這模式是Super-Sample AA和Multi-Sampling的結合，能在畫質及效能上取得平衡。核心能因应每個物件的透明度情況去選擇最合適的AA模式。透明的話就採用Super-Sample AA來達至最佳效果，不透明的話就用Multi-Sampling來取得最佳效能，R520最高支援12X AA。

### 新加入功能：

  - 3D
      - Advanced High Dynamic Range Rendering
      - 128-Bit Floating Point Precision
      - Adaptive Anto-Aliasing
      - High quality Anisotropic Filtering
      - 新的[CrossFire技術](https://zh.wikipedia.org/wiki/CrossFire "wikilink")
      - 64Bit High Dynamic Range Rendering
      - R520容許同時進行HDR及AA運算。[nVidia](https://zh.wikipedia.org/wiki/nVidia "wikilink") [GeForce 7則不能](https://zh.wikipedia.org/wiki/GeForce_7 "wikilink")。
  - 2D
      - 核心支援兩個DVI輸出
      - [AVIVO](https://zh.wikipedia.org/wiki/AVIVO "wikilink")

## Radeon X19 Series

為回應[nVidia的](https://zh.wikipedia.org/wiki/nVidia "wikilink")[GeForce](../Page/GeForce.md "wikilink") 7900系列，ATi推出Radeon X19 Series顯示卡对抗。像素处理单元數目大幅提升至48个。

和X1800时代，ATI与NVIDIA平坐，甚至ATI略微颓势的情况不同，X1900时代与Geforce7对阵，ATI几乎占据全面优势，但持续时间不长便被NVIDIA G80系列打破。

根據ATI统计，像素渲染已成為游戏運算的瓶颈。自从DirectX 8于2001年推出，可编程的渲染引擎被引入，像素渲染開始被大量使用。同時，像素渲染的复杂程度亦不斷的增加。渲染指令分为两类，一個是從顯示記憶體中提取数据作纹理渲染；另一種是利用数学運算作渲染。在2001年時，兩種渲染指令所佔用的資源是相近的。但往後幾年，数学運算型渲染佔用的資源越来越大。到了2006年，比例達到了5：1。根據預測，比例还會持續上升。有鑑於此，ATI將像素处理器和纹理处理器的比例設成3:1。這樣做是確保纹理处理器有足夠頻寬，又會有較多像素处理器作数学運算型渲染。

被喻為最後的ATi顯示卡，Radeon X1950XTX亦已推出。業內人士估計AMD將會取代ATi作為顯示卡品牌。X1950XTX率先支援更快和更低功秏的GDDR4顯示記憶体，使顯核潛能發揮得更淋漓盡至。從X1950XTX CrossFire和7950GX2 Quad SLI的測試可看出，ATI以双顯核擊敗了nVidia的四顯核，可得知Pixel Shader在遊戲的比重非常的大。

[CrossFire方面](https://zh.wikipedia.org/wiki/CrossFire "wikilink")，X1950Pro和X1650XT都內置了 Composting Engine，配置變得簡單，不再需要主卡和接線。

與此同時，ATi亦發佈了數款新顯示卡：

  - X1950XTX - 拥有16條流水线，48個像素处理单元，8個[顶点渲染管线](../Page/頂點_\(電腦圖學\).md "wikilink")，核心速度650Mhz，採用GDDR4記憶體，記憶體速度2000Mhz，記憶體容量512 MB
  - X1950XT - 拥有16條流水线、48個像素处理单元，8個[顶点渲染管线](../Page/頂點_\(電腦圖學\).md "wikilink")，核心速度625Mhz，採用GDDR3記憶體，記憶體速度1800Mhz，記憶體容量由 256 至 512 MB 不等
  - X1950Pro - 拥有12條流水线、36個像素处理单元，8個顶点渲染管线，核心速度600Mhz，採用GDDR3記憶體，記憶體速度1400Mhz，記憶體容量由 256 至 512 MB 不等
  - X1950GT - 拥有12條流水线、36個像素处理单元，8個顶点渲染管线，核心速度500Mhz，採用GDDR3記憶體，記憶體速度1200Mhz，記憶體容量由 256 至 512 MB 不等
  - X1900XT - 拥有16條流水线、48個像素处理单元，8個顶点渲染管线，核心速度625Mhz，採用GDDR3記憶體，記憶體速度1450Mhz，記憶體容量256MB
  - X1650XT - 拥有8條流水线、24個像素处理单元，5個顶点渲染管线，核心速度600Mhz，採用GDDR3記憶體，記憶體速度1400Mhz，記憶體容量256MB
  - X1650GT - X1650XT的降頻版，用料也可簡化，性能强劲，夺取了Geforce7300GT和7600GT大部分市场。
  - X1650Pro - 顯核与X1600XT相同，对抗GeForce 7600GS.
  - X1650 - 顯核与X1600 Pro相同，変相將中階卡降格為高級低階卡，對抗GeForce 7300GT.

## Mobility版本

架構与桌面版本相同，所有版本皆支援DirectX 9.0c,OpenGL和[AVIVO](https://zh.wikipedia.org/wiki/AVIVO "wikilink")。电源管理技术是PowerPlay 6.0。

  - X1700 -
  - X1450 - 支援HyperMemory
  - X1350 - 支援HyperMemory

[Category:ATI顯示卡](https://zh.wikipedia.org/wiki/Category:ATI顯示卡 "wikilink")