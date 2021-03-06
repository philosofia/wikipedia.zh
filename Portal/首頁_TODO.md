## 如何建立

  - <font color=red>注意</font>： 建立[主題前](https://zh.wikipedia.org/wiki/Wikipedia:主題 "wikilink")，請確保你有維護主題頁的決心，建立後不會棄之不顧。可以尽量先创建大家比较关注的首页，这样可以保证有相当的人手来维护。若創建超過三個月仍嚴重未完成的主題，很可能會面臨提刪的命運。
  - **提示**：請主題創建者於頁面創建後，同時發布[工作進展](../Page/Template:工作進展.md "wikilink")、[主題數與](https://zh.wikipedia.org/wiki/Template:主題首頁數 "wikilink")[主題列表](https://zh.wikipedia.org/wiki/Portal:首頁/列表 "wikilink")，這樣大家才知道您所創建之主題，以便於後續共同維護作業。

如你想建立「某題目」的主題頁：

1\. 主題首頁應該放在Portal命名空間，即建立\[\[Portal:某題目|Portal:某題目\]\]，然後輸入：

`{{subst:box portal skeleton| topic=某題目}}`

儲存。

2\. 建立兩個子頁： a) \[\[Portal:某題目/box-header|Portal:某題目/box-header\]\]子頁中輸入：

`{{Portal:box-header | title={{{1}}}`
`|editpage=`
`|border=#aaaaaa <!-- 欄位邊框的顏色 -->`
`|titleforeground=white <!-- 欄位標題文字的顏色 -->`
`|titlebackground=#aaccff <!-- 欄位標題的底色 -->`
`|background=#f9f9ff <!-- 欄位的底色 -->`
`|foreground=black}} <!-- 文字的顏色 -->`

儲存。

以及 b) \[\[Portal:某題目/box-footer|Portal:某題目/box-footer\]\]子頁中輸入：

`{{Portal:box-footer | {{{1}}} }}`

儲存。

3\. 回到主題首頁，即\[\[Portal:某題目|Portal:某題目\]\]，然後開始編輯。

4\. 在其他與「某主題」有關的頁面中加入主題首面的連結，請使用以下的模版：和。

#### 如何加欄位

如果你想加新的欄位，請先到你的主題頁(e.g. [1](http://zh.wikipedia.org/w/index.php?title=Portal:动漫&action=edit))，然後加入：

```
 {{/box-header| 甲 | 乙 }}
 {{ 丙 }}
 {{/box-footer| 丁 }}
```

當中：

  - **"甲"** 是此欄位的名字
  - **"乙"** 是欄位右上角「編輯連結」所連到的路徑，有兩種情況：
    1.  `{{/box-header | 从哪里开始 | Wikipedia:主题/物理/从哪里开始}}`
    2.  `{{/box-header | 从哪里开始 | }}`（不會有編輯連結顯示在欄位中）
  - **"丙"** 是內容的路徑，如：
      - `{{/你知道嗎}}`
  - **"丁"** 是放在右下角的相關連結，有兩種情況：
    1.  `{{/box-footer | [[更多的內容...|更多的內容...]]}}`
    2.  `{{/box-footer | }}`（不會出現連結）

### 例子

以下的碼：

`<div style="float:right; width:50%;">`
**`{{portal:物理/box-header|从哪里开始|portal:物理/从哪里开始}}`**
`{{portal:物理/从哪里开始}}`
**`{{portal:物理/box-footer|}}`**
`</div>`

會生成 --\>

<div style="float:right; width:50%;">

</div>



### 主題頁版面的各區塊

  - 主題頁版面的各區塊應該要使用模板技術，以方便維護該主題頁。（相關範例請參考[Portal:飲食](../Page/Portal:飲食.md "wikilink")或[Portal:電子學](../Page/Portal:電子學.md "wikilink")）

<!-- end list -->

  - **简介**：（必要）用以簡介該主題頁的目標，或所包含的領域範圍。
  - 典范条目：（最好能有）不定期更新，或預先建立多組內容隨機顯示，簡介有一定內容且符合主題的条目。
  - 特色图片：（最好能有）不定期更新，或預先建立多組內容隨機顯示，展示符合主題的圖片。
  - 特色人物：（非必要）不定期更新，或預先建立多組內容隨機顯示，簡介有一定內容且符合主題的人物条目。
  - **分类**：（必要）
  - 新聞：（非必要）如果不能每月經常性更新資訊的話，最好別放。但如果符合主題的領域經常有新消息、新研究、或新產品的話，可以考慮在主題頁使用此區塊
  - 你知道吗：（非必要），以謎題的方式進行相關條目的導覽
  - 主要話題：（最好能有），預先把符合該主題，較為人熟知的條目名稱，整理成一份導覽用列表
  - 欢迎参与：（非必要），放請求條目，或請求翻譯的地方
  - 相關主題：（非必要），提供相關主題頁的連結
  - 维基专题：（非必要），如果有對應或相關的維基專題的話
  - 维基媒体计划：（最好能有），如果在其他维基媒体计划裡，有相關的頁面或分類的話
  - 跨語言的主題頁鏈結：使用\[\[xx:Portal:該語言的主題頁名稱|xx:Portal:該語言的主題頁名稱\]\]

<!-- end list -->

  - 新聞：如果某些領域經常有新消息、新研究可以做，但不是太活躍的領域就可以在特別事件發生時才寫一兩則新聞
  - 相關主題：
  - **該範疇的分支**（必要）
  - 典範條目：不定期更新，介紹程度較充實的項目（現時因為這類條目較少，不是每個領域也有，所以較難做）
  - 新建條目：該要定期更新，以讓人感覺到這是個有生氣的地方。類同首頁的「你知道嗎」
  - 請求條目
  - 主要項目：
  - 相關文檔：例如相關的主題
  - 網站鏈結

### 主題頁導覽

  - 製作「主題導航模板」

<!-- end list -->

  -

<!-- end list -->

  - 在相關的條目或分類頁裡放上您製作的「主題導航模板」

## 參見

  - [Wikipedia:典范条目/存档](https://zh.wikipedia.org/wiki/Wikipedia:典范条目/存档 "wikilink")
  - [Wikipedia:優良條目/存檔](https://zh.wikipedia.org/wiki/Wikipedia:優良條目/存檔 "wikilink")
  - [Wikipedia:每日圖片](https://zh.wikipedia.org/wiki/Wikipedia:每日圖片 "wikilink")