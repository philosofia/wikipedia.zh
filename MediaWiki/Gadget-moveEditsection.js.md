> 本文内容由[MediaWiki:Gadget-moveEditsection.js](https://zh.wikipedia.org/wiki/MediaWiki:Gadget-moveEditsection.js)转换而来。


/\* Der Grossteil der Codes befindet sich in [MediaWiki:Common.js](../MediaWiki/Common.js.md "wikilink") \*/

//================================================================================ //\*\*\* moveEditsection: Moving of the editsection links

/\*

`* moveEditsection`
`* Dieses Script verschiebt die [Bearbeiten]-Buttons vom rechten Fensterrand`
`* direkt rechts neben die jeweiligen Überschriften.`
`* This script moves the [edit]-buttons from the right border of the window`
`* directly right next to the corresponding headings.`
`*`
`* Zum Abschalten die folgende Zeile (ohne führendes Sternchen) in die eigene`
`* monobook.js (zu finden unter `[`Benutzer:Name/monobook.js`](https://zh.wikipedia.org/wiki/Special:Mypage/monobook.js "wikilink")`) kopieren:`
`* var oldEditsectionLinks = true;`
`*`
`* dbenzhuser (de:Benutzer:Dbenzhuser)`
`*/`

$(function() {

`   if (typeof oldEditsectionLinks != 'undefined' && oldEditsectionLinks)   return;`
`   var spans = document.getElementsByTagName("span");`
`   for (var i=0; i<spans.length; i++) {`
`       var span = spans[i];`
`       if (span.className != "editsection")    continue;`
`       span.style.fontSize = "10pt";`
`       span.style.fontWeight = "normal";`
`       span.style.styleFloat = "none"; // IE-Fix für die folgende Zeile`
`       span.style.cssFloat = "none";`
`       span.style.marginLeft = "0px";`
`       span.parentNode.appendChild(document.createTextNode(" "));`
`       span.parentNode.appendChild(span);`
`   }`

});