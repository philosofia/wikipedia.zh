> 本文内容由[模块:Lan](https://zh.wikipedia.org/wiki/模块:Lan)转换而来。


local l={} local getArgs

local args l.fallbackList={

`    ['zh']={'zh','zh-hans','zh-cn','zh-tw','zh-hk','zh-mo','zh-sg','zh-my'}`
`   ,['zh-hans']={'zh-hans','zh-cn','zh-sg','zh-my','zh'}`
`   ,['zh-hant']={'zh-hant','zh-tw','zh-hk','zh-mo','zh'}`
`   ,['zh-cn']={'zh-cn','zh-hans','zh-sg','zh-my','zh'}`
`   ,['zh-sg']={'zh-sg','zh-hans','zh-cn','zh-my','zh'}`
`   ,['zh-my']={'zh-my','zh-hans','zh-cn','zh-sg','zh'}`
`   ,['zh-tw']={'zh-tw','zh-hant','zh-hk','zh-mo','zh'}`
`   ,['zh-hk']={'zh-hk','zh-hant','zh-mo','zh-tw','zh'}`
`   ,['zh-mo']={'zh-mo','zh-hant','zh-hk','zh-tw','zh'}`

}

function l._main(args, frame)

`   local userlanguage=frame:callParserFunction{ name = 'int', args = {'Conversionname'} }`
`   --mw.message.new('Conversionname'):plain()`
`   local fallback=l.fallbackList[userlanguage]`
`   if fallback == nil then`
`       fallback=l.fallbackList['zh']`
`   end`
`   for _,langArgName in ipairs(fallback)  do`
`       if  args[langArgName] ~= nil then`
`           return args[langArgName]`
`       end`
`   end`
`   return ''`

end

function l.main(frame)

`   if not getArgs then`
`       getArgs = require('Module:Arguments').getArgs`
`   end`
`   args = getArgs(frame, {parentFirst=true})`
`       return l._main(args, frame)`

end

return l