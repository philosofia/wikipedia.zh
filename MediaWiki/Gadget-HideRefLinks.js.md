/\*

` 本小工具可隱藏註腳裏的「^」回鏈`

  - /

$(function(){

`var i, j, k, lis, obj, nextSibling;`
`var ols=document.getElementsByTagName("ol");   //擷取所有`

for(i=ols.length; i--\>0; ){

` if(ols[i].className!="references") continue;   //檢查是否為`

<references/>

所產生的

，如否跳至下一個;

` //如是，↓;`

` lis=ols[i].childNodes;   //擷取`

下的子物件

` check_lis:`
` for(j=lis.length; j-->0; ){`
`  //檢查是否為子物件是否為有效的`

<li>

;

`  if( (""+lis[j].tagName).toLowerCase()!="li" ) continue;`
`  if( (""+lis[j].id).indexOf("cite_note-")!=0 ) continue;`
`  if( lis[j].childNodes.length==0 ) continue;`
`  //如否跳至下一個`

<li>

物件；如是，↓;

`  //檢查`

<li>

第一個物件是否為<b>回鏈;

`  obj=lis[j].firstChild;`
`  if( (""+obj.tagName).toLowerCase()=="b" )`
`  if( obj.childNodes.length==1 )`
`  if( (""+obj.childNodes[0].tagName).toLowerCase()=="a" )`
`  if( (""+obj.childNodes[0].href).indexOf("#cite_ref-")!=-1 && obj.childNodes[0].childNodes.length==1)`
`  if( obj.childNodes[0].childNodes[0].nodeName=="#text" )`
`  if( obj.childNodes[0].childNodes[0].nodeValue=="^" ) {`
`   //如是，移除之;`

`   if( obj.nextSibling )`
`   if( obj.nextSibling.nodeName=="#text" ) {`
`    obj.nextSibling.nodeValue=obj.nextSibling.nodeValue.substring(1);`

`    if(obj.nextSibling.nodeValue.split(" ").join("")==""){`
`     obj.nextSibling.parentNode.removeChild(obj.nextSibling);`
`    }`
`   }`
`   obj.parentNode.removeChild(obj);`

`   continue;  //跳至下一個`

<li>

;

`  }`

`  //如不是`<b>`，檢查所有`

<li>

下的子物件

`  //搜查及移除頭個 ^;   `
`  if(obj.nodeName!="#text") continue;`
`  if(obj.nodeValue!="^ ") continue;`

`  if(obj=lis[j].childNodes[0]) do{`
`   nextSibling=obj.nextSibling;`

`   //搜查及移除`<a>`回鏈;`
`   if( (""+obj.tagName).toLowerCase()=="a" )`
`   if( (""+obj.href).indexOf("#cite_ref-")!=-1 && obj.childNodes.length==1 )`
`   if( (""+obj.childNodes[0].tagName).toLowerCase()=="sup" )`
`   if( obj.childNodes[0].childNodes.length==1 )`
`   if( (""+obj.childNodes[0].childNodes[0].tagName).toLowerCase()=="b" )`
`   if( obj.childNodes[0].childNodes[0].childNodes.length==1 )`
`   if( obj.childNodes[0].childNodes[0].childNodes[0].nodeName=="#text" )`
`   if( (""+obj.childNodes[0].childNodes[0].childNodes[0].nodeValue).split(".").length==2 ){`
`    if( obj.nextSibling )`
`    if( obj.nextSibling.nodeName=="#text" ) {`
`     obj.nextSibling.nodeValue=obj.nextSibling.nodeValue.substring(1);`

`     if(obj.nextSibling.nodeValue.split(" ").join("")==""){`
`      obj.nextSibling.parentNode.removeChild(obj.nextSibling);`
`     }else{`
`      lis[j].removeChild(lis[j].firstChild);`
`      obj.parentNode.removeChild(obj);`
`      continue check_lis;`
`     }`
`    }`

`    nextSibling=obj.nextSibling;`
`    obj.parentNode.removeChild(obj);`
`   }`

`   if(obj=nextSibling){`
`    continue;`
`   }else{`
`    lis[j].removeChild(lis[j].firstChild);`
`    break;`
`   }`
`  } while(true);`
` }`
`}`

});