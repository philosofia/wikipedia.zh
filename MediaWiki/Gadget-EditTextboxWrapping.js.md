/\*

` 本工具會在編輯框下增加勾選盒，讓用戶切換編輯框自動換行與否`

  - /

`   $(function(){`
`       var $wpTextbox1=$("form#editform[name='editform'] textarea#wpTextbox1[name='wpTextbox1']");`
`       if($wpTextbox1.length==0) return;`
`       `
`       var $chkIsWrap=$('`<input />`', {`
`           type    : "checkbox",`
`           name    : "chkIsWrap",`
`           id      : "chkIsWrap",`
`           checked : mw.util.getParamValue("nowrap")!=1`
`       });`
`       `
`       var $labIsWrap=$('`<label for="chkIsWrap" />`').text(wgULS("自动换行","自動換行"));`
`       $('`

<div style="text-align:right;" align="right" />

').append(\[$chkIsWrap, $labIsWrap\]).insertAfter($wpTextbox1);

`       var clickfunc=function(){`
`           var setWrap=function($target, wrap){`
`               if($target.get(0).wrap){`
`                   $target.attr("wrap", wrap);`
`               }else{`
`                   var $pos_mark=$("`

<div />

").insertAfter($target);

`                   $target.detach().attr("wrap", wrap).insertAfter($pos_mark);`
`                   $pos_mark.remove();`
`               }`
`           }`
`           `
`           setWrap($("form#editform[name='editform'] textarea#wpTextbox1[name='wpTextbox1']"), ($chkIsWrap.get(0).checked)?"SOFT":"OFF");`
`       }`
`       `
`       $chkIsWrap.click(clickfunc);`
`       clickfunc();`

`       var $editform=$("form#editform[name='editform']");`
`       $editform.find("input#wpPreview[name='wpPreview'], input#wpDiff[name='wpDiff']").click(function(){`
`           var nowrap=($chkIsWrap.get(0).checked)?0:1;`
`           $editform.attr("action", $editform.attr("action").replace(/\&nowrap\=[^\&\?\#]*($|\&)/g, "$1").replace(/\?nowrap\=[^\&\?\#]*(?:$|\&)/, "?").replace(/\?/,"?nowrap="+nowrap+"&").replace(/\&$/, "") );`
`       });`
`       `
`   });`