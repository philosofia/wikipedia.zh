> 本文内容由[MediaWiki:Titleblacklist](https://zh.wikipedia.org/wiki/MediaWiki:Titleblacklist)转换而来。


`# -{}-本页面为“标题黑名单”`
`# 任何匹配本名单`[`正则表达式`](../Page/正则表达式.md "wikilink")的标题会被阻止建立和编辑`。`
`# 本页面用来添加有共性的某一类要被阻止的标题，如果一个很明确的标题要被阻止，请直接在该标题的页面内用保护页面的方式进行。`
`# 請使用「< >」添加屬性，並將屬性寫在括號內（見下面屬性解釋）。如果含有多個屬性，請用「|」分隔。`
`# 请使用“#”来添加注释。如果項目設有屬性，注意必須寫在屬性的後面。`
`# 詳細說明請見`[`:mw:Extension:Title_Blacklist`](https://zh.wikipedia.org/wiki/:mw:Extension:Title_Blacklist "wikilink")`。`
`# 另有白名單`[`MediaWiki:Titlewhitelist來避免過度封鎖`](https://zh.wikipedia.org/wiki/MediaWiki:Titlewhitelist "wikilink")`。`
`# 若為暫時禁止，請務必列明屆滿日期。`

`# -{}-屬性解釋`
`# autoconfirmed - 只有自動確認用戶可以創建/上載/移動該頁`
`# casesensitive - 當檢視黑名單中的標題時，不要忽略大小写`
`# noedit - 用戶亦會被禁止編輯該條目`
`# moveonly - 禁止移動但允許平常創建`
`# reupload - 允許再上載現存於黑名單中的圖片`
`# errmsg - 於此列出自定訊息名稱，以取代標準訊息並展示自訂訊息，已建立訊息請參閱`[`Special:前缀索引/MediaWiki:Titleblacklist`](https://zh.wikipedia.org/wiki/Special:前缀索引/MediaWiki:Titleblacklist "wikilink")
`# 請注意 newaccountonly 在本地不再有效，請加入至`[`Special:滥用过滤器/194`](https://zh.wikipedia.org/wiki/Special:滥用过滤器/194 "wikilink")

`#未整理`
`\d+ <autoconfirmed|noedit|errmsg=Titleblacklist-semiprotected>`
`.*春池玻璃.* <autoconfirmed|errmsg=Titleblacklist-semiprotected>`
`^[^:]*((\d{1,3}\.){3}\d{1,3}|([0-9a-f]{1,4}:){7}[0-9a-f]{1,4}).* <autoconfirmed|errmsg=Titleblacklist-semiprotected>`
`.*(國瑜|換瑜).* <autoconfirmed|errmsg=Titleblacklist-semiprotected> # 破壞`
`.*王[則则]翠慈善基金.* <autoconfirmed|errmsg=Titleblacklist-semiprotected> # 持续绕过存废讨论删除决定`
`.*邱士縉.* <errmsg=Titleblacklist-fullprotected> # 持續繞過存廢討論刪除決定`
`^[\d-]+$ <autoconfirmed|errmsg=Titleblacklist-semiprotected> # X43破壞和韓文廣告或無意義內容破壞`
`^[^:]*沙盒.*$ `<autoconfirmed>
`.*水.*玲.* <autoconfirmed|errmsg=Titleblacklist-semiprotected> # 破壞`
`.*衝上雲霄.* <autoconfirmed|errmsg=Titleblacklist-semiprotected> # 破壞`
`.*TXO.* <autoconfirmed|errmsg=Titleblacklist-semiprotected> # 持續繞過存廢討論刪除決定`
`.*[颛顓].*[儒如] <noedit|errmsg=Titleblacklist-semiprotected> #长期加入错误资讯`
`.*法國.*臺灣.* `<autoconfirmed>` #动态IP创建不当页面`
`.*陳雲林.* `<autoconfirmed>` #动态IP创建不当页面`
`.*臭屄.* `<autoconfirmed>` #IP长期创建攻击性重定向`
`.*([台檯飓颱][风風]|[热熱][带帶][风風]暴).* <autoconfirmed|errmsg=Titleblacklist-semiprotected> # RFPP oldid=36572154 长期破坏`
`.*考试.*答案.* `<autoconfirmed>
`.*航.*电子客票行程单.* `<autoconfirmed>
`.*去哪儿网.* `<autoconfirmed>
`.*航.*电话.* `<autoconfirmed>
`.*丽妃莱.* `<autoconfirmed>
`.*找.*电话.* `<autoconfirmed>
`.*[滙匯]八坊.*`
`.*[\d０-９零一二三四五六七八九年].*兄.*弟.*象.* #防止多次重複建立`
`.*智慧台[湾灣].*`
`.*[宝寶]福[凯凱].* <autoconfirmed|noedit|errmsg=Titleblacklist-semiprotected> `
`.*理.*想.*[语語].* <autoconfirmed|noedit|errmsg=Titleblacklist-semiprotected>`
`.*[双雙].*合.*推.*[导導].* <autoconfirmed|noedit|errmsg=Titleblacklist-semiprotected>`
`User:WhitePhosphorus-bot\/(misc|message|controls).* <autoconfirmed|noedit|errmsg=Titleblacklist-semiprotected>`
`User:Liangent-bot\/message\/.* <noedit|errmsg=Titleblacklist-fullprotected>`
`.*Ashen.* `<autoconfirmed>
`.*97051253.* `<autoconfirmed>
`.*洪.*任.*諭.* `<autoconfirmed>`#違反生者傳記的傀儡破壞`
`.*張.*貼.*病.*歷.* `<autoconfirmed>`#違反生者傳記的傀儡破壞`
`.*裕多亨.* `<autoconfirmed>
`.*(2012|2013|2014).*([空海].*[姐哥乘]|报名|应聘|招生|分数线).* `<autoconfirmed>
`(?!Draft:).*梅州市.* <autoconfirmed|Titleblacklist-custom-draft> #有IP用户多次创建含有此名称的不当页面`
`(?!Draft:).*梅县区.* <autoconfirmed|Titleblacklist-custom-draft> #有IP用户多次创建含有此名称的不当页面`
`User( talk)?:Liangent\/.* <noedit|errmsg=Titleblacklist-fullprotected> # Targeting Jimmy-bot`
`.*[点點]炮.* `<autoconfirmed>
`.*神.*抄.* `<autoconfirmed>
`.*之.*塔.* `<autoconfirmed>
`.*™.* `<autoconfirmed>
`.*[陳陈]丹丹.* `<autoconfirmed>
`#色情广告`
`.*(高雄|台[中南北]|新竹|桃園)?.*([找約叫玩送]妹|情人|3P|特殊服務|陪睡|排毒|[打約]炮|[喝品約找]茶).* `<autoconfirmed>
`.*(裸.*[舞聊]|[激色].*情|情.*色|[做造].*[愛爱]|性.*[愛爱虐交]|(激.*情|成.*人).*([電电].*影|[網网].*[站址]|[論论].*[壇坛])|偷.*拍|[強强彊輪轮伦倫].*[姦奸]|[亂乱].*[伦倫]|[aA]片|[愛爱].*城|丁.*香.*社.*[區区]|就.*去.*[干乾幹榦]).* `<autoconfirmed>
`.*成.*人.*聊.*天.*室.*`
`.*w.*o.*a.*i.*l.*u.*o.*l.*i.*a.*o.* `<autoconfirmed>
`.*(找小姐|援.*交|招.*妓|卖.*淫|小.*姐.*服.*[务務]).* `<autoconfirmed>
`.*性.*奴.* `<autoconfirmed>
`.*艳.*[图照].* `<autoconfirmed>
`.*充.*气.*娃.* `<autoconfirmed>
`.*苍.*井.*空.* `<autoconfirmed>
`.*内.*衣.* `<autoconfirmed>
`.*吸.*奶.* `<autoconfirmed>
`.*色.*戒.* `<autoconfirmed>
`.*虐.*童.* `<autoconfirmed>
`#.*(酒.*店|宾.*馆|套.*房).* `<autoconfirmed>
`.*皮.*条.*客.* `<autoconfirmed>
`.*人.*体.*(艺.*术|彩.*绘|图).* `<autoconfirmed>
`.*女.*(写.*真|壁.*纸).* `<autoconfirmed>
`.*按.*摩.* `<autoconfirmed>
`.*共.*侍.*一.*夫.* `<autoconfirmed>
`.*[㈠一].*夜.*情.* `<autoconfirmed>
`.*((服务|包夜|小姐|电话|信息).*){2}.* `<autoconfirmed>
`.*小.*姐.* `<autoconfirmed>
`.*鸡.*婆.* `<autoconfirmed>
`.*学.*生.*妹.* `<autoconfirmed>
`.*小.*妹.* `<autoconfirmed>
`.*美.*女.* `<autoconfirmed>
`.*找.*学.*生.* `<autoconfirmed>
`.*学.*生.*服.*务.* `<autoconfirmed>
`.*奶.*[妈媽].*`<autoconfirmed>
`.*外.*送.*茶.* `<autoconfirmed>

`#博彩广告`
`.*老虎[机機].*`
`.*百家[乐樂].* <autoconfirmed|noedit|errmsg=Titleblacklist-semiprotected>`
`.*投.*注.* `<autoconfirmed>
`.*博.*彩.* `<autoconfirmed>
`.*彩.*票.* `<autoconfirmed>
`.*[毒赌].*资.* `<autoconfirmed>
`.*[6６六陆陸].*[合何核河盒荷和涸禾闔阖嗑曷菏蓋蝎褐龢閡阂].*[彩采釆採踩睬綵寀倸婇棌跴].* `<autoconfirmed>

`#医药广告`
`.*[医社].*保.* `<autoconfirmed>
`.*[腎肾].* `<autoconfirmed>
`.*癌.* <autoconfirmed|noedit|errmsg=Titleblacklist-semiprotected>`
`.*心.*脏.*病.* `<autoconfirmed>
`.*治.*疗.* `<autoconfirmed>
`.*男.*[科性].* `<autoconfirmed>
`.*妇.*科.* `<autoconfirmed>
`.*整.*[容形].* `<autoconfirmed>
`.*[医醫]院.* `<autoconfirmed>
`.*变.*性.* `<autoconfirmed>
`.*(上环|代开|怀孕|诊断).*[证證]明.* `<autoconfirmed>

`#美容广告`
`.*美.*[容髮发黑白肌].* `<autoconfirmed>
`.*(丰.*胸|燃.*脂|翘.*臀).* `<autoconfirmed>
`.*(遮.*瑕|祛.*斑|肌.*密).* `<autoconfirmed>
`.*颐.*养.* `<autoconfirmed>
`.*(粉.*刺|黑.*头|脂.*肪.*粒).* `<autoconfirmed>
`.*妆.*容.* `<autoconfirmed>
`.*[护護卷].*[髮发].* `<autoconfirmed>
`.*瘦.*[脸臀腿身].* `<autoconfirmed>
`.*揉.*三.*阴.* `<autoconfirmed>
`.*抗.*氧.*化.* `<autoconfirmed>
`.*人.*造.*岭.* `<autoconfirmed>
`.*[春夏秋冬].*季.*护.* `<autoconfirmed>
`.*植[发髮].* `<autoconfirmed>
`.*祛痘.* `<autoconfirmed>
`.*妙.*[技招].* `<autoconfirmed>
`.*光.*[滑亮鮮].* `<autoconfirmed>
`.*[輕轻].*[松鬆].* `<autoconfirmed>
`.*嫩.*白.* `<autoconfirmed>

`#商品广告`
`.*行.*天.*永.* `<autoconfirmed>
`.*(分.*级|真.*空|炒.*冰|饲.*料|发.*电|输.*送|分.*条|捕.*鱼).*机.* `<autoconfirmed>
`.*精.*密.*[机器].* `<autoconfirmed>
`.*(变.*送|普.*方.*电).*器.* `<autoconfirmed>
`.*肯.*德.*基.* `<autoconfirmed>
`.*塑.*钢.*窗.* `<autoconfirmed>
`.*车.*辆.*厂.* `<autoconfirmed>
`.*家.*[居具].* `<autoconfirmed>
`.*儿.*童.*票.* `<autoconfirmed>
`.*情.*侣.*装.* `<autoconfirmed>
`.*[注註][册冊].*师.* `<autoconfirmed>
`.*培[训訓].*中心.* `<autoconfirmed>
`.*研究生.*答案.* `<autoconfirmed>
`.*油.*博.*士.* `<autoconfirmed>
`.*洪.*醒.*夫.* `<autoconfirmed>
`.*金.*夫.*人.* `<autoconfirmed>
`.*[黄鉑鈀铂钯].*金.* `<autoconfirmed>
`.*烘.*干.*线.* `<autoconfirmed>
`.*全.*能.*班.* `<autoconfirmed>
`.*北京gps.* `<autoconfirmed>
`.*北.*欧.*风.*情.* `<autoconfirmed>
`.*五.*谷.*磨.*坊.* `<autoconfirmed>
`.*丝.*袜.* `<autoconfirmed>
`.*旧.*房.* `<autoconfirmed>
`.*二.*手.*[房车].* `<autoconfirmed>
`.*免.*费.*上.*网.* `<autoconfirmed>
`.*水.*电.*改.*造.* `<autoconfirmed>
`.*回.*收.*利.*用.* `<autoconfirmed>
`.*冷.*库.* `<autoconfirmed>
`.*(iphone|ipad|vagaa).* `<autoconfirmed>
`爱车宝洗车器.* `<autoconfirmed>
`.*金宝莱北珍草.* `<autoconfirmed>
`.*冰.*毒.* `<autoconfirmed>
`.*枪支.* `<autoconfirmed>
`.*汽枪.* `<autoconfirmed>
`.*东.*方.*神.*娃.* `<autoconfirmed>
`.*美.*丽.*适.*度.* `<autoconfirmed>
`.*皇.*马.* `<autoconfirmed>
`.*一.*夜.*失.*踪.* `<autoconfirmed>
`.*收.*看.*节.*目.* `<autoconfirmed>
`.*auspicious bir.* `<autoconfirmed>
`.*迷.?[药藥].* `<autoconfirmed>
`.*三.?唑.?[仑侖].* `<autoconfirmed>
`.*杏璞.* `<autoconfirmed>
`.*[凯凱]耀.* `<autoconfirmed>

`#销售广告`
`.*办.*证.*`
`.*[微短].*信.* `<autoconfirmed>
`.*聊.*天.* `<autoconfirmed>
`.*[开開].* [發发髮].* 票.*`
`.*[發发髮].* 票.* `<autoconfirmed>
`.*营.*销.* `<autoconfirmed>
`.*租.*赁.* `<autoconfirmed>
`.*[购購礼].*物.* `<autoconfirmed>
`.*半.*价.* `<autoconfirmed>
`.*订.*餐.* `<autoconfirmed>
`.*打.*折.* `<autoconfirmed>
`.*给.*料.* `<autoconfirmed>
`.*[维装].*修.* `<autoconfirmed>
`.*五.*金.* `<autoconfirmed>
`.*快.*[运递].* `<autoconfirmed>
`.*砍.*价.* `<autoconfirmed>
`.*闪.*拍.* `<autoconfirmed>
`.*保.*修.* `<autoconfirmed>
`.*出.*租.* `<autoconfirmed>
`.*上.*门.* `<autoconfirmed>
`.*加.*盟.* `<autoconfirmed>
`.*[采选].*购.* `<autoconfirmed>
`.*充.*值.* `<autoconfirmed>
`.*点.*击.* `<autoconfirmed>
`.*破解.* `<autoconfirmed>
`.*下.*载.* `<autoconfirmed>
`.*运.*势.* `<autoconfirmed>
`.*亵.*服.* `<autoconfirmed>
`.*代理.* `<autoconfirmed>
`.*取.*名.* `<autoconfirmed>
`.*窍.*门.* `<autoconfirmed>
`.*高.*利.*贷.* `<autoconfirmed>
`.*([还借赔索].*钱|索.*赔).* `<autoconfirmed>
`.*皇.*冠.* `<autoconfirmed>
`.*炒.*作.* `<autoconfirmed>
`.*成.*本.* `<autoconfirmed>
`.*网.*帖.* `<autoconfirmed>
`.*[矽晶硅片].*[收回].*[收购].* `<autoconfirmed>
`.*[收回].*[收购].*[矽晶硅片].* `<autoconfirmed>
`.*信.*用.*卡.* `<autoconfirmed>
`.*套.*[取现現].* `<autoconfirmed>
`.*[信银銀].*[用鼡行].*[套取].*  `<autoconfirmed>
`.*[代贷貸].*[还還开開款].* `<autoconfirmed>
`.*航.*空.*办.*事.*处.* `<autoconfirmed>
`.*航空.*办事处.* <autoconfirmed|>`
`.*客服电话.* `<autoconfirmed>
`.*铅.*弹.* `<autoconfirmed>
`.*投.*[資资].* `<autoconfirmed>
`.*理.*[財财].* `<autoconfirmed>
`.*代.*[购購].* `<autoconfirmed>

`#联系方式`
`.*[Hh][Tt][Tt][Pp]:\/\/.*`
`.*[９9].*[３3].*[７7].*[８8].*[０ｏＯoO0].*[１1LlI\|｜].*[９9].*[７7].*[９9].*`
`.*[3３③⑶⒊⓷🄄㈢㊂三叁].*[7７⑦⑺⒎⓻🄈㈦㊆七柒].*[5５⑤⑸⒌⓹🄆㈤㊄五伍].*[7７⑦⑺⒎⓻🄈㈦㊆七柒].*[9９⑨⑼⒐⓽🄊㈨㊈九玖].*[5５⑤⑸⒌⓹🄆㈤㊄五伍].*[1１①⑴⒈⓵🄂㈠㊀一壹].*[7７⑦⑺⒎⓻🄈㈦㊆七柒].*[6６⑥⑹⒍⓺🄇㈥㊅六陆].*`
`.*[ｑＱqσ]{2}.* `<autoconfirmed>
`.*[0０][4４][6６][0０].* `<autoconfirmed>` #网站广告 `
`(?!(?:User|User talk|Template|Template talk|Draft):).*(?<!\/patch\/)([\d０-９①-⒛⓫-⓿🄀-🄊㉈-㉏㉑-㉟㊱-㊿㊀-㊉㈠-㈩〇一二三四五六七八九零壹贰叁肆伍陆柒捌玖]\s*){7,}.* `<autoconfirmed>

`#问句页面`
`.*(怎样|如何|有没有|有沒有).* `<autoconfirmed>
`.*怎.*[么麼麽].*[办辦].* `<autoconfirmed>
`.*[是为有為]什[么麼麽].* `<autoconfirmed>
`.*什.*[麼麽么].* `<autoconfirmed>
`.*知.*多.*少.* `<autoconfirmed>
`.*想.*[办辦].*法.* `<autoconfirmed>
`.*[哪那].*[里裡裏].* `<autoconfirmed>

`#冒用官方`
`.*人民日报社论[和及]文章.*`
`.*科學愛國會.*`
`.*\.(info|net|com|cn|org).* `<autoconfirmed>
`(?!Draft:).*[网網] <autoconfirmed|errmsg=Titleblacklist-custom-draft>`
`.*平.*台.* `<autoconfirmed>
`.*[論论].*[壇坛].* `<autoconfirmed>
`.*官.*[網网].* `<autoconfirmed>
`#所有音调和顺序与“维基百科”相同的文字组合`
`#所有音调和顺序与“科百基维”相同的文字组合`

`#政治相關`
`中共.*去中[國国]化.*`
`.*[獨独].*立.* `<autoconfirmed>
`.*缓.*刑.* `<autoconfirmed>
`.*诈.*骗.* `<autoconfirmed>
`.*刑.*拘.* `<autoconfirmed>
`.*[逮批].*捕.* `<autoconfirmed>
`(?!Draft:|Talk:).*中.*[共華华國国囯].* `<autoconfirmed>
`(?!User:|User talk:).*(chinese).* `<autoconfirmed>
`(?!User:|User talk:).*(China).* `<autoconfirmed>
`(?!User:|User talk:).*(Taiwan).* `<autoconfirmed>
`.*Hong.*Kong.* `<autoconfirmed>
`.*(Maca[ou]).* `<autoconfirmed>
`.*民.*[國国囯].* `<autoconfirmed>
`.*共.*和.*[國国囯].* `<autoconfirmed>
`.*共.*[產産产匪狗].* `<autoconfirmed>
`.*反.*[中華华共].* `<autoconfirmed>
`.*[臺台藏蔵疆彊殭].*[獨独].* `<autoconfirmed>
`.*打.*倒.* `<autoconfirmed>
`.*[万萬].*[岁歲歳].* `<autoconfirmed>
`.*[漢汉台臺].*奸.* `<autoconfirmed>
`.*日.*帝.* `<autoconfirmed>
`.*[韃鞑鬼].*子.* `<autoconfirmed>
`.*支.*[那共].* `<autoconfirmed>
`.*[独獨].*裁.* `<autoconfirmed>
`.*[洋黑黒].*鬼.* `<autoconfirmed>
`.*[右左]翼.* `<autoconfirmed>
`.*侵略西藏.* `<autoconfirmed>` #有IP用户多次创建含有此名称的不当页面`

`#激进主义`
`.*(轻.*生|自.*杀).* `<autoconfirmed>

`#維基相關用户名`

`#宗教用户名`

`#不雅用户名`
`.*(屄屌屎尿屁閪糞粪|米.*田.*共).* `<autoconfirmed>

`#粤语粗言用户名`

`#拆字破壞用户名`

`#系统占用词汇及常见错误`
`歧义[12]`
`.*目[標标][條条]目.*`
`.*目[標标][頁页]名[称稱].*`
`.*按.*此.*`
`.*正在[編编][輯辑].*`
`.*[．‧•･・].* <errmsg=titleblacklist-middot> #不正确的間隔號，见`[`帮助:间隔号`](https://zh.wikipedia.org/wiki/帮助:间隔号 "wikilink")
`^[^ \f\n\r\t\v\:]+?`\([^IVX]+\)`$ <errmsg= titleblacklist-disambig-space> #避免消歧義空格錯誤。請使用“條目名 (消歧義項)”的格式，詳見`[`相關方針`](https://zh.wikipedia.org/wiki/Wikipedia:命名常规#括号的使用 "wikilink")
`=.+= #最近被人创建的一些错误标题`
`模版[:：].* # 錯字，應為模板`
`.*[-󰀀-󿿽􀀀-􏿽].* # Unicode私有区字符`
`.*﻿.* # `[`位元組順序記號`](../Page/位元組順序記號.md "wikilink")
`.*​.* # `[`零宽空格`](../Page/零宽空格.md "wikilink")
`.*■.* `<autoconfirmed>
`.*新建文章\s\d.* `<autoconfirmed>
`.*[`\(（]\s*图\s*[\)`）].* `<autoconfirmed>
`.*用户信息.* `<autoconfirmed>
`.*大.*事.*记.* `<autoconfirmed>

`#分類`
`Category( talk)?:.*妙詩人.*`

`#模板`
`Template:.*主[题題]名[称稱].*`
`Template:Editnotices\/.* <autoconfirmed|noedit|errmsg=Titleblacklist-semiprotected>`
`Template\:(?:Efn|Notelist)(?!\/doc$|\/Sandbox$|\/沙盒$).* <noedit|errmsg=Titleblacklist-fullprotected> #高風險模板系列`
`Template:Editnotices\/Namespace\/((?!doc$|Sandbox$|沙盒$).)* <noedit|errmsg=Titleblacklist-fullprotected> #高風險模板系列`

`#項目頁面`
`Wikipedia:.* `<autoconfirmed>` #祇允許自動確認用戶創建計畫頁面`
`Help:.* `<autoconfirmed>
`模块:.*(?<!\/doc|\/sandbox|\/沙盒) <autoconfirmed|noedit|errmsg=Titleblacklist-semiprotected> #防止破壞`
`Wikipedia:繁簡體轉換請求\/.* #只允许简体页面`
`Wikipedia( talk)?:Guestbook for non-Chinese-speakers\/Archives\/w\/index\.php`
`Wikipedia( talk)?:Guestbook for non-Chinese-speakers\/w\/w\/index\.php`
`Wikipedia( talk)?:[刪删]除投票.*`
`Wikipedia( talk)?:(页面|图像|档案|文件)存废讨论.* #请使用繁体`
`Wikipedia( talk)?:(頁面|圖像|檔案|文件)存廢討論.* #祇允許建立特定日期格式`
`Wikipedia( talk)?:.*[維维].*基.*[獎奖奬].*[勵励].*\/.*授.*[獎奖奬].*提.*名.*投.*票.*\/.*([見见].*[習习]|助.*理|[執执].*行|[資资].*深).* #請到`[`WP:AH申請`](https://zh.wikipedia.org/wiki/WP:AH "wikilink")
`Wikipedia( talk)?:.*[維维].*基.*[獎奖奬].*[勵励].*\/.*授.*[獎奖奬].*提.*名.*投.*票.* `<autoconfirmed>` #祇允許維基助理編輯提出`
`Wikipedia:建立條目精靈\/.* <autoconfirmed|noedit|errmsg=Titleblacklist-semiprotected>`
`Wikipedia:典範條目\/.* #請使用簡體 Wikipedia:典范条目`
`Wikipedia:優良條目\/.* #請使用簡體 Wikipedia:优良条目`
`Wikipedia:持续出没的破坏者.* <autoconfirmed|noedit|errmsg=Titleblacklist-semiprotected>`
`Wikipedia:条目请求\/.* <autoconfirmed|noedit> # 未註冊使用者（IP使用者）或非自動確認用戶不得放置請求`

`# prevent redundant namespace prefix during page move`
`.*Special talk:.*`
`(talk|Wikipedia|维基百科|維基百科|‏‎WP|Help|帮助|User|用户|Category|Cat|分类|分類|File|Image|文件|MediaWiki|Template|模板|Portal|Module|模块|模組|Draft|草稿)[：;].* <errmsg=titleblacklist-namespace-colon>`
`(Wikipedia|维基百科|維基百科|‏‎WP):(Wikipedia|维基百科|維基百科|‏‎WP):.* <errmsg=titleblacklist-redundant-namespace>`
`(Template|模板):(Template|模板):.* <errmsg=titleblacklist-redundant-namespace>`
`(User|用户):(User|用户):.* <errmsg=titleblacklist-redundant-namespace>`
`(Draft|草稿):(Draft|草稿):.* <errmsg=titleblacklist-redundant-namespace>`
`(Category|Cat|分类|分類):(Category|Cat|分类|分類):.* <errmsg=titleblacklist-redundant-namespace>`

`#用戶頁面`
`用户：.*`
`User:((\d{1,3}\.){3}\d{1,3}|([0-9a-f]{1,4}:){7}[0-9a-f]{1,4}).* <autoconfirmed|errmsg=titleblacklist-ip-userpage> # 禁止建立IP用戶頁，符合CSD G15#5`
`User( talk)?:.*(屄屌屎尿屁閪糞粪|米.*田.*共).*`
`User( talk)?:.*[變变変].*[態态].*`
`User( talk)?:.*陳霆.*`
`User( talk)?:.*狗.*娘.*[養养].*`
`User( talk)?:.*[姦奸淫婊].*`
`User( talk)?:.*人.*渣.*`
`User( talk)?:.*畜.*[牲生].*`
`User( talk)?:.*[鸡雞鷄鶏].*巴.*`
`User( talk)?:.*[雜杂].*[種种].*`
`User( talk)?:.*"Thong Jia Yu".*`
`User( talk)?:.*"Hu Jin Tao".*`
`User( talk)?:.*林士涵.*`
`User( talk)?:.*周[濟済].*`
`User( talk)?:.*黑名[單单].*`
`User( talk)?:.*去死.*`
`User( talk)?:.*老母.*`
`User( talk)?:.*是狗.*`
`User( talk)?:.*Bot1‎.*`
`User( talk)?:.*[無无].*[恥耻].*`
`User( talk)?:.*阮文雄.*`
`User( talk)?:.*[孫孙].*中山.*`
`User( talk)?:.*彥.*良.*`
`User( talk)?:.*王.*存.*臻.*`
`User( talk)?:.*薄.*[国國].*籍.* `
`User( talk)?:.*[馬马].*英.*九.* `
`User( talk)?:.* 梁.*振.*英.*`
`User( talk)?:.*破.*[坏壞].*`
`User( talk)?:.*趙家俊.*`

`#混淆維基人账户`
`.*2011wp.* `<autoconfirmed>` `
`.*[啦拉龟龜菈垃鞡][跨夸咵垮胯挎侉誇骻姱舿銙恗晇][氪克尅剋兙娔勀勊兛兡兞].* `<autoconfirmed>` `
`.*[乌鸟岛烏鳥島钨鎢邬鄔呜坞].*[跨夸咵垮胯挎侉誇骻姱舿銙恗晇][氪克尅剋兙娔勀勊兛兡兞].* `<autoconfirmed>` `
`.*[乌鸟岛烏鳥島钨鎢邬鄔呜坞][啦拉龟龜菈垃鞡].*[氪克尅剋兙娔勀勊兛兡兞].* `<autoconfirmed>
`.*[乌鸟岛烏鳥島钨鎢邬鄔呜坞][啦拉龟龜菈垃鞡][跨夸咵垮胯挎侉誇骻姱舿銙恗晇].* `<autoconfirmed>` `
`.*([MＭｍΜМм][aÁÁáÀàÂâÄäÃãǍǎĀāĂăĄąÅåａＡΑΆАа][kĶķＫｋΚκКкЌќҚқ]|[aÁÁáÀàÂâÄäÃãǍǎĀāĂăĄąÅåａＡΑΆАа][kĶķＫｋΚκКкЌќҚқ][eÉéÈèÊêËëĚěĒēĔĕĖėĘęｅＥΕΈеЕЀѐЄєЁё]).*c(a|Á|Á|á|À|à|Â|â|Ä|ä|Ã|ã|Ǎ|ǎ|Ā|ā|Ă|ă|Ą|ą|Å|å|ａ|Ａ)t.* `<autoconfirmed>` `
`.*Benc(m|nn|rn)q.* `<autoconfirmed>

`# 過度標點符號或反覆 EXCESSIVE PUNCTUATION OR REPETITION`
`.*[!?‽¿]{3}(?<!!!!).*`
`.*[!?‽¿]{2}(?<!!!!).* `<moveonly>
`.*[!?‽¿]\s+[!?‽¿].*`
`.*‽‽.* `<moveonly>` `
`.*¿¿.* `<moveonly>
`.*[\p{Z}]{2}.* # 禁止2個分隔符號鄰接 (mostly funky spaces)`
`.*[^\p{L}\d ]{6}.* # 禁止連續6個非書寫文字、數字、空格的字元`
`.*([^0])\1{4}.* `<moveonly>` # 禁止移動自4個以上相同字元的頁面`
`.*\p{Lu}(\P{L}*\p{Lu}){9}.* <casesensitive | moveonly>  # 禁止移動多於9個大寫字母的頁面`

`# ATTACK TITLES AND/OR 頁面移動破壞對象`
`Hunter (The|Baker|Classic|Original|Mariner|Fan|Berkeley|2|3|4|5|Oasis|Eclipse|Beacon|Custom|Stratford|Low|Summer|Studio).*`
`.*(?:http|https|ftp|mailto|torrent|ed2k)\:\/\/[\w:@\-]+\.[\w\-]+.*`
`.*bajotz.*`
`.*chaos.{0,7}apper.*`
`.*chaos.{0,7}usic.*`
`.*chaos.{0,7}ntert.*`
`.*chaos.{0,5}ashington.*`
`.*chaos.{0,5}iscography.*`
`.*chao\$.*`
`.*Huff Da(l|ll)and.*`
`.*Tiny Toon.*`
`.*Meepsheep.*`
`.*JEWS DID .* `<casesensitive>
`.*[OÓÒÔÖÕǑŌŎǪŐŒØƏΌΟΩῸὈὉὌὊὍὋОӨӦӪ0][N₦ŃÑŅŇṆΝ][ ]?[WŴẀẂẄẆẈ₩][HΉĤĦȞʰʱḢḤḦḨḪНҢӇӉΗἨἩἪἫἬἭἮἯῊᾘЋΗⱧԋњһh][ÉÈËEĘĚĔĖẺẸẾỀỄễỂểȨȩḜḝĒḖḗȄȅȆȇỆệḘḙḚḛ3عڠeēėèéëẽĕęəẻếềẹ][ÉÈËEĘĚĔĖẺẸẾỀỄễỂểȨȩḜḝĒḖḗȄȅȆȇỆệḘḙḚḛ3عڠeēėèéëẽĕęəẻếềẹ]+[L₤ĹĽḶŁĿΛЛЉ7][[S$ŚŜŞŠṢΣЅz5].* `<moveonly>` # Disallows moves with "on wheels" with 2 or more Es`
`.*on wh33ls.*`
`.*on whiels.*`
`.*on wiels.*`
`.*on hueels.*`
`.*onhueels.*`
`.*\bwith wh?iels\b.* `<moveonly>
`.*on rails.* `<moveonly>
`.*on treads.* `<moveonly>
`.*BITCH.* `<casesensitive>
`.*COCK.* `<casesensitive>
`.*[cċĉ¢сćĉçč][óòôöõǒōŏǫőøόδοσоʘǿọơờởỡớợồổỗốộ][cċĉ¢сćĉçč][kķкќқҝҡҟӄ].*`
`.*[ċĉ¢сćĉçč][oóòôöõǒōŏǫőøόδοσоʘǿọơờởỡớợồổỗốộ][cċĉ¢сćĉçč][kķкќқҝҡҟӄ].*`
`.*[cċĉ¢сćĉçč][oóòôöõǒōŏǫőøόδοσоʘǿọơờởỡớợồổỗốộ][ċĉ¢сćĉçč][kķкќқҝҡҟӄ].*`
`.*[cċĉ¢сćĉçč][oóòôöõǒōŏǫőøόδοσоʘǿọơờởỡớợồổỗốộ][cċĉ¢сćĉçč][ķкќқҝҡҟӄ].*`
`.*CUM.* <casesensitive | moveonly>`
`.*DICK.* `<casesensitive>
`.*giiant.*`
`.*giant penis.*`
`.*huge penis.*`
`.*licking my peni[sz].*`
`.*creamy semen.*`
`.*smaller.than.average.* `<moveonly>
`.*have sex.* `<moveonly>
`.*(?:suck|his|your|my) penis.* `<moveonly>
`.*\b((is\s+an?)|are)\s+(?:dick|cunt|fag|bitch|shit|fuck|loser|ass|gay|ghey|moron|retard|stupid|slut|pa?edo).* `<autoconfirmed>
`.*\b((is\s+an?)|are)\s+(?:dick|cunt|fag|bitch|shit|fuck|loser|ass|gay|ghey|moron|retard|stupid|slut|pa?edo).* `<moveonly>
`.*[Ll][Oo][Ll].*[Ww][Uu][Tt].*`
`.*\bnimp\.org.*`
`.*JIHAD, BITCHES.* `<casesensitive>
`.*Vandalism is Terrorism.*`
`.*WANT TO HA.* <casesensitive | moveonly>`
`.*waant to h.* `<moveonly>
`.*Brian.*Peppers.*`
`.*suck my.* `<moveonly>
`.*GE ORGAS.* <casesensitive | moveonly>`
`.*ge orrg.* `<moveonly>
`.*RM, STICKY.* `<casesensitive>
`.*rm sticky.* `<moveonly>
`.*TAIN OUT OF.* <casesensitive | moveonly>`
`.*nig{2,}er.* # nigger`
`.*loves the.* `<moveonly>
`.*cking fail.*`
`.*Epic fail.*`
`.*[L₤ĹĽḶŁĿΛЛЉ][óòôöõǒōŏǫőøόδοσоʘoọ][L₤ĹĽḶŁĿΛЛЉ][,;:.].* `<moveonly>
`.*WHUT.* <casesensitive | moveonly>`
`.*What what.* `<moveonly>
`.*Gr[óòôöõǒōŏǫőøόδοσоʘǿọ]p.* `<moveonly>
`.*[ԍGGĜĢĞĠƓǤǦǴḠԌეอÇ&ΓϜ]r[\w\s]wp.*`
`.*GGER.* `<casesensitive>
`.*RMY.* <casesensitive | moveonly>`
` .*R.M.I.E.* <casesensitive | moveonly>`
`.*R..M..I..E.* <casesensitive | moveonly>`
`.*Rap(e|es|ing) (babies|children|kids).*`
`.*r[\w\s]pl[\w\s]c[\w\s]ng.* `<moveonly>
`.*h [GĜĢĞĠƓǤǦǴḠԌეอÇ&ΓϜ]s.* `<moveonly>
`.*[^\p{L}][GĜĢĞĠƓǤǦǴḠԌეอÇ&ΓϜٯg][GĜĢĞĠƓǤǦǴḠԌეอÇ&ΓϜٯ].* <moveonly|casesensitive>`
`.*ǃ[^!?]ǃ.* `<moveonly>
`.*Ɩ\P{L}Ɩ.* `<moveonly>
`.*has.been.moved.* `<moveonly>
`.*was movėd.* `<moveonly>
`.*NEGRO.* <casesensitive | moveonly>`
`.*COON SPIC.* <casesensitive | moveonly>`
`.*[BΒБВ฿][RŔŖŘȐȒƦʳʴʵʶṘṚṜṞЯ®ΡΡ₧ÞþΡρРрƤṔṖǷґЃrمŕŗřṛṝгΓ][Il1!ÌÍÎÏĨļǏĪĬİḷŀΙЇɨ!łľıĮį][T₮ŢŤṬΤТЋҬtţťṭτтŧ](ph|f)[AΑĄĂÃÀĀΆẠẬẢẤẦẨẮẰẴẲẪẶḀǞǠȀᾼᾺᾈἉᾉἌᾌἊᾊἎᾎἍᾍἋᾋἏᾏÁÂÄÆÅǺ٩4][GĜĞĠĢƓǤǦǴḠ69&Γ].* #Britfag/phag`
`.*\b(moral)?fag\b.* `<moveonly>
`.*\bNWiki\b.*`
`.*\b[L₤ĹĻĽĮḶḸŁĿ](o|[aă]w+|w[aă])l\b.* `<moveonly>
`.*\b[HΉĤĦȞʰʱḢḤḦḨḪНҢӇӉΗἨἩἪἫἬἭἮἯῊᾘЋΗ−ŧſⱧԋњһ\+łƗ!ÌÍÎÏĨļǏĪĬİḷŀΙЇɨ!łľıĮįḹtţťṭτтŧĵſٲٱ]\W+[AΑĄĂÃÀĀΆẠẬẢẤẦẨẮẰẴẲẪẶḀǞǠȀᾼᾺᾈἉᾉἌᾌἊᾊἎᾎἍᾍἋᾋἏᾏÁÂÄÆÅǺ٩4]\W+[GĜĢĞĠƓǤǦǴḠԌეอÇ&ΓϜ].* `<moveonly>
`.*\b[HΉĤĦȞʰʱḢḤḦḨḪНҢӇӉΗἨἩἪἫἬἭἮἯῊᾘЋ\+Η−ŧſⱧԋњһłƗ!ÌÍÎÏĨļǏĪĬİḷŀΙЇɨ!łľıĮįḹtţťṭτтŧĵſٲٱ]\W*[AΑĄĂÃÀĀΆẠẬẢẤẦẨẮẰẴẲẪẶḀǞǠȀᾼᾺᾈἉᾉἌᾌἊᾊἎᾎἍᾍἋᾋἏᾏÁÂÄÆÅǺ٩4]\W*[GĜĢĞĠƓǤǦǴḠԌეอÇ&ΓϜg].* <moveonly|casesensitive>`
`.*[ĜĢĞĠƓǤǦǴḠԌეอÇ&ΓϜٯģğġĝҩ]\s*[ĜĢĞĠƓǤǦǴḠԌეอÇ&ΓϜٯģğġĝҩ].* `<moveonly>
`.*[ĜĢĞĠƓǤǦǴḠԌეอÇ&ΓϜٯģğġĝҩ]{2,5}.* `<moveonly>
`.*Wikipedo.*`
`.*An hero.* <moveonly|casesensitive>`
`.*\.\.\.H.* `<moveonly>
`.*\.\.\.\.H.* `<moveonly>
`.*\bfapped.* `<moveonly>
`.*Krimpet.* `<moveonly>
`.*,,+.* `<moveonly>
`.*;;+.* `<moveonly>
`.*(\pP{2,}\PP){4}.* <moveonly|errmsg=titleblacklist-custom-pagemove> #Antigrawp, works by blocking titles with overused punctuation (eg H..A..G..G..E..R)`
`.*[ÂĄĂÃÀĀΆẠẬẢẤẦẨẮẰẴẲẪẶḀǞǠȀᾼᾺᾈἉᾉἌᾌἊᾊἎᾎἍᾍἋᾋἏᾏÁÂÄÆÅǺ٩][69]{2,5}.* #nonstandard A66`
`.*Faggot.* `<moveonly>
`.*Deletionis.* `<moveonly>
`.*'H'.* `<moveonly>
`.*\*h.* `<moveonly>
`.*H'A.* <casesensitive|moveonly>`
`.*piece of sh[iî][ţt].* `<moveonly>
`.*moved by.* `<moveonly>
` .*[GĜĞĠĢƓǤǦǴḠ69&Γ]\s*[ZŹŽŻ]\s*[FҒ₣]\s*[FҒ₣]\s*[DĐĎḌÐΔ₫₯]\s*[QɊʠ].* `<moveonly>
`.*[GĜĞĠĢƓǤǦǴḠ69&Γ]\s*[DĐĎḌÐΔ₫₯]\s*[QɊʠ]\s*[ĹĻĽḶŁĿ₤ΛLŀ]\s*[XҲΧ].* `<moveonly>
`.*[RŔŖŘȐȒƦʳʴʵʶṘṚṜṞЯ®ΡΡ₧ÞþΡρРрƤṔṖǷґЃŕŗřṛṝгґѓΓя][eēėèéëẽĕęəẻếềẹể][PƤṔṖǷ₧ÞþΡρРр][L₤ĹĽḶŁĿΛЛЉ][AΑÂĄĂÃÀĀΆẠẬẢẤẦẨẮẰẴẲẪẶḀǞǠȀᾼᾺᾈἉᾉἌᾌἊᾊἎᾎἍᾍἋᾋἏᾏÁÂÄÆÅǺ٩4aáàâäãǎāăảąæåάαᾳᾴὰᾲᾶᾷἀᾀἁᾁἄᾄἂᾂἆᾆἅᾅἃᾃἇᾇаӑӓӕạậ]c[eēėèéëẽĕęəẻếềẹể].[eēėèéëẽĕęəẻếềẹể][AΑÂĄĂÃÀĀΆẠẬẢẤẦẨẮẰẴẲẪẶḀǞǠȀᾼᾺᾈἉᾉἌᾌἊᾊἎᾎἍᾍἋᾋἏᾏÁÂÄÆÅǺ٩4aáàâäãǎāăảąæåάαᾳᾴὰᾲᾶᾷἀᾀἁᾁἄᾄἂᾂἆᾆἅᾅἃᾃἇᾇаӑӓӕạậ][cċĉ¢сćĉçč][HНΉĤĦȞʰʱḢḤḦḨḪНҢӇӉΗἨἩἪἫἬἭἮἯῊЋΗ].* `<moveonly>
``.*[ÌÍÎÏĨļǏĪĬİḷ][’'`][dďḍÐ].[HΉĤĦȞʰʱḢḤḦḨḪНҢӇӉΗἨἩἪἫἬἭἮἯῊЋΗſⱧԋh][ÌÍÎÏĨļǏĪĬİḷ]t.[ÌÍÎÏĨļǏĪĬİḷ][tţťṭτтŧ].* ``<moveonly>
`.*\?\s*`\(.{55,200}\)`.* `<moveonly>` # long Hagger parentheticals`
`.*fuċking.*`
`.*cuntmonkey.*`
`.*\([QɊʠIl1!ÌÍÎÏĨļǏĪĬİḷŀΙЇɨ!łľıĮį].{95,200}.* `<moveonly>
`.*[W₩ŴΨШЩ]{1,3}[ǼAÀÁÂÃÄÅĀĂĄǍǞǠǺȀȂȦȺḀẠẢẤẦẨẪẬẮẰẲẴẶÆǢ4@Α]{1,3}[N₦ŃÑŅŇṆΝ]{1,3}[tţťṭτтŧ]{1,3}.[tţťṭτтŧ]{1,3}[OÓÒÔÖÕǑŌŎǪŐŒØƏΌΟΩῸὈὉὌὊὍὋОӨӦӪǿọ]{1,3}.{50,200}.* `<moveonly>
`.*[T₮ŢŤṬΤТЋҬtţťṭτтŧ][OÓÒÔÖÕǑŌŎǪŐŒØƏΌΟΩῸὈὉὌὊὍὋОӨӦӪọóòôöõǒōŏǫőøόδοσоʘǿọ].[Ccċĉ¢сćĉçčUÚÙÛÜŨŮǓŪǖǘǚǜŬŲŰ].{50,200}.* `<moveonly>
`.*pawns.wiki.* `<moveonly>
`.*nimp.org.*`
`.*Tewapack.* `<moveonly>
`.*Colonel.Sanders.* `<moveonly>
`.*kzm\.pas.*  #used to create malicious user talk subpages`
`.*zilog\s*head.* `<autoconfirmed>` # Prolific sock GEORGIEGIBBONS`
`.*on\s*wheels.*edition.* `<autoconfirmed>
`.*shakur green.* #Recreation under different titles; see `[`Wikipedia:Articles``   ``for``   ``deletion/Shakur``   ``Green`](https://zh.wikipedia.org/wiki/Wikipedia:Articles_for_deletion/Shakur_Green "wikilink")
`.* shitt?ing in .*'?s? mouth #A specific page which needs to be SALTed and redacted`
`.* fucking bastard.* #A specific page which needs to be SALTed and redacted`
`.* first male to female transsexuall #A specific page which needs to be SALTed and redacted`
`.*Wimbo Jales .* #Probably will never be used except to insult Jimbo Wales`
`.*Ñ!gG3r.* #A specific page which needs to be SALTed and redacted`
`.* is gay`
`.*inside ?(his|her|its|their) ?anus.*`
`.*exchanges? bodily fluids.*`
`.*\b(eat(s|ing)?|ate)\b.*\bshit\b.*`
`.*f(ú|u)cked up piece of shit.* #A specific page which needs to be SALTed and redacted`
`.*get cocks shoved up (his|her|its|their) ass.*`
`.*Flint Diao.* #Serial spamming`
`.*Mega [Mm]om.* #Blatant hoax`
`.*MLBP.* #Blatant hoax`
`.*Maisani.*  #Continued sockpuppet vandalism`
`.*Bikini Beach.* #Persistent disruption`
`.*(Lucas|Luke) Ullrich.* #Persistent disruption`

`#破坏`
`# 一堆电视节目被加上后缀后创建为新条目`
`.{3,}(特别版|翻版) `<autoconfirmed>
`.*[蔴麻]雀.* `<autoconfirmed>

`#`[`User:影武者`](https://zh.wikipedia.org/wiki/User:影武者 "wikilink")
`#注意：请同时更新71#过滤器`
`.*User( talk)?:.*(Kegns|Lanwi1|T.A Shirakawa).*\/.*(林浩生|阮文雄).* `<autoconfirmed>
`.*阮.*文.*雄.* `<autoconfirmed>` #影武者破坏，禁止创建`[`阮文雄以外的任何条目`](https://zh.wikipedia.org/wiki/阮文雄 "wikilink")

`#`[`User:十字军大屠杀`](https://zh.wikipedia.org/wiki/User:十字军大屠杀 "wikilink")

`#`[`:ja:WP:MACHINE`](https://zh.wikipedia.org/wiki/:ja:WP:MACHINE "wikilink")

`# 长期出没的破坏者`
`.*朱.*(明|日月).* `<autoconfirmed>
`.*王.*存.*臻.* `<autoconfirmed>
`.*李.*(煌|火皇).* `<autoconfirmed>
`.*[力历立屴厉扐礼朸吏扚刕呖杝沥坜苈叓李励里利丽岦沵枥迣例戾疠沴隶苙叕茘轹疬赲俐俪俚砅厘栃荔峛郦栎柂峢悧猁峲涖浰砬栛栗砺珕砾离浬悝秝狸哩唎莅莉逦荲剓娳骊娌粝粒菞婯犁笠悷梸梨唳理琍脷蚸悡蛎傈裡雳棃棙痢鹂犂蛠锂詈跞厤凓喱睙缡粴鉝溧蜊漓裏鳨搮剺睝塛筣蓠慄厯豊蒞蒚艃嫠璃歴盠竰瑮貍蜧厲綟樆暦孷銐黎蔾褵糎鲡犛鋫鋰蝷鲤篥篱罹隷縭錅鴗勵曆歷澧巁醨濿禮磿隸蟍鬁檪癘謧藜釐櫔爄邌嚟鎘離擽鯉鯏曞儮禲蠇犡瓈藶鏫鵹壢嚦攊瓅麗瀝斄鯬櫟礪蟸醴皪蠣瓑糲盭黧爏櫪礫囄麜酈鷅癧鳢纅蠡礰蘺蠫儷灕邐孋轢囇躒觻攦廲讈轣鑗劙攭籬瓥靂穲鱧纚鱱欚驪鱺鸝][巟汻肓怳恍炾衁皇荒晄宺晃朚隍凰偟黄谎奛惶慌黃堭塃媓喤遑崲揘湟徨葟瑝幌詤楻滉愰煌榥潢锽墴熀獚篁蝗艎璜皝曂熿謊穔磺癀諻鳇鍠兤餭簧蟥櫎趪韹爌鎤鐄皩騜鰉鷬鱑][耂老劳労牢佬恅狫姥络窂咾荖珯浶涝烙捞崂唠栳哰铑勞铹痨絡閖嗠耢酪嫪銠僗躼潦嶗憦澇撈嘮憥橯癆磱蟧簩耮醪轑軂鐒顟髝][十饣尸士氏什礻辻矢示石仕失史世丗市师乨卋忕式似戺时竍佦忯识亊豕実柹视始旹饰实呩泽呞侍试使诗势飠驶厔虱事邿鸤屎栅屍恃炻恀拾拭贳施浉峕峙柿眂蚀咶祏冟是室宩昰枾狧狮食姼兘适舐轼眡烒铈時眎栻耆狶莳埘宲逝師視痑畤匙硕秲埶釈啫笶釶絁遈谥葹惿崼貰弑徥寔殖湤湜湿释揓崻筮蒒蓍弒觢軾詩試蒔睗楴獅嵵煶溼溡溮飾勢嗜鉐塒鉇鉃鉂鈰馶誓酾鉽鳲適瑡實榯嘘碩蝕舓蝨奭銴餙噓箷餝鲥駛鳾嬕噬鲺澨鮖澤遾褷諡諟濕螫鍦檡謚簭鼫識籂鯴鼭鰘釋襫醳鶳鰣鰤襹釃].*`<autoconfirmed>
`.*顾晓军.* `<autoconfirmed>

`# `[`Wikipedia:持续出没的破坏者/广州IP破坏`](https://zh.wikipedia.org/wiki/Wikipedia:持续出没的破坏者/广州IP破坏 "wikilink")
`.*(Wan|ang).*(xua|uan).*(\d)*.* `<autoconfirmed>
`.*(\d)*(Wan|ang).*(xua|uan).* `<autoconfirmed>
`.*(aok|oke).*(\d{3,4}).* `<autoconfirmed>
`.*(H|C)at.*(\d{3}).* `<autoconfirmed>
`.*(Mak|ake).*(ca|at).* `<autoconfirmed>
`.*Ji(m|nn)(m|nn)y.*xu.*wrk.* `<autoconfirmed>
`Template:DC11.* <autoconfirmed|noedit|errmsg=Titleblacklist-semiprotected>`
`# Prevent users from creating pages with bad names after searching`
`# <errmsg=titleblacklist-forbidden-prefix>`
`.+ prefix:.*`

`# `[`User:萬聖至尊`](https://zh.wikipedia.org/wiki/User:萬聖至尊 "wikilink")
`.*User( talk)?:.*涉毒.* `<autoconfirmed>

`# Appleeeeeeeeeeeeeee`
`.*Cohaf.* `<autoconfirmed>
`.*M[MC]C\d.* `<autoconfirmed>