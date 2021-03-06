/\*\*

`* Move the coordinates which are at the top of the page`
`* From fr:mediawiki:common.js`
`*/`

function moveCoord() {

` var h1 = document.getElementById('firstHeading');`
` if(!h1) h1 = document.getElementsByTagName('h1')[0]; // Nostalgia, Standard`
` var coord = document.getElementById('coordinates');`
` if ( !coord || !h1 ) return;`
` $(coord).addClass("coordinates-title");`

} $(moveCoord);

// Verwendung von OpenStreetMap in Wikipedia. // (c) 2008 by Magnus
Manske // Released under GPL // Modified version in order to makes it
work with moveCoord() above // From fr:mediawiki:common.js // modified
to makes it work for IT : Otourly

function openStreetMap_Init () {

` var c = document.getElementById ( 'coordinates' ) ;`
` if ( !c || !$(c).hasClass("coordinates-title") ) return ;`

` var a = c.getElementsByTagName ( 'a' ) ;`
` var geohack = false;`
` for ( var i = 0 ; i < a.length ; i++ ) {`
`   var h = a[i].href ;`
`   if ( !h.match(/geohack/) ) continue ;`
`   if (h.match(/skyhack/)) continue;`
`   if (h.match(/_globe:/)) continue; // no OSM for moon, mars, etc`
`   geohack = true ;`
`   break ;`
` }`
` if ( !geohack ) return ;`

` var na = document.createElement ( 'a' ) ;`
` na.href = '`<javascript:openStreetMap_Toggle>`();' ;`
` na.title = wgULS( '显示/隐藏地图', '顯示/隱藏地圖' ) ;`
` na.appendChild ( document.createTextNode ( wgULS( '地图', '地圖' ) ) ) ;`
` c.appendChild ( document.createTextNode ( '（' ) ) ;`
` c.appendChild ( na ) ;`
` c.appendChild ( document.createTextNode ( '）' ) ) ;`

}

function openStreetMap_Toggle () {

` var c = document.getElementById ( 'coordinates' ) ;`
` if ( !c || !$(c).hasClass("coordinates-title") ) return ;`
` var osm = document.getElementById ( 'OpenStreetMap' ) ;`

` if (osm) {`
`   if ( osm.style.display == 'none' ) {`
`     osm.style.display = 'block' ;`
`   } else {`
`     osm.style.display = 'none' ;`
`   }`
`   return;`
` }`

` var found_link = false ;`
` var a = c.getElementsByTagName ( 'a' ) ;`
` var h;`
` for ( var i = 0 ; i < a.length ; i++ ) {`
`   h = a[i].href ;`
`   if ( !h.match(/geohack/) ) continue ;`
`   if (h.match(/skyhack/)) continue;`
`   if (h.match(/_globe:/)) continue; // no OSM for moon, mars, etc`
`   found_link = true ;`
`   break ;`
` }`
` if ( !found_link ) return ; // No geohack link found`

` h = h.split('params=')[1] ;`

` var LargeurEcran = MoveResizeAbsolute_GetScreenWidth();`
` var HauteurEcran = MoveResizeAbsolute_GetScreenHeight();`

` var OSMDiv = document.createElement('div');`
` OSMDiv.id = 'OpenStreetMap' ;`
` OSMDiv.style.position = "absolute";`
` OSMDiv.style.zIndex = 5000;`
` OSMDiv.style.top = (HauteurEcran*10/100) + "px";`
` OSMDiv.style.left = (LargeurEcran*15/100) + "px";`
` OSMDiv.style.width = "70%";`
` OSMDiv.style.height = (HauteurEcran*80/100) + "px";`
` OSMDiv.style.border = "2px solid black";`
` OSMDiv.style.backgroundColor = "white";`
` OSMDiv.style.overflow = "hidden";`

` var MoveArea = document.createElement('div');`
` MoveArea.style.position = "relative";`
` MoveArea.style.top = "0";`
` MoveArea.style.width = "100%";`
` MoveArea.style.height = "50px";`
` MoveArea.title = wgULS( '拖动以移动地图', '拖動以移動地圖' );`

` var CloseLink = document.createElement('a');`
` CloseLink.setAttribute("style", "float:right;margin:10px;");`
` CloseLink.innerHTML = wgULS( '隐藏', '隱藏' );`
` CloseLink.title = wgULS( '点击以隐藏地图', '點擊以隱藏地圖' );`
` CloseLink.href = "`<javascript:openStreetMap_Toggle>`();";`
` MoveArea.appendChild(CloseLink);`

` var iFrame = document.createElement ( 'iframe' ) ;`
` var url = '//toolserver.org/~kolossos/openlayers/kml-on-ol.php?'`
`         + 'lang=' + mw.config.get('wgUserLanguage')`
`         + '&params=' + h`
`         + '&title=' + mw.util.wikiUrlencode( mw.config.get( 'wgTitle' ) )`
`         + ( window.location.protocol == 'https:' ? '&secure=1' : '' ) ;`
` iFrame.style.width = '100%' ;`
` iFrame.style.height = ((HauteurEcran*80/100)-100) + 'px' ;`
` iFrame.style.clear = 'both' ;`
` iFrame.src = url ;`

` var ResizeArea = document.createElement('div');`
` ResizeArea.style.position = "relative";`
` ResizeArea.style.top = "0";`
` ResizeArea.style.width = "100%";`
` ResizeArea.style.height = "50px";`
` ResizeArea.title = wgULS( '拖动以改变地图大小', '拖動以改變地圖大小' );`

` OSMDiv.appendChild(MoveArea);`
` OSMDiv.appendChild(iFrame);`
` OSMDiv.appendChild(ResizeArea);`

` document.body.appendChild ( OSMDiv ) ;`

` var ElementsToMove = new Array(OSMDiv);`
` var ElementsToResize = new Array(OSMDiv, iFrame);`
` var ElementsMinWidth = new Array(150, 150);`
` var ElementsMinHeights = new Array(200, 100);`

` MoveResizeAbsolute_AddMoveArea(MoveArea, ElementsToMove);`
` MoveResizeAbsolute_AddResizeArea(ResizeArea, ElementsToResize, ElementsMinWidth, ElementsMinHeights);`

}

$(openStreetMap_Init);

window.openStreetMap_Toggle = openStreetMap_Toggle;