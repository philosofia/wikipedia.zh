importScript('//en.wikipedia.org/w/index.php?title=User:TheFearow/qstring.js\&action=raw\&ctype=text/javascript');

$(doAddQuickPreview);

function doAddQuickPreview() {

` if ((mw.config.get('wgAction') != "edit") && (mw.config.get('wgAction') != "submit")) return;`
` var qbutton = document.getElementById("wpPreview").cloneNode(false);`
` qbutton.value = wgULS("快速预览", "快速預覽");`
` qbutton.type="button";`
` qbutton.tabindex="6"; `
` qbutton.accessKey="g";`
` qbutton.id="dlQuickPreview";`
` qbutton.title= wgULS("预览您的编辑", "預覽您的編輯");`
` qbutton.addEventListener("click", doQuickPreview, false); `
` document.getElementById("wpPreview").parentNode.insertBefore(qbutton,document.getElementById("wpDiff"));`
` document.getElementById("wikiPreview").style.display="block";`

}

function doQuickPreview() {

` var bt = document.getElementById("dlQuickPreview");`
` document.getElementById("contentSub").innerHTML = wgULS("获取预览……", "獲取預覽……");`
` bt.value= wgULS("获取预览……", "獲取預覽……");`
` bt.disabled=true;`
` var form = document.editform;`
` var postData = {`
`   'wpMinoredit': form.wpMinoredit.checked, `
`   'wpWatchthis': form.wpWatchthis.checked,`
`   'wpStarttime': form.wpStarttime.value,`
`   'wpEdittime': form.wpEdittime.value,`
`   'wpAutoSummary': form.wpAutoSummary.value,`
`   'wpEditToken': form.wpEditToken.value,`
`   'wpSummary': wgULS("快速预览", "快速預覽"),`
`   'wpTextbox1': document.editform.wpTextbox1.value`
` };`

` var addr = document.URL;`
` addr = addr.replace("&action=edit", "&action=submit");`
` addr += "&wpPreview=true&live=true";`

` var qwxmlhttp = sajax_init_object(null);`
` qwxmlhttp.overrideMimeType('text/xml');`
` qwxmlhttp.open( 'POST' , addr, true);`
` qwxmlhttp.setRequestHeader('Content-type','application/x-www-form-urlencoded');`
` qwxmlhttp.onload = function() { `
` document.getElementById("wikiPreview").innerHTML =   unescape(qwxmlhttp.responseText.replace(/>/g,">").replace(/</g,"<").replace(/&/g,"&").replace(/"/g,'"'));`
` bt.disabled=false;`
` bt.value = wgULS("快速预览", "快速預覽");`
` document.getElementById("contentSub").innerHTML = "";`
` }`
` qwxmlhttp.send(QueryString.create(postData));`

}