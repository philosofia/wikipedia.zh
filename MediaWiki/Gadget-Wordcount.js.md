> 本文内容由[MediaWiki:Gadget-Wordcount.js](https://zh.wikipedia.org/wiki/MediaWiki:Gadget-Wordcount.js)转换而来。


`   (function($) {`
`       function bytecount(text) {`
`           text = text.replace(/[\u0000-\u007F]/g, '.');`
`           text = text.replace(/[\u0080-\u07FF\uD800-\uDFFF]/g, '..');`
`           text = text.replace(/[\u0800-\uD7FF\uE000-\uFFFF]/g, '...');`
`           return text.length;`
`       };`
`       function cjkcount(text) {`
`           text = text.replace(/\./g, '');`
`           text = text.replace(/[\u2E80-\u2E99\u2E9B-\u2EF3\u2F00-\u2FD5\u3005\u3007\u3021-\u3029\u3038-\u303B\u3400-\u4DB5\u4E00-\u9FCC\uF900-\uFA6D\uFA70-\uFAD9]|[\uD840-\uD868][\uDC00-\uDFFF]|\uD869[\uDC00-\uDED6\uDF00-\uDFFF]|[\uD86A-\uD86C][\uDC00-\uDFFF]|\uD86D[\uDC00-\uDF34\uDF40-\uDFFF]|\uD86E[\uDC00-\uDC1D]|\uD87E[\uDC00-\uDE1D]/g, '.');`
`           text = text.replace(/[^\.]/g, '');`
`           return text.length;`
`       };`
`       function getwcbytext(text) {`
`           return text.length + ' character(s) (' + cjkcount(text) + ' CJK)`
`' +`
`               bytecount(text) + ' byte(s) in `<a href="' +  mw.config.get('wgScript') + '?title=UTF-8">`UTF-8`</a>` encoding';`
`       };`
`       function getsel() {`
`           if (!window.getSelection) return '';`
`           return getSelection().toString();`
`       };`
`       function dowc(event) {`
`           $('.wordcount').remove(); // or remove after text.length == 0 checking?`
`           var text = getsel();`
`           if (text.length == 0) return;`
`           var divj = $('`

<div />

').html(getwcbytext(text))

`               .css({`
`                   'position': 'fixed',`
`                   'right': '0',`
`                   'bottom': '0',`
`                   'margin': '4px',`
`                   'padding': '6px'`
`               })`
`               .addClass('wordcount ui-state-highlight ui-corner-all')`
`               .appendTo('body');`
`               // we hook keyup, so this may make it flickering`
`               // eg when shift, ctrl.etc key up`
`               //.hide().fadeIn('slow');`
`           setTimeout(function() {`
`               divj.fadeOut('slow');`
`           }, 5000);`
`       };`
`       $(document).mouseup(dowc).keyup(dowc);`
`   })(jQuery);`