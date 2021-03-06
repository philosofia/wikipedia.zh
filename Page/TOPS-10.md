> 本文内容由[TOPS-10](https://zh.wikipedia.org/wiki/TOPS-10)转换而来。


**TOPS-10**是迪吉多電腦公司為其PDP-10迷你電腦所撰寫的作業系統，首次發表為1964年，軟硬體結合後的成果系統也稱為「DECsystem-10」。

TOPS-10支援可共享的記憶體，並且被用來開發第一套多人同時共樂的電腦遊戲程式（[MUD](../Page/MUD.md "wikilink")），這一套遊戲叫DECWAR，是一種文字導向、[星際奇航記](https://zh.wikipedia.org/wiki/星際奇航記 "wikilink")（Star Trek）型態的遊戲，玩家在終端機前輸入文字命令並即時的相互戰鬥。

另一個具開創性的應用程式叫FORUM，這可能是第一個「CB 推演程式」，可以讓使用者透過電腦與另一個使用者對話，如同[聊天室](https://zh.wikipedia.org/wiki/聊天室 "wikilink")（chat room）一樣，這個應用程式展現了多方使用者通訊的潛在可能性，之後此電腦系統也讓CompuServe公司開發出聊天應用程式。

TOPS-10有一套非常強韌的[應用程式介面](https://zh.wikipedia.org/wiki/應用程式介面 "wikilink")（[API](https://zh.wikipedia.org/wiki/API "wikilink")），這套程式介面使用一種叫做UUO（Unimplemented User Operation）的機制。UUO成為一種作業系統的呼叫方式，同時UUO看起來像一堆機器指令。這套API被叫做Monitor Call（監督器呼叫），這種概念與作法其實已遠遠領先當年絕大多數的其他作業系統。也因為有了極具彈性的作業系統API，因此在DECsystem-10上進行系統開發撰寫就變的相當容易與快速有效。

TOPS-10有一個有趣的[排程器以及許多個可執行的](https://zh.wikipedia.org/wiki/排程器 "wikilink")[佇列](https://zh.wikipedia.org/wiki/佇列 "wikilink")，不像[OpenVMS只有](https://zh.wikipedia.org/wiki/OpenVMS "wikilink")2個可執行的[佇列](https://zh.wikipedia.org/wiki/佇列 "wikilink")，並且想在佇列中插入程序還必須倚賴程序[優先權](https://zh.wikipedia.org/wiki/優先權 "wikilink")。TOPS-10也具有使用者檔案及裝置獨立性。再者，在TOPS-10上所發展出來的程式碼概念之後也用在[RSX-11上](https://zh.wikipedia.org/wiki/RSX-11 "wikilink")，更之後也用到OpenVMS上，這些相同的作業系統設計想法也可在今日的作業系統中看見，如[Windows NT](../Page/Windows_NT.md "wikilink")。

附帶一提的是，TOPS-10裡頭也有一、二個[暗藏的軟體訊息](https://zh.wikipedia.org/wiki/彩蛋_\(視覺\) "wikilink")，例如輸入如下的文字命令：

**MAKE LOVE**

就會得到系統發出如下的回應：

**Not War?**

意思就是您輸入「只要做愛」，系統就會自動回應「不要戰爭」，這是一句很盛行的[反戰口號](https://zh.wikipedia.org/wiki/反戰 "wikilink")。直到今天，在OpenVMS中所附的Teco編輯器中，即便是現有的版本都仍然會有如上的命令回應。

最後，就當年而言TOPS-10是當時一套相當快速且彈性的作業系統。

[Category:操作系统](https://zh.wikipedia.org/wiki/Category:操作系统 "wikilink") [Category:DEC作業系統](https://zh.wikipedia.org/wiki/Category:DEC作業系統 "wikilink")