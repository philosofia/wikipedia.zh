> 本文内容由[模块:Chemicals](https://zh.wikipedia.org/wiki/模块:Chemicals)转换而来。


local p = {} local origArgs local error = require( 'Module:Error' ) local element = {} local lib_arg = {} local strings = require( 'Module:String' ) local element_data = {} function p.formula(frame)

`   -- For calling from #invoke.`
`   local args`
`   if frame == mw.getCurrentFrame() then`
`       -- We're being called via #invoke. The args are passed through to the module`
`       -- from the template page, so use the args that were passed into the template.`
`       if lib_arg.getArgs == nil then lib_arg = require('Module:Arguments') end`
`       args = lib_arg.getArgs(frame) --frame.args`
`   else`
`       -- We're being called from another module or from the debug console, so assume`
`       -- the args are passed in directly.`
`       args = frame`
`   end`
`   return p._formula(args)`

end

function p.reaction(frame)

`   -- For calling from #invoke.`
`   local args`
`   if frame == mw.getCurrentFrame() then`
`       -- We're being called via #invoke. The args are passed through to the module`
`       -- from the template page, so use the args that were passed into the template.`
`       if lib_arg.getArgs == nil then lib_arg = require('Module:Arguments') end`
`       args = lib_arg.getArgs(frame) --frame.args`
`   else`
`       -- We're being called from another module or from the debug console, so assume`
`       -- the args are passed in directly.`
`       args = frame`
`   end`
`   return p._reaction(args)`

end

function p.check_CAS(cas_no)

`   arrs = strings.split(cas_no, '-', true, false)`
`   split_num = tonumber(table.getn(arrs))`
`   --avoid nil`
`   if (split_num and split_num  ~= '') then `
`       if (split_num == 3) then `
`           --cas no have 3 pattern`
`       else`
`           return 'false'`
`       end`
`   else`
`       --if nil`
`       return 'false'`
`   end`
`   cas_without_desh = arrs[1] .. arrs[2]`
`   `
`   check_length = {}    -- new array`
`   for seq_it=1, 3 do`
`     check_length[seq_it] = mw.ustring.len(arrs[seq_it])`
`   end`
`   `
`   if (check_length[1] < 2 or check_length[1] > 7) then return 'false' end`
`   if (check_length[2] ~= 2) then return 'false' end`
`   if (check_length[3] ~= 1) then return 'false' end`
`   `
`   cas_check = tonumber(arrs[3])`
`   if (cas_check and cas_check  ~= '') then `
`   else`
`       return 'false'`
`   end`
`   cas_len = mw.ustring.len(cas_without_desh)`
`   cas_sum = 0`
`   for i = 1,cas_len do`
`       index = cas_len + 1 -i`
`       cas_symbol = tonumber(cas_without_desh:sub(index,index))`
`       if (cas_symbol and cas_symbol  ~= '') then `
`           cas_sum = cas_sum + (cas_symbol*i)`
`       else`
`           return 'false'`
`       end`
`   end`
`   if ((cas_sum % 10) == cas_check) then `
`       return 'true'`
`   else`
`       return 'false'`
`   end`
`   return 'false'`

end

function p.check_CAS_test(frame)

`   -- For calling from #invoke.`
`   local load_args`
`   if frame == mw.getCurrentFrame() then`
`       -- We're being called via #invoke. The args are passed through to the module`
`       -- from the template page, so use the args that were passed into the template.`
`       if lib_arg.getArgs == nil then lib_arg = require('Module:Arguments') end`
`       load_args = lib_arg.getArgs(frame) --frame.args`
`   else`
`       -- We're being called from another module or from the debug console, so assume`
`       -- the args are passed in directly.`
`       load_args = frame`
`   end`
`   args = {}`
`   for k, v in pairs( load_args ) do`
`       args[k] = v;       `
`   end `
`   return p._check_CAS_test(args)`

end

function p._check_CAS_test(args)

`   -- For calling from #invoke.`
`   if (args[1] and args[1]  ~= '') then `
`       casid = args[1]`
`   else`
`       casid = "000-00-0"`
`   end`
`   return p.check_CAS(casid)`

end

function put_elements(element_name, count)

`   body = ''`
`   if element._element_symbol == nil then element = require('Module:Element') end`
`   local check_group = mw.ustring.gsub(element_name,"`<官能基/>`","")`
`   if element_name ~= check_group then`
`       if( tonumber(count) ~= nil and tonumber(count) > 1 )then`
`           body = body .. '(' .. check_group .. ')' .. "`<sub>`"``   ``..``   ``tostring(count)``   ``..``   ``"`</sub>`"`
`       else body = body .. check_group end`
`   else`
`       local number = 1 if tonumber(count) ~= nil then number = tonumber(count) end`
`       if(link and link ~= '' or link == 'nolink')then`
`           body = body .. element._element_symbol({element_name,number})`
`       else`
`           body = body .. element._elementlink({element_name,number})`
`       end`
`   end`
`   return body`

end

function p._formula(args)

`   local body = ''`
`   if (args['link'] and args['link']  ~= '') then link = args['link'] end`
`   last=''`
`   if element._element_symbol == nil then element = require('Module:Element') end`
`   for v, x in ipairs(args) do `
`       number=tonumber(x)`
`       lastn=tonumber(last)`
`       if(number)then`
`           if((not (lastn)) and last ~= '')then`
`               body = body .. put_elements(last, x)`
`           else if(body == '' and last == '')then`
`               body = x .. body `
`           else if (lastn)then`
`               if(number==1)then`
`                   body = body .. '`<sup>`+`</sup>`'`
`               else if(number==-1)then`
`                   body = body .. '`<sup>`-`</sup>`'`
`               else if(number>0)then`
`                   body = body .. '`<sup>`'..``   ``number``   ``..'+`</sup>`'`
`               else if(number<0)then`
`                   body = body .. '`<sup>`'..``   ``-number``   ``..'−`</sup>`'`
`               end end end end`
`           end end end`
`       else`
`           if ((not (lastn)) and last ~= '') then`
`               body = body .. put_elements(last, 1)`
`           end`
`       end`
`       last=x`
`   end`
`   lastn=tonumber(last)`
`   if ((not (lastn)) and last ~= '') then`
`       body = body .. put_elements(last, 1)`
`   end`
`   if(link and link ~= '' or link == 'nolink')then`
`       if(link ~= '#' and link ~= 'nolink')then`
`           body = '`[`'``   ``..``   ``body``   ``..'`](https://zh.wikipedia.org/wiki/'_.._link_.._' "wikilink")`'`
`       end`
`   end`
`   return body`

end

function p._reaction(args)

`   local body = ''`
`   last=''`
`   if element._elementlink == nil then element = require('Module:Element') end`
`   for v, x in ipairs(args) do `
`       number=tonumber(x)`
`       lastn=tonumber(last)`
`       local check_text = mw.ustring.gsub(last,"`<文字/>`","")`
`       if(number)then`
`           if((not (lastn)) and last ~= '')then`
`               feq = ''`
`               if(number>1)then feq = feq .. number end`
`               if (last == '+') then`
`                   body = body .. ' + ' .. feq`
`               elseif (last == 'eq' or last == '→') then`
`                   body = body .. ' → ' .. feq`
`               elseif (last == '↑') then`
`                   body = body .. '↑ ' .. feq`
`               elseif (last == '↓') then`
`                   body = body .. '↓ ' .. feq`
`               elseif (last == 'eqm') then`
`                   body = body .. ' `[`Equilibrium.svg`](https://zh.wikipedia.org/wiki/File:Equilibrium.svg "fig:Equilibrium.svg")` ' .. feq`
`               elseif (last ~= check_text) then`
`                   body = body .. check_text .. feq`
`               else`
`                   body = body .. put_elements(last, x)`
`               end`
`           else if(body == '' and last == '')then`
`               body = x .. body `
`           else if (lastn)then`
`               if(number==1)then`
`                   body = body .. '`<sup>`+`</sup>`'`
`               elseif(number==-1)then`
`                   body = body .. '`<sup>`-`</sup>`'`
`               elseif(number>0)then`
`                   body = body .. '`<sup>`'..``   ``number``   ``..'+`</sup>`'`
`               elseif(number<0)then`
`                   body = body .. '`<sup>`'..``   ``-number``   ``..'−`</sup>`'`
`               end`
`           else`
`               body = last .. x .. body `
`           end end end`
`       else`
`           if ((not (lastn)) and last ~= '') then`
`               if (last == '+') then`
`                   body = body .. ' + '`
`               elseif (last == 'eq' or last == '→') then`
`                   body = body .. ' → '`
`               elseif (last == '↑') then`
`                   body = body .. '↑ '`
`               elseif (last == '↓') then`
`                   body = body .. '↓ ' `
`               elseif (last == 'eqm') then`
`                   body = body .. ' `[`Equilibrium.svg`](https://zh.wikipedia.org/wiki/File:Equilibrium.svg "fig:Equilibrium.svg")` '`
`               elseif (last ~= check_text) then`
`                   body = body .. check_text`
`               else`
`                   body = body .. put_elements(last, 1)`
`               end`
`           end`
`       end`
`       last=x`
`   end`
`   lastn=tonumber(last)`
`   if ((not (lastn)) and last ~= '') then`
`       local check_text = mw.ustring.gsub(last,"`<文字/>`","")`
`       if (last == '+') then`
`           body = body .. ' + '`
`       elseif (last == 'eq' or last == '→') then`
`           body = body .. ' → '`
`       elseif (last == '↑') then`
`               body = body .. '↑ '`
`       elseif (last == '↓') then`
`               body = body .. '↓ ' `
`       elseif (last == 'eqm') then`
`           body = body .. ' `[`Equilibrium.svg`](https://zh.wikipedia.org/wiki/File:Equilibrium.svg "fig:Equilibrium.svg")` '`
`       elseif (last ~= check_text) then`
`           body = body .. check_text`
`       else`
`           body = body .. put_elements(last, 1)`
`       end`
`   end`
`   return body`

end

\--本模塊的沙盒(測試)函數 function p.sandbox(frame)

`   -- For calling from #invoke.`
`   local args`
`   if frame == mw.getCurrentFrame() then`
`       -- We're being called via #invoke. The args are passed through to the module`
`       -- from the template page, so use the args that were passed into the template.`
`       if lib_arg.getArgs == nil then lib_arg = require('Module:Arguments') end`
`       args = lib_arg.getArgs(frame) --frame.args`
`   else`
`       -- We're being called from another module or from the debug console, so assume`
`       -- the args are passed in directly.`
`       args = frame`
`   end`
`   return p._reaction(args)`

end function p._sandbox(args)

`   if element.getListID == nil then element = require('Module:Element') end`
`   if element_data[1] == nil then element_data = require('Module:Element/data') end`
`   return element_data[element.getListID(args[1])].name `

end return p