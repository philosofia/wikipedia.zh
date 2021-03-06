> 本文内容由[模块:Football manager history](https://zh.wikipedia.org/wiki/模块:Football_manager_history)转换而来。


\-- Implement [Template:Football manager history](https://zh.wikipedia.org/wiki/Template:Football_manager_history "wikilink") to avoid articles being -- added to [:Category:Pages where template include size is exceeded](https://zh.wikipedia.org/wiki/Category:Pages_where_template_include_size_is_exceeded "wikilink") -- when the template is used many times.

local function clean(text, default)

`   -- Return text, if not empty, after trimming leading/trailing whitespace.`
`   -- Otherwise return default which is nil unless set by caller.`
`   if text then`
`       text = text:match("^%s*(.-)%s*$")`
`       if text ~= '' then`
`           return text`
`       end`
`   end`
`   return default`

end

local function yes(parameter)

`   -- Return true if parameter should be interpreted as "yes".`
`   -- Do not want to accept mixed upper/lowercase.`
`   return ({ Y = true, y = true, yes = true, T = true, ['true'] = true })[parameter]`

end

local function collection()

`   -- Return a table to hold items.`
`   return {`
`       n = 0,`
`       add = function (self, item)`
`           self.n = self.n + 1`
`           self[self.n] = item`
`       end,`
`       addif = function (self, item, fmt)`
`           if item then`
`               self.n = self.n + 1`
`               self[self.n] = fmt and string.gsub(fmt, '%%s', item) or item`
`           end`
`       end,`
`       join = function (self, sep)`
`           return table.concat(self, sep)`
`       end,`
`   }`

end

local function message(msg, caller, nocat)

`   -- Return formatted message text for an error.`
`   -- Can append "#FormattingError" to URL of a page with a problem to find it.`
`   -- If given, caller is the title of the navbox which has the error.`
`   local anchor = '`<span id="FormattingError"></span>`'`
`   local category`
`   if not nocat and mw.title.getCurrentTitle():inNamespaces(0, 10) then`
`       -- Category only in namespaces: 0=article, 10=template.`
`       category = ''`
`   else`
`       category = ''`
`   end`
`   return anchor ..`
`       '`<strong class="error">`Error: ' ..`
`       msg ..`
`       (caller and (' at `[`Template:'``   ``..``   ``caller``   ``..``   ``'`](https://zh.wikipedia.org/wiki/Template:'_.._caller_.._' "wikilink")`') or '') ..`
`       '`</strong>`' ..`
`       category .. '\n'`

end

local function make_entry(name, from, to, islast)

`   local result =`
`       '*`<span class="vevent">`' ..`
`       '`<span class="agent attendee vcard">`' ..`
`       '`<span class="fn org summary">`' ..`
`       name ..`
`       '`</span></span>` (`<span class="dtstart">`' ..`
`       from ..`
`       '`</span>`'`
`   if to then`
`       result = result .. '–' .. to`
`   elseif islast then`
`       result = result .. '–'`
`   end`
`   result = result .. ')`</span>`'`
`   return result`

end

local function make_list(text, note, dissolved)

`   -- Return a list of formatted items.`
`   -- Input is a string of multiple lines, one item per line.`
`   -- Each item is 'NAME FROM to TO' or 'NAME FROM', where`
`   --   NAME = manager name (any text)`
`   --   FROM = four digits (from year)`
`   --     TO = 1, 2, 3 or 4 digits (to year), or empty`
`   -- Alternatively, an item can use syntax (TEXT is any text, possibly empty):`
`   --   NAME from=TEXT`
`   --   NAME from=TEXT to=TEXT`
`   -- The code detects the end of NAME from the start of FROM.`
`   -- A dash is added to the last line (to show the manager is continuing) if`
`   -- no 'to' year is given, but no dash is added if the club is dissolved.`
`   text = text or ''`
`   if text:find('<span class=', 1, true) then`
`       -- To allow a transition period where some navboxes use the old syntax, the`
`       -- given text is used if it appears to have come from the old subtemplates.`
`       return text`
`   end`
`   -- Get the non-blank lines first so can tell when am processing the last line.`
`   -- Each line is left- and right-trimmed.`
`   local lines = collection()`
`   for line in string.gmatch(text .. '\n', '[\t ]*(.-)[\t\r ]*\n') do`
`       if line ~= '' then`
`           lines:add(line)`
`       end`
`   end`
`   if lines.n <= 0 then`
`       return ''`
`   end`
`   local ilast = dissolved and -1 or lines.n`
`   local entries = collection()`
`   entries:add('`

<div>

')

`   for i, line in ipairs(lines) do`
`       -- Need to detect lines like "Name from=1930 & 1935" (probably should`
`       -- not be like that, but that is not up to the template to enforce).`
`       local name, from, to = line:match('^([^=]-)%s+(%d%d%d%d)%s+to%s+(%d%d?%d?%d?)$')`
`       if not name then`
`           name, from = line:match('^([^=]-)%s+(%d%d%d%d)$')`
`           if not name then`
`               name, from, to = line:match('^(.-) from=(.-) to=(.*)')`
`               if not name then`
`                   name, from = line:match('^(.-) from=(.*)')`
`               end`
`           end`
`       end`
`       name = clean(name)`
`       from = clean(from, '')`
`       to = clean(to)`
`       if ((name or '=') .. (from or '=') .. (to or '')):find('=', 1, true) then`
`           -- name and from must be defined (from can be ''); to is optional.`
`           -- Reject '=' to avoid typos in items like 'to=x' or 'from=xto=y'`
`           -- from being displayed.`
`           error('Invalid line "' .. mw.text.nowiki(line) .. '"', 0)`
`       end`
`       entries:add(make_entry(name, from, to, i == ilast))`
`   end`
`   entries:add('`

</div>

')

`   entries:addif(note)`
`   return entries:join('\n')`

end

local function arg_style(bgcolor, textcolor, bordercolor)

`   local result = collection()`
`   result:addif(clean(bgcolor), 'background:%s;')`
`   result:addif(clean(textcolor), 'color:%s;')`
`   result:addif(clean(bordercolor), `
`       '-moz-box-shadow: inset 1px 1px 0 %s,' ..`
`       'inset -1px -1px 0 %s;' ..`
`       '-webkit-box-shadow: inset 1px 1px 0 %s,' ..`
`       'inset -1px -1px 0 %s;' ..`
`       'box-shadow: inset 1px 1px 0 %s,' ..`
`       'inset -1px -1px 0 %s;')`
`   result:add('width: 87%;')`
`   return result:join(' ')`

end

local function arg_title(title, teamname, managerlist, textcolor, american_english)

`   title = clean(title)`
`   teamname = clean(teamname, 'MISSING "teamname"')`
`   managerlist = clean(managerlist)`
`   textcolor = clean(textcolor)`
`   american_english = clean(american_english)`
`   local spancolor = textcolor and ('`<span style="color:' .. textcolor .. ';">`') or '`<span>`'`
`   local mgr = spancolor .. (american_english and 'Head coaches' or '歷任領隊') .. '`</span>`'`
`   return`
`       '`<span class="fn org">`[[' .. teamname .. '|' ..`
`       spancolor ..`
`       (title or teamname) .. '`</span>`]]`</span>` – ' ..`
`       (managerlist and ('`[`'``   ``..``   ``mgr``   ``..``   ``'`](https://zh.wikipedia.org/wiki/'_.._managerlist_.._' "wikilink")`') or mgr)`

end

local function _main(args)

`   -- Return wikitext for a navbox.`
`   -- Code does not do much checking of inputs but will throw an error`
`   -- if input is found to be invalid.`
`   local style = arg_style(args.bgcolor, args.textcolor, args.bordercolor)`
`   local dissolved = args.dissolved`
`   if dissolved then`
`       -- May be a number of two or more digits (year club was dissolved; compatible`
`       -- with ``), or an alias for 'yes'.`
`       dissolved = dissolved:match('^%d%d+$') and true or yes(args.dissolved)`
`   end`
`   local navargs = {`
`       bodyclass = 'vcard',`
`       name = clean(args.name),`
`       state = clean(args.state, 'autocollapse'),`
`       titlestyle = style,`
`       title = arg_title(args.title, args.teamname, args.managerlist, args.textcolor, args.american_english),`
`       listclass = 'hlist',`
`       nowrapitems = 'yes',`
`       list1 = make_list(args.list, clean(args.note), dissolved),`
`       belowstyle = style,`
`       below = clean(args.below),`
`   }`
`   local navbox = require('Module:Navbox')._navbox`
`   return navbox(navargs)`

end

local function main(frame)

`   -- Return wikitext for a navbox or an error message.`
`   local args = frame:getParent().args`
`   -- Read arguments in order of output (Module:Navbox says this puts`
`   -- reference numbers in the right order).`
`   local _`
`   _ = args.title`
`   _ = args.list`
`   _ = args.below`
`   local success, result = pcall(_main, args)`
`   if success then`
`       return result`
`   end`
`   return message(result, clean(args.name), clean(args.nocat))`

end

return { main = main, _main = _main }

[Category:Football_template_errors](https://zh.wikipedia.org/wiki/Category:Football_template_errors "wikilink")