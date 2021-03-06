> 本文内容由[MediaWiki:Gadget-CX-Template Translated page.js](https://zh.wikipedia.org/wiki/MediaWiki:Gadget-CX-Template_Translated_page.js)转换而来。


( function( $, mw, undefined ) {

`   mw.hook( 'mw.cx.translation.published' ).add( function( sourceLanguage, targetLanguage, sourceTitle, targetTitle ) {`
`       var article = new mw.Title( targetTitle );`
`       var talk = new mw.Title( article.getMainText(), article.getNamespaceId() | 1 );`
`       var sourceTitleArg = sourceTitle.indexOf( '=' ) == -1 ? sourceTitle : '2=' + sourceTitle;`
`       var template = '{\{Translated page|' + sourceLanguage + '|' + sourceTitleArg + '|version=' + mw.cx.sourceRevision + '}\}\n';`
`       var api = new mw.Api(), tries = 0;`
`       `
`       var addTemplate = function() {`
`           if ( tries++ > 10 ) {`
`               mw.notify( '为' + talk.getPrefixedText() + '标记Translated page模板失败。' );`
`               return;`
`           }`
`           api.get( {`
`               action: 'query',`
`               prop: 'revisions',`
`               titles: talk.getPrefixedText(),`
`               rvprop: [ 'timestamp', 'content' ],`
`               indexpageids: true,`
`               curtimestamp: true`
`           } ).done( function( data ) {`
`               if ( !data.query ) {`
`                   addTemplate();`
`                   return;`
`               }`
`               var revision = ( data.query.pages[data.query.pageids[0]].revisions || [] )[0] || {}, params = {`
`                   action: 'edit',`
`                   title: talk.getPrefixedText(),`
`                   summary: '为翻译页面标记{\{`[`Translated``   ``page`](https://zh.wikipedia.org/wiki/Template:Translated_page "wikilink")`}\}',`
`                   starttimestamp: data.curtimestamp`
`               }, text = revision['*'];`
`               if ( text !== undefined ) {`
`                   params.basetimestamp = revision.timestamp;`
`                   // TODO: extend regex to include more aliases`
`                   params.text = template + text.replace( /\{\{\s*Translated page\s*\|[^\{\}]+\}\}\n?/g, '' );`
`               } else {`
`                   params.createonly = true;`
`                   params.text = template;`
`               }`
`               api.postWithEditToken( params ).done( function( data ) {`
`                   if ( !data.edit || data.edit.result !== 'Success' ) {`
`                       addTemplate();`
`                       return;`
`                   }`
`                   mw.notify( '已为' + talk.getPrefixedText() + '标记Translated page模板。' );`
`               } ).fail( addTemplate );`
`           } ).fail( addTemplate );`
`       };`
`       addTemplate();`
`   } );`

} )( jQuery, mediaWiki );