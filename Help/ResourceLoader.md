自1.17版本开始，MediaWiki引入了[ResourceLoader将多个JavaScript和](https://zh.wikipedia.org/wiki/mw:ResourceLoader "wikilink")/或CSS合并及压缩后传送，以加速载入。这可能对本地开发工作带来一些影响。

## 致使用者

对于所有使用ResourceLoader的部件，包括标记有\[ResourceLoader\]参数的小工具、大部分其他MediaWiki扩展、和一些MediaWiki的核心功能，其JavaScript和/或CSS可能被合并后载入。这（主要在JavaScript方面）会导致以下现象：如果其中一个部件含有代码错误，其他同时载入的，即使编写完全正常的部件可能不能工作。若您遇到了此类故障（或者，任何脚本故障，若您不能辨认的话），请按以下步骤测试后报告：

1.  在遇到故障时，在网址栏的URL末尾加入`debug=true`参数重新打开。（如果URL中包含有`?`，则应在URL末尾加上`&debug=true`；不含则在末尾加入`?debug=true`）
2.  重新测试是否仍遇到故障。
    1.  若故障不再出现，通常是缓存问题。请[清除浏览器缓存后再试试](https://zh.wikipedia.org/wiki/Help:绕过浏览器缓存 "wikilink")。
    2.  若故障仍然出现，请报告此时有故障的部件。如果可能，请提供错误信息。
          - [Mozilla Firefox](https://zh.wikipedia.org/wiki/Mozilla_Firefox "wikilink")、[Iceweasel](../Page/Iceweasel.md "wikilink")、[Google Chrome](../Page/Google_Chrome.md "wikilink")、[Chromium](../Page/Chromium.md "wikilink")：按下后重新载入页面，复制其中的错误信息。
          - 其他浏览器：*（请补充）*。

若故障在已登录时出现，请尝试退出登录以及清空缓存和Cookies后再试（或使用浏览器的隐私浏览模式），并检查是否仍有故障。若故障仍然存在，请重复上面的步骤，并将相关信息同样报告。

## 致开发者

目前（1.19）的大致脚本载入顺序为：ResourceLoader小工具（可能为异步载入）、其他小工具、[`MediaWiki:Common.js`](../MediaWiki/Common.js.md "wikilink")和`MediaWiki:`*`skin_name`*`.js`、用户JavaScript、用户组JavaScript，因此在小工具执行时[`MediaWiki:Common.js`](../MediaWiki/Common.js.md "wikilink")中定义的函数可能不存在。目前部分中文维基百科常用函数（包括字词转换的`wgULS`和`wgUVS`）存放于[`MediaWiki:Gadget-site-lib.js`](../MediaWiki/Gadget-site-lib.js.md "wikilink")，若小工具代码中使用了这些函数，应先通过ResourceLoader引入`ext.gadget.site-lib`模块。