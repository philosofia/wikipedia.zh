/\*\*

`* Dynamic Navigation Bars. See `[`Wikipedia:NavFrame`](https://zh.wikipedia.org/wiki/Wikipedia:NavFrame "wikilink")
`* `
`* Based on script from en.wikipedia.org, 2008-09-15.`
`*`
`* @source www.mediawiki.org/wiki/MediaWiki:Gadget-NavFrame.js`
`* @maintainer Helder.wiki, 2012–2013`
`* @maintainer Krinkle, 2013`
`* @maintainer Fantasticfears, 2013-2014`
`*/`

( function () {

var collapseCaption = wgULS('隐藏', '隱藏'); var expandCaption = wgULS('显示',
'顯示');

var navigationBarHide = collapseCaption + '▲'; var navigationBarShow =
expandCaption + '▼';

/\*\*

`* Shows and hides content and picture (if available) of navigation bars.`
`*`
`* @param {number} indexNavigationBar The index of navigation bar to be toggled`
`* @param {jQuery.Event} e Event object`
`*/`

function toggleNavigationBar( indexNavigationBar, e ) {

`       var toggle = $( '#NavToggle' + indexNavigationBar ),`
`               frame = $( '#NavFrame' + indexNavigationBar ),`
`               isFrameCollapsed;`

`       if ( !frame || !toggle ) {`
`               return false;`
`       }`

`   isFrameCollapsed = frame.hasClass( 'collapsed' );`
`       if ( isFrameCollapsed ) {`
`               frame.find( '> .NavPic, > .NavContent, > .toogleShow' ).each( function() {`
`                       $( this ).css( 'display', 'block' );`
`               });`
`               frame.find( '> .toggleHide' ).each( function() {`
`                       $( this ).css( 'display', 'none' );`
`               });`
`               toggle.text( navigationBarHide );`
`               frame.removeClass( 'collapsed' );`
`       } else {`
`               frame.find( '> .NavPic, > .NavContent, > .toogleShow' ).each( function() {`
`                       $( this ).css( 'display', 'none' );`
`               });`
`               frame.find( '> .toggleHide' ).each( function() {`
`                       $( this ).css( 'display', 'block' );`
`               });`
`               toggle.text( navigationBarShow );`
`               frame.addClass( 'collapsed' );`
`       }`

}

/\*\*

`* Adds show/hide-button to navigation bars.`
`*`
`* @param {jQuery} $content`
`*/`

function createNavigationBarToggleButton( $content ) {

`       // Iterate over all (new) nav frames`
`       $content.find( 'div.NavFrame' ).each( function( indexNavigationBar ) {`
`               var frame = $( this ).attr( 'id', 'NavFrame' + indexNavigationBar );`
`               // If found a navigation bar`
`               var navToggle = $( '`<span class="NavToggle" id="NavToggle' + indexNavigationBar + '"></span>`' );`
`               frame.find( '> .NavHead' ).each( function() {`
`                       $( this ).on( 'click', $.proxy( toggleNavigationBar, null, indexNavigationBar ) );`
`                   return false;`
`       });`
`               if ( frame.hasClass( 'collapsed' ) ) {`
`                       frame.find( '> .NavPic, > .NavContent, > .toggleHide' ).each( function() {`
`                               $( this ).css( 'display', 'none' );`
`                       });`
`               } else {`
`                       frame.find( '> .toggleShow' ).each( function() {`
`                               $( this ).css( 'display', 'none' );`
`                       });`
`               }`

`               var showNavigationBarHide = true;`
`               frame.find( '> .NavPic, > .NavContent' ).each( function() {`
`                       if ( $( this ).css( 'display' ) === 'none' ) {`
`                               showNavigationBarHide = false;`
`                               return false;`
`                       }`
`               });`

`               navToggle.text( showNavigationBarHide? navigationBarHide: navigationBarShow );`

`               frame.find( '> .NavHead' ).each( function() {`
`                       $( this ).append( navToggle );`
`                       return false;`
`               });`
`       });`

}

`       mw.hook( 'wikipage.content' ).add( createNavigationBarToggleButton );`

}());