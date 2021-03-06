> 本文内容由[MediaWiki:Guidedtour-tour-twa3.js](https://zh.wikipedia.org/wiki/MediaWiki:Guidedtour-tour-twa3.js)转换而来。


// The Wikipedia Adventure Mission 3

( function ( window, document, $, mw, gt ) {

//automatic api:edit function to send yourself messages function sendMessage( targetPage, msgPage, linkTo ) {

`   var api = new mw.Api();`
`   api.post( {`
`       'action' : 'edit',`
`       'title' : targetPage,`
`       'appendtext' : "\n``",`
`       'summary' : '新訊息（`[`維基百科大歷險自動模擬`](https://zh.wikipedia.org/wiki/WP:TWA "wikilink")`3）',`
`       'token' : mw.user.tokens.get('csrfToken')`
`   } ).done( function () {`
`       window.location.href = linkTo;`
`   } );`

}

// Fail gracefully post-save but not postedit var postEditButtons = \[\]; if ( mw.config.get( 'wgAction' ) === 'view' && \!gt.isPostEdit() ) {

`       postEditButtons.push( {`
`               name: '按此返回並進行編輯',`
`               onclick: function() {`
`                       window.location.href = new mw.Uri().extend( { action: 'edit' } ).toString();`
`               }`
`       } );`

}

// Fail gracefully post-save but not postedit for visual editor var postEditButtonsVisual = \[\]; if ( mw.config.get( 'wgAction' ) === 'view' && \!gt.isPostEdit() ) {

`       postEditButtonsVisual.push( {`
`               name: '返回',`
`               onclick: function() {`
`                       window.location.href = window.location.href +`

"\&veaction=edit";

`               }`
`       } );`

}

gt.defineTour( {

`       name: 'twa3',`
`       shouldLog: true,`
`       steps: [ {`
`               //1`
`               title: '第三關開始！',`
`               description: '`

<div align="right">

[TWA_guide_right_top.png](https://zh.wikipedia.org/wiki/File:TWA_guide_right_top.png "fig:TWA_guide_right_top.png")

</div>

蓋亞女郎在〈地球〉條目那兒等着我們呢。

一起出發吧。

',

`               onShow: gt.parseDescription,`
`               overlay: true,`
`               closeOnClickOutside: false,`
`               buttons: [ {`
`                       name: '向地球出發*',`
`                       onclick: function()  {  if(!mw.config.get('wgUserName')){  alert( "請登入。" );   return;   } sendMessage( 'User:' + mw.config.get( 'wgUserName' ) + '/TWA/Earth', 'Wikipedia:TWA/Earth/1' , mw.util.getUrl( 'Special:MyPage/TWA/Earth' ) + '?tour=twa3&step=2'); }`
`               } ],`
`               allowAutomaticOkay: false`

`       },  {`
`               //2`
`               title: '這就是地球了！',`
`               description: '`
`維基百科條目以百科條目的體例縱覽敘述對象，向讀者介紹關於敘述對象的重要資訊。`

`',`
`               onShow: gt.parseDescription,`
`               overlay: false,`
`               closeOnClickOutside: false,`
`               buttons: [ {`
`                       name: '`<big>`←`</big>`',`
`                       action: 'externalLink',`
`                       url: mw.util.getUrl( 'Wikipedia:TWA/3/Start' ) + '?tour=twa3&step=1'          `
`               } , {`
`                       name: '去看看',`
`                       action: 'next',`
`               } ],`
`               allowAutomaticOkay: false`

`       },  {`
`               //3`
`               title: '看看有沒有地方要修正？',`
`               description: '`

<div align="left">

[TWA_guide_left_top.png](https://zh.wikipedia.org/wiki/File:TWA_guide_left_top.png "fig:TWA_guide_left_top.png")

</div>

我留意到條目的一些筆誤，看起來很是礙眼。你找到了多少處？

',

`               attachTo: '#content.mw-body',`
`               position: 'bottom',`
`               onShow: gt.parseDescription,`
`               overlay: false,`
`               closeOnClickOutside: false,`
`               buttons: [ {`
`                       name: '`<big>`←`</big>`',`
`                       action: 'externalLink',`
`                       url: mw.util.getUrl( 'Special:MyPage/TWA/Earth' ) + '?tour=twa3&step=2'          `
`               } , {`
`                        name: '糾錯',`
`                        action: 'next'`
`               } ],`
`               allowAutomaticOkay: false               `

`       },  {`
`               //4`
`               title: '糾錯',`
`               description: '`
`找到了五處筆誤嗎？`

`第山——`<b>`第三`</b>
`似大——`<b>`四大`</b>
`散個——`<b>`三個`</b>` `
`洞植物——`<b>`動植物`</b>
`人累——`<b>`人類`</b>`',`
`               attachTo: '#content.mw-body',`
`               position: 'bottom',`
`               onShow: gt.parseDescription,`
`               overlay: false,`
`               closeOnClickOutside: false,`
`               allowAutomaticOkay: false,`
`               buttons: [ {`
`                       name: '`<big>`←`</big>`',`
`                       action: 'externalLink',`
`                       url: mw.util.getUrl( 'Special:MyPage/TWA/Earth' ) + '?tour=twa3&step=3'          `
`               } , {`
`                       name: '都找到了',`
`                       action: 'next',`
`               } ],`

`       },  {`
`               //5`
`               title: '修正筆誤',`
`               description: '`
`鍛煉一下自己的編輯技能，把這些筆誤修正好吧。按「編輯」。`

`',`
`               attachTo: '#ca-edit',`
`               position: 'bottom',`
`               onShow: gt.parseDescription,`
`               overlay: false,`
`               closeOnClickOutside: false,`
`               allowAutomaticOkay: false,`
`               buttons: [ {`
`                       name: '`<big>`←`</big>`',`
`                       action: 'externalLink',`
`                       url: mw.util.getUrl( 'Special:MyPage/TWA/Earth' ) + '?tour=twa3&step=4'          `
`               } ],`
`               shouldSkip: function() {`
`                       return gt.hasQuery( { action: 'edit' } );`
`               }`

`       },  {`
`               //6`
`               title: '五項修訂',`
`               description: '`
`第山——`<b>`第三`</b>
`似大——`<b>`四大`</b>
`散個——`<b>`三個`</b>` `
`洞植物——`<b>`動植物`</b>
`人累——`<b>`人類`</b>`',`
`               onShow: gt.parseDescription,`
`               overlay: false,`
`               attachTo: '#wpTextbox1', `
`               position: 'bottomRight',`
`               closeOnClickOutside: false,`
`               buttons: [ {`
`                       name: '`<big>`←`</big>`',`
`                       action: 'externalLink',`
`                       url: mw.util.getUrl( 'Special:MyPage/TWA/Earth' ) + '?tour=twa3&step=5'          `
`               } , {`
`                       name: '已修正',`
`                       action: 'next',`
`                       } ],`
`               allowAutomaticOkay: false`

}, {

`               //7`
`               title: '寫下編輯摘要和儲存',`
`               description: '`
`給大家知道你「修正了五處筆誤。」`

`準備好了以後，就`<b>`儲存`</b>`。',`
`               attachTo: '#wpSave',`
`               position: 'bottomRight',`
`               autoFocus: 'yes',`
`               onShow: gt.parseDescription,`
`               overlay: false,`
`               closeOnClickOutside: false,`
`               allowAutomaticOkay: false,`
`               buttons: [ {`
`                       name: '`<big>`←`</big>`',`
`                       action: 'externalLink',`
`                       url: mw.util.getUrl( 'Special:MyPage/TWA/Earth' ) + '?tour=twa3&step=6&action=edit'          `
`               } ],`
`               shouldSkip: function() {`
`                       return gt.isPostEdit();`
`               },`
`               buttons: postEditButtons`

} , {

`               //8`
`               title: '放膽改正！',`
`               description: '獲得新工具：  `<b>`校對員獎章`</b>

<center>

[TWA_badge_4.png](https://zh.wikipedia.org/wiki/File:TWA_badge_4.png "fig:TWA_badge_4.png")

</center>


哇⋯⋯現在全世界都能夠看到由你改善的新版本了！這挺酷的喔！

繼續完成幾項修訂吧。就把文章開頭「<b>地球</b>」這個詞加粗吧。

這樣讀者就能迅速把目光移向條目的敘述對象了。按「編輯」。

',

`               onShow: gt.parseDescription,`
`               overlay: false,`
`               attachTo: '#ca-edit',`
`               position: 'bottom',`
`               closeOnClickOutside: false,`
`               allowAutomaticOkay: false,`
`               buttons: [ {`
`                       name: '`<big>`←`</big>`',`
`                       action: 'externalLink',`
`                       url: mw.util.getUrl( 'Special:MyPage/TWA/Earth' ) + '?tour=twa3&step=7&action=edit'          `
`               } ],`
`               shouldSkip: function() {`
`                       return gt.hasQuery( { action: 'edit' } );`
`               }`
`               `

} , {

`               //9`
`               title: '加粗！',`
`               description: '`

<div align="right">

[TWA_guide_right_top.png](https://zh.wikipedia.org/wiki/File:TWA_guide_right_top.png "fig:TWA_guide_right_top.png")

</div>

和之前一樣，要加粗，就要把文中第一個「地球」加亮，然後按下編輯工具列的B字。

',

`               attachTo: '#wpTextbox1', `
`               position: 'bottomRight',`
`               autoFocus: 'yes',`
`               onShow: gt.parseDescription,`
`               overlay: false,`
`               closeOnClickOutside: false,`
`               buttons: [ {`
`                       name: '`<big>`←`</big>`',`
`                       action: 'externalLink',`
`                       url: mw.util.getUrl( 'Special:MyPage/TWA/Earth' ) + '?tour=twa3&step=8'          `
`               } , {`
`                       name: '已加粗',`
`                       action: 'next',`
`                       } ],`
`               allowAutomaticOkay: false`

} , {

`               //10`
`               title: '寫下編輯摘要和儲存',`
`               description: '`
`給大家知道你「把字詞加粗。」`

`準備好了以後，就`<b>`儲存`</b>`。',`
`               attachTo: '#wpSave',`
`               position: 'bottomRight',`
`               autoFocus: 'yes',`
`               onShow: gt.parseDescription,`
`               overlay: false,`
`               closeOnClickOutside: false,`
`               allowAutomaticOkay: false,`
`               buttons: [ {`
`                       name: '`<big>`←`</big>`',`
`                       action: 'externalLink',`
`                       url: mw.util.getUrl( 'Special:MyPage/TWA/Earth' ) + '?tour=twa3&step=9&action=edit'          `
`               } ],`
`               shouldSkip: function() {`
`                       return gt.isPostEdit();`
`               },`
`               buttons: postEditButtons`

} , {

`               //11`
`               title: '哇哦⋯⋯好興奮欸！',`
`               description: '`

<div align="left">

[TWA_guide_left_top.png](https://zh.wikipedia.org/wiki/File:TWA_guide_left_top.png "fig:TWA_guide_left_top.png")

</div>

你已經開始掌握這些技能了。看來你會善用這些技能，好好編輯。

嘿，您又收到一則新留言了...

',

`               onShow: gt.parseDescription,`
`               overlay: false,`
`               closeOnClickOutside: false,`
`               allowAutomaticOkay: false,`
`               buttons: [ {`
`                       name: '`<big>`←`</big>`',`
`                       action: 'externalLink',`
`                       url: mw.util.getUrl( 'Special:MyPage/TWA/Earth' ) + '?tour=twa3&step=10&action=edit'          `
`               } , {`
`                       name: '查看你的新訊息*',`
`                       onclick: function()  {  if(!mw.config.get('wgUserName')){  alert( "請登入。" );   return;   } sendMessage( 'User talk:' + mw.config.get( 'wgUserName' ) + '/TWA', 'Wikipedia:TWA/MyTalk/3a' , mw.util.getUrl( 'Special:MyTalk/TWA' ) + '?tour=twa3&step=12'); }`
`               } ],`

} , {

`               //12`
`               title: '新內容...',`
`               description: '`

<div align="left">

[TWA_guide_left_top.png](https://zh.wikipedia.org/wiki/File:TWA_guide_left_top.png "fig:TWA_guide_left_top.png")

</div>

來看看有甚麼新內容吧

',

`               onShow: gt.parseDescription,`
`               attachTo: '#content.mw-body',`
`               position: 'bottom',`
`               overlay: false,`
`               closeOnClickOutside: false,`
`               buttons: [ {`
`                       name: '`<big>`←`</big>`',`
`                       action: 'externalLink',`
`                       url: mw.util.getUrl( 'Special:MyPage/TWA/Earth' ) + '?tour=twa3&step=11'          `
`               } , {`
`                       name: '查看新內容*',`
`                       onclick: function()  {  if(!mw.config.get('wgUserName')){  alert( "請登入。" );   return;   } sendMessage( 'User:' + mw.config.get( 'wgUserName' ), 'Wikipedia:TWA/Badge/4template2' , mw.util.getUrl( 'Wikipedia:TWA/3/End' ) + '?tour=twa3&step=13'); } `
`               } ],`
`               allowAutomaticOkay: false`

`} , {`
`               //13`
`               title: '第三關完成！',`
`               description: '`
[<File:Wesnothmusic.ogg>`   ``(short).ogg`](https://zh.wikipedia.org/wiki/File:Wesnothmusic.ogg_\(short\).ogg "fig:File:Wesnothmusic.ogg (short).ogg")
<b>`踏上第四關⋯⋯`</b>`',`
`               onShow: gt.parseDescription,`
`               overlay: false,`
`               closeOnClickOutside: false,`
`               buttons: [ {`
`                       name: '恭喜自己！',`
`                       action: 'end'`
`               } ],`
`               allowAutomaticOkay: false`

}\]

} );

} (window, document, jQuery, mediaWiki, mediaWiki.guidedTour ) ) ;