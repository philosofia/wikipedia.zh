> 本文内容由[NVIDIA GeForce 8](https://zh.wikipedia.org/wiki/NVIDIA_GeForce_8)转换而来。


**GeForce 8系列**，代號**G80**，是[NVIDIA的第八代GeForce顯示晶片](https://zh.wikipedia.org/wiki/NVIDIA "wikilink")。在7900 GTX发布后八个月，NVIDIA於2006年11月推出GeForce 8800 GTX，它是建基於G80核心。G80是全球首款支援[DirectX](../Page/DirectX.md "wikilink") 10的顯示晶片，核心的架构和技术比前代GeForce 7系列顯示晶片有很大的不同。縱使它是為DirectX 10而設計，但由於架構的改進，G80在DirectX 9环境下仍可以發揮出強大的效能。

## DirectX 10的改進

虽然DirectX受人歡迎，但是DirectX 9的規格始終為遊戲開發者帶來限制。在圖形[API誕生前](https://zh.wikipedia.org/wiki/API "wikilink")，當時的程式開發者能利用指令來控制顯示卡。但不同的架構就需要不同的指令，這就造成兼容性問題。為此，業界為了統一規格，就發展出最普遍的DirectX和OpenGL兩種規格。縱使API能解決兼容性問題，但是衍生出新的問題。在3D環境中，所有東西都以物件方式存在，而物件的運算則順序由程式、API和[驅動程式之間傳輸](https://zh.wikipedia.org/wiki/驅動程式 "wikilink")。而[CPU必須參與這個過程](https://zh.wikipedia.org/wiki/CPU "wikilink")。物件愈多，CPU負荷愈重。所以物件數量不能過多，但畫面質素就不能大幅提升。 新的DirectX 10則解決了這個問題。當物件第一次運算時，CPU會參與這個過程，但到了第二次時，CPU不會再參與這個過程。物件數量就能大幅提升，畫質就能相應提高。

除了以上措施能減低CPU負擔，DirectX 10亦新增了兩個減低CPU負擔的功能。

[NVIDIA_GeForce_8800_Ultra.png](https://zh.wikipedia.org/wiki/File:NVIDIA_GeForce_8800_Ultra.png "fig:NVIDIA_GeForce_8800_Ultra.png") [NVIDIA_GeForce_8800_Ultra_Board.jpg](https://zh.wikipedia.org/wiki/File:NVIDIA_GeForce_8800_Ultra_Board.jpg "fig:NVIDIA_GeForce_8800_Ultra_Board.jpg")

### 纹理阵列

以往，多紋理轉換動作使用大量CPU資源。DirectX 10的纹理阵列功能能解決這個問題。在每个纹理阵列中，最多可以保存512個同样大小的纹理。纹理的最高解像度由DirectX 9的4096x4096提升至8192x8192。每一個Shader能使用128個纹理，為上一代DirectX 9的8倍。Render Targets由4個增加到8個。所以在DirectX 10中，物件有更多細節，更富真實感。

### 繪製斷言

在一個3D場景中，物件會遮住其他物件，不會在畫面顯示。預早偵測出不會在畫面顯示的物件，能減少不必要的運算，增加資源。雖然以往的顯示核心已擁有這個功能，但始終有些物件不會被預早偵測。程式設計者會採用**繪製斷言**這個技術，將物件製作成方塊，當方塊不能在前景中顯示，就可以省下該物件的運算。過往這個過程需要CPU介入，但在DirectX 10中，顯示核心完全負責這個過程，增加CPU資源。

### Shader Model 4.0

[DirectX](../Page/DirectX.md "wikilink") 10採用[Shader Model](https://zh.wikipedia.org/wiki/Shader_Model "wikilink") 4.0版本，進一步減少資源限制。例如[Register的資源不足問題](https://zh.wikipedia.org/wiki/Register "wikilink")。

以下為減少資源限制的措施的列表：

  - Temporary Registers Buffers : 4096
  - Constant Registers Buffers : 65536

### Higher Level Shading Lanagage(HLSL)

它在DirectX 9中首次出現。在DirectX 10中，會採用HLSL 10版本。亦新增**纹理阵列**功能（請參考上面）。

改进列表：

  - 常數缓存：渲染過程中需要很多常數，来定义各样的参数\[1\]，例如身件的位置，光线的颜色，觀察者的位置等等。在渲染過程中，常數會不斷被更新。更新時就需要到常數缓存。DirectX 10的常數缓存容量是DirectX 9的16倍，而且架构更有效率。

<!-- end list -->

  - Views：以往在[頂點著色器的缓存無法被像素著色器利用](https://zh.wikipedia.org/wiki/頂點著色器 "wikilink")，反之亦然。这就限制了很多资源的利用。DirectX 10就解決了這個問題。当资源被著色器建立後，就成為数据块，並且用Views结构标示出來。這樣资源就可以以不同方式利用得到。例如图形数据被像素著色器处理成纹理数据，頂點著色器能將纹理数据处理成几何数据\[2\]。這樣资源就能夠被靈活運用。

<!-- end list -->

  - Integer and Bitwise Instructions：不用將浮点數據转换成整数數據就能直接进行整数算法，[GPGPU的处理能力就能提高](https://zh.wikipedia.org/wiki/GPGPU "wikilink")。

<!-- end list -->

  - Switch Statement：支持[转换陈述](https://zh.wikipedia.org/wiki/转换陈述 "wikilink")，簡易著色编程的线路计算。

### [HDR](https://zh.wikipedia.org/wiki/HDR "wikilink")

DirectX 10支援兩種新的HDR模式。第一種採用11-Bit紅色和綠色、10-Bit藍色。另一種採用5-Bit共享運算，另加每一種顔色以9-Bit作尾數運算。新的HDR模式能增加資源使用效率。DirectX 10亦支援FP32，提高HDR質素。G80提供全新的128bit精度的HDR運算，並可與抗鋸齒技術同時運作，讓HDR+AA不再是ATI的專利。

### Geometry Shader（幾何著色引擎）

DirectX 10首次加入Geometry Shader，功用是將點、線、及三角連接起來，以為此過程由頂點著色器負責。它能有效提升模板陰影特效、動態立方體貼圖和[位移貼圖的執行效率](https://zh.wikipedia.org/wiki/位移映射 "wikilink")。它能減少CPU的負擔，增加系統資源。當頂點著色引擎產生出一組[頂點數據後](../Page/頂點_\(電腦圖學\).md "wikilink")，隨後的幾何著色引擎能將數據化成最高1024個[頂點](../Page/頂點_\(電腦圖學\).md "wikilink")，即是將數據頂點數據增多。幾何著色引擎亦可將多餘的頂點數據除去，增加顯示核心的運算效率。

幾何著色引擎能使位移貼圖技術配合鑲嵌圖形技術。位移貼圖十分常見，通常用於非即時3D渲染中。位移貼圖的原理是首先建構一個簡單的平面模型，然後增加[頂點數量](../Page/頂點_\(電腦圖學\).md "wikilink")。顯示核心會根據一張灰階紋理，去將該平面模型立體化。而鑲嵌圖形技術則會把一個模型鑲嵌更多多邊形，增加細節。

上一代的DirectX 9並不可以完好的支援鑲嵌圖形技術。DirectX 10的幾何著色引擎就解決了這個問題。位移貼圖技術和鑲嵌圖形技術可一同進行運算，物件表面更真實。

此外，幾何著色引擎的運算結果能直接傳送到顯示記憶體中，不用通過像素著色引擎，提升效率。將來，顯示核心能集中處理物理運算。

### 其它DirectX 10的改进

  - Alpha to coverage：复杂的几何图形通常会被透明多边形代替，例如树叶和鐵絲網這些重复性很高的物件。想像一塊平面，標示透明和不透明地方後，渲染後就成為鐵絲網。但透明和不透明的连接地方會有很多锯齿，雖然利用Alpha渲染可以解决問題，但性能损失十分大。Alpha to coverage能減少性能损失。

<!-- end list -->

  - 阴影帖图过滤：減少阴影的锯齿，使之更柔和。

<!-- end list -->

  - Access to Multi-sampling Sub-Samples：可以存取MSAA的子样本，並控制它。

## 產品架構

[NVIDIA_G80_GPU.jpg](https://zh.wikipedia.org/wiki/File:NVIDIA_G80_GPU.jpg "fig:NVIDIA_G80_GPU.jpg") [NVIDIA_NVIO-1-A3_RAMDAC.jpg](https://zh.wikipedia.org/wiki/File:NVIDIA_NVIO-1-A3_RAMDAC.jpg "fig:NVIDIA_NVIO-1-A3_RAMDAC.jpg")\]\] GeForce 8採用統一管線結構。傳統顯示核心的架構分為[頂點著色引擎和像素著色引擎](https://zh.wikipedia.org/wiki/頂點著色引擎 "wikilink")。當頂點著色引擎負荷很重時，像素著色引擎可能閒置著，反之亦然。這就造成顯示核心運算能力不被充分發揮，浪費資源。DirectX 10將[頂點著色](../Page/頂點_\(電腦圖學\).md "wikilink")、幾何著色和像素著色合併成一個渲染流程。所以每一個統一流处理器都能處理頂點、幾何和像素數據，不會有閒置問題，效率顯著提升。

G80顯示核心擁有128個流处理器，每16個為一組，每一組有8個材质过滤单元和4個材质寻址单元，每一組流处理器都擁有L1和l2緩衝記憶体。G80可同時執行過千個執行緒，nVIDIA稱之為GigaThread技術。某程度上，nVIDIA參考了ATI的設計，使其顯示核心能進行異類運算工作，例如物理運算和影像編碼。

物理運算方面，G80已作出強化，nVIDIA稱之為Quantum Effects技術，效率比CPU高很多。

nVIDIA終於加入Early-Z技術，它的目的與繪製斷言相似，但原理不一樣。現先介紹一下Z缓存技术，通过测试像素深度和缓存数据比较，可測量到每一个像素的最后位置。若像素被其他像素遮挡住，被遮挡住的像素的數據则會被去掉。但很多無用的像素數據沒有去掉，依然通過像素流水線，造成資源浪費。基於以往的技術限制，要預先偵測無用像素數據，必需通過整條像素流水線。Early-Z技術能解決這個問題。像素數據在進入像素著色器前，會預先被偵測，若果是無用的數據，就不用通過像素單位，省下資源。理論上，支援Early-Z技術的8800GTX比7900 GTX快4倍去篩選无用的像素數據。

G80可并行计算材质數據，而不用像以往的顯示核心般，存有等待時間。

### Lumenex 引擎

G80的強化畫質引擎稱為Lumenex，它支援Anti-Aliasing（反鋸齒技術）、High Dynamic Range和Anisotropic Filtering（各向异性过滤）。反鋸齒方面，將同時利用覆盖采样和几何採樣。這個新模式稱為Coverage Sample Anti-aliasing(CSAA)，程度分為8x、8xQ、16x和16xQ。其中的Q版本畫質較高。CSAA 16x的画质比常规反锯齿4x好，但是性能趺幅相近。縱使CSAA 16x影像質素高，但當遊戲採用大量模板陰影時，會影響到CSAA運算效率。

各向异性过滤方面，G80加入了Angular LOD控制，能有效加强锐利度。

影像輸出方面，G80支援10-Bit（十億種色彩）影像輸出，比上一代的8-Bit（一干六百萬種色彩）影像輸出質素大幅提升。但比ATI遲了一代。

### 第二代[PureVideo](https://zh.wikipedia.org/wiki/PureVideo "wikilink") HD

GeForce 8800系列顯示卡都支援[HDCP](../Page/HDCP.md "wikilink")（High-bandwidth Digital Content Protection）。HDCP會保護[HDTV](https://zh.wikipedia.org/wiki/HDTV "wikilink")、[Blu-Ray及](https://zh.wikipedia.org/wiki/BD "wikilink")[HD-DVD的影像內容](https://zh.wikipedia.org/wiki/HD-DVD "wikilink")，防止非法拷貝。不支援HDCP的顯示卡，解像度會強行由1080p降至540p。

暫時只有8800GT和8800GTS(G92,512MB)高階顯示卡支援新一代[PureVideo](https://zh.wikipedia.org/wiki/PureVideo "wikilink") HD技術，首次支援高清影訊雜訊消除和邊緣強化技術。在HQV影像測試中，取得128分高分，為現時最佳成績。它除了支援720p、1080i及1080p等解像度外，並支援H.264 、VC-1、WMV-HD及MPEG-HD硬件解碼。

而G84和G86所支援的PureVideo HD技術更強，將所有影像解碼工作交由顯示核心（VP2）負責，大幅降低CPU佔用率。亦新加入BitStream Processor，能夠完全硬體解碼H.264及部分硬體解碼VC-1的影片。最後，加入了AES128運算引擎，就能硬體解碼[AACS](../Page/AACS.md "wikilink")，由於Windows Vista的關係，這種解碼方式將被頻繁使用，硬體解碼就變得必要。

## 產品型號

### [桌面平臺](https://zh.wikipedia.org/wiki/桌面平臺 "wikilink")

#### GeForce 8100

是整合於[MCP78S晶片組中的顯示核心](https://zh.wikipedia.org/wiki/nForce_700 "wikilink")，有16個流處理器，核心頻率為500 MHz，不支援PureVideo功能。

#### GeForce 8200

同GeForce 8100一樣是整合於MCP78S晶片組中的顯示核心，規格相同，但支援PureVideo功能。

#### GeForce 8300

是GeForce 8系列的最低端獨立顯示卡。只會出現於[OEM市場](https://zh.wikipedia.org/wiki/OEM "wikilink")，並不會出現於[零售](../Page/零售.md "wikilink")市場。8300 GS把記憶體頻寬降至64bit，更不支援PureVideo功能。

#### GeForce 8400系列

起初8400 GS(G86)的PureVideo HD是不可以支援VC-1硬體解碼。之後，NVIDIA推出了採用新核心的8400 GS顯示卡。核心代號是G98，是繼G92後的第二款採用65nm工藝製造的顯示核心。核心由[聯電生產](https://zh.wikipedia.org/wiki/聯電 "wikilink")，核心頻率是567MHz。新的核心，已新增支援VC-1硬體解碼。所以，新的8400 GS已完整支援，[H.264和VC](https://zh.wikipedia.org/wiki/H.264 "wikilink")-1解碼。但是，HDCP Key Rom仍然未整合到顯示核心中，須要另加晶片支援。[HDMI](../Page/HDMI.md "wikilink")方面，音頻信號須透過[SPIDF輸入](https://zh.wikipedia.org/wiki/SPIDF "wikilink")，顯示核心仍然不像HD系列顯示卡般，能直接處理音頻信號。另外，新版本的8400 GS顯示核心只有8個流處理器，效能會比第一代差。

在2008年初，第三版的8400GS推出。這次使用與8600GT一樣的G84核心，流處理器數量與G86一樣。廠商亦會使用較高速的顯示記憶體。\[3\]

#### GeForce 8500系列

這個系列採用G86顯示核心，定位是主流級。它擁有16個統一流處理器，8個Texture Filtering Unit，8個Texture Address Unit和 4個光柵操作單元。目前只有一款形號，就是GeForce 8500 GT。對於HDCP的支援，廠商可自由選擇是否支援。顯示記憶體方面，G86核心最高支援GDDR4記憶體，而記憶體頻寬只有128bit，是高端G80的三分一。影像方面，支援第二代的PureVideo HD。

#### GeForce 8600系列

[Galaxy_NVIDIA_GeForce_8600GT.JPG](https://zh.wikipedia.org/wiki/File:Galaxy_NVIDIA_GeForce_8600GT.JPG "fig:Galaxy_NVIDIA_GeForce_8600GT.JPG") 這個系列採用G84顯示核心，定位是中端。它擁有32個統一流處理器，16個Texture Filtering Unit，16個Texture Address Unit和 8個光柵操作單元。值得注意的是，在G80核心中，每個可編程運算單元有4個Texture Addressing Unit；而在G84和G86核心中，每個可編程運算單元有8個Texture Addressing Unit。所以G84和G86核心不是單純的從G80簡化而成。整個8600系列有兩款顯示卡形號，它們是Geforce 8600 GTS和8600 GT版本。當中的分別是GTS版本顯示核心和記憶體的頻率較高。還有，GTS版本是強制性支援[HDCP](../Page/HDCP.md "wikilink")，而GT版本則可有可無。顯示記憶體方面，G84核心最高支援GDDR4記憶體，而記憶體頻寬只有128bit，是高端G80的三分一。影像方面支援第二代的PureVideo HD。

#### GeForce 8800系列

[Geforce8800gts.jpg](https://zh.wikipedia.org/wiki/File:Geforce8800gts.jpg "fig:Geforce8800gts.jpg") G80於2006年11月8日推出。高階形號為GeForce 8800，核心擁有6億8千1百萬個電晶體，為上一代G70的兩倍。現時有三個高階形號，分別是Ultra、GTX和GTS版本。G80採用90奈米制程由[TSMC代工](https://zh.wikipedia.org/wiki/台灣積體電路製造公司 "wikilink")。GTX版本會取代GeForce 7950 GX2，GTS版本則取代GeForce 7900 GTX。GeForce 8800 GTX (G80-300) 擁有128個統一流處理器，64個Texture Filtering Unit，32個Texture Address Unit和 24個光柵操作單元。核心頻率是575MHz，但部份流處理器的頻率是1.35GHz，運算效能高達519 gigaflops。G80最高支援384-Bit顯示記憶體頻寬，最高顯示記憶體容量為768MB，預設顯示記憶體頻率是1.8GHz。 顯示卡長10.5吋，功耗達185W，需要兩組外接 6 pin 電源。

  - GeForce 8800 GTX需採用450W電源供應器驅動，若只插入一個電源接口，顯示卡會降低核心頻率。縱使卡上擁有兩個MIO接口，但現時只需接上一個接口即可開啟[SLI模式](https://zh.wikipedia.org/wiki/SLI "wikilink")。顯示卡板上多了一顆晶片，名為NVIO-1。它負責所有顯示輸出，包括模擬和數碼輸出。未來若追加新顯示輸出制式，例如[HDMI](../Page/HDMI.md "wikilink")和[VideoPort](https://zh.wikipedia.org/wiki/VideoPort "wikilink")，就只需推出新的NVIO晶片，不需更改顯示核心設計。

<!-- end list -->

  - GeForce 8800GTS (G80-100) 是G80核心的平價版本，核心與GTX版本相同，規格差異請看下-{表}-。它擁有96個統一流處理器，48個Texture Filtering Unit、24個Textyre Address Unit和20個光柵操作單元。顯示卡長9吋，功耗是150W，需採用400W電源供應器驅動，只需一組外接電源。卡上擁有一個MIO接口。

<!-- end list -->

  - GeForce 8800 Ultra (G80-450) 是新近推出的GTX升級版，Geforce 8800 Ultra的ASIC版本由8800 GTX的A2版本升级到A3版本，但仍舊只有128個統一流處理器，64個Texture Filtering Unit，32個Texture Address Unit和24個光柵操作單元。核心頻率提高至612MHz，部份流處理器的頻率是1.5GHz，運算效能高達576 gigaflops。顯示記憶體容量與GTX同為 768MB，但因使用-0.8ns記憶體顆粒，預設顯示記憶體頻率高達2.16GHz。至於採用新製程的G80-400核心，就在耗電一環稍有進步。建議零售價與規格一樣驚人，達 829[美元](../Page/美元.md "wikilink")。另外，它支援三路[SLI](https://zh.wikipedia.org/wiki/SLI "wikilink")。

下一代G92核心的首張產品是8800 GT，2007年10月29日推出。核心以65[奈米製程生產](https://zh.wikipedia.org/wiki/奈米 "wikilink")，熱量更低，效能更高。顯示記憶體方面，支援256-bit頻寬。雖然頻寬比舊有的320-bit少，但成本可以大幅下降，只需要8顆記憶體就可以實現。事實亦證明，256-bit的效能與320-bit不相伯仲。值得注意的是，在9800 GT推出後，有廠商的8800 GT顯示卡只支援128-bit記憶體頻寬，流處理器的數量亦由112下降到96個，效能比9600 GSO更差，NVIDIA表示對此並不知情\[4\]。G92核心亦支援新的顯示卡介面PCI-E 2.0。視頻播放加速方面，是第一張NVIDIA的高端顯示卡支援PureVideo HD技術。經過測試在預設頻率下效能已更勝同廠產品8800 GTS 320MB及8800 GTS 640MB，以及ATI的HD 2900 XT 512MB及HD 2900 Pro 512MB。而採用G92核心的新板8800 GTS，流處理器的數量亦有所提升，由96個增加到128個。纹理拾取单元的數量亦倍增。

### [行動平臺](https://zh.wikipedia.org/wiki/行動平臺 "wikilink")

  - GeForce 8200M G，是整合於[MCP77MV和](https://zh.wikipedia.org/wiki/nForce_700 "wikilink")[MCP79MV行動晶片組中的顯示核心](https://zh.wikipedia.org/wiki/nForce_700 "wikilink")，擁有8個流處理器，核心頻率500 MHz。
  - GeForce 8400M G，核心編號G86M，擁有8個流處理器，核心頻率400 Mhz，最大顯示記憶體64MB。
  - GeForce 8400M GS，核心編號G86M，擁有16個流處理器，最大顯示記憶體128MB，其他規格與8400M G相同。
  - GeForce 8400M GT，核心編號G86M，擁有16個流處理器，核心頻率600 Mhz，最大顯示記憶體256MB。
  - GeForce 8600M GS，核心編號G84M，擁有16個流處理器，其他規格與8400M GT相同。該顯卡曾傳出散熱不良的問題，曾多次召回更換。下面核心代號相同的8600M GT和8700M GT也受牽連。
  - GeForce 8600M GT，核心編號G84M，擁有32個流處理器，核心頻率475 Mhz，最大顯示記憶體512MB。
  - GeForce 8700M GT，核心編號G84M，擁有32個流處理器，核心頻率625 Mhz，其他規格與8600M GT相同。
  - GeForce 8800M GTS，採用下一代65奈米顯示核心G92M，擁有64個流處理器，核心頻率500 Mhz，512位最大顯示記憶體頻寬。
  - GeForce 8800M GTX，採用下一代65奈米顯示核心G92M，擁有96個流處理器，核心頻率500 Mhz，512位最大顯示記憶體頻寬。

## 參考條目

  - [GeForce 8系列規格列表](https://zh.wikipedia.org/wiki/NVIDIA顯示核心列表#GeForce_8 "wikilink")
  - [GeForce 8 M系列規格列表](https://zh.wikipedia.org/wiki/NVIDIA顯示核心列表#GeForce_8_M "wikilink")
  - [Radeon R600](https://zh.wikipedia.org/wiki/Radeon_R600 "wikilink")

## 參考

## 外部連結

  - [NVIDIA的GeForce 8系列](http://www.nvidia.com/page/geforce8.html)
  - [Guru 3d Review of Geforce 8](http://www.guru3d.com/article/Videocards/391/1/)
  - [中关村在线 - 离电影画质有多远？详谈DX10最新特效](http://vga.zol.com.cn/41/418722.html)

[Category:GeForce系列](https://zh.wikipedia.org/wiki/Category:GeForce系列 "wikilink") [Category:2006年面世的產品](https://zh.wikipedia.org/wiki/Category:2006年面世的產品 "wikilink")

1.
2.
3.  [三英战吕布！入门级HD3450对决8400GS](http://www.pcpop.com/doc/0/267/267516.shtml)
4.  [小心 市场可能出现缩水版8800 GT显卡](http://news.mydrivers.com/1/112/112796.htm)