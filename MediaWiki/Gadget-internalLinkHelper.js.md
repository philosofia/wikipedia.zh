/\* [Template:Internal link helper](https://zh.wikipedia.org/wiki/Template:Internal_link_helper "wikilink") 辅助脚本 \*/

importScript( "MediaWiki:Tooltips.js" );

var dynamicTooltip = {

` toggle : false,`

` doTip : function (evt)`
` {`
`   x = evt.pageX ||`
`       evt.clientX + ((document.documentElement ? document.documentElement.scrollLeft : 0)`
`                      || document.body.scrollLeft || 0);`
`   y = evt.pageY ||`
`       evt.clientY + ((document.documentElement ? document.documentElement.scrollTop : 0)`
`                      || document.body.scrollTop || 0);`
`   var tip = document.createElement ('div');`
`   var text = document.createTextNode ('Initial mouse coordinates: x = ' + x + ', y = ' + y);`
`   if (this.tt_toggle) {`
`     // Make the whole stuff a dummy link every second time.`
`     var lk = document.createElement ('a');`
`     lk.appendChild (text);`
`     lk.setAttribute ('href', '#');`
`     tip.appendChild (lk);`
`   } else {`
`     tip.appendChild (text);`
`   }`
`   this.tt_toggle = !this.tt_toggle;`
`   return tip;`
` }`

}

function setTooltips (){

`   var close_imgs = new Array(3);`
`   close_imgs[0] = document.createElement('img');`
`   close_imgs[0].src = "//upload.wikimedia.org/wikipedia/commons/f/f8/Tooltip-CloseButton.png";`
`   close_imgs[1] = document.createElement('img');`
`   close_imgs[1].src = "//upload.wikimedia.org/wikipedia/commons/5/5a/Tooltip-CloseButton-Hover.png";`
`   close_imgs[2] = document.createElement('img');`
`   close_imgs[2].src = "//upload.wikimedia.org/wikipedia/commons/d/df/Tooltip-CloseButton-Active.png";`
`   close_imgs[0].width = close_imgs[1].width = close_imgs[2].width = "16";`
`   function createTips(clsname,tipclsname,attrs,isChild){`
`       var items = getElementsByClassName(document, 'span', 'ILHItem');`
`       for(var i = 0, item; item = items[i]; i ++) {`
`           if(!hasClass(item, 'ILHExist')) {`
`               var chinese = getElementsByClassName(item, 'span', 'ILHChinese')[0];`
`               var original = getElementsByClassName(item, 'span', 'ILHOriginal')[0];`
`               var langname = getElementsByClassName(item, 'span', 'ILHLang')[0];`
`               var tip = document.createElement('div');`
`               chinese.className = clsname;`
`               tip.className = tipclsname;`
`               tip.style.display = 'none';`
`               html = chinese.innerHTML + wgULS('指向的页面不存在，可参考', '指向的頁面不存在，可參考') + `
`                      langname.innerHTML + wgULS('维基百科的对应页面', '維基百科的對應頁面') + `
`                      original.innerHTML + '。';`
`               tip.innerHTML = html;`
`               new Tooltip(isChild?chinese.firstChild:chinese,tip,attrs);`
`           }`
`           comment = getElementsByClassName(item, 'span', 'ILHComment')[0];`
`           comment.parentNode.removeChild(comment);`
`       }`
`   }`
`   createTips(`
`       'ILHClickButton',`
`       'ILHClickButton_tip',`
`       {`
`           mode : Tooltip.MOUSE,`
`           close_button : close_imgs,`
`           activate: Tooltip.CLICK,`
`           deactivate : Tooltip.CLICK_ELEM`
`       },`
`       true`
`   );`

}

$(setTooltips);