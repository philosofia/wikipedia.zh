> 本文内容由[Big.LITTLE](https://zh.wikipedia.org/wiki/Big.LITTLE)转换而来。


**ARM big.LITTLE**或**big.LITTLE**是由[安謀國際科技公司](https://zh.wikipedia.org/wiki/安謀國際科技 "wikilink")（ARM）提出的[異質運算](https://zh.wikipedia.org/wiki/異質運算 "wikilink")[多核心處理器](../Page/多核心處理器.md "wikilink")組態結構配置。在這個組態，將比較耗電、但運算能力強的處理器核心組成的「big叢集」與低耗電、運算能力弱的處理器核心組成的「LITTLE叢集」結合在一起，這些處理器核心共用[記憶體區段](https://zh.wikipedia.org/wiki/記憶體 "wikilink")，並能夠在不同的CPU叢集之間線上實時分派、切換負載。\[1\]這個多核心處理器組態結構運用在-{zh-hant:行動計算;zh-cn:移动计算}-上，從而能夠做出計算高效能，但是平均耗電低的多核心處理器，ARM的市場資料稱在某些運算操作中這個組態配置相比只使用與「big叢集」相同CPU核心數量的處理器可節省多達75%的功耗。\[2\]

本組態配置式在2011年10月ARM發表[Cortex-A7時首次對外公布](../Page/ARM_Cortex-A7_MPCore.md "wikilink")，[Cortex-A15也能夠與這個架構相容](../Page/ARM_Cortex-A15_MPCore.md "wikilink")。\[3\]2012年10月，ARM公司宣布與（[ARMv8](https://zh.wikipedia.org/wiki/ARMv8 "wikilink")）也能與這個架構相容。\[4\]2014年2月ARM發表，同一年在[Computex 2013上ARM又發表了](../Page/台北國際電腦展覽會.md "wikilink")，這兩種CPU核心也可用於big.LITTLE配置式中的「big叢集」上（「LITTLE叢集」由Cortex-A7擔當）。\[5\]\[6\]

2017年5月，ARM發表DynamIQ取代big.LITTLE。\[7\]與big.LITTLE相比，DynamIQ允許更為靈活的CPU核心配置和更大規模的叢集設計（每個CPU叢集可以有八顆CPU核心）、叢集數量更多（一塊CPU上最大可擴充至32個叢集）、更精確的電源控制（每個核心內有更多的時鐘門控和電壓控制）以及更快速的L2快取存取操作。然而DynamIQ僅適用於[Cortex-A75](https://zh.wikipedia.org/wiki/ARM_Cortex-A75 "wikilink")、[Cortex-A55及往後推出的ARM](https://zh.wikipedia.org/wiki/ARM_Cortex-A55 "wikilink") CPU核心。

## 運行狀態遷移切換方式

big.LITTLE中，節電的「LITTLE叢集」和高效能的「big叢集」之間有三種切換方式，均要求線上實時操作，除了電路設計以外還需要作業系統的配合得當（一些方式需要依賴作業系統的工作流排程實作）\[8\]\[9\]

### 叢集切換

[Big.Little_Cluster_Switching.png](https://zh.wikipedia.org/wiki/File:Big.Little_Cluster_Switching.png "fig:Big.Little_Cluster_Switching.png") 最早也是最簡單的big.LITTLE組態實作是這種大小核心叢集的切換，高效能CPU核心亦即大核心組成「big叢集」，而低功耗CPU核心亦即小核心，則是組成「LITTLE叢集」。作業系統的排程器在某一時間點上只能見到一組CPU叢集，整個處理器的負載高低變化時，系統會在不同叢集間轉移負載。當負載從一個CPU叢集轉移至另一CPU叢集時，相關的資料、執行狀態等被保存在這些叢集共用的[二級快取](https://zh.wikipedia.org/wiki/CPU快取 "wikilink")（L2 Cache）當中，先前運作的CPU叢集斷電關閉然後加電壓開啟另一個叢集。叢集的資料轉移還需要使用快取一致性互聯（CCI）。這種big.LITTLE的第一個實作是[三星](../Page/三星電子.md "wikilink")[Exynos](https://zh.wikipedia.org/wiki/Exynos "wikilink") 5410 Octa。\[10\]這種方式的一大缺點是CPU叢集間的切換延時較高，並且CPU核心的利用率較低。

### 內核內建切換器（CPU遷移）

[In_Kernel_Switcher.jpg](https://zh.wikipedia.org/wiki/File:In_Kernel_Switcher.jpg "fig:In_Kernel_Switcher.jpg") 這種切換方式自叢集切換方式演變，主要區別在於每一個叢集對作業系統排程器來說都是可見的。在此種方式中，任務在CPU核心之間切換使用內核內建切換器（in-kernel switcher，IKS），晶片設計上是一個高效能CPU核心和一個低功耗CPU核心組成一個復合叢集，這一個叢集作為一個「虛擬的」核心來供作業系統操作，同一時間點上這一對CPU核心只有一顆在運作，高效能CPU核心僅在有高效能運算需求時才開啟，運算效能需求低時則是只開啟低功耗核心。當虛擬核心內負載在高低之間變化時，先開啟將要切換到的CPU核心，轉移執行狀態，轉移完成後關閉先前運行的CPU核心，由該CPU核心繼續執行先前的處理進程。切換工作需要通過cpufreq框架完成。[Linux](../Page/Linux.md "wikilink") 3.11內核開始提供了big.LITTLE IKS完整實作所需內核元件模組。

[蘋果公司的](https://zh.wikipedia.org/wiki/蘋果公司 "wikilink")[A10 Fusion以及A](../Page/Apple_A10_Fusion.md "wikilink")10X Fusion即採用此種big.LITTLE組態。不過，更複雜多樣的「大小核心」CPU核心分組，也是有可能的，一隻採用IKS方式的處理器上容許一個虛擬核心內有一顆以上的高效能CPU核心或低功耗CPU核心，或者是相同的CPU核心而分成主副CPU核心。[輝達的](https://zh.wikipedia.org/wiki/輝達 "wikilink")[Tegra 3](https://zh.wikipedia.org/wiki/Tegra_3 "wikilink") SoC也採用類似IKS切換方式，但Tegra 3上採用的是相同的CPU核心，多個主CPU核心與一個副CPU核心的設計。

### 異質多處理機（全域任務排程）

[Global_Task_Scheduling.jpg](https://zh.wikipedia.org/wiki/File:Global_Task_Scheduling.jpg "fig:Global_Task_Scheduling.jpg") 異質多處理（heterogeneous multi-processing，HMP）是big.LITTLE組態中最靈活也是效能最強勁的使用模式，在這種組態中，同一時間點上所有的物理CPU核心都是可用的並且可以同時全部開啟使用，也可以將高效能CPU核心全數關閉而只使用低功耗CPU核心。高優先級或者對運算速度吃重的執行緒可以被分派至高效能CPU核心上，而低優先級或對運算速度要求不高的執行緒（如背景任務），則是由低功耗CPU核心負責完成\[11\]\[12\]

最早的實作是三星電子的Exynos Octa 5420/5422/5430。\[13\]\[14\]而現時大部分實現big.LITTLE組態的ARM架構相容處理器，多採用這種切換方式。迫於行動裝置對CPU核心規模的控制，蘋果公司的[Apple A11也採用此種排程方式](https://zh.wikipedia.org/wiki/Apple_A11 "wikilink")。\[15\]

全域任務排程的優勢：

  - 對各個CPU核心有更細粒度的工作量控制。因為作業系統排程器直接對各個CPU核心分配及搬移任務、降低作業系統內核態的額外開銷而令節電效果和效能相應地獲得提升
  - 相比內核內建切換器（IKS）依賴cpufreq框架來實現，直接使用任務排程器來實現CPU核心的切換來得快，而且更容易實現
  - 更靈活的CPU叢集組合（像是兩個Cortex-A15和四個Cortex A7組成的SoC CPU部分）
  - 相比固定只能使用虛擬核心數量的CPU核心數，如有需要，可以實現SoC內所有的CPU核心一同運作以最大限度發揮SoC的運算效能

## 任務排程

對於大小CPU核心（叢集）成對配置的，它們之間的切換過程對作業系統來說是透明的，[作業系統使用現成的動態電壓與時鐘信號調整](https://zh.wikipedia.org/wiki/作業系統 "wikilink")（DVFS）功能來實現。作業系統核心現成的DVFS支援（像是[Linux](../Page/Linux.md "wikilink")核心的`cpufreq`）將根據負載輕重，從預先設定的一個時鐘信號-核心電壓參數配置表中以合適的參數設定CPU的電壓與時脈，和此前僅需調整核心電壓、時脈的CPU一樣，然而，較低的參數設定則會開啟節電（小）CPU核心，而較高的參數設定則是開啟高效能（大）CPU核心。

另一種相對的，則是所有的CPU核心都呈現給作業系統內核排程器，排程器將依據請求決定由哪個核心執行哪個行程或執行緒。這種排程方式需要非成對配置的CPU核心（叢集），不過成對配置的CPU核心（叢集）也可能允許使用。不過這種排程方式更考驗作業系統內核排程器的調校功力（多核心處理器的效能最佳化），至少當前大多數的硬體中，多核心處理器的結構使用的是[對稱多處理器系統](https://zh.wikipedia.org/wiki/对称多处理 "wikilink")，big.LITTLE組態其實也不例外。

## 參見

  -
  -
  -
  -
  -
  -
  -
## 參考資料

## 外部連結

  - [big.LITTLE Processing](https://web.archive.org/web/20121022055646/http://www.arm.com/products/processors/technologies/bigLITTLEprocessing.php)
  - [Big.LITTLE Processing with ARM CortexTM-A15 & Cortex-A7](https://web.archive.org/web/20131017064722/http://www.arm.com/files/downloads/big_LITTLE_Final_Final.pdf) (PDF)

[Category:ARM架構](https://zh.wikipedia.org/wiki/Category:ARM架構 "wikilink")

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
11. [A Survey Of Techniques for Architecting and Managing Asymmetric Multicore Processors](https://www.academia.edu/18301534/A_Survey_Of_Techniques_for_Architecting_and_Managing_Asymmetric_Multicore_Processors), ACM Computing Surveys, 2015.
12.
13.
14.
15.