> 本文内容由[MediaWiki:Gadget-EditToolbarThunks.js](https://zh.wikipedia.org/wiki/MediaWiki:Gadget-EditToolbarThunks.js)转换而来。


if ((mw.config.get('wgAction') == 'edit' || mw.config.get('wgAction') == 'submit') && window.jQuery) {

`   window.addButton = true;`
`   window.mwCustomEditButtons = [];`
`   window.ettSetup1a = {`
`       sections: {`
`           'oldbuttons': {`
`               type: 'toolbar',`
`               label: '更多'`
`           }`
`       }`
`   };`
`   window.ettSetup1b = {`
`       sections: {`
`           'oldmenus': {`
`               type: 'toolbar',`
`               label: '菜单'`
`           }`
`       }`
`   };`
`   window.ettSetup2 = {`
`       section: 'oldbuttons',`
`       groups: {`
`           'buttons': {`
`               label: ''`
`           }`
`       }`
`   };`
`   window.ettSetup3 = {`
`       section: 'oldmenus',`
`       groups: {`
`           'menus': {`
`               label: ''`
`           }`
`       }`
`   };`
`   window.ettSetupButtons = {`
`       section: 'oldbuttons',`
`       group: 'buttons',`
`       tools: {}`
`   };`
`   window.ettSetupMenus = {`
`       section: 'oldmenus',`
`       group: 'menus',`
`       tools: {}`
`   };`
`   window.ettHasButtons = window.ettHadMenus = false;`
`   var convertAction = function(obj) {`
`       if ('action' in obj && jQuery.isFunction(obj.action)) {`
`           var callback = function(context) {`
`               obj.action();`
`               // from `<https://github.com/wikimedia/mediawiki-extensions-WikiEditor/blob/master/modules/jquery.wikiEditor.toolbar.js>
`               if ( typeof context.$iframe !== 'undefined' ) {`
`                   context.$iframe[0].contentWindow.focus();`
`               }`
`               // end`
`           };`
`           return {`
`               type: 'callback',`
`               execute: callback`
`           };`
`       } else {`
`           return {`
`               type: 'encapsulate',`
`               options: {`
`                   pre: obj.tagOpen,`
`                   peri: obj.sampleText,`
`                   post: obj.tagClose`
`               }`
`           };`
`       }`
`   };`
`   var convertDropdown = function(optionList) {`
`       var list = {};`
`       jQuery.each(optionList, function() {`
`           list[this.id] = {`
`               label: this.text,`
`               action: convertAction(this)`
`           };`
`       });`
`       return list;`
`   };`
`   /*`
`   jQuery(document).on('edittoolsAddDropdownMenu', function(event, name, label, optionList, attrs) {`
`       window.ettHasMenus = true;`
`       if (name in window.ettSetupMenus.tools) {`
`           jQuery.extend(window.ettSetupMenus.tools[name].list, convertDropdown(optionList));`
`       } else {`
`           window.ettSetupMenus.tools[name] = {`
`               label: label,`
`               type: 'select',`
`               list: convertDropdown(optionList)`
`           };`
`       }`
`   });`
`   // They will be added in the following function. */`
`   jQuery(document).on('edittoolsDropdownMenuAdd', function(event, name, label, attrs, text, value, tagOpen, sampleText, tagClose, summary, minor, action) {`
`       if (typeof(value) == 'undefined') {`
`           return;`
`       }`
`       window.ettHasMenus = true;`
`       if (!(name in window.ettSetupMenus.tools)) {`
`           window.ettSetupMenus.tools[name] = {`
`               label: label,`
`               type: 'select',`
`               list: {}`
`           };`
`       }`
`       window.ettSetupMenus.tools[name].list[value] = {`
`           label: text,`
`           action: convertAction({`
`               tagOpen: tagOpen,`
`               sampleText: sampleText,`
`               tagClose: tagClose,`
`               action: action`
`           })`
`       };`
`   });`
`   jQuery(document).on('edittoolsAddEditButton', function(event, name, attrs) {`
`       window.ettHasButtons = true;`
`       window.ettSetupButtons.tools[name] = {`
`           label: attrs.speedTip,`
`           type: 'button',`
`           icon: '//upload.wikimedia.org/wikipedia/commons/' + attrs.src,`
`           action: convertAction(attrs)`
`       };`
`   });`

$( function() {

// new method according to [usability:Toolbar customization](https://zh.wikipedia.org/wiki/usability:Toolbar_customization "wikilink"), begin

// Check that the toolbar is available if ( typeof $j \!= 'undefined' && typeof $.fn.wikiEditor \!= 'undefined' ) {

`   // Execute on load`
`   $( document ).ready( function() {`
`               if ( window.ettHasButtons ) {`
`                   $( '#wpTextbox1' ).wikiEditor( 'addToToolbar', window.ettSetup1a );`
`                   $( '#wpTextbox1' ).wikiEditor( 'addToToolbar', window.ettSetup2 );`
`                   $( '#wpTextbox1' ).wikiEditor( 'addToToolbar', window.ettSetupButtons );`
`               }`
`               if ( window.ettHasMenus ) {`
`                   $( '#wpTextbox1' ).wikiEditor( 'addToToolbar', window.ettSetup1b );`
`                   $( '#wpTextbox1' ).wikiEditor( 'addToToolbar', window.ettSetup3 );`
`                   $( '#wpTextbox1' ).wikiEditor( 'addToToolbar', window.ettSetupMenus );`
`               }`
`   } );`

}

// end

} );

}