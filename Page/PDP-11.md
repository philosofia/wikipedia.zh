> 本文内容由[PDP-11](https://zh.wikipedia.org/wiki/PDP-11)转换而来。


[Pdp-11-40.jpg](https://zh.wikipedia.org/wiki/File:Pdp-11-40.jpg "fig:Pdp-11-40.jpg")\]\]

**PDP-11**為[迪吉多](../Page/迪吉多.md "wikilink")電腦於1970到1980年代所銷售的一系列[16位元](https://zh.wikipedia.org/wiki/16位元 "wikilink")[迷你電腦](../Page/小型计算机.md "wikilink")。PDP-11是迪吉多電腦的[PDP-8系列的後續機種](https://zh.wikipedia.org/wiki/PDP-8 "wikilink")。PDP-11有著許多創新的特色，而且比起其前代機種更容易撰寫[程式](https://zh.wikipedia.org/wiki/程式 "wikilink")。當[32位元](../Page/32位元.md "wikilink")的後續擴充機型[VAX](../Page/VAX.md "wikilink")-11推出時，PDP-11已經廣受[程式設計師的喜愛](https://zh.wikipedia.org/wiki/程式設計師 "wikilink")。這兩個機型後續的[市場](https://zh.wikipedia.org/wiki/市場 "wikilink")，則多由[IBM PC](../Page/IBM_PC.md "wikilink")、[蘋果二號與](../Page/Apple_II.md "wikilink")[昇陽電腦](../Page/昇陽電腦.md "wikilink")的[工作站](../Page/工作站.md "wikilink")電腦等[個人電腦所取代](https://zh.wikipedia.org/wiki/個人電腦 "wikilink")。

## PDP-11系列的特色

### 指令集

PDP-11深受程式設計師喜愛的原因，主要是在於其高度[正規化指令集的設計](https://zh.wikipedia.org/wiki/正規化指令集 "wikilink")，使得程式設計師可以容易地分別記住所有的運算碼，以及指定[運算子的方法](https://zh.wikipedia.org/wiki/運算子 "wikilink")。如此一來，給定運算子的方法（或稱之為[定址模式](https://zh.wikipedia.org/wiki/定址模式 "wikilink")）便可以很容易地預測，這樣子就不用去背一堆例外條件，或是特別受限的定址方式。

PDP-11所使用的指令集結構影響了[C語言的語法](https://zh.wikipedia.org/wiki/C語言 "wikilink")。例如在c語言中，有著暫存器定址模式的增值與減值語法 *++i*與*i--*。如果*i*與*j*都是暫存器變數，那麼*\*(--i) = \*(j++)*這樣子的表示式就可以編譯為單一機器碼指令。由於對單精確與雙精確浮點數沒有不同的運算碼，也造成C語言中缺乏單精確浮點數運算的運算模式。

就某種邏輯來看，指令集中的定址模式可以視為一種"基底"，而指令集中的運算碼則為另一個基底。每個雙引數指令可以分為兩個6位元的引數識別（分別包含了一個3位元的暫存器號碼，和一個3位元的定址模式碼）與一個4位元的[運算碼](https://zh.wikipedia.org/wiki/運算碼 "wikilink")。而單引數指令，則有一個6位元的引數識別和一個10位元的運算碼。所有的運算碼都可以使用任何的定址模式，雙引數指令還可以分別組合使用。在八個暫存器（編號0到7）當中，有七個是一般用途的T暫存器可作為平常運算使用，不過暫存器6則是某些指令下作為硬體識別[堆疊](https://zh.wikipedia.org/wiki/堆疊 "wikilink")[指標之用](https://zh.wikipedia.org/wiki/指標 "wikilink")。暫存器7則是[程式計數器](../Page/程式計數器.md "wikilink")，是處理器執行程式碼的位址標記。這項創新與一些定址模式，提供了暫存器內容定址，絕對位址定址與相對位址定址。

16位元字元組是以[小端序即低位元在前的方式儲存的](https://zh.wikipedia.org/wiki/字节序#小端序 "wikilink")。而32位元字元組則通常是以一種不常見的[混合序格式儲存](https://zh.wikipedia.org/wiki/字节序#混合序 "wikilink")。由於PDP-11的風行，這種格式也被引用為*pdp-資料次序*（PDP-endian）。

### 無專用的輸出入埠

PDP-11與其他早期電腦最大的差異點，在於沒有專用的[輸出入](https://zh.wikipedia.org/wiki/I/O "wikilink")[匯流排](../Page/总线.md "wikilink")。PDP-11-{只}-有一個稱作為[Unibus的記憶體匯流排](https://zh.wikipedia.org/wiki/Unibus "wikilink")。所有外部的設備，都分別對應到不同的記憶體位址，所以不需要特殊的I/O指令。而其[中斷](../Page/中斷.md "wikilink")系統的設計，也刻意的簡單化，以確保沒有任何的中斷程序會被遺漏。外部的設備可以從單一的輸入線到四條優先度線路之一，發出中斷要求。而處理器可以從[階層式的接受線路來回應中斷要求](https://zh.wikipedia.org/wiki/階層式 "wikilink")。（階層式的架構，是由一系列的[邏輯閘](../Page/邏輯閘.md "wikilink")所構成，來接受一系列按照優先順序的事件。就一般來說，第一個邏輯閘的要求會優先被接受。而階層式的要求，是按照設備的優先度來處理的。）

而就PDP-11的設計來說，這代表中斷要求被接受的順序，是根據實際上硬體在匯流排上與處理器的接近程度來決定的。當處理器回應的時候，外部設備會將其向量位址放在匯流排上，這是一個4位元的記憶體。之後處理器會從向量位置表讀取到[状态寄存器與](https://zh.wikipedia.org/wiki/状态寄存器 "wikilink")[程式計數器](../Page/程式計數器.md "wikilink")。 而新的狀態暫存器會暫時取消掉其他的中斷要求，來避免中斷的重複發生。而取出的程式暫存器，則是指向中斷處理程序的起始位址。中斷處理程序將會先處裡這個硬體的要求，完成後再重新接受其他的中斷要求。最後，一個特別的RTI程序（自中斷回復）會將處理器回復到發生中斷之前的狀態。（這也可能是一個優先權較低的中斷處理程序）一個值得注意的是，處理器會避免遺漏掉中斷要求，假使中斷沒有被回應，將仍然會被保留著到之後循環。假使程序不正常的啟動了，處理器會發生一個特別的逾時錯誤，使用者將會得知這個硬體的錯誤。

### 為大量生產而設計

最後，由於PDP-11的設計，只需要半專業的人員來進行生產組裝。產品在尺寸精確上的要求，並不是非常要緊的。PDP-11的[背版使用](https://zh.wikipedia.org/wiki/背版 "wikilink")[繞線連接的方式](https://zh.wikipedia.org/wiki/繞線連接 "wikilink")，也就是內部的[印刷電路板插入背版上的接頭](https://zh.wikipedia.org/wiki/印刷電路板 "wikilink")。這個接頭上的端子以導線纏繞於上的方式來連接，端子可以切開導線的絕緣層，與導線金屬的部份形成氣密連接。這種類似型式的接頭也可於[電信模組上見到](https://zh.wikipedia.org/wiki/電信模組 "wikilink")。

## LSI-11

LSI-11是第一個使用[大型積體電路技術製造的PDP](https://zh.wikipedia.org/wiki/大规模集成电路 "wikilink")-11機型。整個處理器包含了四個由[威騰](../Page/威騰電子.md "wikilink")（Western Digital）所製造的[大型積體電路晶片](https://zh.wikipedia.org/wiki/大规模集成电路 "wikilink")。而其匯流排是一個類似Unibus的[Q-Bus](https://zh.wikipedia.org/wiki/Q-Bus "wikilink")，不同點在於位址與資料以多工的方式來共用資料線，而Unibus則是使用分別的線路。而且另一個不同點在於其I/O設備的定址方式，可以容納到22位元寬的實體位址（Unibus只有18位元的寬度），並且有支援阻斷式（block mode）的運作。

處理器的[微碼包含了一個除錯器](https://zh.wikipedia.org/wiki/微碼 "wikilink")，可以經由標準的[RS-232終端機來操作](https://zh.wikipedia.org/wiki/RS-232 "wikilink")。這在當時是一項創舉，因為微碼是計算機最基本的一個部份，也是最關鍵的[控制單元](https://zh.wikipedia.org/wiki/控制單元 "wikilink")。假使無法運作，便稱不上是一個計算機。除錯器提供了一個檢驗處理器中暫存器、記憶體與輸出入設備的方法。因此，只要處理器可以運作，便能夠檢驗與修正計算機的內部狀態。這個內建的除錯器，省卻了昂貴與不方便操作的一大堆在面板上的開關與燈號，那是傳統上唯一能夠與快掛掉的電腦溝通的方式。

其微碼包含了一個通用的[開機啟動程序](https://zh.wikipedia.org/wiki/開機啟動程序 "wikilink")，相容於所有DEC的磁碟設備。

這兩項創新使得LSI-11總是可以開始運作。當其無法從大型磁碟啟動時，會嘗試由其軟碟啟動。而當硬體開始運作後，便可以從熟悉的終端機來使用。

## PDP-11的式微

PDP-11最基本的設計是非常優良的，而且也一直有更新加入新的技術。然而，PDP-11還是必須面對其16位元的架構是有極限的，這是沒有辦法透過校調或是擴充來克服的。雖然有些機型可以支援更大的實體記憶體定址，但所有的應用程式仍然被侷限在一個16位元的[虛擬定址空間而只能夠使用](https://zh.wikipedia.org/wiki/address_space "wikilink")64K的記憶體。當1980年代[超大型積體電路的技術使得](../Page/超大规模集成电路.md "wikilink")[記憶體晶片能夠更便宜](https://zh.wikipedia.org/wiki/記憶體 "wikilink")，但是PDP-11的軟體仍然無法享受到更大的記憶體所帶來的便利。

DEC在PDP-11的下一代處理器為[VAX](../Page/VAX.md "wikilink")（是"Virtual Address Extension (to the PDP-11)"的縮寫）克服了這些問題，但最初只針對高階市場來進行推廣。而英特爾的[8086與](https://zh.wikipedia.org/wiki/8086 "wikilink")[8088提供了一個四位元的擴充](https://zh.wikipedia.org/wiki/8088 "wikilink")"節"在其16位元的定址上，使得定址空間提升到1M而不需要更改為32位元的設計。這對當時逐漸擴充的IBM個人電腦相容機市場來說，已經是足夠的了。雖然在能夠支援更大節定址空間的[80286與擁有](https://zh.wikipedia.org/wiki/80286 "wikilink")32位元定址空間的[80386推出前](https://zh.wikipedia.org/wiki/80386 "wikilink")，就有到達1M的需求。

當工程師轉移到有更大的定址空間的架構時，支援32位元的運算也開始在如[摩托羅拉](https://zh.wikipedia.org/wiki/摩托羅拉 "wikilink")[68000和](https://zh.wikipedia.org/wiki/Motorola_68000 "wikilink")[英特爾](https://zh.wikipedia.org/wiki/英特爾 "wikilink")[80386等後續的](https://zh.wikipedia.org/wiki/80386 "wikilink")[微處理器晶片上提供了](https://zh.wikipedia.org/wiki/微處理器 "wikilink")。最後這些晶片的經濟規模大到一個程度後，PDP-11就相對而言不夠划算。DEC的一個[DEC Professional系列](https://zh.wikipedia.org/wiki/DEC_Professional_\(computer\) "wikilink")，也就因此在市場上失敗了，同時兩個之後的DEC個人電腦系列也面臨相同的命運。

DEC最後在1997年中止了PDP-11的機型，並且把其相關的設計與作業系統授權賣給了一家愛爾蘭公司[Mentec](https://zh.wikipedia.org/wiki/Mentec "wikilink")。這家公司是負責生產LSI-1的Q-Bus機板與個人電腦的ISA架構機板。

到了1990年末，DEC與大部分美國東北部六州（New England）的迷你電腦商，都在UNIX與windows伺服器的興起下，逐漸衰敗。

## 架構細節

以下內容可參考<cite>PDP-11處理器手冊</cite> （詳見Gordon Bell's [1969年版](http://research.microsoft.com/users/GBell/Digital/PDP%2011%20Handbook%201969.pdf)）。

### 通用暫存器的[定址模式](https://zh.wikipedia.org/wiki/定址模式 "wikilink")

（R為通用暫存器，有0至7號；(R)為暫存器的內容）

  -
    0.暫存器 - 數值來自或存入暫存器中：OPR R ; R含有參數
    1.暫存器指定位址 - 暫存器用來指定讀寫的記憶體位址：OPR (R) ; R存有位址
    2.自動增值：OPR (R)+ ; R記憶體位址上的數值增加（R）
    3.自動增值指定位址：OPR @(R)+ ; R存有位址，其內容 (R)加2
    4.自動減值：OPR -（R）；記憶體位址R上的數值 (R)減少
    5.自動減值指定位址：OPR @-（R）；記憶體位址R上的數值 (R)減2
    6.索引：OPR X(R) ; (R)+X為記憶體位址，在指令的第二字元
    7.索引指定位址：OPR @X(R) ; (R)+X為指令的第二字元記憶體位址的位址

### 程式計數器的[定址模式](https://zh.wikipedia.org/wiki/定址模式 "wikilink")

程式計數器（program counter，簡稱PC）亦可以用來作為一般暫存器使用，因此有以下的定址模式，可參照前面的通用暫存器：

  -
    2.直接定值：OPR \#N；引數包含在指令中
    3.絕對位址：OPR @\#A；絕對位址包含在指令中
    6.相對定址：OPR A ; PC+2+X為記憶體位址。PC+2為更新後的PC
    7.相對參考定址：OPR @A ; PC+2+X為記憶體位址。PC+2為更新後的PC

### PDP-11指令

  - 單引數指令 - 指令的長度為雙字元組，一部分用來指定動作，稱之為"運算碼"（OP-Code）或"運算元"。而第二部份則用來指定引數（運算子）的位址。

|     |    |     |  |  |  |  |  |  |   |   |  |   |   |  |   |
| --- | -- | --- |  |  |  |  |  |  | - | - |  | - | - |  | - |
| 15  |    |     |  |  |  |  |  |  | 6 | 5 |  | 3 | 2 |  | 0 |
| 運算碼 | 模式 | 暫存器 |  |  |  |  |  |  |   |   |  |   |   |  |   |

  -   - CLR（清除）, COM（取一的補數）, INC（增值）, DEC（減值）, NEG（取二的補數之負數）, TST（測試）, ASR（數學位元右移）, ASL（數學位元左移）, ROR（向右位元轉動）, ROL（向左位元轉動）, SWAB（字元置換）, ADC（加法進位）, SBC（減法進位）, SXT（擴張正負號）。

  - 雙引數指令 - 指令雙字元組的一部分用來指定動作，而其餘的部份則用來指定兩個引數的位址。

|     |    |     |    |     |  |   |   |  |   |   |  |   |   |  |   |
| --- | -- | --- | -- | --- |  | - | - |  | - | - |  | - | - |  | - |
| 15  |    |     | 12 | 11  |  | 9 | 8 |  | 6 | 5 |  | 3 | 2 |  | 0 |
| 運算碼 | 模式 | 暫存器 | 模式 | 暫存器 |  |   |   |  |   |   |  |   |   |  |   |

  -   - MOV（資料搬移）, ADD, SUB（加減法）, BIT（位元測試）, BIC（位元清除）, BIS（改動位元）, XOR（互斥或運算）。

  - 程式控制指令 - 指令雙字元組的第一部分用來指定動作，而第二部份則用來指定要執行的程式碼位址。

|     |     |  |  |  |  |  |   |   |  |  |  |  |  |  |   |
| --- | --- |  |  |  |  |  | - | - |  |  |  |  |  |  | - |
| 15  |     |  |  |  |  |  | 8 | 7 |  |  |  |  |  |  | 0 |
| 運算碼 | 位移值 |  |  |  |  |  |   |   |  |  |  |  |  |  |   |

  -   - BR（無條件分支）, BNE（非零值時分支）, BEQ（數值為零時分支）, BPL（正數時分支）, BMI（負數值時分支）, BVC（溢位清除時分支）, BVS（發生溢位時分支）, BCC（進位清除時分支）, BCS（發生進位時分支）。
      - BLE（分支if \<= 0）, BGE（分支if \>= 0）, BLT（分支if \< 0）, BGT（分支if \> 0，正負號比較）
      - BLO（小於時分支）, BHI（大於時分支）, BLOS（小於或等於時分支）, BHIS（大於或等於時分支，無正負號比較）
      - SOB（暫存器減一後為零時分支）。

  - 跳躍與子程序指令

      - JMP（跳躍）, JSR（跳入副程式）, RTS（自副程式跳回主程式）
      - EMT（模擬器錯誤時觸發）, TRAP, BPT（中斷點觸發）, IOT（輸出入錯誤時觸發）, RTI & RTT（自副程式跳回時觸發）

  - 其他指令

<!-- end list -->

  -   - HALT, WAIT（等候中斷觸發）, RESET（重置UNIBUS）, MTPD（移至前一個資料空間）, MTPI（移至前一個指令空間）, MFPD（移自前一個資料空間）, MFPI（移自前一個指令空間）, MTPS（移至處理器狀態字元組）, MFPS（移自處理器狀態字元組）

<!-- end list -->

  - 條件碼操作
      - CLC, CLV, CLZ, CLN, CCC（清除相關的條件碼）, SEC, SEV, SEZ, SEN, SCC（設定相關的條件碼）
      - 處理器狀態字元組（processor status word - 簡稱PSW）的狀態碼共有四種：
          - N負數
          - Z零值
          - V溢位
          - C進位

<!-- end list -->

  - "擴充指令集"（EIS），在11/35/40和11/03為選購，在更新的處理器則為內建功能
      - MUL, DIV暫存器組的整數相乘與相除
      - ASH, ASHC算數位元位移暫存器或暫存器組，正數位移向左，負數向右

<!-- end list -->

  - "浮點數指令集"（FIS），在11/35/40和11/03為選購
      - FADD, FSUB, FMUL, FDIV堆疊位址上的單精數運算，由暫存器定址
  - "浮點數處理器"（FPP），在11/45和大部分該系列的機種為選購
      - 完整的浮點數運算，包含單精數與倍精數運算子，以浮點狀態暫存器指定精確度
      - 單精浮點數運算的資料格式為IEEE 754格式的基礎：正負位元，8位元指數，23位元底數與第24位隱藏用

<!-- end list -->

  - 商用指令集 (CIS), 11/23/24為選購微碼，11/44為附加模組與11/74的其中一版
      - 支援[COBOL](../Page/COBOL.md "wikilink")與[Dibol的多種字串與十進位數相關指令](https://zh.wikipedia.org/wiki/Dibol "wikilink")

## 組合語言範例

[Papertape.jpg](https://zh.wikipedia.org/wiki/File:Papertape.jpg "fig:Papertape.jpg")\]\]

以下是一個完整的"[Hello, world\!](https://zh.wikipedia.org/wiki/Hello_world_program "wikilink")"巨集組合語言程式，可以在組譯後於[RT-11執行](https://zh.wikipedia.org/wiki/RT-11 "wikilink")：

.TITLE HELLO WORLD .MCALL .TTYOUT,.EXIT HELLO:: MOV \#MSG,R1；字串起始位址 1$: MOVB (R1)+,R0；迴圈取得下一個字元 BEQ DONE；遇到字串結尾跳出 .TTYOUT；輸出至TTY BR 1$；迴圈結尾 DONE: .EXIT

MSG: .ASCIZ /Hello, world\!/ .END HELLO

假設檔名為`HELLO.MAC`，RT-11的組譯，連結與執行的指令為：

.MACRO HELLO ERRORS DETECTED: 0

.LINK HELLO

.R HELLO Hello, world\! .

（RT-11的命令提示字元為"`.`"）而更複雜的MACRO-11程式，以下是兩個隨意選自Kevin Murrell's [KPUN.MAC](http://www.ps8computing.co.uk/PDP11/kpun_mac.htm)與Farba Research's [JULIAN](https://web.archive.org/web/20080905182149/http://www.farbaresearch.com/examples/julian.htm)程式。更進階的PDP-11函式庫程式碼可免費從[Metalab](http://www.ibiblio.org/pub/academic/computer-science/history/pdp-11/)和[Trailing Edge](http://pdp-11.trailing-edge.com/)來查閱。

這些程式也可以在PDP-11模擬器上運行。[Bob Supnik所寫的名為](https://zh.wikipedia.org/wiki/Bob_Supnik "wikilink")[SIMH模擬器](https://zh.wikipedia.org/wiki/SIMH "wikilink")，可以優秀地模擬PDP-11與許多其他的架構，同時包含了軟體套件與原生作業系統（包含RT-11）。

## PDP-11的機種

PDP-11處理器依據其原始設計，以及I/O匯流排的種類，可以歸類為以下幾種系列。在這些類別當中，大部份都有兩種以上的版本，其中一種為[OEM代工的機型](https://zh.wikipedia.org/wiki/OEM "wikilink")，另一種則是提供給最終使用者。

### Unibus的機種

[PDP-11-70-DDS570.jpg](https://zh.wikipedia.org/wiki/File:PDP-11-70-DDS570.jpg "fig:PDP-11-70-DDS570.jpg") 下列機種使用[Unibus作為其擴充匯流排](https://zh.wikipedia.org/wiki/Unibus "wikilink")：

  - PDP-11（後稱為PDP-11/20）和[PDP-11/15](https://zh.wikipedia.org/wiki/PDP-11/15 "wikilink") -- 原始，無微程式的處理器，由Jim O'Loughlin所設計。
  - [PDP-11/35和](https://zh.wikipedia.org/wiki/PDP-11/35 "wikilink")[11/40](https://zh.wikipedia.org/wiki/11/40 "wikilink") -- 微程式化的／20後續機型，由Jim O'Loughlin所帶領的團隊設計的。
  - [PDP-11/45](https://zh.wikipedia.org/wiki/PDP-11/45 "wikilink")，[11/50](https://zh.wikipedia.org/wiki/11/50 "wikilink")，和[11/55](https://zh.wikipedia.org/wiki/11/55 "wikilink") -- 更快的微程式化的處理器，並且可以使用半導體記憶體或是[核心記憶體](https://zh.wikipedia.org/wiki/核心記憶體 "wikilink")。
  - [PDP-11/70](https://zh.wikipedia.org/wiki/PDP-11/70 "wikilink") -- 11/45的擴充機型，經由獨立記憶體匯流排支援4 [MB實體記憶體與](https://zh.wikipedia.org/wiki/megabyte "wikilink")2 [KB快取記憶體](https://zh.wikipedia.org/wiki/kilobyte "wikilink")，並藉由[Massbus提供更快的I](https://zh.wikipedia.org/wiki/Massbus "wikilink")/O設備連結。
  - [PDP-11/05和](https://zh.wikipedia.org/wiki/PDP-11/05 "wikilink")[11/10](https://zh.wikipedia.org/wiki/11/10 "wikilink") -- 11/20的精減版。
  - [PDP-11/34和](https://zh.wikipedia.org/wiki/PDP-11/34 "wikilink")[11/04](https://zh.wikipedia.org/wiki/11/04 "wikilink") -- 11/35和11/05的後續精減版。PDP-11/09和11/39機型只有DEC內部文件記載，並沒有生產銷售。PDP-11/34的概念是由Bob Armstrong提出的。
  - [PDP-11/44](https://zh.wikipedia.org/wiki/PDP-11/44 "wikilink") -- 11/34的擴充型，增加了[快取記憶體和](https://zh.wikipedia.org/wiki/快取記憶體 "wikilink") [浮點運算單元為標準功能](https://zh.wikipedia.org/wiki/浮點 "wikilink")。這一型並有一個特別的序列埠終端且支援4 MB實體記憶體。設計團隊由John Sofio所帶領。
  - [PDP-11/60](https://zh.wikipedia.org/wiki/PDP-11/60 "wikilink") -- 有使用者可程式化微控制碼的PDP-11，這是由Jim O'Loughlin所帶領的另一組團隊所設計的。
  - [PDP-11/24](https://zh.wikipedia.org/wiki/PDP-11/24 "wikilink") - 最早使用超大形積體電路PDP-11和Unibus，使用"Fonz-11" (F11)晶片組
  - [PDP-11/84](https://zh.wikipedia.org/wiki/PDP-11/84 "wikilink") - 使用超大形積體電路"Jaws-11" (J11)晶片組
  - [PDP-11/94](https://zh.wikipedia.org/wiki/PDP-11/94 "wikilink") - J11為基礎，比11/84更快

### Q-Bus的機種

下列機種使用[Q-Bus作為其擴充匯流排](https://zh.wikipedia.org/wiki/Q-Bus "wikilink")：

  - [PDP-11/03](https://zh.wikipedia.org/wiki/PDP-11/03 "wikilink")（也稱為LSI-11/03）-- 第一個[大型積體電路](https://zh.wikipedia.org/wiki/大规模集成电路 "wikilink")（LSI）技術的PDP-11，使用威騰（[Western Digital](https://zh.wikipedia.org/wiki/Western_Digital "wikilink")）生產的晶片組。

<!-- end list -->

  - [PDP-11/23](https://zh.wikipedia.org/wiki/PDP-11/23 "wikilink") -- 第二代大型積體電路（F-11），早期只支援248KB記憶體，但可以修改支援到4MB記憶體。
  - [PDP-11/23+](https://zh.wikipedia.org/wiki/PDP-11/23+ "wikilink")／MicroPDP-11/23 -- 11/23改良版，在處理器卡上提供更多功能（實際上為四倍大小）

<!-- end list -->

  - [MicroPDP-11/73](https://zh.wikipedia.org/wiki/PDP-11/73 "wikilink") -- 第二代大型積體電路PDP，這個系統使用"Jaws-11" (J-11)晶片組。

<!-- end list -->

  - [MicroPDP-11/53](https://zh.wikipedia.org/wiki/MicroPDP-11/53 "wikilink") -- 較慢的11/73有內建記憶體

<!-- end list -->

  - [MicroPDP-11/83](https://zh.wikipedia.org/wiki/MicroPDP-11/83 "wikilink") -- 更快的11/73有內部記憶體連結（PMI）

<!-- end list -->

  - [MicroPDP-11/93](https://zh.wikipedia.org/wiki/MicroPDP-11/93 "wikilink") -- 更快的11/83，最終DEC Q-Bus PDP-11機型。

<!-- end list -->

  - [Mentec M100](https://zh.wikipedia.org/wiki/Mentec_M100 "wikilink") -- Mentec重新設計的11/93，使用J-11晶片組時脈為19.66MHz，含4個內建序列埠，1-4MB內建記憶體，FPU為選購。

<!-- end list -->

  - [Mentec M11](https://zh.wikipedia.org/wiki/Mentec_M11 "wikilink") -- 處理器升級子板，最後的微碼PDP-11架構，指令集是由Mentec設計的。使用TI 8832 ALU和德州儀器[Texas Instruments製造的TI](https://zh.wikipedia.org/wiki/Texas_Instruments "wikilink") 8818微序列器。

<!-- end list -->

  - [Quickware QED-993](https://zh.wikipedia.org/wiki/Quickware_QED-993 "wikilink") -- 高性能PDP-11/93處理器升級子板

### 無匯流排的機種

  - PDT-11/110
  - PDT-11/130
  - PDT-11/150

PDT為桌上型系統，以"智慧型終端機"來銷售。其中／110與／130使用[VT100終端機模式](https://zh.wikipedia.org/wiki/VT100 "wikilink")。

  - PRO-325
  - PRO-350
  - PRO-380

[DEC Professional系列為桌上型個人電腦](https://zh.wikipedia.org/wiki/DEC_Professional_\(computer\) "wikilink")，作為對抗IBM早期基於8088與80286個人電腦的競爭機種。這些機型配備有5 1/4"軟碟機與硬碟機，而325則是沒有配備硬碟的機型。中央處理器為LSI-11產品線，以P/OS為作業系統，這是以[RSX-11M+為基礎的選單式系統](https://zh.wikipedia.org/wiki/RSX-11 "wikilink")。由於設計上刻意避免與PDP-11機種的軟體相容性，其市場上最後失敗的命運並不令人意外。

### 計劃中但未上市機種

  - [PDP-11/27](https://zh.wikipedia.org/wiki/PDP-11/27 "wikilink") -- Jaws-11機型的實作，計劃採用[VAXBI Bus作為I](https://zh.wikipedia.org/wiki/VAXBI_Bus "wikilink")/O匯流排。

<!-- end list -->

  - [PDP-11/68](https://zh.wikipedia.org/wiki/PDP-11/68 "wikilink") -- PDP-11/60的後續機型，支援4 [MB的實體記憶體](https://zh.wikipedia.org/wiki/MB "wikilink")。

<!-- end list -->

  - [PDP-11/74](https://zh.wikipedia.org/wiki/PDP-11/74 "wikilink") -- PDP-11/70擴充為多處理器的機型。最多可以使用四顆處理器，但是電纜線也會因此多到難以管理。另一個11/74的變形則是可以支援多處理器與內建商用指令集。有相當數量的11/74原型機（包含數種不同的子機型）生產出來以及至少二路的多處理器系統提供給客戶作為外部測試（beta test）使用。但是實際上自始至終這個機型都沒有正式的進行銷售過。一套四路的多處理器系統由RSX-11作業系統的開發團隊所維護，作為測試使用。而一套單處理器的版本則作為PDP-11工程一般時程分割之用。11/74之所以沒有上市，主要是由於剛好與新的32位元產品與VAX 11/780這個第一個VAX機型的上市撞期。謠言流傳與[陰謀論者](http://www.miim.com/faq/hardware/multipro.html)認為11/74被取消的原因，是由於其效能相較於11/780系列要來得更佳：鑑於行銷的考量，推出效能更好的的PDP-11機型將會影響並減緩客戶轉移到新的VAX機型的速度。然而，在該領域中維護產品的能力才是主要的原因。要說是陰謀論也好，DEC始終無法成功地將其所有的客戶從PDP-11轉移到VAX系列，這個主要的原因不是在於效能好壞，而是在於PDP-11優良的即時回應能力。

### 特殊用途版本

[GT40_Lunar_Lander.jpg](https://zh.wikipedia.org/wiki/File:GT40_Lunar_Lander.jpg "fig:GT40_Lunar_Lander.jpg")

  - GT40 -- 使用PDP-11/05的向量圖形終端機
  - [GT44](https://zh.wikipedia.org/wiki/GT44 "wikilink") -- 使用PDP-11/40的向量圖形終端機
  - [H-11](https://zh.wikipedia.org/wiki/H-11 "wikilink") -- [Heathkit代製版的LSI](https://zh.wikipedia.org/wiki/Heathkit "wikilink")-11/03
  - [VT103](https://zh.wikipedia.org/wiki/VT103 "wikilink") -- VT100使用LSI-11背版
  - VT173 -- 使用PDP-11/03的頂級終端機系列
  - [MINC-11](https://zh.wikipedia.org/wiki/MINC-11 "wikilink") -- 使用PDP-11/03或11/23的實驗室系統
  - [C.mmp](https://zh.wikipedia.org/wiki/C.mmp "wikilink") -- 來自[卡內基美隆大學的多處理器系統](https://zh.wikipedia.org/wiki/卡內基美隆大學 "wikilink")

### 海盜版相容機

由於PDP-11相當風行的緣故，在当时遭受禁運的[东欧](../Page/东欧.md "wikilink")[社会主义](../Page/社会主义.md "wikilink")國家有許多未經授權的相容機被生產出來。有些甚至與DEC的PDP-11各系列接腳相容，而可以與原廠產品共用週邊設備與軟體。這些包含了：

  - [SM-4](https://zh.wikipedia.org/wiki/SM-4 "wikilink")，[SM-1420](https://zh.wikipedia.org/wiki/SM-1420 "wikilink")，[SM-1600](https://zh.wikipedia.org/wiki/SM-1600 "wikilink")，[Electronics BK-0010](https://zh.wikipedia.org/wiki/Electronics_BK-0010 "wikilink")，[DVK](https://zh.wikipedia.org/wiki/DVK "wikilink")，[UKNC](https://zh.wikipedia.org/wiki/UKNC "wikilink")（[蘇聯](https://zh.wikipedia.org/wiki/蘇聯 "wikilink")）
  - [SM-4](https://zh.wikipedia.org/wiki/SM-4 "wikilink")，[SM-1420](https://zh.wikipedia.org/wiki/SM-1420 "wikilink")，[IZOT-1016與週邊設備](https://zh.wikipedia.org/wiki/IZOT-1016 "wikilink")（[保加利亞](https://zh.wikipedia.org/wiki/保加利亞 "wikilink")）。
  - [SM-1420](https://zh.wikipedia.org/wiki/SM-1420 "wikilink")（[東德](../Page/東德.md "wikilink")）
  - [Mera](../Page/Mera.md "wikilink")（[波蘭](https://zh.wikipedia.org/wiki/波蘭 "wikilink")）
  - [SM-4](https://zh.wikipedia.org/wiki/SM-4 "wikilink")（[匈牙利](../Page/匈牙利.md "wikilink")）
  - 獨立設備（[羅馬尼亞](../Page/羅馬尼亞.md "wikilink")）

## 作業系統

PDP-11有數種可用的[作業系統](https://zh.wikipedia.org/wiki/作業系統 "wikilink")

迪吉多電腦：

  - DOS/BATCH
  - [IAS](https://zh.wikipedia.org/wiki/RSX-11 "wikilink")
  - [P/OS](https://zh.wikipedia.org/wiki/RSX-11 "wikilink")
  - [RSX-11](https://zh.wikipedia.org/wiki/RSX-11 "wikilink")
  - CAPS-11
  - [RT-11](https://zh.wikipedia.org/wiki/RT-11 "wikilink")
  - [RSTS/E](https://zh.wikipedia.org/wiki/RSTS/E "wikilink")
  - [Ultrix](https://zh.wikipedia.org/wiki/Ultrix "wikilink")-11

協力廠商：

  - [ANDOS](https://zh.wikipedia.org/wiki/ANDOS "wikilink")
  - [MKDOS](https://zh.wikipedia.org/wiki/MKDOS "wikilink")
  - [MONECS](https://zh.wikipedia.org/wiki/MONECS "wikilink")
  - [CSIDOS](https://zh.wikipedia.org/wiki/CSIDOS "wikilink")
  - [TRIPOS](https://zh.wikipedia.org/wiki/TRIPOS "wikilink")
  - [MUMPS](https://zh.wikipedia.org/wiki/MUMPS "wikilink")
  - [Unix](https://zh.wikipedia.org/wiki/Unix "wikilink")（有許多版本，包含[Version 7 Unix與](https://zh.wikipedia.org/wiki/Version_7_Unix "wikilink")[2BSD](https://zh.wikipedia.org/wiki/Berkeley_Software_Distribution "wikilink")）
      - [DEMOS](https://zh.wikipedia.org/wiki/DEMOS "wikilink")（[蘇聯](https://zh.wikipedia.org/wiki/蘇聯 "wikilink")）
  - [TSX-Plus](https://zh.wikipedia.org/wiki/TSX-Plus "wikilink")

## 外部連結

  - [PDP-11的FAQ](https://web.archive.org/web/20110514104628/http://www.village.org/pdp11/faq.html)
  - [保留PDP-11系列的16位元迷你電腦](http://www.pdp11.org)
  - [另一個PDP-11愛好者網站](http://www.psych.usyd.edu.au/pdp-11/)
  - [俄國PDP-11相容機](http://www.pdp11.org.ru/)（俄語網站）。
  - [蘇聯計算機歷史博物館](https://web.archive.org/web/20060830200334/http://www.bashedu.ru/konkurs/tarhov/english/index_e.htm)
  - [Gordon Bell與Bill](https://zh.wikipedia.org/wiki/Gordon_Bell "wikilink") Strecker於1975年發表的論文：[我們從PDP-11學到了什麼](http://research.microsoft.com/users/GBell/Digital/Bell_Strecker_What_we%20_learned_fm_PDP-11c%207511.pdf)
  - [Gordon Bell的網站](http://research.microsoft.com/users/GBell/Digital/DECMuseum.htm)可以找到更多的論文與連結。
  - [PDP-11後端程式](http://www.telegraphics.com.au/sw/info/lcc-pdp11.html)（程式範本產生器）支持可重定位ANSI [Little C編譯器](https://zh.wikipedia.org/wiki/Little_C_compiler "wikilink")
  - [Mentec](https://web.archive.org/web/20060813131029/http://www.mentec-inc.com/)，PDP-11系統軟體目前的所有者（除IAS外）

[Category:迷你電腦](https://zh.wikipedia.org/wiki/Category:迷你電腦 "wikilink") [Category:PDP-11](https://zh.wikipedia.org/wiki/Category:PDP-11 "wikilink")