/\* 所有用戶在加載任何頁面時，這裡的JavaScript都會加載

  - /

mw.log.deprecate( window, 'JSConfig', {} );

mw.loader.using(\['mediawiki.util', 'ext.gadget.site-lib'\], function ()
{

` (function ($, mw) {`

`   /* 當需要時載入對應的 scripts */`
`   var importScriptRL=function(page){`
`       mw.loader.load(mw.config.get('wgScript')+'?title='+mw.util.wikiUrlencode(page)+'&action=raw&ctype=text/javascript&_='+Math.floor((new Date())/1000/60/60/24/7));`
`   };`
`   `
`   if (mw.config.get('wgAction') == "edit" || mw.config.get('wgAction') == "submit" || mw.config.get('wgCanonicalSpecialPageName') == 'Search') { // scripts specific to editing pages`
`     importScriptRL('MediaWiki:Common.js\/edit.js');`
`   }`

`   // wiki URL`
`   window.wgProjectURL = {`
`     en: '//en.wikipedia.org',`
`     de: '//de.wikipedia.org',`
`     fr: '//fr.wikipedia.org',`
`     pl: '//pl.wikipedia.org',`
`     ja: '//ja.wikipedia.org',`
`     it: '//it.wikipedia.org',`
`     nl: '//nl.wikipedia.org',`
`     pt: '//pt.wikipedia.org',`
`     es: '//es.wikipedia.org',`
`     sv: '//sv.wikipedia.org',`
`     // 僅列前十名其它語言百科`
`     m: '//meta.wikimedia.org',`
`     b: '//zh.wikibooks.org',`
`     q: '//zh.wikiquote.org',`
`     n: '//zh.wikinews.org',`
`     wikt: '//zh.wiktionary.org',`
`     mw: '//www.mediawiki.org',`
`     commons: '//commons.wikimedia.org'`
`   };`

`   /**`
`    * Helper script for .hlist class in Common.css`
`    * Add pseudo-selector class to last-child list items in IE8`
`    * @source mediawiki.org/wiki/Snippets/Horizontal_lists`
`    * @revision 6 (2014-08-23)`
`    * @author `[`User:Edokter`](../Page/User:Edokter.md "wikilink")
`    */`
`   var profile = $.client.profile();`
`   if ( profile.name === 'msie' && profile.versionNumber === 8 ) {`
`       mw.hook( 'wikipage.content' ).add( function ( $content ) {`
`           $content.find( '.hlist' ).find( 'dd:last-child, dt:last-child, li:last-child' )`
`               .addClass( 'hlist-last-child' );`
`       } );`
`   }`

`   /* Fixes for Windows XP font rendering */`
`   if (navigator.appVersion.search(/windows nt 5/i) != -1) {`
`       mw.util.addCSS('.IPA {font-family: "Lucida Sans Unicode", "Arial Unicode MS";} ' + `
`                      '.Unicode {font-family: "Arial Unicode MS", "Lucida Sans Unicode";}');`
`   }`
`   `

`   // 修正摺疊後定位變化`
`   $(function () {`
`     if (location.hash) {`
`       location.href = location.hash;`
`     }`
`   });`

`   /* 避免在主條目的註腳中出現捲軸框 */`
`   if (!mw.config.get("wgCanonicalNamespace")) $(function () {`
`       `
`       $("div#mw-content-text ol.references")`
`       .each(function(){`
`           var needobjs=[], $curobj=$(this);`
`           `
`           do{`
`               $curobj=$curobj.parent();`
`               if( !$curobj ) break;`
`               if( $curobj.attr("id")=="mw-content-text" || $curobj.prop("tagName").toLowerCase()=="body") break;`
`               `
`               if(`
`                   $curobj.css("overflow").match(/(?:auto|scroll)/i)`
`                   || $curobj.css("overflow-x").match(/(?:auto|scroll)/i)`
`                   || $curobj.css("overflow-y").match(/(?:auto|scroll)/i)`
`               ){}else continue;`
`               `
`               if( (""+$curobj.attr("class")).split(" ").indexOf("noprint")>=0 ) return;`
`               `
`               needobjs.push($curobj.get(0));`
`               `
`           }while(true);`
`       `
`           $(needobjs)`
`           .css("overflow","visible")`
`           .css("overflow-x","visible")`
`           .css("overflow-y","visible")`
`           .css("height","")`
`           .css("max-height","")`
`           .css("border","")`
`           ;`
`       });`
`   });`

`   /** metaBox`
`    *`
`    * Funcionament de la Plantilla:Metacaixa`
`    * Implementat per: Usuari:Peleguer.`
`    * Actualitzat per Joanjoc seguint les indicacions d'en Martorell`
`    */`
`   function MetaCaixaInit() {`
`     // S'executa al carregar-se la pàgina, si hi ha metacaixes,`
`     // s'assignen els esdeveniments als botons`
`     //alert("MetaCaixaInit");`
`     var i = 0; // Inicialitzem comptador de caixes`
`     for (i = 0; i <= 9; i++) {`
`       var vMc = document.getElementById("mc" + i);`
`       if (!vMc) break;`
`       //alert("MetaCaixaInit, trobada Metacaixa mc"+i);`
`       var j = 1; // Inicialitzem comptador de botons dins de la caixa`
`       var vPsIni = 0; // Pestanya visible inicial`
`       for (j = 1; j <= 9; j++) {`
`         var vBt = document.getElementById("mc" + i + "bt" + j);`
`         if (!vBt) break;`
`         //alert("MetaCaixaInit, trobat botó mc"+i+"bt"+j);`
`         vBt.onclick = MetaCaixaMostraPestanya; // A cada botó assignem l'esdeveniment onclick`
`         //alert (vBt.className);`
`         if (vBt.className == "mcBotoSel") vPsIni = j; // Si tenim un botó seleccionat, en guardem l'index`
`       }`
`       //alert ("mc="+i+", ps="+j+", psini="+vPsIni );`
`       if (vPsIni === 0) { // Si no tenim cap botó seleccionat, n'agafem un aleatòriament`
`         vPsIni = 1 + Math.floor((j - 1) * Math.random());`
`         //alert ("Activant Pestanya a l'atzar; _mc"+i+"bt"+vPsIni +"_");`
`         document.getElementById("mc" + i + "ps" + vPsIni).style.display = "block";`
`         document.getElementById("mc" + i + "ps" + vPsIni).style.visibility = "visible";`
`         document.getElementById("mc" + i + "bt" + vPsIni).className = "mcBotoSel";`
`       }`
`     }`
`   }`

`   function MetaCaixaMostraPestanya() {`
`     // S'executa al clicar una pestanya,`
`     // aquella es fa visible i les altres s'oculten`
`     var vMcNom = this.id.substr(0, 3); // A partir del nom del botó, deduïm el nom de la caixa`
`     var vIndex = this.id.substr(5, 1); // I l'index`
`     var i = 1;`
`     for (i = 1; i <= 9; i++) { // busquem totes les pestanyes d'aquella caixa`
`       //alert(vMcNom+"ps"+i);`
`       var vPsElem = document.getElementById(vMcNom + "ps" + i);`
`       if (!vPsElem) break;`
`       if (vIndex == i) { // Si és la pestanya bona la mostrem i canviem la classe de botó`
`         vPsElem.style.display = "block";`
`         vPsElem.style.visibility = "visible";`
`         document.getElementById(vMcNom + "bt" + i).className = "mcBotoSel";`
`       } else { // Sinó, l'ocultem i canviem la classe de botó`
`         vPsElem.style.display = "none";`
`         vPsElem.style.visibility = "hidden";`
`         document.getElementById(vMcNom + "bt" + i).className = "mcBoto";`
`       }`
`     }`
`     return false; // evitem la recàrrega de la pàgina`
`   }`
`   $(MetaCaixaInit);`

`   /* 智能讨论页编辑（新建） */`
`   $(function () {`
`     var catalk = $('#ca-talk');`
`     if (catalk.hasClass('new') && mw.config.get('wgNamespaceNumber') != 2) {`
`       var a = $('a:first', catalk);`
`       a.attr('href', a.attr('href') + '&section=new');`
`     }`
`   });`

/\*\*

`* Magic editintros ****************************************************`
`*`
`* Description: Adds editintros on disambiguation pages, BLP pages, policy pages and guidlines.`
`* Maintainers: `[`User:RockMFR`](../Page/User:RockMFR.md "wikilink")
`*/`

function addEditIntro( name ) {

`   $( '.mw-editsection, #ca-edit' ).find( 'a' ).each( function ( i, el ) {`
`       el.href = $( this ).attr( 'href' ) + '&editintro=' + name;`
`   } );`

}

if ( mw.config.get( 'wgNamespaceNumber' ) === 0 ) {

`   $( function () {`
`       if ( document.getElementById( 'disambigbox' ) ) {`
`           addEditIntro( 'Template:Disambig_editintro' );`
`       }`
`   } );`

`   $( function () {`
`       var cats = mw.config.get('wgCategories');`
`       if ( !cats ) {`
`           return;`
`       }`
`       if ( $.inArray( '在世人物', cats ) !== -1 ) {`
`           addEditIntro( 'Template:BLP_editintro' );`
`       }`
`   } );`

} else if ( mw.config.get( 'wgNamespaceNumber' ) === 4 ) {

`   $( function () {`
`       var cats = mw.config.get('wgCategories');`
`       if ( !cats ) {`
`           return;`
`       }`
`       if ( $.inArray( '维基百科方针', cats ) !== -1 ||`
`           $.inArray( '维基百科指引', cats ) !== -1 ||`
`           $.inArray( '维基百科方针与指引', cats ) !== -1) {`
`               addEditIntro( 'Template:Policy editintro' );`
`           }`
`   } );`

}

`   /* 引用錯誤標籤名字解碼 */`
`   $(function () {`
`     $('.anchordecodeme').each(function () {`
`       $(this).text(decodeURIComponent($(this).text().replace(/\.([0-9A-F]{2})/g, '%$1')));`
`     });`
`   });`

`   /** &withCSS= and &withJS= URL parameters`
`    * Allow to try custom scripts from MediaWiki space `
`    * without editing personal .css or .js files`
`    */`

/\*\*

`* @source www.mediawiki.org/wiki/Snippets/Load_JS_and_CSS_by_URL`
`* @rev 6`
`*/`

var extraCSS = mw.util.getParamValue( 'withCSS' ),

`   extraJS = mw.util.getParamValue( 'withJS' );`

if ( extraCSS ) {

`   if ( extraCSS.match( /^MediaWiki:[^&<>=%#]*\.css$/ ) ) {`
`       importStylesheet( extraCSS );`
`   } else {`
`       mw.notify( '只允许从MediaWiki名字空间加载。', { title: '无效的withCSS值' } );`
`   }`

}

if ( extraJS ) {

`   if ( extraJS.match( /^MediaWiki:[^&<>=%#]*\.js$/ ) ) {`
`       importScript( extraJS );`
`   } else {`
`       mw.notify( '只允许从MediaWiki名字空间加载。', { title: '无效的withJS值' } );`
`   }`

}

`   /* 页面历史加&hilight=高亮 */`
`   {`
`      var hilight = mw.util.getParamValue('hilight');`
`      if (mw.config.get('wgAction') === 'history' && hilight) {`
`         $.each(hilight.split(','), function (_, v) {`
`            $('input[name=oldid][value=' + v + ']').parent().addClass('not-patrolled');`
`         });`
`      }`
`   }`

`   /* Main page hacks */`
`   if ( mw.config.get( 'wgIsMainPage' ) && mw.config.get( 'wgAction' ) == 'view' ) {`
`       /* 维基百科语言列表 */`
`       $( function () {`
`           mw.util.addPortletLink(`
`               'p-lang',`
`               mw.util.getUrl( 'Wikipedia:维基百科语言列表' ),`
`               wgULS( '维基百科语言列表', '維基百科語言列表' ),`
`               'interwiki-completelist',`
`               wgULS( '维基百科的完整各语言列表', '維基百科的完整各語言列表' )`
`           );`
`       } );`
`       /* Remove red links */`
`       $( '#mw-content-text a.new' ).contents().unwrap();`
`   }`
` })(jQuery, mediaWiki);`

});

/\* Check for any client-side simplified/traditional Chinese conversion
\*/ /\* This routine must be placed here to make sure the field is
inserted in time \*/ $('\#antispam-container').append(

`   $('`<input type="text" />`').attr({`
`       id: 'wpAntiConv',`
`       value: '\u6c49\u6f22'`
`   })`

);

//临时修复！侧边栏的“打印页面”移动到“打印/导出”章节
$('div\#p-electronPdfService-sidebar-portlet-heading div.body
ul').append($('li\#t-print'));