> 本文内容由[MediaWiki:Gadget-ViewSourceMode.js](https://zh.wikipedia.org/wiki/MediaWiki:Gadget-ViewSourceMode.js)转换而来。


/\*

` 此小工具為頁面提供源碼查看模式，在此模式下編輯框將被設為唯讀而不能編輯，模擬被全保護那般的狀態。`

  - /

mw.loader.using('ext.gadget.site-lib', function(){

`   var getParamValue=mw.util.getParamValue;`
`   var old_title, old_txt;`
`   `
`   //立即執行段 開始`
`   (function(){`
`       //如進入源碼模式`
`       if(mw.config.get('wgAction')=="edit" && getParamValue("viewsource")==1){}else return null; //如不是，離開`
`       `
`       //改變標題`
`       var viewSrcTitle="查看"+wgULS("“","「")+mw.config.get('wgPageName')+wgULS("”的源代码","」的原始碼")+((getParamValue("section")===null)?"":"（段落）");`
`       `
`       old_title=document.title;`
`       document.title=viewSrcTitle;`
`       var wikititle=old_title.split("-");`
`       if(wikititle.length>1) document.title+=" -"+wikititle[wikititle.length-1];`
`       `
`       //盡快將原版的編輯界面隱藏`
`       var hideBodyContent=function(){`
`           if($("div#bodyContent").addClass("realBodyContent").css("display", "none").length>0){`
`               old_txt=$("h1.firstHeading#firstHeading").text();`
`               $("h1.firstHeading#firstHeading").text(viewSrcTitle);`
`               return null;`
`           }`
`           `
`           setTimeout("hideBodyContent()", 1);`
`       };`
`       `
`       hideBodyContent();`
`       `
`   })();`
`   //立即執行段 結束`
`   `
`   `
`   //載入完成後執行段 開始`
`   $( function(){`
`       `
`       if(mw.config.get('wgAction')=="view"){`
`           //如果是閱讀模式`
`           `
`           //加一個源碼頁籤在編輯頁籤後面，源碼連結加載viewsource查詢字串`
`           var displayText=wgULS("源码","源碼"), $goodCaEdit;`
`           `
`           (`
`               $goodCaEdit=$("li#ca-edit:has(a[href*='action=edit'])")`
`               .filter(function(idx){`
`                   return $(this).text().match(/[編编][輯辑]/g)!==null;`
`               })`
`               .eq(0)`
`           )`
`           .clone(true)`
`           .attr("id", "ca-viewsource")`
`           .insertAfter($goodCaEdit)`
`           .find("a[href*='action=edit']")`
`           .text(displayText)`
`           .attr("title","")`
`           .each(function(){`
`               $(this).attr("href", $(this).attr("href")+"&viewsource=1");`
`           });`
`           `
`           //在各個編輯段落連結後面都加一個源碼連結，源碼連結在得到焦點時加載viewsource查詢字串`
`           $("span.mw-editsection a[href*='action=edit']")`
`           .each(function(){`
`               var $this=$(this);`
`               if($this.text().match(/[編编][輯辑]/g)===null) return;`
`               `
`               $this.clone(true)`
`               .text(displayText)`
`               .attr("title","")`
`               .insertAfter($this)`
`               .get(0).href+="&viewsource=1";`
`               `
`               $(document.createTextNode("/")).insertAfter($this);`
`           });`
`           `
`       }else if(mw.config.get('wgAction')=="edit" && getParamValue("viewsource")==1){`
`           //如果已進入源碼模式`
`           `
`           //先定義恢復正常編輯功能`
`           var resumeEditFunc=function(){`
`               var $viewSrcBodyContent=$("div.viewSrcBodyContent#bodyContent");`
`               `
`               setTimeout( function(){`
`                   $("body").css("display", "none");`
`                   `
`                   setTimeout(function(){`
`                       window.scrollTo(0,0);   //滾到最頂;`
`                       `
`                       $("div.viewSrcBodyContent#bodyContent").empty().remove();  //移除源碼模式界面;`
`                       `
`                       //復原標題`
`                       document.title=old_title;`
`                       $("h1.firstHeading#firstHeading").text(old_txt);`

`                       $("li#ca-edit").addClass("selected"); //編輯頁籤改為已選取;`
`                       $("div.realBodyContent#bodyContent").css("display", "inline").removeClass("realBodyContent"); //重新顯示編輯模式界面;`
`                       `
`                       $("body").css("display", "inline");`
`                   }, 500*resumeEditFunc.msec);`
`               }, 300*resumeEditFunc.msec);`
`               `
`               return false;`
`           };`
`           resumeEditFunc.msec=1;`
`           //定義恢復正常編輯功能 結束;`
`           `
`           //偵測編輯框及是否為可編輯操作`
`           //如皆否，恢復編輯界面並離開本功能`
`           var $wpTextbox1=$("form#editform[name='editform'] textarea#wpTextbox1[name='wpTextbox1']");`
`           if( $("form#editform[name='editform'] input#wpDiff[name='wpDiff']").length>0 && $wpTextbox1.length>0){`
`           }else{`
`               resumeEditFunc.msec=0.01;`
`               resumeEditFunc();`
`               return null;`
`           }`
`           `
`           //如果以上皆是`
`           $("li#ca-edit").removeClass("selected"); //編輯頁籤改為未選取;`
`           //建立源碼模式界面`
`           $('`

<div id="bodyContent" class="viewSrcBodyContent" />

')

`           .append(`
`               $('`

您可以'+wgULS("查看并复制本页面的源代码", "檢視並複製本頁面的原始碼")+'：

')

`               .append(["[", $('`<a href="#">`'+wgULS("开始编辑","開始編輯")+'`</a>`').click(resumeEditFunc), "]"])`
`           )`
`           .append($wpTextbox1.clone().attr("readonly", true))`
`           .append($('`

返回到<a href="'+mw.config.get('wgArticlePath').replace('$1', mw.util.rawurlencode(mw.config.get('wgPageName')))+'" title="'+mw.config.get('wgPageName')+'">'+mw.config.get('wgPageName')+'</a>。

'))

`           .insertAfter($("div.realBodyContent#bodyContent"));`
`       }`
`       `
`   });`
`   //載入完成後執行段 結束`
`   `

});

$(function(){

`   $("body").css("display", "block");`

});