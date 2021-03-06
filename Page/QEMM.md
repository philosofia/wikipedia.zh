> 本文内容由[QEMM](https://zh.wikipedia.org/wiki/QEMM)转换而来。


**Quarterdeck擴充記憶體管理器**（Quarterdeck Expanded Memory Manager，簡稱 QEMM），是由[Quarterdeck公司於](https://zh.wikipedia.org/wiki/Quarterdeck公司 "wikilink")1980年代末期至1990年代末期所發展的一套記憶體管理軟體。在當時，這是[MS-DOS](../Page/MS-DOS.md "wikilink")和其他[DOS](../Page/DOS.md "wikilink")[作業系統最流行的](https://zh.wikipedia.org/wiki/作業系統 "wikilink")[記憶體管理](../Page/記憶體管理.md "wikilink")軟體。

## 概述

QEMM可以存取[上層記憶區](https://zh.wikipedia.org/wiki/上層記憶區 "wikilink")（UMA 或 UMBs）、[擴展記憶體](../Page/擴展記憶體.md "wikilink")（EMS）、[延伸記憶體](https://zh.wikipedia.org/wiki/延伸記憶體 "wikilink")（XMS）。因為大部分的[DOS](../Page/DOS.md "wikilink")程式需要大量的傳統記憶體，QEMM可以把一些程式載入到上述記憶體區域，因而增加傳統記憶體的自由空間。當時許多軟體，例如[Lotus 1-2-3](../Page/Lotus_1-2-3.md "wikilink")、[Microsoft Windows及一些遊戲軟體](https://zh.wikipedia.org/wiki/Microsoft_Windows "wikilink")，都有使用EMS、XMS。

## 歷史

它本來叫做QEMM-386。[微軟在MS](https://zh.wikipedia.org/wiki/微軟 "wikilink")-DOS 4.01加入了HIMEM.SYS for XMS, EMM386.EXE for EMS。較早的 Windows/386 2.1也包含內建EMM提供Windows內的DOS視窗所需的EMS。但這個版本並沒有造出Upper Memory Blocks.

1991年發行的MS-DOS 5.0終於提供了UMBs。MS-DOS的EMM386一定要HIMEM先被載入，但是另一品牌的作業系統[DR-DOS](../Page/DR-DOS.md "wikilink")卻不用。MS與DR的DOS都要上層記憶區被手動找到並載入，而且MS-DOS需要使用者預先定好多少記憶體要給EMS，多少記憶體要給XMS；然而功能強大的QEMM都不用以上這些額外步驟。

雖然QEMM功能較好，但是仍不敵微軟搭配MS-DOS出售的自行開發軟體，如MS-DOS 6的Memmaker程式。它的最後一版是QEMM 97，可以相容Windows 95/98/ME， 但技術已經不太一樣。[Windows 3.0與其後來版本加入了](https://zh.wikipedia.org/wiki/Windows_3.0 "wikilink")386增強模式，要求關閉所有的記憶體管理軟體。由於同一時間不可能有多個保護模式核心，而事實上，QEMM是叫Windows 載入特定的VxD週邊驅動程式，取代 Windows原本的功能，那就是WINHIRAM.VXD、WINSTLTH.VXD。

[Category:DOS軟體](https://zh.wikipedia.org/wiki/Category:DOS軟體 "wikilink") [Category:DOS内存管理](https://zh.wikipedia.org/wiki/Category:DOS内存管理 "wikilink")