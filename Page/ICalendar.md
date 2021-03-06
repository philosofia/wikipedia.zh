> 本文内容由[ICalendar](https://zh.wikipedia.org/wiki/ICalendar)转换而来。


**iCalendar**是“[日曆數據交換](https://zh.wikipedia.org/wiki/日曆 "wikilink")”的標準（RFC 5545）。 此標準有時指的是“iCal”，即[蘋果公司的出品的一款同名日曆軟件](https://zh.wikipedia.org/wiki/蘋果公司 "wikilink")（見[iCal](https://zh.wikipedia.org/wiki/行事曆_\(Apple\) "wikilink")），這個軟件也是此標準的一種實現方式。

iCalendar允許用戶通過電子郵件的方式發送“會議請求”或“任務”。收信人使用支持iCalendar郵件客戶端，便可以很方便地回應發件人，接受請求或另外提議一個新的會議時間。

iCalendar已得到很多產品的支持。通常情況下，iCalendar數據是使用電子郵件交換，但它也可以獨立使用，而不局限於某種傳輸協議。例如，可以通過[WebDav伺服器或](https://zh.wikipedia.org/wiki/WebDav "wikilink")[SyncML](../Page/SyncML.md "wikilink")來進行共享與修改。簡單的網頁伺服器（只使用HTTP協議）也常常被用來分發公共事件的iCalendar數據，或發佈個人的時間謀劃安排。發佈者可以使用[hCalendar把iCalendar數據嵌入到網頁中](https://zh.wikipedia.org/wiki/hCalendar "wikilink")。（hCalendar是一種通過[（X）](../Page/XHTML.md "wikilink")[HTML](../Page/HTML.md "wikilink")來表現iCalendar的[微格式](../Page/微格式.md "wikilink")）

## 歷史與設計

iCalendar是由[互联网工程任务组](../Page/互联网工程任务组.md "wikilink")的[日曆與計劃工作組設計](https://zh.wikipedia.org/wiki/日曆與計劃工作組 "wikilink")（OpenText公司的Anik Ganguly主導），並由[蓮花公司的Frank](https://zh.wikipedia.org/wiki/蓮花公司 "wikilink") Dawson和[微軟的Derik](https://zh.wikipedia.org/wiki/微軟 "wikilink") Stenerson發表。iCalendar本身是基於[互聯網郵件協會（IMC）的](https://zh.wikipedia.org/wiki/互聯網郵件協會（IMC） "wikilink")[vCalendar開發設計而來的](https://zh.wikipedia.org/wiki/vCalendar "wikilink")。它通常是以文件名後綴為.ics或.ifb的文本文件保存的。現有標准是於2009年九月發布的\[<http://tools.ietf.org/html/rfc5545>| RFC 5545\]，上一個標準是\[<http://tools.ietf.org/html/rfc2445>| RFC 2445\]。

以.ics為後綴名的文件（在Apple Mac系統中使用"iCal"類型代碼），表示該文件包含了日曆和計劃信息。而以.ifb為後綴名的文件（在Apple Mac系統中使用"iFBf"類型代碼），表示該文件包含 了空閒和忙碌時間信息。

通常iCalendar使用[UTF-8](../Page/UTF-8.md "wikilink")字符編碼；但也可以使用[MIME中的charset參數來指其它的字符編碼](https://zh.wikipedia.org/wiki/MIME "wikilink")（如果它的傳送協議支持MIME的話）。

在iCalendar文件中，每一行必須以[CR+LF](https://zh.wikipedia.org/wiki/CR+LF "wikilink")（十六進制代碼為0D0A）為結尾。每一行不得超過75[字節](https://zh.wikipedia.org/wiki/字節 "wikilink")/[八位元組](../Page/八位元組.md "wikilink")。如果一行數據長於這個限制，則必須換行；後面一行使用空格符（十六進制代碼為20）或者制表符（十六進制代碼為09）作開始，以表示本行內容是上面一行內容的繼續。內容數據中的換行符，可以反斜杠符'/'後跟數字（UTF-8中為5C 6E或5C 4E）來表示。

iCalendar的MIME類型被定義為*text/calendar*。

## 局限和發展

iCalendar格式只是被設計用來傳送日曆和計劃表數據，如事件；而故意沒有定義操作這些數據的行為。因為，在編寫程序時需要協商如何操作它們。

iCalendar本意是提供一種公共格式來定義開放的互聯網可交換的日曆和計劃表數據。當這些特性被廣泛支持應用後，很多性能問題逐漸顯現出來了。比如，大多數應用都不支持旅行（VJOURNAL）。"在標準中，循環重復的會議有一些含糊不清，這導致在現有不同的應用之間仍然無法真正地互動。"

iCalendar中的日曆無法兼容非[格里高利曆](https://zh.wikipedia.org/wiki/格里高利曆 "wikilink")，比如[以色列](../Page/以色列.md "wikilink")的[希伯來曆](../Page/希伯來曆.md "wikilink")和[沙特阿拉伯](../Page/沙特阿拉伯.md "wikilink")的[伊斯曆都是](https://zh.wikipedia.org/wiki/伊斯曆 "wikilink")[陰曆](https://zh.wikipedia.org/wiki/陰曆 "wikilink")。

“日曆訪問協議”備忘錄（\[<http://tools.ietf.org/html/rfc4324>| RFC 4324\]）首次嘗試建立一個統一的創建實時日曆系統。可能是因為過於複雜，這個協議最終被放棄了。

無論如何，像[GroupDav和](https://zh.wikipedia.org/wiki/GroupDav "wikilink")[CalDAV這些基於iCalendar的協議已經越來越廣泛地應用在客戶端和服務端軟件包中了](https://zh.wikipedia.org/wiki/CalDAV "wikilink")。

互联网工程任务组的日曆與計劃工作組 已經提交了關於iCalendar標准的附加修改提案。但這個工作組於2011年一月份被解散了。他們大部分工作重心轉移到了前一個標准的條款解釋。而後續的創新工作由[日曆和計劃協會](https://zh.wikipedia.org/wiki/日曆和計劃協會 "wikilink")（簡稱為Calconnect）來完成。

## 技術標準

### 核心對象

iCalendar中的頂級元素是日曆和計劃核心對象，一組日曆和計劃信息。通常情況下，這些信息應該只包含單一的iCalendar對象。但可以聲明一個組包含多個iCalendar對象。

第一行必須是"BEGIN:VCALENDER"，最後一行必須是"END:VCALENDER"；兩行之間數據稱之為"icalbody"。

icalbody由一系列日曆屬性和一個以上的日曆組件組成。日曆屬性被應用於整個日曆。日曆組件則是由若干日曆屬性描述成的一個日曆語義。比如，日曆組件可以指定一個事件、一個待辦事項列表、一個旅行事項、時區信息、繁忙/空閒時間信息，或者一個警報。在許多協議實現（比如Google Calendar）中不允許出現空行。

下在是一個簡單的iCalendar對象示例，它描述了[法国国庆日](https://zh.wikipedia.org/wiki/法国国庆日 "wikilink")，即從1997年七月14日 17:00到1997年七月15日 03:59:59的[巴士底日](https://zh.wikipedia.org/wiki/巴士底日 "wikilink")。

`BEGIN:VCALENDAR`
`VERSION:2.0`
`PRODID:-//hacksw/handcal//NONSGML v1.0//EN`
`BEGIN:VEVENT`
`UID:uid1@example.com`
`DTSTAMP:19970714T170000Z`
`ORGANIZER;CN=John Doe:MAILTO:john.doe@example.com`
`DTSTART:19970714T170000Z`
`DTEND:19970715T035959Z`
`SUMMARY:Bastille Day Party`
`END:VEVENT`
`END:VCALENDAR`

### 事件（VEVENT）

VEVENT描述一個事件，在日曆上一系列計劃好的時間點。通常，當用戶接受一個日曆事件，這將導致在那個時間裡，用戶被認為是忙碌的。VEVENT可以包含一個VALARM對象來允許一個警報。事件應該有一個DTSTART來描述事件的開始時間，和一個DTEND來描述事件的結束時間。如果事件是循環的，則DTSTART應該設置第一個事件的開始時間。

VEVENT同樣可以應用在沒有特定時間的日曆事件上，比如周年紀念日、每日提醒。

如果你需要發送取消事件的請求。那麼在請求中事件組件中，UID屬性應該與原事件一致並且，下面這些屬性應該設置成cancel。

`METHOD:CANCEL`
`STATUS:CANCELLED`

為了發送事件的更新請求，除了設置UID和其它更新屬性值外。還需要設置新序列值

`SEQUENCE:`<新序列值>

比如，第一個更新版本

`SEQUENCE:1`

在Microsoft Outlook中，SUMMARY屬性應當與"Appointment"中的"Subject"項一致，DESCRIPTION 屬性緊跟著SUBJECT屬性。另外，Outlook 2003要求指定UID和DTSTAMP屬性。

### 待辦事項（VTODO）

VTODO描述一條待辦事項。

下面的例子描述了一個應於1998年四月15日的待辦事項。屆時一個響鈴將會響起。在待辦事項完成前，將會一小時提醒一次，共提醒四次。SEQUENCE屬性顯示這條提醒在創建之後，還被修改了兩次。

`BEGIN:VCALENDAR`
`VERSION:2.0`
`PRODID:-//ABC Corporation//NONSGML My Product//EN`
`BEGIN:VTODO`
`DTSTAMP:19980130T134500Z`
`SEQUENCE:2`
`UID:uid4@host1.com`
`ACTION:AUDIO`
`TRIGGER:19980403T120000`
`ATTACH;FMTTYPE=audio/basic:http://example.com/pub/audio-`
`    files/ssbanner.aud`
`REPEAT:4`
`DURATION:PT1H`
`END:VTODO`
`END:VCALENDAR`

### 旅行事項（VJOURNAL）

VJOURNAL是一個旅行事項。它們將一段描述文字關聯一個詳細的日曆日期上，這可以被用戶記錄活動和成長日誌，或者描述待辦事項的進展。VJOURNAL日曆組件不會影響日曆上的時間狀況，所以不會對空閒和繁忙狀態有任何影響。在實踐上，有很少的程序支持VJOURNAL項，不過也有存在一些實現。比如：Plum Canary's Chirp軟件將VJOURNAL和VTODO一起使用。KDE中的[KOrganizer也支持VJOURNAL](https://zh.wikipedia.org/wiki/KOrganizer "wikilink")。

下面就是旅行事項的例子

`BEGIN:VCALENDAR`
`VERSION:2.0`
`PRODID:-//ABC Corporation//NONSGML My Product//EN`
`BEGIN:VJOURNAL`
`DTSTAMP:19970324T120000Z`
`UID:uid5@host1.com`
`ORGANIZER:MAILTO:jsmith@example.com`
`STATUS:DRAFT`
`CLASS:PUBLIC`
`CATEGORIES:Project Report, XYZ, Weekly Meeting`
`DESCRIPTION:Project xyz Review Meeting Minutes\n`
`    Agenda\n1. Review of project version 1.0 requirements.\n2.`
`    Definition`
`    of project processes.\n3. Review of project schedule.\n`
`     Participants: John Smith, Jane Doe, Jim Dandy\n-It was`
`      decided that the requirements need to be signed off by`
`      product marketing.\n-Project processes were accepted.\n`
`     -Project schedule needs to account for scheduled holidays`
`      and employee vacation time. Check with HR for specific`
`      dates.\n-New schedule will be distributed by Friday.\n-`
`     Next weeks meeting is cancelled. No meeting until 3/23.`
`END:VJOURNAL`
`END:VCALENDAR`

**注意**: 这个例子中来自于\[<http://tools.ietf.org/html/rfc2445>| RFC 2445\]。在这里将原文中的CATEGORY修正为CATEGORIES，这是原文中的一个错误。

### 空闲/繁忙时间（VFREEBUSY）

VFREEBUSY被用在 空闲/繁忙时间 设置请求，这种请求的回应，以及繁忙时间的发布中。 下面就是一个系统时间发布的例子。

`BEGIN:VCALENDAR`
`VERSION:2.0`
`PRODID:-//RDU Software//NONSGML HandCal//EN`
`BEGIN:VFREEBUSY`
`ORGANIZER:MAILTO:jsmith@example.com`
`DTSTART:19980313T141711Z`
`DTEND:19980410T141711Z`
`FREEBUSY:19980314T233000Z/19980315T003000Z`
`FREEBUSY:19980316T153000Z/19980316T163000Z`
`FREEBUSY:19980318T030000Z/19980318T040000Z`
`URL:http://www.example.com/calendar/busytime/jsmith.ifb`
`END:VFREEBUSY`
`END:VCALENDAR`

### 其它组件类型

其它组件类型还有**VTIMEZONE**（时区）和**VALARAM**（警报）。还有一些组件允许包含其它组件（VALARAM通常被包含于其它组件）。

### 发布更新

当计划事件更改，UID字段将发布更新。首先事件创建时会生成一个[全局唯一标识符作为UID](https://zh.wikipedia.org/wiki/UUID "wikilink")。之后当有一个事件跟随这个UID发布，则认为这是早先事件的修改版本，并替换掉它。

### 日历扩展

iCalendar支持私有扩展，即在属性名前冠以"X-"前缀。

比如：

  - X-RECURRENCE-ID
  - X-EPOCAGENDAENTRYTYPE
  - X-FUNAMBOL-AALARMOPTIONS
  - X-FUNAMBOL-ALLDAY
  - X-MICROSOFT-CDO-ALLDAYEVENT
  - X-MICROSOFT-CDO-BUSYSTATUS
  - X-WR-CALNAME
  - X-WR-CALDESC
  - X-WR-RELCALID
  - X-WR-TIMEZONE
  - X-PUBLISHED-TTL

[Category:文件格式](https://zh.wikipedia.org/wiki/Category:文件格式 "wikilink") [Category:日程管理軟體](https://zh.wikipedia.org/wiki/Category:日程管理軟體 "wikilink")