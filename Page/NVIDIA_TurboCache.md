> 本文内容由[NVIDIA TurboCache](https://zh.wikipedia.org/wiki/NVIDIA_TurboCache)转换而来。


**TurboCache**技術是[nVidia發明](https://zh.wikipedia.org/wiki/nVidia "wikilink")，顯示卡會透過PCI-E介面借用系統記憶體，作為顯示記憶體。這是動態借用的，當執行2D程序時，便會釋放借用了的系統記憶體。而顯示卡上亦會內建記憶體，作為緩衝。nVidia最先將此技術应用在[GeForce](../Page/GeForce.md "wikilink") 6200 TC上。

其实顯示卡能借用系統記憶體，全因為晶片組的設計。晶片組能指示系統借用系統記憶體，作為顯示記憶體。在AGP 2X時代，晶片組已有此功能，但AGP頻寬比較小，業者不太乐意釆用，怕會嚴重影響顯示卡效能。但現在的PCI-E 16x 頻寬充足，同時系統記憶體最少也有256MB。nVidia在不大幅影響效能的情況下，率先应用，以降低顯示卡成本。

## 記憶體定義

如果顯示卡上使用的是8x32的32MB顆粒，預設時脈將會為550MHz DDR。 如果顯示卡上使用的是4x32的16MB顆粒，預設時脈將會為700MHz DDR。

  - 當顯示卡上的[記憶體頻寬是](../Page/内存带宽.md "wikilink")32Bit，16MB記憶體，而其有效頻寬則变為64Bit，最高可使用128MB記憶體。
  - 當顯示卡上的記憶體頻寬是32Bit，32MB記憶體，而其有效頻寬則变為64Bit，最高可使用128MB記憶體。
  - 當顯示卡上的記憶體頻寬是64Bit，32MB記憶體，而其有效頻寬則变為128Bit，这模式效能最佳。
  - 當顯示卡上的記憶體頻寬是64Bit，64MB記憶體，而其有效頻寬則变為128Bit，最高可使用256MB記憶體。但記憶體的時脈較低，效能竟較差。

註：系統需有512MB系統記憶體。若系統記憶體少过512MB，顯示卡最高只可使用64MB記憶體。

## 產品支援

  - GeForce 6200 TC
  - GeForce 6100/6150（整合繪圖晶片於主機板上）
  - GeForce 6500 TC
  - GeForce 7300 LE/GS
  - GeForce 7500 LE
  - GeForce 8400GS
  - GeForce 8500 GT

## 優點

  - 降低顯示卡成本

## 缺點

  - 由於使用者觀念关係，顯示卡價格也降低不少，造成6200TC銷售情形普普，之後支援TurboCache的只有低階卡和OEM裝機的顯示卡。

<!-- end list -->

  - 有部分顯示卡廠商利用此技術虛標顯示卡內建記憶體容量。(直接標示TC後的記憶體大小且通常TC字樣寫的不明顯)

## 对手產品

  - [ATi](https://zh.wikipedia.org/wiki/ATi "wikilink") [HyperMemory](https://zh.wikipedia.org/wiki/HyperMemory "wikilink")
  - [S3 Graphics](../Page/S3_Graphics.md "wikilink") AcceleRAM LowFB
  - [XGI](https://zh.wikipedia.org/wiki/XGI "wikilink") eXtreme Cache

## 參見

[Category:英伟达](https://zh.wikipedia.org/wiki/Category:英伟达 "wikilink")