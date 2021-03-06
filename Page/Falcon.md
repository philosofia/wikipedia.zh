> 本文内容由[Falcon](https://zh.wikipedia.org/wiki/Falcon)转换而来。


**Falcon编程语言**（），又稱**Falcon P.L.**、**Falconpl**或**Falcon**，是一个[开源](https://zh.wikipedia.org/wiki/开源 "wikilink")、多范式[编程语言](../Page/编程语言.md "wikilink")，其设计和推廣由Giancarlo Niccolai领导。

## 歷史

Haste於2002年編寫一個小型項目，用以實現一小型[虛擬機](https://zh.wikipedia.org/wiki/虛擬機 "wikilink")，該項目很快的發展成Falcon語言。2008年，此語言以[開源項目的方式成為](https://zh.wikipedia.org/wiki/開源項目 "wikilink")[Ubuntu](../Page/Ubuntu.md "wikilink")的附加軟體，並且被包含在[Kross](../Page/Kross.md "wikilink")。

## 核心

不同于关注于一个编程风格或范式（paradigm），Falcon在一个简单的框架（framework）里融合了几种不同的风格。在实现级别上，Falcon是「服务概念」驱动，当不作为一个单一的工具被使用时脚本引擎被看做一个服务脚本，模块和内嵌的应用。

## Hello Falcon

尽管有各种形式的基本I/O，一个"hello world"（全世界朋友你好\!）例子使用*fast print*(快速列印):

`> "Hello World!"`

[Unicode支持](https://zh.wikipedia.org/wiki/Unicode "wikilink")，下面是一个国际化例子的介绍：

`// International class; name and street`
`class 国際(なまえ, Straße)`
`   // set class name and street address`
`   नाम = なまえ`
`   شَارِع = Straße`
`   // Say who am I!`
`   function 言え!()`
`     >@"I am $(self.नाम) from ",self.شَارِع`
`   end`
`end`
`// all the people of the world!`
`民族 = [国際("高田 Friederich", "台湾"),`
`   国際("Smith Σωκράτης", "Cantù"),`
`   国際("Stanisław Lec", "południow")]`

`for garçon in 民族：garçon.言え!()`

### 数据类型

  - Nil - The *nil*关键字，一个空值.
  - Integer - 一个64位整数值.
  - Numeric - 一个IEEE 64位浮点值.
  - Range - 一组上限，下限和步长.
  - MemBuf - Raw内存缓冲，每一个地址是一个无符号的1,2,3,或者4字节整数.
  - Function - 函数（可调用实体）.
  - String - 不定长的UNICODE字符序列 (但是它们能作为字节缓冲被使用).
  - Array - 不定长的元素序列.
  - Dictionary - 不定长有序键/值对的集合;键能是任何Falcon元素.
  - Object - 来源于类的实例或者单一的非类对象.
  - Class - 能创建实例的类，实体.
  - Method - 实例的不变部分，使用函数形式关联.

## 范式

Falcon融合六种*主流*编程范式。

  - 过程式（procedural）
  - 函数式（functional）
  - 面向对象（object oriented）
  - 面向原型对象（prototype OOP）
  - 面向消息（message oriented）
  - 表格化编程（tabular programming）

### 过程式

过程式编程通过典型的函数声明和调用被支持。每一个函数支持隐式变量参数调用和占位参数（Positional Parameters）命名参数（Named Parameters）。提供了一套过程式风格的语句（如for, while, if, switch语句）。

下面，一个完整的过程式程序，突出一部分在**Falcon**里用来减少一些编程任务中固有的pre-body-post（前置-本體-後置）处理的困扰的设计理念

`function sayList( saying )`
`   for elem in saying`
`       >> elem`
`       formiddle: >> " "`
`       forlast: > "!"`
`   end`
`end`

`sayList( List("Have", "a", "nice", "day") )`

### 函数式

Falcon有个称为Sigma-reductor的求值引擎，它允许程序人员编写纯函数式程序，看起来和用[Lisp没什么不同](https://zh.wikipedia.org/wiki/Lisp "wikilink")。混合式编程风格允许在函数式语句序列使用不同的范式（例如OOP或者过程化），或者在不同的过程化方式期间中使用函数式求值。

函数式语句序列被描述为标准语言数组；交叉不同的求值和在Sigma-reduction求值方式期间这都意味着语句序列能被程序本身创建，审查和被动态修改。下面的例子在列表循环调用*late binding*修改一个指定变量的引用。

` pnext = [ printl, '"', &value, '"' ]`

` dolist( function(p); seq.value = p; eval(seq); end,`
`         ["Have", "a", "nice", "day"] )`

如果他们第一个成员变量是一个自身可调用元素，标准数组作为函数被调用，如下面的例子。

` [printl "Prompt> "]( "Real data to print" )`

同一个级别函数式语句序列（如在上面例子）能被作为存储的调用来按照定义处理，并且一次性分配给一个变量，它们在语意上等同于一个函数符号。

函数式范式包含一个*out of band*元素标记。元素能接收一个通过语言操作符和函数被测试的*oob*特征标记，并且当在函数式语句序列中移动时指明一个特殊含义的值。例如，很多函数式循环，如*floop*和*times*，能重新开始执行循环，或者被从包含的函数返回的无论*1*或*0*的out of band中断。*map*函数通过一个映射函数转换一个数组中的所有值，如果它是一个*nil*out of band将忽略返回值（丢弃它）；通过这个方法可以在某处执行映射和过滤。

### 面向对象

通过类，一个继承模型，静态类成员，属性初始化和实例构造器，Falcon编程语言提供一个OOP范式。在至多一个潜在的父类是被反射成原生数据的条件下支持多继承。访问基类成员被支持。

实例的结构是固定和不变的，但是由于Falcon函数式特质，函数看上去就是一种特定种类的数据，它能动态设置实例成员为无格式数据或者函数（变成他们的方法）。

Falcon支持单一对象，可能是classless或者父类派生，在虚拟机执行主脚本之前实例化和被准备。在可能涉及程序模块中一个在其他的对象时，实例消除顺序由Falcon链接器追踪以确保单一对象的适当的初始化。

通过函数式语句序列类实例能被创建，如实例化的一个类在语意上等于调用它的符号，因此，对一个第一个元素是一个类的函数式语句序列求值，它有创建一个实例的效果。

Falcon的OOP模型完整支持操作符重载，它允许创建一个针对数学和逻辑的拥有指定的行为操作符的类。

### 面向原型对象

原型OOP比OOP更简单，但它去掉类的概念。实例全是classless，他们的结构能被动态改变。Falcon语言字典（排列好的键/值集合）能包含函数，那时字典能被*祝福*，通知语言他们作为classless实例被处理，并且使用*点访问符*使他们的值作为属性或方法被处理。在下面的例子，一个字典变成一个对象：

`dict = bless([ 'state' => 0, 'incme' = > function(); self.state++; end ])`
`dict.incme()`
`> dict.state  // will print '1'`

简单地运行绑定的数组。

`array = [1,2,3]`
`array.showMe = function()`
`   for item in self`
`       > item`
`   end`
`end`

`array.showMe()`

### 面向消息

当一个消息被广播时面向消息编程允许间接调用一个或者更多注册的监听器。消息的内容是任意的并且能包含任何语言元素，包括但不限于哪个创建创建实例的类，函数序列或者表。监听器不是完整接受消息和执行他们，就是通过有次序的步骤分享在构建中的一个消息的通用应答。消息能被广播和包含一个实时的应答或者能被保存在环境用来接收和处理更多的后来者（在**Falcon**里被称作*断言*）。

面向消息编程拥有一个在虚拟机里的直接接口，关于扩展原生模块和嵌入应用能相互作用。例如，一个多线程应用可能抛给虚拟机来自不同的线程消息，为了在脚本级别上序列化处理和稍后广播直接来自脚本的处理解决方案。

### 表格化

表格式编程能看做是一种OOP编程的特殊扩展，一个类通过一个表格被描述，他们的列是属性，每一行是一个实例。不同于一起保持全部实例，允许每个实例影响父表周围的行，关于表的修改被动态反射到每个实例。

表格提供一个方法来在有限选择的集合之间选择行为，或者混合行为并合并它们，提供模糊逻辑引擎。如每一行，实质上的一个Falcon数组，能包含表中数据和逻辑或者私有逻辑（通过数组绑定），在表格里一个通过全局选择逻辑选择的实体能提供专门的处理能力。

## 特性

随着多范式编程，**Falcon**为编程人员呈现多种多样的特色。

### 模板文件

通过预处理符号**\<? .. ?\>**或者'''

<?fal .. ?>

**，**Falcon*'允许脚本成为文本文档的一部分，、。保存为".ftd"的脚本被作为一个文本文件来处理并且在遇到其中一个预处理符号之前简单输出。下面的*.ftd''例子里包含其中的脚本被执行：

`  You called this script with <? print( args.len() ) ?> parameters.`

FTD文件能通过标准Falcon脚本被整合到各式应用，在动态模板（FTD文件）中的是表现逻辑，应用逻辑被储存在Falcon模块。

FTD文件能被用来驱动动态网站，一些流行的网页服务器（当前的[Apache 2](../Page/Apache_HTTP_Server.md "wikilink")），拥有直接分析和执行".fal"和".ftd"脚本的模块，提供整合到网页服务器引擎的一个API。用CGI脚本也能使用动态FTD页面。

### 异常

**Falcon**由*raise*, *try*和*catch*语句支持错误处理。raise语句能抛出任何Falcon元素，包括Nil，numbers, strings, objects等等。库函数和扩展模块将通常引发错误类的实例，或者派生自他的实例。

catch语句能捕获任何类型的元素，一个某种类型（如string（字串）或interger（整數）），或者某种类的实例。捕获的类被按层次组织，所以它能像下面的例子一样支持更多一般性错误处理（*TypeError*是一个派生自*Error*类库）:

`try`
`   ... code that can raise ...`
`catch TypeError in error`
`   ... if we mixed up types ...`
`catch Error in error`
`   ... another generic error ...`
`catch StringType in error`
`   ... an explicit raise "something" was issued ...`
`catch in error`
`   ... no idea of what has been raised.`
`end`

catch语句中的*in*子句是可选的（这意味着错误可以忽略自身）。

*catch*语句模仿*select*语句，能被用一个给出的类型或者类转向。

### 可嵌入运行时

使用可链接运行时库*libfalcon*，**Falcon**被设计成可嵌入和可扩展其他系统的。

### 文档生成器

**Falcon**装载着一个整合的文档系统，叫做*faldoc*，是特别设计来提供可维护的文档的Falcon基础库（是原生C++代码或者用Falcon编写的模块）。

### 虚拟文件系统

所有发生在引擎或者虚拟机（脚本执行器）等级的I/O操作被委派给一个中央虚拟文件系统组件（centralized Virtual Filesystem Provider），外部模块或者可嵌入的应用设备被允许动态注册。订阅的虚拟文件系统抽象I/O操作如目录读取，创建文件和打开流，通过URI能在脚本内部寻址。这使得他能从任何VFS（如网络资源或者压缩加密的文件）读取模块或者打开资源，通过第三方模块且或通过嵌入引擎的应用程序可以包含特殊的虚拟位置的支持。

### 并发支持

在更新到0.8.x版本，*Threading*模块提供脚本完整多线程。线程模型是*面向代理（agent oriented）*，跨线程数据必须通过几种可行共享机制明确地共享。每一个线程运行一个不同的虚拟机，分离的运行发生在其内部任何操作（如垃圾回收）。这允许有效的并行处理和在脚本开发者控制之外的0竞争。

### 协同处理

**Falcon**支持准并发协同处理。协同处理是指通过虚拟机在同一时间片或者在空闲时间里执行代码。它们支持一个接近于完整线程模块的更轻量级的并发处理，通过不同的协同处理允许程序的全局数据完全可见。除了每个协同处理的合作，（如在调度读取之前每个协同处理必须检查数据可用性）。

### 元编译器

**Falcon''编译器有一个支持宏展开的元编译器，在一个标准编译器中元编译器由Falcon虚拟机驱动；自元编译器生成的输出被发送到语言的语法分析器就像他是原始代码的一部分。使用**\[...\]'''退出序列，通过打印他能动态记录被编译的程序内容。

` `\[printl( "printl( 'Hello world' )" )\]

*macro*关键字提供一个简单的转到编译时元编程的*语法糖果（candy-grammar）*接口。

### 原生国际化

用一个前缀'i'的字符串被认为是一个输出（国际化）字符串。在一个模块中通过使用*directive*语句声明使用的语言，它能指示哪个字符串用什么自然语言编写，如下面的例子：

` directive lang=fr_FR           // uses 5 characters ISO language code`

` > i"Bonjour à tout le monde!"`

一个命令行工具*fallc*被用来输出'i'字符串到XML定义文件，能被作为模板来支持翻译到不同的语言。

在读取模块的时候一个已翻译的字符表被应用到模块。

## 特色

完整地支持[模块化编程](https://zh.wikipedia.org/wiki/模块化编程 "wikilink")，**Falcon**装载着*特色（Feathers）*，标准模块套件。*特色（Feathers）*模块当前包括：

  - 编译器 - 反射型编译器和动态插件引导器。
  - 配置分析器 - 完成配置文件分析支持。
  - MXML - 非常快速和简洁的*迷你*XML分析器（兼容XML 1.0）。
  - 正则表达式 - PCRE 7.x兼容正则表达式库接口。
  - 套接字（Socket） - BSD套接字跨平台网络支持。
  - ZLib - 简洁的压缩程序接口。

## 实现

核心VM和官方模块，（包括特色模块和社区提供支持的模块）都是用C++编写.一些非常底层的模块和引擎元素是用C和汇编编写。

## 可用资源

在[Mac OS X和](https://zh.wikipedia.org/wiki/Mac_OS_X "wikilink")[MS-Windows系统上Falcon通过安装程序发布](https://zh.wikipedia.org/wiki/Windows "wikilink")，构建和安装是一个清晰的过程，或者在各种开源系统如[Linux](../Page/Linux.md "wikilink")或[OpenSolaris](../Page/OpenSolaris.md "wikilink")上通过自构建源代码包。

在后者系统上，*Falcon编程语言*通常支持各种发行版本并保持更新的，其中有：

  - [Ubuntu](../Page/Ubuntu.md "wikilink")
  - [Fedora](../Page/Fedora.md "wikilink")
  - [Gentoo](../Page/Gentoo_Linux.md "wikilink")
  - [Slackware](../Page/Slackware.md "wikilink")
  - [Arch Linux](https://zh.wikipedia.org/wiki/ArchLinux "wikilink")

在基于[Solaris](../Page/Solaris.md "wikilink")系统的发行版本上通过[Blastwave项目和](https://zh.wikipedia.org/wiki/Blastwave "wikilink")[OpenSolaris](../Page/OpenSolaris.md "wikilink")系统的 \[AuroraUX <http://en.wikipedia.org/wiki/AuroraUX>\] 发行版本Falcon编程语言是可用的。

## 参考

## 外部链接

  - [Falcon网站](http://www.falconpl.org/)
  - [文档](http://www.falconpl.org/index.ftd?page_id=manuals)
  - [Falcon community wiki](http://old.falconpl.org/wiki)
  - [Falcon community论坛](https://web.archive.org/web/20090303130953/http://old.falconpl.org/forum/)
  - [linuxjournal上的相关文章](https://web.archive.org/web/20081215081914/http://www.linuxjournal.com/article/10161)
  - [发表在Free Software Magazine](https://web.archive.org/web/20090228065115/http://www.freesoftwaremagazine.com/articles/falcon_programming_language_brief_tutorial)

[Category:2003年編成語言](https://zh.wikipedia.org/wiki/Category:2003年編成語言 "wikilink") [Category:脚本语言](https://zh.wikipedia.org/wiki/Category:脚本语言 "wikilink") [Category:MySQL](https://zh.wikipedia.org/wiki/Category:MySQL "wikilink")