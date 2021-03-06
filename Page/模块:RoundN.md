> 本文内容由[模块:RoundN](https://zh.wikipedia.org/wiki/模块:RoundN)转换而来。


local numberToChinese = require('Module:NumberToChinese')._numberToChinese

local p = {

`   RD = {`
`       '半準決賽',`
`       '準決賽',`
`       '決賽',`
`       '季軍戰'`
`   },`
`   bgColor = {head = '#F2F2F2', 'gold', 'silver', '#CD7F32', '#F9F9F9'},`
`   reuseStr = {},`
`   saveStr = function(self, name, ...)`
`       if not self.reuseStr[name] then`
`           self.reuseStr[name] = table.concat{...}`
`       end`
`       return self.reuseStr[name]`
`   end`

}

\--Provides a convenient naming shortcut up to {{\#invoke:RoundN|N512}} =  for columns = 1, 9 do

`   local N = math.pow(2, columns)`
`   p['N' .. N] = function(frame)`
`       return p.main(frame.args, columns)`
`   end`
`   p['n' .. N] = p['N' .. N]--to make case insensitive`

end

\--saves memory and avoids errors when using a nil as a table by providing a temporary table; if using nil as false; use 'table(k)' to look up table\[k\] p.nilAsTab = {

`   __index = function(t, i)`
`       return setmetatable({}, setmetatable(p.nilAsTab, {__index = {t = t, i = i}}))`
`   end,`
`   __newindex = function (pt, pi, v) --store new values in actual table rather than temporary`
`       rawset(p.nilAsTab.t, p.nilAsTab.i, {})[p.nilAsTab.i][pi] = v`
`       setmetatable(p.nilAsTab.t[p.nilAsTab.i], {__call = p.nilAsTab.__call})`
`   end,`
`   __call = function(t, i)`
`       return t and rawget(t, i)`
`   end`

} --never assign a value to these or they will stop being empty local infiniteEmpty = setmetatable({}, {__index = setmetatable({}, p.nilAsTab), p.nilAsTab}) -- infiniteEmpty\[1\]\[2\]\[3\]...\[infinity\] = {} local callableEmpty = setmetatable({}, p.nilAsTab)

local rowNum, head, m, col, tab, esc = {}, {}, {num = 1, phase = 0, bold = infiniteEmpty}, {}, mw.html.create'table', {

`   bs = require'Module:Escape',--backslash`
`   comma = {['(%([^,]*),([^%)]*%))'] = '%1|@!#|%2'},--escape commas in ()`

} local nodeFunc = {

`   scanPattern = function(self, args, step)`
`       self.pattern = nil`
`       if args[step] then`
`           self.pattern, self.nonFunc = string.match(esc.bs:text(args[step]), '^node_function{(.-)}(.*)')`
`       end`
`       if self.pattern then`
`           for k, v in pairs(esc.comma) do`
`               self.pattern = self.pattern:gsub(k, v)`
`           end`
`           self.nonFunc = self.nonFunc and esc.bs:undo(self.nonFunc)`
`           self.pattern = mw.text.split(self.pattern, '%s*,%s*')`
`           for k, v in ipairs(self.pattern) do`
`               local func, arg = string.match(v, '^(%w+)%(?([^%)]*)')`
`               if func and self[func] and self[func].main then`
`                   self.pattern[k] = func`
`                   if arg then`
`                       for x, y in pairs(esc.comma) do`
`                           arg = esc.bs:undo(arg):gsub(y:gsub('%%%d', ''), x:match('%)([^%(])%(') or x:gsub('\\', ''))`
`                       end`
`                       self[func].arg = self[func].arg or {}`
`                       self[func].arg[m.num] = arg`
`                   end`
`               end`
`           end`
`       end`
`       return self.pattern`
`   end,`
`   helper = {`
`       topBranch = function()--node is top of fork if top is 0`
`           return (m.num - col.top) % 2`
`       end,`
`       addText = function(text)`
`           if text and text ~= '' then`
`               tab.r:wikitext(text)`
`           end`
`       end`
`   },`
`   line = {--this node is omitted and replaced with a line`
`       main = function(x)`
`           local h = p.getNodeFunc()`
`           if m.available then`
`               local text, topId, isTop, notTop = h.line.arg[m.num] or '', h.topBranch()`
`               isTop = topId == 0`
`               notTop = {[isTop and 1 or 0] = p.reuseStr.solid}`
`               for k = 0, 1 do`
`                   tab.r = rowNum[m.r + k * 4]:tag'td'`
`                       :css(notTop[k] and`
`                           {[isTop and 'border-top' or 'border-bottom'] = notTop[k]}`
`                           or {}`
`                       )`
`                       :attr{`
`                           rowspan = ({[0] = 4, 2})[k],`
`                           colspan = p.colspan`
`                       }`
`                   h.addText(text or h.nonFunc)`
`                   text = nil`
`               end`
`               m.available = false`
`           else`
`               return nil`
`           end`
`           return x`
`       end`
`   },`
`   bridge = {--Draw a line to the neighboring node in the same column that is not connected to the current node`
`       main = function(x)`
`           local h = p.getNodeFunc()`
`           h.bridge.lay[col.c][m.num - col.top + 1 + (h.topBranch() == 1 and 1 or -1)] = true`
`           h.addText(nonFunc)`
`           return x`
`       end,`
`       lay = setmetatable({}, p.nilAsTab)`
`   },`
`   canvas = {--Merges all cells in node. Content will be the next parameter.`
`       main = function(x)`
`           local h = p.getNodeFunc()`
`           if m.available then`
`               tab.r = rowNum[m.r]:tag'td'`
`                   :attr{`
`                       rowspan = 6,`
`                       colspan = p.colspan`
`                   }`
`               h.addText(h.nonFunc)`
`               m.available = false`
`               return x`
`           else`
`               return nil`
`           end`
`       end`
`   },`
`   orphan = {--sets a flag for skipMatch to be set by p._main`
`       main = function(x)`
`           p.getNodeFunc().orphan.num = m.num`
`           return x`
`       end`
`   },`
`   skipAllowed = {--table of supported node functions when node is skipped (i.e. by skipmatch)`
`       bridge = true,`
`       canvas = true`
`   }`

}

setmetatable(nodeFunc.helper, {__index = nodeFunc}) function p.getNodeFunc()

`   return nodeFunc.helper`

end

local function newRow(bodyRow)

`   local first = p.flex_tree.merge and mw.clone(p.flex_tree.cell) or p.flex_tree.cell`
`   tab.r = tab:tag'tr'`
`       :node(first)`
`   if bodyRow then`
`       table.insert(rowNum, bodyRow, tab.r)`
`       if p.flex_tree.merge then`
`           rowNum[bodyRow].first = first`
`           rowNum[bodyRow].first.unchanged = true`
`       end`
`   end`

end

local function drawHead(text, row3rd)

`   local td = (row3rd and rowNum[row3rd]:tag'td':attr{rowspan = 2}`
`       or head.row:tag'td')`
`       :attr{colspan = p.colspan}`
`   if text ~= 'omit_label' then`
`       td:wikitext(text):css{`
`           ['text-align'] = 'center',`
`           border = '1px solid #aaa',`
`           background = p.bgColor.head`
`       }`
`   end`

end

local function spacer(width)

`   tab.r:tag'td'`
`       :attr{width = width}`
`       :wikitext(p.no_column_head and '' or ' ')`

end

local function dpBox(v, r)

`   p.dpBoxBase = p.dpBoxBase or mw.html.create'td':attr{rowspan = 2, colspan = p.colspan}`
`   if not v then`
`       p.dpBoxEmpty = p.previewnumbers and mw.clone(p.dpBoxBase) or p.dpBoxEmpty or mw.clone(p.dpBoxBase):wikitext(p.flex_tree.wt)`
`       rowNum[r]:node(p.dpBoxEmpty)`
`   else`
`       rowNum[r]:node(mw.clone(p.dpBoxBase):wikitext(v))`
`   end`

end

p.scoreWasher = {

`   numberFormat = '%-?%d+%.?%d*',`
`   main = function (self, s)`
`       if s then`
`           for _, cycle in ipairs(self.cycles) do`
`               s = s:gsub(unpack(cycle))`
`           end`
`           if p.scoreSumBox and self.plus then`
`               local t = 0`
`               for _, part in ipairs(mw.text.split(s, self.plus)) do`
`                   t = t + (tonumber(part:match('%-?%d+%.?%d*')) or 0)`
`               end`
`               return t`
`           end`
`           return tonumber(s:match(self.numberFormat)) or math.huge`
`       end`
`       return 0`
`   end,`
`   spin = function(self, v)`
`       table.insert(self, v)`
`       return self`
`   end,`
`   load = function (self, cycle)`
`       local wash, rinse = 0, {spin = self.spin}`
`       for v in cycle:gfind('%(([^%(%)]-)%)') do`
`           if v == '_plus_' then`
`               self.plus = v`
`               rinse:spin(v)`
`               cycle = cycle:gsub('%(_plus_%)', '', 1)`
`           else`
`               wash = wash + 1`
`               rinse:spin('%'):spin(wash)`
`           end`
`       end`
`       table.insert(self.cycles, {esc.bs:undo(cycle, '%%'), table.concat(rinse)})`
`   end,`
`   init = function(self, setting)`
`       self.cycles = {original = setting}`
`       for cycle in (setting and esc.bs:text(setting) or '{<.->} {[^%d]*}'):gfind('{(.-)}') do`
`           self:load(cycle)`
`       end`
`   end,`
`       sum = function (clean)`
`       local sum = {0, 0}`
`       for _, box in ipairs(clean) do`
`           for team, score in ipairs(box) do`
`               sum[team] = sum[team] + score`
`           end`
`       end`
`       return unpack(math.max(unpack(sum)) == math.huge and {'—', '—'} or sum)`
`   end`

}

local function boldWin(s1, s2)

`   return setmetatable(`
`       p.bold and s1 ~= s2 and (math[({'min', 'max'})[p.bold]](s1, s2) == s1 and {true} or {[2] = true}) or callableEmpty,`
`       p.nilAsTab`
`   )`

end

local function maxSpan(span, start, rows)

`   return math.min(span, math.max(0, rows - start + 1))`

end

\--in case of templates like RDseed need padding value p.teamBoxPadding = function()

`   return '.6ex'`

end p.teamBoxPadTab = {padding = '0 ' .. p.teamBoxPadding()} p.teamBoxNormal = {border = '1px solid \#aaa', background = p.bgColor\[4\]} local function teamBox(v, r, f)

`   if p.flex_tree.merge and not v and f.phase == 2 then`
`       for i = -2, 0 do`
`           if rowNum[r + i].first.unchanged then`
`               rowNum[r + i].first.unchanged = nil`
`               rowNum[r + i].first:node(p.unflex_div)`
`           end`
`       end`
`       tab.r:attr{rowspan = 4}:css{['vertical-align'] = 'center'}`
`   else`
`       if not p.bold then`
`       --backwards compatability (wikitemplates bold each arg individually)`
`           local hasBold, b = tostring(v):gsub("([^']*)'''([^']*)", '%1`<b>`%2`</b>`')`
`           if b == 1 then`
`               v = hasBold`
`           end`
`       end`
`       local cell`
`       if f[1] then`
`           cell = f.sumBox and f.sumBox[1] and`
`               {padding = f.sumBox[1]}`
`               or {['border-left'] = f.borderLeft}`
`           cell['text-align'] = v and f[1]`
`       else`
`           cell = p.teamBoxPadTab`
`       end`
`       tab.r = rowNum[r]:tag'td'`
`           :css(p.teamBoxCSS)`
`           :css(cell)`
`           :attr{rowspan = 2}`
`           :node(mw.html.create(f.bold and 'b'):wikitext(v or f[1] and '' or ' '))`
`   end`

end

function p._main(args)

`   function args:clean(key, params)--prevent html comments from breaking named args and reduces repeat concatenation`
`       params = params or {}`
`       local clean = args[key] or params.ifNil`
`       if clean then`
`           params.append = params.append or ''`
`           clean = mw.text.decode(clean):gsub('<!%-.-%->', ''):gsub(params.pattern or '[^%w-;%.]', '') .. params.append`
`           clean = clean ~= params.append and clean or params.ifNil`
`       end`
`       args[key] = params.keepOld and args[key] or clean`
`       return clean`
`   end`
`   p.cols = tonumber(args:clean('columns', {pattern = '%D'}))`
`   p.tCols = (tonumber(args:clean('final_RDs_excluded', {pattern = '%D'})) or 0) + p.cols`
`   local matchPer = {`
`       pattern = '%d*per%d+[%-x]%d+',`
`       vals = '(%d*)per(%d+)([%-x])(%d+)'`
`   }`
`   local skipMatch, unBold  = {}, {}--(skip|manualbold)match# to boolean`
`   for k, _ in pairs(args) do`
`       local mType, mNum = string.match(k, '^(%l+)match(%d*)$')`
`       mType, mNum = ({skip = skipMatch, manualbold = unBold})[mType], tonumber(mNum)`
`       if mType then`
`           if mNum then`
`               mType[mNum] = args:clean(k) == 'yes' or args[k] == 'true'`
`           else`
`               for pattern in args:clean(k, {ifNil = ''}):gfind(matchPer.pattern) do`
`                   local d1, period, op, d2 = pattern:match(matchPer.vals)`
`                   d1 = tonumber(d1) or 1`
`                   d2 = op == '-' and d2 or (d1 + period * (d2 - 1))`
`                   for y = d1, d2, period do`
`                       mType[y] = true`
`                   end`
`               end`
`               for _, x in ipairs(mw.text.split(args[k]:gsub(matchPer.pattern, ''):gsub('[;%-%a][;%-%a]+', ';'):match('^;*(.-)[;%-]*$'), ';')) do`
`                   x = mw.text.split(x, '-')`
`                   for y = tonumber(x[1]) or 1, tonumber(x[2] or x[1]) or 0 do`
`                       mType[y] = true`
`                   end`
`               end`
`           end`
`       end`
`   end`
`   for _, v in ipairs({--more args to boolean`
`       'widescore',`
`       'template',`
`       'article_include',`
`       'color',`
`       '3rdplace',`
`       'omit_blanks',`
`       'scroll_head_unlock',`
`       'previewnumbers',`
`       'flex_tree',`
`       'no_column_head',`
`       'short_brackets',`
`       'branch_upwards'`
`   }) do`
`       if args[v] and (p[v] == nil or type(p[v]) == 'boolean') then`
`           p[v] = args:clean(v) == 'yes' or args[v] == 'true'`
`       end`
`   end`
`   p.namespace = mw.title.getCurrentTitle().namespace`
`   p.previewnumbers = p.namespace ~= 0 and p.previewnumbers`
`   p.scoreWasher:init(args['score-clean'])`
`   p.scoreWasher.demo = args.demoWash and tonumber(args:clean('demoWash', {pattern = '%D'}), 10)`
`   p.scoreSumBox = args['score-boxes'] and args['score-boxes']:match('%d ?%+ ?sum')`
`   p.bold = ({low = 1, high = 2})[args:clean('bold_winner')] or p.scoreSumBox and 2`
`   local sumBox = p.scoreSumBox and 1 or 0`
`   p.scoreBoxes = (tonumber(args:clean('score-boxes', {pattern = '%D'})) or 1) + sumBox`
`   p.scoreSumBox = p.scoreBoxes > 0 and p.scoreSumBox or nil`
`   local boxStyle = p.scoreBoxes > 1 and`
`       (p.scoreSumBox and`
`           setmetatable(`
`               {{}, [p.scoreBoxes] = {'0 1ex'}},`
`               {__call = function(t, i) if t[i] then return nil end return 0 end}`
`           )`
`           or setmetatable(`
`               {},`
`               {__call = function() return 0 end}`
`           )`
`       )`
`       or setmetatable({}, {__call = function() return nil end})`
`   p.colspan = p.scoreBoxes > 0 and (p.scoreBoxes + 1) or nil`
`   local nodeArgs = {`
`       score = p.scoreBoxes - sumBox,`
`       team = {offset = 1 + p.scoreBoxes - sumBox}`
`   }`
`   nodeArgs.all = 1 + nodeArgs.team.offset * 2`
`   nodeArgs.tableSum = {`
`       __add = function(v, t)`
`           if #t == 3 then`
`               return v + nodeArgs.all`
`           end`
`           local s = v`
`           for i, n in ipairs(t) do`
`               s = s + n`
`           end`
`           return s--`[`+``   ``(p.scoreSumBox``   ``and``   ``#t``   ``==``   ``3``   ``and``   ``-2``   ``or``   ``0)``   ``--merging``   ``disabled``   ``with``   ``score``   ``boxes,``   ``uncomment``   ``if``   ``enable`](https://zh.wikipedia.org/wiki/+_\(p.scoreSumBox_and_#t_==_3_and_-2_or_0\)_--merging_disabled_with_score_boxes,_uncomment_if_enable "wikilink")
`       end`
`   }`
`   nodeArgs.team[1] = 1--constant to be replaced later by new param`
`   nodeArgs.team[2] = nodeArgs.team[1] + nodeArgs.team.offset`
`   nodeArgs.blank = setmetatable({}, nodeArgs.tableSum)`
`   p.unflex_div = mw.html.create'div'`
`                   :css{overflow = 'hidden', height = '1ex'}`
`                   :wikitext' '`
`   p.flex_tree = setmetatable({},{__index = {`
`       merge = p.flex_tree and p.scoreBoxes == 0,`
`       wt = p.flex_tree and '' or ' ',`
`       cell = mw.html.create'td'`
`           :node(not p.flex_tree and p.unflex_div or nil)`
`   }})`
`   if args:clean'scroll_height' then`
`       local fontSize, fontUnit = args.style and args.style:match('font%-size *: *(%d+)([^ ]+)')`
`       if fontSize then`
`           local units = {`
`               em = 1,`
`               ex = 2,`
`               ['%'] = 0.01`
`           }`
`           fontSize, fontUnit = {fontSize * fontUnit}`
`       end`
`   end`
`   tab`
`       :cssText(table.concat{args.scroll_height and 'padding' or 'margin', ':', fontSize and (math.ceil(fontSize * 10) / 10) or '.9', 'em 2em 1em 1em;border:0;', fontSize and '' or 'font-size:90%;border-collapse:separate;', args.style})`
`       :attr{cellpadding = 0, cellspacing = 0}`
`   if not p.no_column_head then--headings row`
`       newRow()`
`       head.row = tab.r`
`           :css{['white-space'] = args.scroll_height and 'nowrap'}`
`       newRow()`
`   else`
`       tab.r = tab:tag'tr'`
`       tab.r:tag'td'`
`   end`
`   local sp = {--set column widths`
`       args['team-width'] or 170,`
`       p.widescore and 40 or 30,`
`       p.short_brackets and 6 or 15,`
`       p.short_brackets and 4 or 20`
`   }`
`   local scoreWidth = args:clean('score-width', {pattern = '[^%d;]'}) and mw.text.split(args['score-width'], ';') or {}`
`   scoreWidth[1] = tonumber(scoreWidth[1], 10)`
`   if p.scoreSumBox and #scoreWidth ~= 1 then`
`       local _scoreWidth = {}`
`       for k = 1, p.scoreBoxes - 1 do`
`           _scoreWidth[k] = tonumber(scoreWidth[k], 10) or math.ceil(sp[2] * 0.75)`
`       end`
`       setmetatable(scoreWidth, _scoreWidth)`
`   end`
`   if p.template or p.article_include then`
`       p.template = mw.title.new(args.name)`
`       p.templateFixedName = (p.template.namespace == 0 and not p.article_include and 'Template:' or '') .. p.template.fullText`
`   end`
`   p.template = p.template and mw.title.new(args:clean('name', {pattern = ''}))`
`   local head_br = {`
`       count = 0,`
`       compare = function (self, text)`
`           if text and args.scroll_height then`
`               local _, count = text:gsub('<br[ >/]', '%1')`
`               self.count = math.max(self.count, count)`
`           end`
`           return text`
`       end`
`   }`
`   p.branch_upwards = p.branch_upwards and 0`
`   for k = 1, p.cols do`
`       if k > 1 then`
`           spacer(sp[3])`
`           spacer(sp[4])`
`           if not p.no_column_head then`
`               head.row:tag'td':attr{colspan = 2}`
`           end`
`       end`
`       spacer(sp[1])`
`       for s = 1, p.scoreBoxes do`
`           spacer(#scoreWidth == 1 and scoreWidth[1] or scoreWidth[s] or sp[2])`
`       end`
`       if not p.no_column_head then`
`           head.wt = head_br:compare(args:clean('RD' .. k, {pattern = ''}))`
`               or p.RD[#p.RD + k - p.tCols - 1]`
`               or (numberToChinese(math.pow(2, p.tCols - k + 1)) .. '強賽')`
`           drawHead(`
`               k == 1 and p.template and mw.getCurrentFrame():expandTemplate{`
`                   title = 'navbar-header',`
`                   args = {head.wt, p.templateFixedName}`
`               } or head.wt`
`           )`
`       end`
`   end`
`   sp.row = tab.r`
`   col.tot = math.pow(2, p.tCols - 1)`
`   local step, bump, bumpBase, rows = 1, 0, mw.html.create'td':attr{colspan = p.colspan}, col.tot * 6--Begin body row output`
`   args.line_px = table.concat{args:clean('line_px') or 3, args.line_px ~= '0' and 'px' or nil}`
`   tab.line = {--reduces concats and 'or' statements`
`       {`
`           [true] = args.line_px,`
`           [false] = 0`
`       },`
`       args.line_px:rep(2):gsub('(%a)(%d)', '%1 %2', 1)`
`   }`
`   p['3rdplace'] =  p.tCols == p.cols and (p['3rdplace'] or p.cols > 3 and nil == p['3rdplace'] and not p.no_column_head)`
`   if p['3rdplace'] then`
`       p.textThird = args.Consol or args['RD' .. (p.cols + 1)] or p.RD[4]`
`       local no3rdText = p.no_column_head or p.textThird and p.textThird:match('omit_label')`
`       rowNum.third = math.max(math.pow(2, p.branch_upwards and -3 or p.cols - 2) * 9 + (no3rdText and 4 or 9), no3rdText and 12 or 17, rows)`
`   end`
`   for r = 1, rowNum.third or rows do`
`       newRow(r)`
`   end`
`   p:saveStr('solid', tab.line[1][true], ' solid')`
`   p.cornerDiv = mw.html.create'div':css{height = tab.line[1][true], ['border-right'] = p.reuseStr.solid}`
`   for c = 1, p.cols do`
`       col.c = c`
`       local bumps = bump`
`       if c > 1 then`
`           col.tot = col.tot + math.pow(2, p.tCols - c)`
`           if p.branch_upwards then`
`               bumps = 0`
`               rowNum[1]:tag'td':attr{rowspan = 4}`
`           else`
`           rowNum[1]:node(c < p.cols and`
`               mw.clone(bumpBase):attr{rowspan = bump}`
`               or p.no_column_head and p.template and`
`                   mw.html.create'td':wikitext(mw.getCurrentFrame():expandTemplate{`
`                       title = 'navbar-header',`
`                       args = {'', p.templateFixedName}`
`                   })`
`           )`
`           end`
`       end`
`       col.top = m.num`
`       p.span = p.tCols > c and bump * 2 or p.branch_upwards or math.max((bump - 1) / 2, 2)`
`       col.show3rd = p['3rdplace'] and c == p.tCols and rowNum.third`
`       local colorFinal, bumpMid = p.color and c == p.tCols, p.span > 0 and mw.clone(bumpBase):attr{rowspan = p.span} or nil`
`       for r = 1, col.show3rd or rows, 2 do`
`           m.r = r + bumps`
`           if col.show3rd or rowNum[m.r] and m.num <= col.tot then`
`               if m.phase == 0 then`
`                   m.showBox = setmetatable({1, nodeArgs.team.offset, nodeArgs.team.offset}, nodeArgs.tableSum)`
`                   if nodeFunc:scanPattern(args, step) then`
`                       nodeFunc.called = {}`
`                       m.available = true`
`                   else`
`                       m.available = nil`
`                   end`
`               end`
`               if skipMatch[m.num] then`
`                   if m.phase == 0 then`
`                       if nodeFunc.pattern then`
`                           for x, y in ipairs(nodeFunc.pattern) do`
`                               if nodeFunc.skipAllowed[y] then`
`                                   nodeFunc.called[y] = nodeFunc[y].main(x)`
`                               end`
`                           end`
`                       end`
`                       local canvas = nodeFunc.pattern and nodeFunc.called.canvas and 6`
`                       rowNum[m.r + (canvas or 0)]:tag'td':attr{rowspan = maxSpan((canvas and 0 or 6) + bump * 2, m.r + (canvas or 0), rows), colspan = p.colspan}`
`                   elseif m.phase == 2 then`
`                       if nodeFunc.pattern and (nodeFunc.called.bridge or nodeFunc.called.canvas) then`
`                           step = step + 1`
`                       end`
`                       m.num = m.num + 1`
`                       step = step + (p.omit_blanks and 0 or m.showBox)`
`                       bumps = bumps + (col.show3rd and 0 or maxSpan(p.span, m.r, rows))`
`                   end`
`               elseif m.phase == 0 then`
`                   if nodeFunc.pattern then`
`                       for x, y in ipairs(nodeFunc.pattern) do`
`                           if nodeFunc[y] and nodeFunc[y].main then`
`                               nodeFunc.called[y] = nodeFunc[y].main(x)`
`                           end`
`                       end`
`                       if m.available == false then`
`                           m.showBox = nodeArgs.blank`
`                           step = step + 1`
`                       end`
`                   end`
`                   if m.showBox[1] then`
`                       if col.show3rd then`
`                           col.show3rd = (m.num - col.top) * 2`
`                           if col.show3rd == 2 then`
`                               if p.textThird:match('omit_label') then`
`                                   p.textThird = nil`
`                               end`
`                               if rowNum[rows + 1] and p.cols > 1 then --if 3rd place extends below bottom cell`
`                                   rowNum[rows + 1]:tag'td':attr{`
`                                       rowspan = m.r + 9 - rows - (text and 0 or 2),`
`                                       colspan = (p.cols - 1) * (3 + p.scoreBoxes)`
`                                   }`
`                               end`
`                               if p.tCols == 1 then`
`                                   bumps = p.textThird and 3 or 0`
`                               elseif p.branch_upwards then`
`                                   r = 7`
`                                   bumps = p.textThird and 2 or 0`
`                               end`
`                               m.r = r + bumps`
`                               if p.textThird then`
`                                   drawHead(p.textThird, m.r)`
`                                   bumps = bumps + 2`
`                                   m.r = r + bumps`
`                               end`
`                           end`
`                       end`
`                       dpBox(nodeFunc.pattern and nodeFunc.nonFunc or args[step], m.r)`
`                       if p.previewnumbers then                    `
`                           rowNum[m.r].nodes[#rowNum[m.r].nodes]`
`                               :tag'div'`
`                                   :css{`
`                                       float = 'left',`
`                                       border = '1px solid red',`
`                                       padding = '0 .5ex',`
`                                       ['color'] = 'red'`
`                                   }`
`                                   :wikitext(m.num)`
`                                   :attr{title = 'Number only visible outside article space (e.g. template) when |numberpreview=yes'}`
`                       end`
`                   end`
`                   if p.colspan then`
`                       m.nonEmpty = {}`
`                       for s = step + 2, step + nodeArgs.team.offset do`
`                           local i = {s, s + nodeArgs.team.offset}`
`                           if args[i[1]] or args[i[2]] then`
`                               table.insert(m.nonEmpty, i)`
`                           end`
`                       end`
`                       if p.bold and m.showBox[2] and m.showBox[3] and not unBold[m.num] then`
`                           m.bold = {`
`                               box = {},`
`                               clean = {}`
`                           }`
`                           local notSummed = not p.scoreSumBox or #m.nonEmpty < 2`
`                           for s, i in ipairs(m.nonEmpty) do`
`                               m.bold.clean[s] = {p.scoreWasher:main(args[i[1]]), p.scoreWasher:main(args[i[2]])}`
`                               m.bold.box[s] = notSummed and boldWin(m.bold.clean[s][1], m.bold.clean[s][2]) or callableEmpty`
`                           end`
`                           if p.scoreSumBox and m.nonEmpty[2] then`
`                               local i = {-step, -step - 1}`
`                               table.insert(m.nonEmpty, i)`
`                               args[i[1]], args[i[2]] = p.scoreWasher.sum(m.bold.clean)`
`                               m.bold.box[p.scoreBoxes] = boldWin(args[i[1]], args[i[2]])`
`                           end`
`                           getmetatable(boxStyle).__index = p.scoreSumBoxes and {[#m.nonEmpty] = boxStyle[p.scoreBoxes]}`
`                           m.bold.win = m.bold.box[#m.nonEmpty] or callableEmpty`
`                       else`
`                           m.bold = infiniteEmpty`
`                       end`
`                   end`
`               else`
`                   if m.showBox[m.phase] then`
`                       p.teamBoxCSS = colorFinal and`
`                           {border = p.teamBoxNormal.border, background = p.bgColor[m.phase + (col.show3rd or 0)]}`
`                           or p.teamBoxNormal`
`                       local f = {phase = m.phase, bold = m.bold.win(m.phase)}`
`                       teamBox(args[step + nodeArgs.team[m.phase]], m.r, f)`
`                       f[1] = 'center'`
`                       if p.colspan then`
`                           if m.nonEmpty[1] then`
`                               local loneSum`
`                               if #m.nonEmpty < p.scoreBoxes then`
`                                   loneSum = #m.nonEmpty == 1 and boxStyle[p.scoreBoxes]`
`                                   tab.r:attr{colspan = 1 + p.scoreBoxes - #m.nonEmpty}`
`                               end`
`                               for s, i in ipairs(m.nonEmpty) do`
`                                   f.borderLeft = boxStyle(s)`
`                                   f.sumBox = loneSum or boxStyle[s]`
`                                   f.bold = m.bold.box[s](m.phase)`
`                                   teamBox(args[i[m.phase]], m.r, f)`
`                               end`
`                           else`
`                               for s = 1, p.scoreBoxes do`
`                                   f.borderLeft = boxStyle(s)`
`                                   teamBox(nil, m.r, f)`
`                               end`
`                           end`
`                       end`
`                   end`
`                   if m.phase == 2 then`
`                       col.show3rd = col.show3rd ~= 2 and col.show3rd or nil`
`                       if p.scoreWasher.demo and p.scoreWasher.demo == m.num and p.namespace ~= 0 then`
`                           table.insert(m.bold.clean, 1, {args[step + nodeArgs.team[1]], args[step + nodeArgs.team[2]]})`
`                           return table.concat{`
`                               'Score data for match specified by |demoWash=:`
`',`
`                               mw.dumpObject{scores = m.bold.clean, cycles = p.scoreWasher.cycles, sum = p.scoreSumBox and {m.nonEmpty[#m.nonEmpty][1], m.nonEmpty[#m.nonEmpty][1]}},`
`                               '`

<table>

',

`                               tostring(sp.row), '`

<tr>

',

`                               tostring(rowNum[m.r - 4]), '`

<tr>

',

`                               tostring(rowNum[m.r - 2]), '`

<tr>

',

`                               tostring(rowNum[m.r]), '`

</table>

',

`                           }`
`                       end`
`                       if nodeFunc.orphan.num == m.num then`
`                           skipMatch[m.num] = 'orphan'`
`                       end`
`                       step = step + m.showBox`
`                       m.num = m.num + 1`
`                       if bump > 0 and rowNum[m.r + 2] and not (nodeFunc.pattern and nodeFunc.called.canvas) then`
`                           bumps = bumps + p.span`
`                           rowNum[m.r + 2]:node(bumpMid)`
`                       end`
`                       r = r + (col.show3rd or bump)`
`                   end`
`               end`
`               m.phase = (m.phase + 1) % 3`
`           end`
`       end`
`       if p.cols > c then--draw lines to next round`
`           p.unit = bump + 3`
`           bump = 3 * math.pow(2, c) - 3`
`           bumps = p.branch_upwards and 4 or (p.unit + 1)`
`           rowNum[1]`
`               :tag'td':attr{rowspan = bumps}`
`           if not p.branch_upwards then`
`               rowNum[1]:tag'td'`
`                   :attr{rowspan = (p.branch_upwards or bump) + 4}`
`                   :css(nodeFunc.bridge.lay[c](0) and`
`                       {['border-right'] = p.reuseStr.solid}`
`                       or {}`
`                   )`
`           end`
`           col.n = 0`
`           for r = bumps + 1, rows, p.unit * 2 do`
`               tab.r = rowNum[r]:tag'td'`
`               local interval = ((r - bumps - 1) / (p.unit * 2)) % 4`
`               if interval % 2 == 0 then`
`                   --col.t and col.t2 control whether lines are drawn`
`                   col.t = col.t2 or skipMatch[col.tot + col.n / 2 + 1] and 3 or ((skipMatch[col.top] and 1 or 0) + (skipMatch[col.top + 1] and 2 or 0))`
`                   col.n = col.n + 2`
`                   col.t2 = skipMatch[col.tot + col.n / 2 + 1] and 3 or ((skipMatch[col.top + col.n] and 1 or 0) + (skipMatch[col.top + col.n + 1] and 2 or 0))`
`                   if col.t == 0 then`
`                       tab.r`
`                           :attr{rowspan = maxSpan(p.unit * 2, r, rows)}`
`                           :css(skipMatch[col.tot + col.n / 2] and {} or {`
`                               border = p.reuseStr.solid,`
`                               ['border-left'] = 0`
`                           })`
`                   else`
`                       tab.r`
`                           :attr{rowspan = maxSpan(p.unit, r, rows)}`
`                           :cssText(col.t == 2 and`
`                               p:saveStr('topRight', 'border-width:', tab.line[2], ' 0 0;border-style:solid')`
`                               or col.t == 1 and (nodeFunc.bridge.lay[c](col.n - 2) and`
`                                   p:saveStr('right', ';border-right:', p.reuseStr.solid)`
`                                   or 'vertical-align:bottom'`
`                               )`
`                               or nil`
`                           )`
`                           :node(col.t == 1 and interval > 0 and not nodeFunc.bridge.lay[c](col.n - 2) and p.cornerDiv)`
`                       rowNum[r + (p.branch_upwards and (4 - bump) or p.unit)]:tag'td'`
`                           :attr{rowspan = maxSpan(p.unit, r + p.unit, rows)}`
`                           :cssText(col.t == 1 and`
`                               p:saveStr('bttmRght', 'border-width:0 ', tab.line[2], ' 0;border-style:solid')`
`                               or col.t == 2 and (nodeFunc.bridge.lay[c](col.n + 2) and`
`                                   p:saveStr('right', '; border-right:', p.reuseStr.solid)`
`                                   or 'vertical-align:top'`
`                               )`
`                               or nil`
`                           )`
`                           :node(col.t == 2 and interval ~= 2 and not nodeFunc.bridge.lay[c](col.n + 2) and p.cornerDiv)`
`                   end`
`                   col.t = {`
`                       col.t < 3,`
`                       rowNum[r + p.unit * 5] and col.t2 < 3 or false`
`                   }`
`                   rowNum[r + (p.branch_upwards or p.unit)]:tag'td'`
`                       :attr{rowspan = maxSpan(p.unit * 4, r + (p.branch_upwards and (4 - bump) or p.unit), rows)}`
`                       :css(interval == 0 and (col.t[1] or col.t[2]) and {`
`                           ['border-width'] = table.concat{tab.line[1][col.t[1]], ' 0 ', tab.line[1][col.t[2]]},`
`                           ['border-style'] = 'solid'`
`                       } or {})`
`               else`
`                   tab.r`
`                       :attr{rowspan = maxSpan(p.unit * 2, r, rows)}`
`                       :css(nodeFunc.bridge.lay[c](col.n) and`
`                           {['border-right'] = p.reuseStr.solid}`
`                           or {}`
`                       )`
`               end`
`           end`
`       end`
`   end`
`   local lock_height = (head_br.count or 0) + 1`
`   return args.scroll_height and`
`       mw.html.create'div'`
`           :cssText'border-bottom:1px solid #eee; display:inline-block'`
`           :node(not (p.scroll_head_unlock or p.no_column_head) and mw.html.create'div'`
`               :css{`
`                   overflow = 'hidden',`
`                   height = lock_height * 1.4 + 1.6 .. 'em',`
`                   ['border-bottom'] = 'inherit',`
`                   ['margin-right'] = '17px'`
`               }`
`               :node(mw.clone(tab))`
`           )`
`           :tag'div'`
`               :css{`
`                   ['overflow-y'] = 'scroll',`
`                   ['max-height'] = tonumber(args.scroll_height, 10) and args.scroll_height .. 'px' or args.scroll_height`
`               }`
`               :node(not (p.scroll_head_unlock or p.no_column_head) and`
`                   tab:css{['margin-top'] = math.floor(-10 * (lock_height * 1.4 + 1.6)/(fontSize or .9)) / 10 .. 'em', ['padding-top'] = '-3px'}`
`                   or tab`
`               )`
`           :done()`
`       or tab`

end

\--[local standard = { 'beta' = { bold_winner = 'high', omit_blanks = 'yes', auto_3rd = 'yes' } }--](https://zh.wikipedia.org/wiki/local_standard_=_{_'beta'_=_{_bold_winner_=_'high',_omit_blanks_=_'yes',_auto_3rd_=_'yes'_}_}-- "wikilink") function p.main(frame, columns)

`   local args = require'Module:Arguments'.getArgs(frame, {trim = false})`
`   args.columns = args.columns or columns`
`   return p._main(args)`

end

function p.seed(frame)

`   local parent = frame:getParent() or frame`
`   local function arg(k, alt)`
`       return parent.args[k] or frame.args[k] or alt`
`   end`
`   local padding, width = arg(2, p.teamBoxPadding()), arg(3, arg('widescore') and 40 or 30)`
`   padding = tonumber(padding) and tonumber(padding) .. 'px' or padding`
`   width = tonumber(width) and tonumber(width) .. 'px' or width`
`   return mw.html.create'div'`
`       :css{`
`           margin = ('-1px %s -1px -%s'):format(padding, padding),`
`           float = 'left',`
`           ['background'] = p.bgColor.head,`
`           border = '1px solid #aaa',`
`           ['text-align'] = 'center',`
`           width = width`
`       }`
`       :wikitext(arg(1, ' '))`

end

return p