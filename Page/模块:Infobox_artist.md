> 本文内容由[模块:Infobox artist](https://zh.wikipedia.org/wiki/模块:Infobox_artist)转换而来。


\--本模块用于执行  及  模板 --后续会将  模板亦改为通过此模块执行，但艺人信息框模板结构较为复杂，故实现起来需要更长的时间。

local p = {}

local getArgs = require('Module:Arguments').getArgs

local infobox = require('Module:Infobox').infobox

local parameterListAR -- lazily initialized

local parameterListCV -- lazily initialized

local function getDataAR(args, idx)

`   if not parameterListAR then`
`       parameterListAR = mw.loadData('Module:Infobox artist/parameterListAR')`
`   end`
`   for _, k in ipairs(parameterListAR[idx]) do`
`       if args[k] then return args[k] end`
`   end`

end

local function getDataCV(args, idx)

`   if not parameterListCV then`
`       parameterListCV = mw.loadData('Module:Infobox artist/parameterListCV')`
`   end`
`   for _, m in ipairs(parameterListCV[idx]) do`
`       if args[m] then return args[m] end`
`   end`

end

local function PageNameBase ()

`   local pagename = require('Module:String').replace{ args = { `
`       mw.title.getCurrentTitle().baseText,`
`       '%s+%b()$',`
`       '',`
`       '1',`
`       'false',`
`   } }`
`   return pagename`

end

\-- 颜色选择器、语言选择器等部件继续沿用既有的模板实现方式。 -- 等抽出时间再将其Lua化 local function getColor(frame)

`   local args = getArgs(frame)`
`   return getColor(args)`

end

local function getColor(args)

`   local color = (mw.getCurrentFrame():expandTemplate({`
`       title = '藝人/color selector',`
`       args = {args[1]}`
`       } ))`
`   return color`

end

local function getLanguage(frame)

`   local args = getArgs(frame)`
`   return getLanguage(args)`

end

local function getLanguage(args)

`   local lang = (mw.getCurrentFrame():expandTemplate({`
`       title = '藝人/lang selector',`
`       args = {args[1]}`
`       } ))`
`   return lang`

end

\-- 生/卒年月日转换 local function dateofbirth(frame)

`   local args = getArgs(frame)`
`   return dateofbirth(args)`

end

local function dateofbirth(args)

`   local dob = ''`
`   local count = 0`
`   `
`   if args.birthdate then`
`       dob = args.birthdate`
`   else`
`       if args.birthyear then`
`           count = count + 1`
`           if args.birthmonth then`
`               count = count + 1`
`               if args.birthday then`
`                   count = count + 1`
`               end`
`           end`
`       end`
`       if count < 3 then`
`           if args.birthyear then`
`               dob = args.birthyear .. '年'`
`           end`
`           if args.birthmonth then`
`               dob = dob .. args.birthmonth .. '月'`
`               if args.birthday then`
`                   dob = dob .. args.birthday .. '日'`
`               end`
`           end`
`       else`
`           if args.deathyear or args.deathmonth or args.deathday then`
`               dob = (mw.getCurrentFrame():expandTemplate({`
`                   title = 'Birth date',`
`                   args = {args.birthyear, args.birthmonth, args.birthday}`
`                   } ))`
`           else`
`               dob = (mw.getCurrentFrame():expandTemplate({`
`                   title = 'Birth date and age',`
`                   args = {args.birthyear, args.birthmonth, args.birthday}`
`                   } ))`
`           end`
`       end`
`   end`
`   return dob`

end

local function dateofdeath(frame)

`   local args = getArgs(frame)`
`   return dateofdeath(args)`

end

local function dateofdeath(args)

`   local dod = ''`
`   local count = 0`
`   `
`   if args.deathdate then`
`       dod = args.deathdate`
`   else`
`       if args.deathyear then`
`           count = count + 1`
`           if args.deathmonth then`
`               count = count + 1`
`               if args.deathday then`
`                   count = count + 1`
`                   if args.birthyear then`
`                       count = count + 1`
`                       if args.birthmonth then`
`                           count = count + 1`
`                           if args.birthday then`
`                               count = count + 1`
`                           end`
`                       end`
`                   end`
`               end`
`           end`
`       end`
`       if count < 6 then`
`           if args.deathyear then`
`               dod = args.deathyear .. '年'`
`           end`
`           if args.deathmonth then`
`               dod = dod .. args.deathmonth .. '月'`
`               if args.deathday then`
`                   dod = dod .. args.deathday .. '日'`
`               end`
`           end`
`       else`
`           dod = (mw.getCurrentFrame():expandTemplate({`
`               title = 'Death date and age',`
`               args = {args.deathyear, args.deathmonth, args.deathday, args.birthyear, args.birthmonth, args.birthday}`
`               } ))`
`       end`
`   end`
`   return dod`

end

\-- 维基数据图片检测 local function renderTrackingPhotos(frame)

`   local args = getArgs(frame)`
`   return renderTrackingPhotos(args)`

end

local function renderTrackingPhotos(args)

`   local cat = (mw.getCurrentFrame():expandTemplate({`
`       title = 'Wikidata image',`
`       args = {args[1]}`
`       } ))`
`   return cat`

end

function p.artist(frame)

`   if not parameterListAR then`
`       parameterListAR = mw.loadData('Module:Infobox artist/parameterListAR')`
`   end`
`   local args = getArgs(frame)`
`   return p._artist(args)`

end

function p._artist(args)

`   -- 艺术家信息框模板。`
`   -- --请将新增参数加于模块:Infobox artist/parameterListAR`
`   local list = {}`
`   local cont = 5`
`   `
`   list.bodyclass = 'vcard plainlist'`
`   `
`   list.above = (mw.getCurrentFrame():expandTemplate({ `
`       title = 'Br separated entries', `
`       args = { `
`           (getDataAR(args, 'honorific_prefix') and`
`               '`<span class="honorific-prefix" style="font-size:small; font-weight:normal;">`' .. getDataAR(args, 'honorific_prefix') .. '`</span>`' or ''),`
`           '`<span class=fn">`' .. (getDataAR(args, 'name') or PageNameBase() ) .. '`</span>`',`
`           (getDataAR(args, 'honorific_suffix') and`
`               '`<span class="honorific-suffix" style="font-size:small; font-weight:normal;">`' .. getDataAR(args, 'honorific_suffix') .. '`</span>`' or ''),`
`       } }))`
`   `
`   list.abovestyle = 'font-size: 120%; background: ' .. (getDataAR(args, 'death_date') and 'silver;' or (getDataAR(args, 'death_place') and 'silver;' or '#6495ED;') )`
`   list.headerstyle = 'background: ' .. (getDataAR(args, 'death_date') and 'silver;' or (getDataAR(args, 'death_place') and 'silver;' or '#6495ED;') )`
`   list.labelstyle = 'white-space:nowrap;'`
`   `
`   list.image = require('Module:InfoboxImage').InfoboxImage{ args = { `
`       image = getDataAR(args, 'image'),`
`       size = getDataAR(args, 'image_size'),`
`       sizedefault = 'frameless',`
`       upright = '1',`
`       alt = getDataAR(args, 'alt'),`
`       suppressplaceholder = yes,`
`   } }`
`   list.caption = list.image and getDataAR(args, 'caption')`
`   `
`   --list.header1 = '艺术家'`
`   `
`   list.label2 = '原文名'`
`   list.data2 = (getDataAR(args, 'native_name') and`
`       '<span class="nickname"' .. (getDataAR(args, 'native_name_lang') and ' lang="' .. getDataAR(args, 'native_name_lang') .. '" "xml:lang="' .. getDataAR(args, 'native_name_lang') .. '"' or '') .. '>-{' .. getDataAR(args, 'native_name') .. '}-`</span>`' or '')`
`   `
`   list.label3 = '出生'`
`   list.data3 = (mw.getCurrentFrame():expandTemplate({`
`       title = 'Br separated entries',`
`       args = {`
`           (getDataAR(args, 'birth_name') and`
`               '`<span class="nickname">`' .. getDataAR(args, 'birth_name') .. '`</span>`' or ''),`
`           getDataAR(args, 'birth_date'),`
`           (getDataAR(args, 'birth_place') and`
`               '`<span class="birthplace">`' .. getDataAR(args, 'birth_place') .. '`</span>`' or ''),`
`           } } ))`
`   `
`   list.label4 = '逝世'`
`   list.data4 = (mw.getCurrentFrame():expandTemplate({`
`       title = 'Br separated entries',`
`       args = {`
`           getDataAR(args, 'death_date'),`
`           (getDataAR(args, 'death_place') and`
`               '`<span class="deathplace">`' .. getDataAR(args, 'death_place') .. '`</span>`' or ''),`
`           } } ))`
`   `
`   list.label5 = '墓地'`
`   list.data5 = (mw.getCurrentFrame():expandTemplate({`
`       title = 'Br separated entries',`
`       args = {getDataAR(args, 'resting_place'), getDataAR(args, 'resting_place_coordinates')}`
`       } ))`
`   `
`   for i, k in ipairs(parameterListAR) do`
`       local data = getDataAR(args, i)`
`       if data then`
`           cont = cont + 1`
`           list['data'..cont] = data`
`           list['label'..cont] = k.label`
`           list['header'..cont] = k.header`
`       end`
`   end`
`   `
`   list.class1 = 'title role'`
`   list.class5 = 'label'`
`   list.class6 = 'category'`
`   list.class11 = 'category'`
`   list.class12 = 'category'`
`   list.class14 = 'note'`
`   list.class15 = 'org'`
`   list.rowclass17 = 'note'`
`   list.class18 = 'url'`
`   `
`   return infobox(list) .. renderTrackingPhotos( {getDataAR(args, 'image')} )`

end

function p.CV(frame)

`   if not parameterListCV then`
`       parameterListCV = mw.loadData('Module:Infobox artist/parameterListCV')`
`   end`
`   local args = getArgs(frame)`
`   return p._CV(args)`

end

function p._CV(args)

`   -- 声优模板。`
`   -- --请将新增参数加于模块:Infobox artist/parameterListCV`
`   local list = {}`
`   local cont = 12`
`   `
`   list.child = (getDataCV(args, 'embed') and getDataCV(args, 'embed'):lower() or '')`
`   list.decat = 'yes'`
`   `
`   list.bodyclass = 'vcard plainlist'`
`   `
`   if list.child == 'yes' then`
`       list.title = '\'\'\'配音生涯\'\'\''`
`   end`
`   `
`   list.aboveclass = 'fn'`
`   list.above = (getDataCV(args, 'name') or PageNameBase() )`
`   `
`   list.abovestyle = 'font-size: 120%; background: ' .. getColor( {'配音员'} )`
`   if list.child ~= 'yes' then`
`       list.headerstyle = 'background: ' .. getColor( {'配音员'} )`
`   end`
`   list.labelstyle = 'white-space:nowrap;'`
`   `
`   list.image = require('Module:InfoboxImage').InfoboxImage{ args = { `
`       image = getDataCV(args, 'image'),`
`       size = getDataCV(args, 'image_size'),`
`       sizedefault = 'frameless',`
`       upright = '1',`
`       alt = getDataCV(args, 'alt'),`
`       suppressplaceholder = yes,`
`   } }`
`   list.caption = list.image and getDataCV(args, 'caption')`
`   `
`   if list.child ~= 'yes' then`
`       list.header1 = '-{zh-hans:配音演员;zh-hant:配音員;}-'`
`   end`
`   `
`   list.label2 = '本名'`
`   list.data2 = getDataCV(args, 'real_name')`
`   `
`   list.label3 = '原文名'`
`   list.data3 = (getDataCV(args, 'native_name') and`
`       '<span class="nickname"' .. (getDataCV(args, 'native_name_lang') and ' lang="' .. getLanguage( {getDataCV(args, 'native_name_lang')} ) .. '" "xml:lang="' .. getLanguage( {getDataCV(args, 'native_name_lang')} ) .. '"' or '') .. '>-{' .. getDataCV(args, 'native_name') .. '}-`</span>`' or '')`
`   `
`   list.label4 = '罗马拼音'`
`   list.data4 = (getDataCV(args, 'romanized_name') and`
`       '`<span class="nickname" lang="en" xml:lang="en">`' .. getDataCV(args, 'romanized_name') .. '`</span>`' or '')`
`   `
`   list.label5 = '英文名'`
`   list.data5 = (getDataCV(args, 'english_name') and`
`       '`<span class="nickname" lang="en" xml:lang="en">`' .. getDataCV(args, 'english_name') .. '`</span>`' or '')`
`   `
`   list.label6 = '昵称'`
`   list.data6 = getDataCV(args, 'nickname')`
`   `
`   list.label7 = '艺名'`
`   list.data7 = getDataCV(args, 'other_name')`
`   `
`   list.label8 = '国籍'`
`   list.data8 = getDataCV(args, 'nationality')`
`   `
`   list.label9 = '籍贯'`
`   list.data9 = getDataCV(args, 'hometown')`
`   `
`   list.label10 = '出生'`
`   list.data10 = (mw.getCurrentFrame():expandTemplate({`
`       title = 'Br separated entries',`
`       args = {`
`           (getDataCV(args, 'birth_name') and`
`               '`<span class="nickname">`' .. getDataCV(args, 'birth_name') .. '`</span>`' or ''),`
`           dateofbirth( {`
`               birthyear = getDataCV(args, 'birthyear'),`
`               birthmonth = getDataCV(args, 'birthmonth'),`
`               birthday = getDataCV(args, 'birthday'),`
`               deathyear = getDataCV(args, 'deathyear'),`
`               deathmonth = getDataCV(args, 'deathmonth'),`
`               deathday = getDataCV(args, 'deathday')`
`               } ),`
`           (getDataCV(args, 'birth_place') and`
`               '`<span class="birthplace">`' .. getDataCV(args, 'birth_place') .. '`</span>`' or ''),`
`           } } ))`
`   `
`   list.label11 = '出身地'`
`   list.data11 = getDataCV(args, 'origin_place')`
`   `
`   list.label12 = '逝世'`
`   list.data12 = (mw.getCurrentFrame():expandTemplate({`
`       title = 'Br separated entries',`
`       args = {`
`           dateofdeath( {`
`               birthyear = getDataCV(args, 'birthyear'),`
`               birthmonth = getDataCV(args, 'birthmonth'),`
`               birthday = getDataCV(args, 'birthday'),`
`               deathyear = getDataCV(args, 'deathyear'),`
`               deathmonth = getDataCV(args, 'deathmonth'),`
`               deathday = getDataCV(args, 'deathday')`
`               } ),`
`           (getDataCV(args, 'death_place') and`
`               '`<span class="deathplace">`' .. getDataCV(args, 'death_place') .. '`</span>`' or ''),`
`           } } ))`
`   `
`   for i, m in ipairs(parameterListCV) do`
`       local data = getDataCV(args, i)`
`       if data then`
`           cont = cont + 1`
`           list['data'..cont] = data`
`           list['label'..cont] = m.label`
`           list['header'..cont] = m.header`
`       end`
`   end`
`   `
`   cont = cont + 1`
`   list['header'..cont] = (getDataCV(args, 'years_active') and '活动' or (getDataCV(args, 'debut_work') and '活动' or (getDataCV(args, 'famous_work') and '活动' or '' ) ) )`
`   `
`   cont = cont + 1`
`   list['label'..cont] = '任职纪录'`
`   list['data'..cont] = getDataCV(args, 'years_active')`
`   `
`   cont = cont + 1`
`   list['label'..cont] = '出道作'`
`   list['data'..cont] = getDataCV(args, 'debut_work')`
`   `
`   cont = cont + 1`
`   list['label'..cont] = '代表作'`
`   list['data'..cont] = getDataCV(args, 'famous_work')`
`   `
`   cont = cont + 1`
`   list['label'..cont] = '网站'`
`   list['data'..cont] = getDataCV(args, 'website')`
`   `
`   cont = cont + 1`
`   list['label'..cont] = '其他'`
`   list['data'..cont] = getDataCV(args, 'footnotes')`
`   `
`   cont = cont + 1`
`   list['data'..cont] = getDataCV(args, 'misc')`
`   `
`   list.class1 = 'title role'`
`   list.class2 = 'nickname'`
`   list.class6 = 'nickname'`
`   list.class7 = 'nickname'`
`   list.class8 = 'category'`
`   list.class18 = 'category'`
`   list.class24 = 'url'`
`   list.class25 = 'note'`
`   `
`   if list.child ~= 'yes' then`
`       list.belowclass = 'noprint'`
`       list.below = '`[`-{zh-hans:配音演员;zh-hant:配音員;}-`](../Page/配音員.md "wikilink")`：`[`模板`](https://zh.wikipedia.org/wiki/Template:配音員 "wikilink")` | `[`分类`](https://zh.wikipedia.org/wiki/Category:配音員 "wikilink")`'`
`       list.belowstyle = 'border-top:1px solid #aaa; padding-top:0.2em; text-align:right; font-size:80%;'`
`       return infobox(list) .. renderTrackingPhotos( {getDataCV(args, 'image')} )`
`   else`
`       return infobox(list)`
`   end`

end

return p