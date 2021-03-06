> 本文内容由[模块:Airport destination list](https://zh.wikipedia.org/wiki/模块:Airport_destination_list)转换而来。


local p = {}

local function isnotempty(s)

`   return s and s:match( '^%s*(.-)%s*$' ) ~= ''`

end

function p.table(frame)

`   local args = (frame.args[1] ~= nil) and frame.args or frame:getParent().args`
`   local cols`
`   if isnotempty(args['4thcoltitle']) and isnotempty(args['3rdcoltitle']) then`
`       cols = 4`
`   elseif isnotempty(args['3rdcoltitle']) then cols = 3`
`   else cols = 2`
`   end`

`   -- compute the maximum cell index`
`   local cellcount = 0`
`   for k, v in pairs( args ) do`
`       if type( k ) == 'number' and isnotempty(v) then`
`           cellcount = math.max(cellcount, k)`
`       end`
`   end`
`   -- compute the number of rows`
`   local rows = math.ceil(cellcount / cols)`

`   -- create the root table`
`   local root = mw.html.create('table')`
`   root`
`       :addClass('wikitable')`
`       :addClass('sortable')`
`       :css('font-size', '85%')`

`   -- add the header row`
`   local row = root:tag('tr')`
`   local cell= row:tag('th')`
`   cell:wikitext('航空公司')`
`   cell= row:tag('th')`
`   cell:addClass('unsortable')`
`   cell:wikitext('目的地')`
`   if (isnotempty(args['3rdcoltitle'])) then`
`       cell= row:tag('th')`
`       cell:css('width','10%')`
`       if (isnotempty(args['3rdcolunsortable'])) then`
`           cell:addClass('unsortable')`
`       end`
`       cell:wikitext(args['3rdcoltitle'])`
`   end`
`   if (isnotempty(args['4thcoltitle'])) then`
`       cell= row:tag('th')`
`       if (isnotempty(args['4thcolunsortable'])) then`
`           cell:addClass('unsortable')`
`       end`
`       cell:wikitext(args['4thcoltitle'])`
`   end`
`   -- loop over rows`
`   for j=1,rows do`
`       row = root:tag('tr')`
`       for i=1,cols do`
`           cell= row:tag('td')`
`           if (i > 2) then cell:css('text-align','center') end`
`           cell:wikitext(args[cols*(j - 1) + i] or '')`
`       end`
`   end`
`   -- return the root table`
`   return tostring(root)`

end

return p