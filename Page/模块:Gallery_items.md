> 本文内容由[模块:Gallery items](https://zh.wikipedia.org/wiki/模块:Gallery_items)转换而来。


\-- this module implements [template:gallery items](https://zh.wikipedia.org/wiki/template:gallery_items "wikilink") local p = {}

function p.main(frame)

`   local getArgs = require('Module:Arguments').getArgs`
`   local args = getArgs(frame)`

`   local width = args.width or '150'`

`   local items = {}`
`   for k, v in pairs(args) do`
`       if k ~= nil and tonumber(k) and math.fmod(k,2) == 1 then`
`           local i = math.floor(k/2) + 1`
`           local item = mw.html.create('li')`
`               :addClass('gallerybox')`
`               :css('width', (args['width' .. k] or width)+5 .. 'px')`
`           local itemdiv = item:tag('div'):css('width', (args['width' .. k] or width)+5 .. 'px')`
`           itemdiv:tag('div')`
`                   :addClass('thumb')`
`                   :css('width', (args['width' .. k] or width) .. 'px')`
`                   :css('text-align', args['itemalign'])`
`                   :wikitext('`

<div style="margin:0px auto">

' .. args\[k\] .. '

</div>

')

`           if args[tonumber(k)+1] then`
`               itemdiv`
`                   :tag('div')`
`                   :addClass('gallerytext')`
`                   :css('text-align', args['captionalign'])`
`                   :wikitext('`

' .. args\[tonumber(k)+1\] .. '

')

`           end`
`           items[i] = tostring(item) .. ' '`
`       end`
`   end`
`   local root = mw.html.create('ul')`
`       :addClass('gallery mw-gallery-nolines gallery-items')`
`       :addClass(args.class)`
`       :cssText(args.style)`
`       :wikitext(table.concat(items))`
`   `
`   return frame:extensionTag {name = 'templatestyles', args = {src = 'Gallery items/styles.css'}} .. frame:extensionTag{ name = 'gallery' } .. tostring(root)`

end

return p