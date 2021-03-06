> 本文内容由[ATI Radeon X](https://zh.wikipedia.org/wiki/ATI_Radeon_X)转换而来。


**Radeon X Series**（代号R420為X800）於2004年推出，是[ATi的一款显卡](https://zh.wikipedia.org/wiki/ATi "wikilink")，以[台積電](https://zh.wikipedia.org/wiki/台積電 "wikilink")[0.13微米Low](https://zh.wikipedia.org/wiki/0.13微米製程 "wikilink")-k製程生產。只支援DirectX 9.0b，不支援DirectX 9.0c。核心与[Radeon 9 Series相似](https://zh.wikipedia.org/wiki/Radeon_9_Series "wikilink")，新的核心只做了些改進。所以不支援 ShaderModel 3.0、[HDR等功能](https://zh.wikipedia.org/wiki/HDR "wikilink")。ATi声稱X800 XT PE的效能Radeon 9800 XT高出2倍。此系列的X850 XT PE是最快的AGP显卡。

## 与前代的改進

  - 更多頂點著色單元（Vertex Shader）
  - 更多改良过的像素著色單元（Pixel Shader）
      - 暫存器（Temporary Registers）數量由12個增加到32個
      - 像素著色指令 (Instructions) 由 120 道增加到1536道
      - 改善了F-buffer（Fragment-Stream FIFO buffer）
          - 像素著色程式不需重新運算，即可繼續處理下一道指令；所以理論上Shader程式碼長度是無限長（將Shader程式碼斬件處理）
          - 这个新F-buffer只會把下一回處理到的像素保存下來，只不是整个畫面。
  - 改良了記憶體控制單元
  - 加入新的曲面法線貼圖（Normal Mapping）的壓縮技術，即3Dc

3Dc是一種新的材質壓縮技術。它能提供細緻影像，並減少使用記憶體頻寬。其採用了Normal Map的技術，令Texture表面的光影效果更具質感。假設有一個3D模型原需15,000個多邊型砌出來，然後再建立一个相似模型，但用1,000個多邊型砌出來。3Dc技術就會把兩个模型的分別，存成Normal Map。之後在遊戲時，只需要用上1,000個多邊型，再運用3Dc存取Normal Map還元，就能達成14,000個多邊型的效果，減少使用記憶體頻寬。

  - 加入新的SmartShader HD、Smoothvision HD及Hyber Z HD，加快处理高解像度畫面
      - SmartShader HD
          - Vertex Shaders - 其六個頂點著色單元，可在每個周期控制兩個Shader工作，效能較Radeon 9800 XT高出2倍。
          - Pixel Shaders - 暫存器最大Texture指令數目由32條增至512條，Vector指令數目及Scalar指令數目由64條增至512條
      - Smoothvision HD
          - 反線性過濾 - 使用者可隨心選擇'雙線性過濾模式'或'多線性過濾模式'。當使用雙線性過濾，效能比較好。當使用多線性過濾，畫質比較好。使用者亦可選擇混合模式，讓駆动衡量那模式比較好。最高支援16X反線性過濾。
          - 加入新的頁框交錯全景反鋸齒（Temporal FSAA）

假設有一連串畫面，並標示為單數頁與雙數頁。而顯視卡在單數頁負責a樣式的2X FSAA運算，在雙數頁負責b樣式的2X FSAA運算。快速播放時，好像兩个樣式重疊了，做成了4X FSAA效果。花2x FSAA的效能，就達到4x FSAA的畫質。

但不支援DirectX 9.0c成了整个系列的致命傷。与此同时，[nVidia](https://zh.wikipedia.org/wiki/nVidia "wikilink") [GeForce 6 Series正逐漸收復失地](https://zh.wikipedia.org/wiki/GeForce_6 "wikilink")。浮點精確度只是24bit，而不是[nVidia](https://zh.wikipedia.org/wiki/nVidia "wikilink") [GeForce 6 Series的](https://zh.wikipedia.org/wiki/GeForce_6 "wikilink")32bit，所以被对手挪喻“顏色不準”。

## 系列初期顯視卡型号

  - X800XT Platinum Edition - 16條管線，核心時脈：520 MHz，記憶體時脈：560 MHz，記憶體頻寬為256bit,6組頂點著色單元。因 X800XT 效能不及 6800Ultra 而衍生出來的高頻版。
  - X800XT - 16條管線，核心時脈：500 MHz，記憶體時脈：500 MHz，記憶體頻寬為256bit,6組頂點著色單元 原定對手為 GeForce 6800Ultra
  - X800 Pro - 12條管線，核心時脈：475 MHz，記憶體時脈：560 MHz，記憶體頻寬為256bit,6組頂點著色單元。原定对手是 GeForce 6800GT
  - X800 SE - 8條管線，6個頂點著色單元。主攻 OEM 市場
  - X600 - 4條管線，原定对手是GeForce PCX 5700/5750/6600
  - X300 - 4條管線，原定对手是GeForce PCX 5300/6200TC
  - X800GTO -12条管线，核心频率由厂商自定，記憶體頻寬為256bit,6組頂點著色單元 原定對手為 Geforce 6600GT DDR3，后来对手为Geforce 7300GT /7600GS/7600GT/6800GS

X800 XT內有1億6,000萬顆電晶體。

後來，ATi發現X800Pro性能上並非6800GT的對手，X600(9600)亦不是6600的对手，遂推出新一代建基於 R520 的顯示卡。

唯一一个对NVIDIA造成较大麻烦的型号是ATI作为高性价比产品推出的X800 GTO，这种12管线的X800成本较低，且使用了改良的工艺，并有机会破解成16管线，在与NVIDIA Geforce6600GT的竞争中佔据完全优势，而价格相差不大。以至于在后期与NVIDIA更新的Geforce7300GT和7600GT的竞争中继续能够保持一定的优势，让X800的低端产品成功延续了两代，实际上代替了X600XT,X1300Pro和X1600Pro对阵了NVIDIA前后两代DX9.0C的产品。

## 之後顯示卡型號

  - X850 Series
      - X850 PRO, 12管線，取代 X800Pro，與 X800XL 一樣，對手為 6800GT
      - X850 XT，取代 X800XT
      - X850 XT PE，取代 X800XT PE，經三次小轉款終於取下效能之王寶座
  - X800 Series
      - X800 GTO,12條管線，對手是GeForce 6800GS
      - X800,12條管線，對手是GeForce 6800
      - X800 GT，即 X800SE，因 X700XT 良率不佳無法推出而把對手定為GeForce 6600 GT
  - X700 Series
      - X700Pro，效能夾於6600GT和6600之間
      - X700SE，因6600GT和6600之間有很大的效能分野，所以X700SE效能亦夾於6600GT和6600之間，比X700Pro慢一點點
  - X550 Series，因當年9550的成功而再推相同類型的顯示卡，但計劃並非很成功
  - X300 [HM](https://zh.wikipedia.org/wiki/HyperMemory "wikilink")，對手是GeForce 6200 [TC](https://zh.wikipedia.org/wiki/TurboCache "wikilink")

[Category:ATI顯示卡](https://zh.wikipedia.org/wiki/Category:ATI顯示卡 "wikilink")