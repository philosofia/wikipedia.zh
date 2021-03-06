> 本文内容由[Visual Basic for Applications](https://zh.wikipedia.org/wiki/Visual_Basic_for_Applications)转换而来。


**V**isual **B**asic for **A**pplications（**VBA**）是[Visual Basic的一種](../Page/Visual_Basic.md "wikilink")[巨集語言](https://zh.wikipedia.org/wiki/宏 "wikilink")，主要能用來擴展Windows的應用程式功能，特別是[Microsoft Office軟體](../Page/Microsoft_Office.md "wikilink")。也可說是一種應用程式視覺化的Basic Sc​​ript。 1994年發行的[Excel](https://zh.wikipedia.org/wiki/Excel "wikilink") 5.0版本中，即具備了VBA的巨集功能。

## 數據類型

### 基本數據類型

即Primary Type Data，下述列表的括號內為字節數：

  - Byte (1)：无符号类型，取值范围0-255
  - Boolean (2)
  - Integer (2)
  - Long (4)
  - Single (4)
  - Double (8)
  - Currency (8)
  - Decimal (14)
  - Date (8)
  - String
  - Object (4)
  - Variant （根据分配确定）

### 自定义的数据类型

相当于C语言的struct，例如：

`Type 自定义类型名`
`     元素名  As 类型`
`      …`
`     [元素名 As 类型]`
`End Type `

### 數組

``` vb
Option Base 0 '數組索引值從0開始
Option Base 1 '數組索引值從1開始
Dim MyArray(10) '聲明一個數組變量，10是最大的可用的數組索引值
MyArray(5) = 101 '給數組的元素賦值
Dim Data(10,5) '聲明一個二維數組變量
Data(1,1) = "A001" '給數組元素賦值
Dim cArr(-11 To 20, 1 To 3) As String '聲明一個數組，定義數組索引值的上下界
Dim dArr() As String '聲明動態數組
ReDim dArr(0 To 5, 1 To 2) '改變動態數組的尺寸默認把原數據清除。如果保留原來的數據，必須加上參數Preserve。
                                '使用Preserve參數時只能改變最後一維的大小
If UBound(vTemp) = -1 Then
     '判斷數組變量vTemp是否為 空數組
End If
Erase MyArrar, Data 'Eras​​e語句清除數組元素，釋放變量佔用的空間
```

## 常量

日期常量由符号“\#”将字符括起来，如\#2012-1-1\#。

系统定义常量有3个：True、False和Null。

固有常量是编程时引用的对象库定义的常量。所有固有常量都可以在宏或VBA代码中使用。通常，固有常量通过前两个字母来指明定义该常量。来自VB库的常量则以“vb”开头。来自Access的常量以“ac”开头。可以使用对象浏览器来查看所有对象库中的固有常量列表。

可以自行定义常量。如：

`Global Const 符号常量名称 = 常量值`

## 调用DLL

例如：

`Private Declare Function getFrequency Lib "kernel32" _ Alias "QueryPerformanceFrequency" (cyFrequency As Currency) As Long`
`Private Declare Function getTickCount Lib "kernel32" _ Alias "QueryPerformanceCounter" (cyTickCount As Currency) As Long`

## 控制結構

### if 語句

`if 條件1 then`
`   語句1`
`elseif 條件2 then`
`   語句2`
`elseif ...`
`    ...`
`else`
`   語句n`
`end if`

### Select Case 語句

`Select Case 表達式`
`   Case 表達式列表1`
`       語句1`
`   Case 表達式列表2`
`       語句2`
`       ...`
`   Case 表達式列表n`
`       語句n`
`End Select `

其中的表達式列表可以为：

  - 表达式 例： "A"
  - 用逗号分隔的一组枚举表达式 例：2,4,6,8
  - 表达式1 To 表达式2 例：60 To 100
  - Is 关系运算符表达式 例：Is \< 60

### Do...Loop 語句

`Do While或Until 條件`
`   語句塊1`
`   Exit Do`
`   語句塊2`
`Loop`

`Do`
`   語句塊1`
`   Exit Do`
`   語句塊2`
`Loop While或Until 條件`

### For...Next語句

`For 循環控制變量=初值To 終值Step 步長`
`   語句塊 ‘Exit For語句可以跳出循環體`
`Next`

### For Each … Next語句

`For Each 循環控制變量 In 集合變量`
`   語句塊 `
`   Exit For語句可以跳出循環體`
`Next 循環控制變量`

### 跳出本次循环的continue语句

VBA没有类似C语言的continue语句。通常可如此写程序：

``` vb
 For 循環控制變量=初值 To 終值 Step 步長
    Do '用于模拟continue
        語句塊
        If 条件 Then Exit Do '用于模拟continue
        語句塊
    Loop While False '用于模拟continue
 Next
```

### With語句

`With 對象引用`
`   語句塊`
`End With`

### On Error語句

`On Error Goto 出錯處理語句的label '跳轉到出錯處理語句`

或

`On Error Resume Next '遇到錯誤，不管錯誤，繼續往下執行`

### 具有控制作用的函数

  - IIf(条件式,表达式1,表达式2)
  - Switch(条件式1,表达式1,\[条件式2,表达式2\[,...,条件式n,表达式n\]\])
  - Choose(索引式,选项1\[,选项2,...\[,选项n\]\]) '这是基于1的索引

## 其他語句

### 註釋語句

使用REM或者單引號開始的行。

### 語句的連寫與續行

如果一行包括多條語句，用冒號分割各個語句。跨多行的語句，在行末用“空格加下劃線”表示續行。

## 過程與函數

`Sub 過程名(參數表)`
`    語句塊`
`    Exit Sub`
`    語句塊`
`End Sub`

 

`Function 函數名(參數表) As Type`
`   語句塊`
`   函數名=表達式`
`   Exit Function`
`End Function`

可以是Private、Public、Friend、Static等修飾。

调用函数/过程时，可以加括号或者不加括号。如果调用表达式作为一行的一部分，那么必须用参数，例如函数调用的返回值赋给变量。 调用过程时， 可以使用/不使用call关键字。使用call语句调用过程，如果无参数，则不加括号；如果有参数，必须加括号。如果调用时用括号包住单个参数，则该参数强行按值传递。需要特别注意，不用call不加括号的调用，形参与实参是传值(passed by value)而不是传引用(passed by reference)，这会导致一些对象的方法调用失败。例如：

``` vb
    Dim cn As ADODB.Connection
    Set cn = CurrentProject.Connection
    Dim rs As New ADODB.Recordset
    rs.Open "SELECT * FROM myTable" , cn

    Dim ExcelApp As New Excel.Application
    Dim ExcelWst As Worksheet
    Set ExcelWst = ExcelApp.Workbooks.Add.Worksheets(1)

    ExcelWst.Range("A2").CopyFromRecordset(rs) '失败，无法执行该行
    ExcelWst.Range("A2").CopyFromRecordset rs  '可成功执行该行
```

## 常用内置函数

VBA的常用内置函数列表参见：[1](https://msdn.microsoft.com/en-us/library/jj692811.aspx)

  - MsgBox
  - InputBox
  - 舍入函数：Fix 向0取整,Int向下取整, Round四舍五入
  - Rnd 返回0-1内的单精度随机数
  - 字符串函数：
      - Filter：对字符串的一维数组的过滤
      - InStr(\[Start, \]<Str1>,<Str2>\[, Compare\])与InStrRev： 查找子串
      - Len 字符串长度
      - Join：连接一维数组中的所有子字符串
      - Left,Right,Mid 截取子字符串
      - Space(数值) 生成空格字符串
      - Ucase,Lcase 大小写转换函数
      - Ltrim, Rtrim,Trim 删除首尾空格
      - Replace
      - Split：分割一个字符串成为一维数组
      - StrComp：字符串比较
      - StrConv：字符串转换
      - String(number, character)：制定字符重复若干次
      - StrReverse
  - 日期/时间有关函数：
      - Year, Month, Day, WeekDay,Hour,Minute,Second 截取日期时间分量
      - DateAdd 日期/时间增量函数
      - DateDiff(<间隔类型>,<日期1>,<日期2>\[,W1\]\[,W2\])日期/时间的距离函数
      - DatePart(<分割类型>,<日期>\[,w1\]\[,w2\])时间分割函数
      - DateSerial(<表达式1>,<表达式2>,<表达式3>) 合成日期；DateValue(“字符串表达式”)返回日期；
      - Date,Time,Now,Timer 返回日期时间
      - DateValue
      - TimeSerial：由时间序列得到时间对象
      - TimeValue：由时间字符串得到时间对象
      - Weekday：获得日期的周几
      - WeekdayName
  - 转换函数：CBool、CByte、CCur、 CDate、 CDbl、CDec、CInt、 CLng、CLngLng、CLngPtr、CSng、CStr、CVar、CVErr、Asc(<字符串表达式>)返回第一个字符的Ascii编码值、Chr(ASCII码)返回字符、Hex、Oct、Str(<数值表达式>)返回字符串、Val(string)、Format、FormatCurrency、FormatDateTime、FormatNumber、FormatPercent、MonthName
  - Nz(表达式或字段属性值\[,规定值\])如果是空，则返回0或者""或者函数的第二个参数值
  - 验证函数：isNumeric、isDate、isNull、isEmpty IsArray、IsError、IsMissing、IsObject
  - 数学函数：Abs、Sqr、Tan、Atn（即atan）、Sin、Cos、Exp（e为基的指数）、Log自然对数
  - Array:构造一个Array对象
  - CallByName: get or set a property, or invoke a method at run time using a string name.
  - 控制流：Choose:类似于C语言的select语句、IIf相当于IF-ELSE语句、Switch
  - Command：获取命令行参数
  - CreateObject：创建ActiveX对象
  - CurDir：返回指定驱动器的当前工作路径
  - 由基本数学函数导出的函数：Sec、Cosec、Cotangent、Cotan、Arcsin、Arccos、Arcsec、Arccosec、Arccotan、HSin、HCos、HTan、HSec、HCosec、HCotan、HArcsin、HArccos、HArctan、HArcsec、HArccosec、HArccotan、LogN
  - DoEvents：暂时把CPU控制权交回给系统。
  - Environ：返回环境变量的值
  - 文件操作：
      - Dir：返回满足条件的所有文件、目录的名字
      - EOF
      - FileAttr
      - FileDateTime
      - FileLen
      - FreeFile Function
      - GetAttr：返回文件、目录的属性值
      - Input：读取文件
      - Loc：文件指针位置
      - LOF：文件打开时的指针位置
      - Seek：文件指针定位
      - Spc：使用Print做position output
      - Tab：用于Print函数
  - Error:错误号对应的错误消息
  - [Windows Registry中的数据](https://zh.wikipedia.org/wiki/Windows_Registry "wikilink")：GetAllSettings、SaveSetting、DeleteSetting、GetSetting
  - GetObject：ActiveX组建的引用
  - IMEStatus：返回当前Input Method Editor (IME)。
  - Macintosh平台：MacID、MacScript
  - 金融函数：
      - DDB：使用double-declining balance计算贬值
      - FV:计算固定利率的年金
      - IPmt：计算利率
      - IRR：计算利率
      - MIRR：计算利率
      - NPer：计算周期数
      - NPV：计算net present value
      - Pmt：计算支付数
      - PPmt：计算本金支付数
      - PV：计算present value
      - Rate：利息率
      - SLN：straight-line depreciation
      - SYD：计算sum-of-years' digits depreciation
  - Partition：返回字符串，表示一个数值名字落在各个range内。常用于SQL select语句
  - QBColor：颜色值
  - RGB：颜色值
  - TypeName：得到变量的类型名
  - VarType：得到变量的类型数

## 表达式

比较特殊的运算符有指数运算^，浮点除法/，整数除法\\，取模运算Mod，不等逻辑比较运算\<\>

## 參考文獻

  - \[<https://msdn.microsoft.com/en-us/library/dd941266(v=office.14>).aspx VBA Language Reference for MS Office 2013\]
  - \[<https://msdn.microsoft.com/zh-cn/library/office/gg2>​​64383.aspx Office VBA 語言參考中文版for MS Office 2013\]
  - [Office VBA 對像庫的引用for MS Office 2013](https://web.archive.org/web/20151225071350/https://msdn.microsoft.com/ZH-CN/library/office/ff862474.aspx)
  - [VBA & Visual Basic Sc​​ripting 中文版語言參考](http://www.jb51.net/shouce/vbs/vtoriVBScript.htm)

## 外部連結

  - 官方網站：[大陸簡體](http://msdn.microsoft.com/zh-cn/office/ff688774.aspx)[台灣正體](http://msdn.microsoft.com/zh-tw/office/ff688774.aspx)

[Category:Microsoft_Office](https://zh.wikipedia.org/wiki/Category:Microsoft_Office "wikilink") [Category:程序設計語言](https://zh.wikipedia.org/wiki/Category:程序設計語言 "wikilink")