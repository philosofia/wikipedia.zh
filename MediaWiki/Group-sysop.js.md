/\* Any JavaScript here will be loaded for sysops only \*/

mw.loader.using('ext.gadget.site-lib', function(){

`   //保護選項校正`
`   if (mw.config.get('wgAction') == "protect") {`

`       $(function () {`
`           var pform = document.getElementById("mw-Protect-Form");`
`           var timeoptions;`

`           timeoptions = pform["wpProtectExpirySelection-edit"].options;`
`           if (timeoptions[0].value != "existing") {`
`               timeoptions[timeoptions.length - 1].selected = true;`
`               ProtectionForm.updateExpiryList(pform["wpProtectExpirySelection-edit"]);`
`           }`

`           timeoptions = pform["wpProtectExpirySelection-move"].options;`
`           if (timeoptions[0].value != "existing") {`
`               timeoptions[timeoptions.length - 1].selected = true;`
`               ProtectionForm.updateExpiryList(pform["wpProtectExpirySelection-move"]);`
`           }`

`       });`

`   }`

`   //擷取選單文字按鈕`
`   $(function () {`

`       var addGetMenuTextButton = function (id, $srcMenu, $targetText, tiptext, afterSelIdx) {`
`           if($srcMenu.length==0 || $targetText.length==0) return null;`

`           var $btnAdd = $('`<input type="button">`', {`
`               'id': id,`
`               'name': id`
`           }).attr("value", ((!tiptext) ? "(+)" : tiptext) );`

`           $btnAdd.get(0).srcMenu = $srcMenu.get(0);`
`           $btnAdd.get(0).targetText = $targetText.get(0);`
`           $btnAdd.get(0).afterSelIdx = (!afterSelIdx || isNaN(afterSelIdx)) ? 0 : afterSelIdx;`

`           $btnAdd.click( function () {`
`               this.targetText.value += this.srcMenu.options[this.srcMenu.selectedIndex].value;`
`               this.srcMenu.selectedIndex = this.afterSelIdx;`
`           }).insertAfter($srcMenu);`

`           return $btnAdd;`
`       }`

`       if (mw.config.get('wgAction').match(/(?:un)?protect/i)) { //保護理由`
`           addGetMenuTextButton("wpProtectReasonSelectionAdd", $("form[id='mw-Protect-Form'] select#wpProtectReasonSelection"), $("form[id='mw-Protect-Form'] input[id='mwProtect-reason']"), "加到附加的理由", 0);`
`       } else if (("" + mw.config.get('wgCanonicalSpecialPageName')).match(/block(?:ip)?/i) ) { //封禁理由`
`           mw.loader.using('jquery.colorUtil').then(function() {`
`               var button = new OO.ui.ButtonInputWidget({`
`                   label: wgULS("加到附带原因", "加到附帶原因"),`
`               }).on('click', function() {`
`                   if ($('form select[name="wpReason"]')[0].options[$("form select[name='wpReason']")[0].selectedIndex].value== 'other') return;`
`                   $('[name="wpReason-other"]')[0].value = $('form select[name="wpReason"]')[0].options[$("form select[name='wpReason']")[0].selectedIndex].value + '：' + $('[name="wpReason-other"]')[0].value;`
`                   $("form select[name='wpReason']")[0].selectedIndex = $("form select[name='wpReason'] option[value='other']")[0].index;`
`               });`
`               $('#mw-input-wpReason-select').append(button.$element);`
`           });`
`       }`

`   });`

});