> 本文内容由[MediaWiki:Centralnotice-template](https://zh.wikipedia.org/wiki/MediaWiki:Centralnotice-template)转换而来。


<style type="text/css">

1.  siteNotice {

`   text-align: left;`
`   text-decoration: none;`

} .rtl \#siteNotice {

`   text-align: right;`

} .fundraiser-box {

`   margin-top: 12px;`
`   font-style: normal;`

} .fundraiser-box a.hidelink {

`   color: black;`
`   text-decoration: none;`

} .fundraiser-box a.hidelink small, .fundraiser-box a.hidelink .showlink {

`   color: #002bb8;`

} .fundraiser-text {

`   height: 75px;`
`   padding: 0px 8px;`
`   background: #fdece5;`
`   border: solid 2px #f3e4dd;`
`   text-align: left;`

} .rtl .fundraiser-text {

`   text-align: right;`

} .fundraiser-headline {

`   font-size: 14px;`
`   margin-top: 0px;`
`   padding: 0px;`
`   color: #0a3c27;`
`   font-weight: bold;`

} .fundraiser-headline a.hidelink {

`   color: #0a3c27;`

} .fundraiser-quote {

`   font-family: Monaco, monospace;`
`   font-size: 11px;`
`   background: white;`
`   `
`   height: 1.5em;`
`   padding: 2px 8px;`
`   border: solid 2px #efedee;`
`   `
`   overflow: hidden;`

} .fundraiser-quote marquee {

`   width: 384px;`

} .fundraiser-quote .fundquote {

`   padding-right: 1.5em;`

} .fundraiser-quote {

`   margin-top: 5px;`
`   margin-bottom: 0px;`

}

</style>

<div id="siteNoticeBig">

<table class="fundraiser-box">

<tr>

<td class="fundraiser-text">

<div class="fundraiser-headline">

`               `<a href="$target" class="hidelink">`$headline`</a>
`           `

</div>

<div class='fundraiser-meter'>

`               `<a href="$target" class="hidelink">`$meter`</a>
`           `

</div>

<div class='fundraiser-quote'>

`               `<a href="$target" class="hidelink">`$quote`</a>
`           `

</div>

</td>

<td width="109" height="75">

`           `<a href="//wikimediafoundation.org/donate/2007/psa/" class="hidelink"><img src="//upload.wikimedia.org/wikipedia/commons/a/ab/Movie.png?2" alt="Video" /></a>
`       `

</td>

</tr>

<tr class="siteNoticeToggle">

<td colspan="2" align="right">

`           [`<a href="#" onclick="toggleNotice()">`$hide`</a>`]`
`       `

</td>

</tr>

</table>

</div>

<div id="siteNoticeSmall" class="fundraiser-folded">

<a href="$target">$meter</a> <span class="siteNoticeToggle">\[<a href="#" onclick="toggleNotice()">$show</a>\]</span>

</div>