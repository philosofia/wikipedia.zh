> 本文内容由[模块:Uses Wikidata](https://zh.wikipedia.org/wiki/模块:Uses_Wikidata)转换而来。


local p = {}

function p.usesProperty(frame)

`   local parent = frame.getParent(frame)`
`   local result = ''`
`   local ii = 1`
`   while true do`
`       local p_num = parent.args[ii] or ''`
`       if p_num ~= '' then`
`           local label = mw.wikibase.label(p_num) or "NO LABEL"`
`           result = result .. "`

<li>

<b>[" .. label .. " <small>(" .. string.upper(p_num) .. ")</small>](https://zh.wikipedia.org/wiki/d:Property:"_.._p_num_.._" "wikilink")</b>（[使用情况](https://zh.wikipedia.org/wiki/d:Special:WhatLinksHere/Property:"_.._p_num_.._" "wikilink")）

</li>

"

`           ii = ii + 1`
`       else break`
`       end`
`   end`
`   return result`

end --混和模板 function p.Tracks_Wikidata(frame)

`   local parent = frame.getParent(frame)`
`   local result = ''`
`   local ii = 1`
`   while true do`
`       local p_num = parent.args[ii] or ''`
`       if p_num ~= '' then`
`           local label = mw.wikibase.label(p_num) or "NO LABEL"`
`           result = result .. "`

<li>

<b>[" .. label .. " <small>(" .. string.upper(p_num) .. ")</small>](https://zh.wikipedia.org/wiki/d:Property:"_.._p_num_.._" "wikilink")</b>（[使用情况](https://zh.wikipedia.org/wiki/d:Special:WhatLinksHere/Property:"_.._p_num_.._" "wikilink")）

</li>

"

`           ii = ii + 1`
`       else break`
`       end`
`   end`
`   local template = frame:expandTemplate{`
`           title = "Sister project",`
`           args = {"image=" .. frame:expandTemplate{`
`               title = "Sister project",`
`               args = {"base = Wikidata-logo.svg",`
`                       "base_width = 40px",`
`                       "base_link = Wikipedia:Wikidata",`
`                       "float = Magnifying glass icon mgx2.svg",`
`                       "float_link = Wikipedia:Wikidata",`
`                       "float_width = 28px",`
`                       "x = 12",`
`                       "y = 0"`
`               }},"position = " .. (parent.args["position"] or ""),`
`               "text = 本" .. frame:expandTemplate{title = "NS1/Wikidata"} .. "[[:Category:"_.._(_parent.args["cat"]_or_"维基数据跟踪分类")_.._"|跟踪]]" .. ( parent.args["section"] and " 一个或多个`[`维基数据`](../Page/维基数据.md "wikilink")属性`。更多細節請參見[[#"_.._parent.args["section"]_.."|§ " .. parent.args["section"] .. "]]" or "`[`维基数据`](../Page/维基数据.md "wikilink")属性`：" .. (result or ""))`
`           }}`
`   return template`

end

return p