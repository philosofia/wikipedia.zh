(function ($, mw) { $( function() {

`   /** Advanced Site Notices ********`
`    * Allow to custom dynamic site notices`
`    * Maintainer: `[`User:PhiLiP`](https://zh.wikipedia.org/wiki/User:PhiLiP "wikilink")
`    */`
`   if (typeof(window.customASNInterval) == 'undefined') {`
`       window.customASNInterval = 15;`
`   }`
`   $(function () {`
`       if (window.closeASNForever || mw.config.get('wgAction') == 'edit' || mw.config.get('wgAction') == 'submit') {`
`           return;`
`       }`

`       var ln = $('#siteNotice');`
`       if (!ln.length) {`
`           return;`
`       }`
`       var cname = 'dismissASN';`
`       var cval = $.cookie(cname);`
`       if (cval == '') {`
`           cval = -1;`
`       }`
`       var rev = 0;`
`       var toid = null;`

`       var tb = $('`

<table id="asn-dismissable-notice" width="100%" style="background: transparent;"/>

');

`       var ct = $('`

<div id="advancedSiteNotices" style="word-break: break-word;" class="mw-parser-output"/>

');

`       var sd = $('`<a href="#">`' + wgULS('关闭', '關閉') + '`</a>`');`
`       tb.append($('`

<tr/>

').append($('

<td/>

').append(ct)).append($('

<td/>

').append('\[').append(sd).append('\]')));

`       var nts = null;`
`       var styles = [];`

`       sd.click(function () {`
`           $.cookie(cname, rev, {`
`               expires: 30,`
`               path: '/'`
`           });`
`           clearTimeout(toid);`
`           tb.remove();`
`           return false;`
`       });`

`       var matchCriteria = function( nt ) {`
`           var cache = nt.data( 'asn-cache' );`
`           if ( cache !== undefined ) {`
`               return cache;`
`           }`
`           var criteria = nt.attr( 'data-asn-criteria' );`
`           if ( criteria === undefined ) {`
`               criteria = nt.attr( 'class' ) ? 'false' : 'true';`
`               if ( nt.hasClass('only_sysop') ) {`
`                   criteria += '||in_group("sysop")';`
`               }`
`               if ( nt.hasClass('only_logged') ) {`
`                   criteria += '||in_group("user")';`
`               }`
`               if ( nt.hasClass('only_anon') ) {`
`                   criteria += '||!in_group("user")';`
`               }`
`               if ( nt.hasClass('only_zh_cn') ) {`
`                   criteria += '||only_for("zh-cn")';`
`               }`
`               if ( nt.hasClass('only_zh_hk') ) {`
`                   criteria += '||only_for("zh-hk")';`
`               }`
`               if ( nt.hasClass('only_zh_sg') ) {`
`                   criteria += '||only_for("zh-sg")';`
`               }`
`               if ( nt.hasClass('only_zh_tw') ) {`
`                   criteria += '||only_for("zh-tw")';`
`               }`
`           } else {`
`               criteria = decodeURIComponent( criteria.replace(/\+/g, '%20') );`
`               criteria = $.trim( criteria );`
`           }`
`           if ( criteria === '' ) {`
`               criteria = 'true';`
`           }`
`           var testCriteria = function() {`
`               var in_country = function( country ) {`
`                   return window.Geo === undefined || Geo.country === country;`
`               }, in_region = function( region ) {`
`                   return window.Geo === undefined || Geo.region === region;`
`               }, in_city = function( city ) {`
`                   return window.Geo === undefined || Geo.city === city;`
`               }, in_group = function( group ) {`
`                   return $.inArray( group, mw.config.get( 'wgUserGroups' ) ) > -1;`
`               }, only_for = function( userlang ) {`
`                   return userlang === mw.config.get('wgUserLanguage');`
`               };`
`               return eval( criteria );`
`           };`
`           cache = testCriteria();`
`           nt.data( 'asn-cache', cache );`
`           return cache;`
`       };`

`       var loadNotices = function (pos) {`
`           if (!tb.length) {`
`               return;`
`           }`
`           ct.css('min-height', ct.height() + 'px');`
`           tb.css('min-height', tb.height() + 'px');`
`           var l = nts.length;`
`           var nt = null;`
`           var rt = 0;`
`           while ( rt++ < l ) {`
`               nt = $( nts[pos] );`
`               if ( matchCriteria( nt ) ) {`
`                   break;`
`               }`
`               pos = (pos + 1) % l;`
`           }`
`           if ( rt >= l ) {`
`               return;`
`           }`
`           if ( typeof nt.data( 'asn-style' ) == 'string' ) {`
`               var style = mw.util.addCSS( decodeURIComponent( nt.data( 'asn-style' ).replace(/\+/g, '%20') ) );`
`               nt.data( 'asn-style', null );`
`               nt.data( 'asn-style-id', styles.length );`
`               style.disabled = true;`
`               styles.push( style );`
`           }`
`           if ( typeof nt.data( 'asn-html' ) == 'string' ) {`
`               nt.data( 'asn-html-raw', decodeURIComponent( nt.data( 'asn-html' ).replace(/\+/g, '%20') ) );`
`               nt.data( 'asn-html', null );`
`           }`
`           var styleId = nt.data( 'asn-style-id' );`
`           nt = nt.data( 'asn-html-raw' ) || nt.html();`
`           var cthtml = ct.html();`
`           if ( cthtml ) {`
`               if ( cthtml !== nt ) {`
`                   ct.stop().fadeOut(function () {`
`                       $.each( styles, function() {`
`                           this.disabled = true;`
`                       } );`
`                       if ( styles[styleId] ) {`
`                           styles[styleId].disabled = false;`
`                       }`
`                       ct.html(nt).fadeIn();`
`                   });`
`               }`
`           } else if (rev == cval) {`
`               return;`
`           } else {`
`               $.cookie( cname, null );`
`               tb.appendTo(ln);`
`               if ( styles[styleId] ) {`
`                   styles[styleId].disabled = false;`
`               }`
`               ct.html(nt).fadeIn();`
`           }`
`           toid = setTimeout(function () {`
`               loadNotices( (pos + 1) % l );`
`           }, window.customASNInterval * 1000);`
`       };`

`       $.get(mw.util.wikiScript( 'api' ), {`
`           page: 'Template:AdvancedSiteNotices/ajax',`
`           variant: mw.config.get('wgUserVariant'),`
`           prop: 'text',`
`           action: 'parse',`
`           format: 'json',`
`           maxage: 3600,`
`           smaxage: 3600`
`       }, function (d) {`
`           d = $( '`

<div />

' ).html( d.parse.text\['\*'\] ).find( 'ul.sitents' );

`           nts = $('li', d);`
`           rev = d.data( 'asn-version' );`
`           var l = nts.length;`
`           loadNotices(Math.floor(Math.random() * l));`
`       });`
`   });`

}); })(jQuery, mediaWiki);