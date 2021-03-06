> 本文内容由[Whitespace](https://zh.wikipedia.org/wiki/Whitespace)转换而来。


[Whitespace_in_vim2.png](https://zh.wikipedia.org/wiki/File:Whitespace_in_vim2.png "fig:Whitespace_in_vim2.png") **Whitespace**是種[深奥的编程语言](../Page/深奥的编程语言.md "wikilink")。它由Edwin Brady和Chris Morris開發，2003年4月1日發佈。大部分的現代程式設計語言都不將空白字元視為語法的一部分。但Whitespace卻只視[空格](../Page/空格.md "wikilink")（space）、[制表符](https://zh.wikipedia.org/wiki/Tab鍵 "wikilink")（tabs）和[換行](../Page/換行.md "wikilink")（new lines）為語法的一部分，它的直譯器忽略所有非空白字元。

它本身是個[指令式](../Page/指令式編程.md "wikilink")、基於[堆疊的語言](https://zh.wikipedia.org/wiki/堆疊 "wikilink")。其程式運行在上的[虛擬機器](../Page/虛擬機器.md "wikilink")均有一個堆疊（Stack）和[堆](https://zh.wikipedia.org/wiki/堆 "wikilink")（Heap）。程式員可自由將整數推進堆疊中（只可以是整數，因為暫時並無浮點數或實數工具）。使用者亦可通過堆作為變數和資料結構的暫存區。

这种语言有和[Brainfuck](../Page/Brainfuck.md "wikilink")一样的优点，能方便地写程序注释，写的注释根本不需要标识，编译器直接跳过你写的文字信息。还有，借助这种语言，可以在满篇空白的代码中插入一篇文章，从而在看起来完全无关的文章中隐藏一段代码。对于一些需要保证安全性的工作来说，这种语言帮助很大，因为它可以防止别人把代码打印出来拿走。

## 語法

### IMP

IMP ( Instruction Modification Parameter)是whitespace語法中的一種特色，在每個指令前要指名要使用哪種形式的IMP，之後在進行屬於每個IMP裡的不同操作。

| IMP              | 意義   |
| ---------------- | ---- |
| \[Space\]        | 堆疊操作 |
| \[Tab\]\[Space\] | 數學運算 |
| \[Tab\]\[Tab\]   | 堆積存取 |
| \[LF\]           | 流程控制 |
| \[Tab\]\[LF\]    | I/O  |

虛擬機（程式所運行的地點）中有一個堆疊與堆積. 程式設計者可以任意的將整數放入堆疊( 只有整數 ,目前沒有浮點數與實數的實作). 堆積也可以任意且永久的儲存變數或資料結構. 許多命令需要數字或是標籤（label）作為參數. 整數可以為任意長度的位元(bits), 以一系列的空白（Space）與製表符（Tab）表現, 以換行（LF）作為結束. 空白代表數位上的"0",製表符則代表"1".給定的第一個字元代表整數的正負號, 空白為正號而製表符為負號. 要注意兩號並非互補, 只是單純代表正負號. 標籤也是由一系列空白與製表符組成而以\[LF\]作為結尾. 所有標籤必須是獨一無二而不能重複的.

### 堆疊操作 (IMP: \[Space\])

堆疊操作為一常用運算, 所以使用IMP裡面最簡短的\[Space\]. 這裡有四種操作方式.

| 指令               | 參數 | 意義               |
| ---------------- | -- | ---------------- |
| \[Space\]        | 數字 | 將某個數字放入堆疊        |
| \[Tab\]\[Space\] | 數字 | 將堆疊裡的第n個元素複製到堆疊頂 |
| \[Tab\]\[LF\]    | 數字 | 將堆疊裡的第n個元素從堆疊裡移除 |
| \[LF\]\[Space\]  | \- | 複製堆疊最上方的元素       |
| \[LF\]\[Tab\]    | \- | 交換兩個堆疊最上層的元素     |
| \[LF\]\[LF\]     | \- | 屏棄堆疊最上層的元素       |

### 算術 (IMP: \[Tab\]\[Space\])

算術運算會取堆疊最上方的兩個元素做運算, 並以運算結果取代原本的元素. 先進入堆疊的元素將被視為運算子左方的運算元.

| 指令                 | 參數 | 意義       |
| ------------------ | -- | -------- |
| \[Space\]\[Space\] | \- | 加        |
| \[Space\]\[Tab\]   | \- | 減        |
| \[Space\]\[LF\]    | \- | 乘        |
| \[Tab\]\[Space\]   | \- | 整數除法     |
| \[Tab\]\[Tab\]     | \- | 模運算（取餘數） |

### 堆積操作 (IMP: \[Tab\]\[Tab\])

堆積操作會由堆疊中尋找將被儲存或被取回的物件位址. 要儲存一個物件至堆積裡, 先將位址放入堆疊, 而後放入物件的值再執行儲存指令. 要取出堆積裡的一個物件, 將位址放入堆疊而後執行取回指令, 取回的值會被存放在堆疊的最上方.

| 指令        | 參數 | 意義 |
| --------- | -- | -- |
| \[Space\] |    | 儲存 |
| \[Tab\]   |    | 取回 |

### 控制敘述 (IMP: \[LF\])

控制敘述也是常見指令. 子程序會藉由標籤（label）作標記（用於進行有條件或無條件跳轉）, 此為迴圈（loop）實作的原理. 程式必須藉由\[LF\]\[LF\]\[LF\]這行命令才能才能讓直譯器乾淨（clearly）的結束程式.

| 指令                 | 參數 | 意義              |
| ------------------ | -- | --------------- |
| \[Space\]\[Space\] | 標籤 | 標記程式中某一個流程      |
| \[Space\]\[Tab\]   | 標籤 | 標籤呼叫子程序         |
| \[Space\]\[LF\]    | 標籤 | 從某標籤無條件跳躍至另一標籤  |
| \[Tab\]\[Space\]   | 標籤 | 如果堆疊頂為0則跳躍至某標籤  |
| \[Tab\]\[Tab\]     | 標籤 | 如果堆疊頂為負數則跳躍至某標籤 |
| \[Tab\]\[LF\]      |    | 結束目前子程序並跳躍回呼叫者  |
| \[LF\]\[LF\] -     |    | 結束程式            |

### 輸入輸出 (IMP: \[Tab\]\[LF\])

最後, 我們必須與使用者互動. 這裡的輸入輸出操作有讀入或寫出數字或單獨的字元. 有了這些指令, 我們就可以進行資料流的輸入輸出. 讀入指令會取用堆積地址以將結果寫入堆疊最上方.

| 指令                 | 參數 | 意義              |
| ------------------ | -- | --------------- |
| \[Space\]\[Space\] |    | 輸出堆疊最上方的字元      |
| \[Space\]\[Tab\]   |    | 輸出堆疊最上方的數字      |
| \[Tab\]\[Space\]   |    | 讀入一字元並寫入堆疊頂的位址裡 |
| \[Tab\]\[Tab\]     |    | 讀入一數字並寫入堆疊頂的位址裡 |

## 範例

這是一個簡單的輸出"Hello ,world\!"的程式, 每個 <span style="color:#ffffff;background:#ff9999">空白</span>, <span style="color:#ffffff;background:#9999ff">製表符</span>, 或是換行字元被分別以 "S", "T", 和"L", 代表:

`S`<span style="background:#ff9999">` `</span>`S`<span style="background:#ff9999">` `</span>`S`<span style="background:#ff9999">` `</span>`T`<span style="background:#9999ff">`   `</span>`S`<span style="background:#ff9999">` `</span>`S`<span style="background:#ff9999">` `</span>`T`<span style="background:#9999ff">`   `</span>`S`<span style="background:#ff9999">` `</span>`S`<span style="background:#ff9999">` `</span>`S`<span style="background:#ff9999">` `</span>`L`

T<span style="background:#9999ff"> </span>L S<span style="background:#ff9999"> </span>S<span style="background:#ff9999"> </span>S<span style="background:#ff9999"> </span>S<span style="background:#ff9999"> </span>S<span style="background:#ff9999"> </span>T<span style="background:#9999ff"> </span>T<span style="background:#9999ff"> </span>S<span style="background:#ff9999"> </span>S<span style="background:#ff9999"> </span>T<span style="background:#9999ff"> </span>S<span style="background:#ff9999"> </span>T<span style="background:#9999ff"> </span>L T<span style="background:#9999ff"> </span>L S<span style="background:#ff9999"> </span>S<span style="background:#ff9999"> </span>S<span style="background:#ff9999"> </span>S<span style="background:#ff9999"> </span>S<span style="background:#ff9999"> </span>T<span style="background:#9999ff"> </span>T<span style="background:#9999ff"> </span>S<span style="background:#ff9999"> </span>T<span style="background:#9999ff"> </span>T<span style="background:#9999ff"> </span>S<span style="background:#ff9999"> </span>S<span style="background:#ff9999"> </span>L T<span style="background:#9999ff"> </span>L S<span style="background:#ff9999"> </span>S<span style="background:#ff9999"> </span>S<span style="background:#ff9999"> </span>S<span style="background:#ff9999"> </span>S<span style="background:#ff9999"> </span>T<span style="background:#9999ff"> </span>T<span style="background:#9999ff"> </span>S<span style="background:#ff9999"> </span>T<span style="background:#9999ff"> </span>T<span style="background:#9999ff"> </span>S<span style="background:#ff9999"> </span>S<span style="background:#ff9999"> </span>L T<span style="background:#9999ff"> </span>L S<span style="background:#ff9999"> </span>S<span style="background:#ff9999"> </span>S<span style="background:#ff9999"> </span>S<span style="background:#ff9999"> </span>S<span style="background:#ff9999"> </span>T<span style="background:#9999ff"> </span>T<span style="background:#9999ff"> </span>S<span style="background:#ff9999"> </span>T<span style="background:#9999ff"> </span>T<span style="background:#9999ff"> </span>T<span style="background:#9999ff"> </span>T<span style="background:#9999ff"> </span>L T<span style="background:#9999ff"> </span>L S<span style="background:#ff9999"> </span>S<span style="background:#ff9999"> </span>S<span style="background:#ff9999"> </span>S<span style="background:#ff9999"> </span>S<span style="background:#ff9999"> </span>T<span style="background:#9999ff"> </span>S<span style="background:#ff9999"> </span>T<span style="background:#9999ff"> </span>T<span style="background:#9999ff"> </span>S<span style="background:#ff9999"> </span>S<span style="background:#ff9999"> </span>L T<span style="background:#9999ff"> </span>L S<span style="background:#ff9999"> </span>S<span style="background:#ff9999"> </span>S<span style="background:#ff9999"> </span>S<span style="background:#ff9999"> </span>S<span style="background:#ff9999"> </span>T<span style="background:#9999ff"> </span>S<span style="background:#ff9999"> </span>S<span style="background:#ff9999"> </span>S<span style="background:#ff9999"> </span>S<span style="background:#ff9999"> </span>S<span style="background:#ff9999"> </span>L T<span style="background:#9999ff"> </span>L S<span style="background:#ff9999"> </span>S<span style="background:#ff9999"> </span>S<span style="background:#ff9999"> </span>S<span style="background:#ff9999"> </span>S<span style="background:#ff9999"> </span>T<span style="background:#9999ff"> </span>T<span style="background:#9999ff"> </span>T<span style="background:#9999ff"> </span>S<span style="background:#ff9999"> </span>T<span style="background:#9999ff"> </span>T<span style="background:#9999ff"> </span>T<span style="background:#9999ff"> </span>L T<span style="background:#9999ff"> </span>L S<span style="background:#ff9999"> </span>S<span style="background:#ff9999"> </span>S<span style="background:#ff9999"> </span>S<span style="background:#ff9999"> </span>S<span style="background:#ff9999"> </span>T<span style="background:#9999ff"> </span>T<span style="background:#9999ff"> </span>S<span style="background:#ff9999"> </span>T<span style="background:#9999ff"> </span>T<span style="background:#9999ff"> </span>T<span style="background:#9999ff"> </span>T<span style="background:#9999ff"> </span>L T<span style="background:#9999ff"> </span>L S<span style="background:#ff9999"> </span>S<span style="background:#ff9999"> </span>S<span style="background:#ff9999"> </span>S<span style="background:#ff9999"> </span>S<span style="background:#ff9999"> </span>T<span style="background:#9999ff"> </span>T<span style="background:#9999ff"> </span>T<span style="background:#9999ff"> </span>S<span style="background:#ff9999"> </span>S<span style="background:#ff9999"> </span>T<span style="background:#9999ff"> </span>S<span style="background:#ff9999"> </span>L T<span style="background:#9999ff"> </span>L S<span style="background:#ff9999"> </span>S<span style="background:#ff9999"> </span>S<span style="background:#ff9999"> </span>S<span style="background:#ff9999"> </span>S<span style="background:#ff9999"> </span>T<span style="background:#9999ff"> </span>T<span style="background:#9999ff"> </span>S<span style="background:#ff9999"> </span>T<span style="background:#9999ff"> </span>T<span style="background:#9999ff"> </span>S<span style="background:#ff9999"> </span>S<span style="background:#ff9999"> </span>L T<span style="background:#9999ff"> </span>L S<span style="background:#ff9999"> </span>S<span style="background:#ff9999"> </span>S<span style="background:#ff9999"> </span>S<span style="background:#ff9999"> </span>S<span style="background:#ff9999"> </span>T<span style="background:#9999ff"> </span>T<span style="background:#9999ff"> </span>S<span style="background:#ff9999"> </span>S<span style="background:#ff9999"> </span>T<span style="background:#9999ff"> </span>S<span style="background:#ff9999"> </span>S<span style="background:#ff9999"> </span>L T<span style="background:#9999ff"> </span>L S<span style="background:#ff9999"> </span>S<span style="background:#ff9999"> </span>S<span style="background:#ff9999"> </span>S<span style="background:#ff9999"> </span>S<span style="background:#ff9999"> </span>T<span style="background:#9999ff"> </span>S<span style="background:#ff9999"> </span>S<span style="background:#ff9999"> </span>S<span style="background:#ff9999"> </span>S<span style="background:#ff9999"> </span>T<span style="background:#9999ff"> </span>L T<span style="background:#9999ff"> </span>L S<span style="background:#ff9999"> </span>S<span style="background:#ff9999"> </span>L L L

## 外部連結

  - [Whitespace官方網站](https://web.archive.org/web/20151101230744/http://compsoc.dur.ac.uk/whitespace/tutorial.html)
  - [在Slashdot上的發佈聲明](http://developers.slashdot.org/article.pl?sid=03/04/01/0332202)
  - [Matrix67上的介绍](http://www.matrix67.com/blog/archives/169)
  - [Wandsea'Blog上的介绍](https://web.archive.org/web/20090421134110/http://wandsea.com/blog/65.htm)
  - [Adreaman'Blog上的介绍](https://web.archive.org/web/20151106212650/http://adreaman.com/1212more-whitespace-program.html)

[Category:深奥的编程语言](https://zh.wikipedia.org/wiki/Category:深奥的编程语言 "wikilink")