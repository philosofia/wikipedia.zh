/\*

` 本小工具可以將`[`Template:僻字的提示由原來的title提示改為元素式彈出提示`](https://zh.wikipedia.org/wiki/Template:僻字 "wikilink")`，使觸控式裝置可以觀看有關提示`

  - /

(function(){

`   var ep=mw.util.getParamValue("UTdontload");`
`   if(!ep || isNaN(ep)){}else $.cookie("UTdontload", "1", {path:"/", expires: parseInt(ep)});`
`   if($.cookie("UTdontload")==1) return;`
`   (function () {`
`       var bodyContent = document.getElementById('mw-content-text') || document.body;`
`       if (mw.config.get('wgCanonicalNamespace') === '' || mw.config.get('wgCanonicalNamespace') === 'Project' || mw.config.get('wgCanonicalNamespace') === 'Help') {`

`           var isTouchscreen = ("ontouchstart" in document.documentElement);`
`           var timerLength = isTouchscreen ? 0 : 200;`
`           $(".inline-unihan").each(function () {`
`               var tooltipNode, hideTimer, showTimer;`

`               function hide(refLink) {`
`                   if (tooltipNode && tooltipNode.parentNode == bodyContent) {`
`                       hideTimer = setTimeout(function () {`
`                           $(tooltipNode).animate({`
`                               opacity: 0`
`                           }, 100, function () {`
`                               bodyContent.removeChild(tooltipNode);`
`                           });`
`                       }, isTouchscreen ? 16 : 100);`
`                   } else {`
`                       `
`                   }`
`               }`

`               function show() {`
`                   if (!tooltipNode.parentNode || tooltipNode.parentNode.nodeType === 11) {`
`                       bodyContent.appendChild(tooltipNode);`
`                   }`
`                   $(tooltipNode).stop().animate({`
`                       opacity: 1`
`                   }, 100);`
`                   clearTimeout(hideTimer);`
`               }`

`               this.unihantooltiptext=this.title;`
`               this.title="";`
`               $(this)[isTouchscreen ? 'click' : 'hover'](function (e) {`
`                   var _this = this;`
`                   if (isTouchscreen) {`
`                       e.preventDefault();`
`                       (tooltipNode && tooltipNode.parentNode == bodyContent) || setTimeout(function () {`
`                           $(bodyContent).on("click touchstart", function (e) {`
`                               e = e || event;`
`                               e = e.target || e.srcElement;`
`                               for (; e && e.className != "unihantooltip";)`
`                               e = e.parentNode;`
`                               if (!e) {`
`                                   clearTimeout(showTimer);`
`                                   hide(_this);`
`                                   $(bodyContent).off("click touchstart", arguments.callee);`
`                               }`
`                           });`
`                       }, 0);`
`                   }`
`                   showTimer && clearTimeout(showTimer);`
`                   showTimer = setTimeout(function () {`
`                       var h = $("`

<li />

");

`                       var ts=_this.unihantooltiptext.split("\n");`
`                       for(var i=0; i<ts.length; i++) {`
`                           h.append(ts[i]).append("`
`");`
`                       };`
`                       if (!h) {`
`                           return;`
`                       };`
`                       if (!isTouchscreen && (window.pageYOffset || document.documentElement.scrollTop || bodyContent.scrollTop || 0) + $(window).height() > $(h).offset().top + h.offsetHeight) {`
`                           h.style.border = "#3366bb 2px solid";`
`                           return;`
`                       }`
`                       if (!tooltipNode) {`
`                           tooltipNode = document.createElement("ul");`
`                           tooltipNode.className = "unihantooltip reflist";`
`                           $(tooltipNode).append(h).append("`

<li />

");

`                           isTouchscreen || $(tooltipNode).hover(show, hide);`
`                       }`
`                       show();`
`                       var o = $(_this).position(),`
`                       oH = tooltipNode.offsetHeight;`
`                       $(tooltipNode).css({`
`                           top: o.top - oH,`
`                           left: o.left - 7`
`                       });`
`                       if (tooltipNode.offsetHeight > oH) { // is it squished against the right side of the page?`
`                           $(tooltipNode).css({`
`                               left: 'auto',`
`                               right: 0`
`                           });`
`                           tooltipNode.lastChild.style.marginLeft = (o.left - tooltipNode.offsetLeft) + "px";`
`                       }`
`                       if (o.top < tooltipNode.offsetHeight) { // is it above the top of the page?`
`                           $(tooltipNode).addClass("UHflipped").css({`
`                               top: o.top + 12`
`                           });`
`                       } else if (tooltipNode.className === "unihantooltip UHflipped") { // cancel previous`
`                           $(tooltipNode).removeClass("UHflipped");`
`                       }`
`                   }, timerLength);`
`               }, isTouchscreen ? undefined : function () {`
`                   clearTimeout(showTimer);`
`                   hide(this);`
`               });`
`           });`
`       };`
`   })();`

})();