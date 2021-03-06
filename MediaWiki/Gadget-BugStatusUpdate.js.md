> 本文内容由[MediaWiki:Gadget-BugStatusUpdate.js](https://zh.wikipedia.org/wiki/MediaWiki:Gadget-BugStatusUpdate.js)转换而来。


/\*

`* Bug Status Update Gadget`
`*`
`* Authors:`
`* Written by Rob Moen (robm).`
`* Ported to Phabricator by Matthew Flaschen (Mattflaschen (WMF))`
`*`
`* Description:`
`*  Finds and updates bug status templates on a page.`
`*  Makes 1 JSONP request to phabricator-bug-status API (maintained by Matthew Flaschen)`
`*  (which passes the request to Phabricator's Conduit API)`
`* Source: `[`mw:User:Robmoen/bugStatusUpdate.js`](https://zh.wikipedia.org/wiki/mw:User:Robmoen/bugStatusUpdate.js "wikilink")
`*/`

( function( $ ){

`   var ids = [],`
`       target = '`<https://tools.wmflabs.org/phabricator-bug-status/queryTasks>`';`

`   var getParams = function( ids ) {`
`       return $.param( { ids: JSON.stringify( ids ) } );`
`   };`

`   // Get the Phabricator task id numbers on the page`
`   // The template should provide a data attribute, for simplicity and probably better performance.  There`
`   // should also be a class, so it could quickly be found.  E.g.`
`   // data-phabricator-task="123" class="trakfab ..." ...`
`   // This could then be selected easily, and the number could be accessed with .data( 'phabricatorTask' )`
`   $( '.mw-trackedTemplate a[title^="phabricator:T"]' ).each( function() {`
`       var titleMatch = $( this ).attr( 'title' ).match( /phabricator:T(\d*)/ );`
`       if ( titleMatch !== null ) {`
`           ids.push( parseInt( titleMatch[1], 10 ) );`
`       }`
`   });`

`   // Do not query if no ids were found`
`   if ( !ids.length ) {`
`       return;`
`   }`

`   // Make jsonp`
`   $.ajax( {`
`       url: target,`
`       dataType: 'jsonp',`
`       timeout: 5000, // Give up if Tool Labs is being slow today`
`       data: getParams( ids ),`
`       success: function ( data ) {`

`           var     color = {`
`                       "resolved": "green"`
`                   },`
`                   statusProps = {`
`                       'font-weight': 'bold',`
`                       'text-transform': 'uppercase'`
`                   },`
`                   phid, taskInfo, taskNumber, selector,`
`                   trackedTemplate, $taskLink, $title, $item,`
`                   $status;`

`           for( phid in data ) {`
`               taskInfo = data[phid];`
`               taskNumber = taskInfo.id;`
`               // Find the right task to update`
`               selector = '.mw-trackedTemplate a[title^="phabricator:T' +  taskNumber + '"]';`
`               $taskLink = $( selector );`
`               $title = $taskLink.find( '.trakfab-T' + taskNumber );`
`               if ( $title ) {`
`                   $title.text( taskInfo.title );`
`               }`

`               $item = $taskLink.closest( '.mw-trackedTemplate' );`
`               if( $item ) {`
`                   // Find child, if exists`
`                   // This is very fragile; this needs a class.`
`                   $status = $item.children( 'span' );`

`                   // Create the status element if it does not exist`
`                   if( $status.length === 0 ) {`
`                       $status = $( '`<span></span>`' )`
`                           .css( statusProps );`
`                       $item.append( '`
`', $status );`
`                   }`

`                   // Update the status element`
`                   // This matches Template:Tracked itself, where only resolved has a color`
`                   // defined for Phabricator (everything else is black).`
`                   $status`
`                       .text( taskInfo.statusName )`
`                       .css( 'color', color[taskInfo.status] || 'black' );`
`               }`
`           }`
`       }`
`   } );`

})( jQuery );