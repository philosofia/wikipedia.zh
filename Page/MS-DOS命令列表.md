> 本文内容由[MS-DOS命令列表](https://zh.wikipedia.org/wiki/MS-DOS命令列表)转换而来。


以下是[微软](../Page/微软.md "wikilink")的[DOS](../Page/DOS.md "wikilink")[操作系统](../Page/操作系统.md "wikilink")（[MS-DOS](../Page/MS-DOS.md "wikilink")）的DOS命令列表。其它DOS的命令和用法可能类似。

後期版本的 DOS 可以通过help命令来得到命令與參數列表，通过help *<命令>*或者*<命令>* /?来获得命令的详细信息。

## [內部命令](https://zh.wikipedia.org/wiki/壳层内建指令 "wikilink")

### DIR

命令类型：内部命令

命令功能：显示某个磁盘指定目录下的全部或部分文件目录和子目录，显示信息包括文件名、扩展名、文件长度、文件创建日期和时间。同时给出所显示文件的总数和所剩余的磁盘空间。

命令格式：DIR filespec\[/P\] \[/W\] \[/S\] 命令使用说明：

1.  开关符
    1.  \[/P\]表示分屏显示。当文件较多，每显示完一整屏后屏幕暂停，并提示“请按任意键继续”，用户按键后显示下一屏，重复该过程直至显示完毕。
    2.  \[/W\]表示以简洁形式（紧缩格式）显示文件清单，目录中只显示文件名和扩展名。
    3.  \[/S\]对于给定的文件标志符，显示其在指定目录及指定目录所有下级子目录中的相应位置清单。
2.  文件标志符filespec中的文件名和扩展名可以使用通配符？和\*
3.  当文件名是\*.\*时，可以省略不写。例如：\*.ext,filename.\*可简写为filename.。
4.  该命令可以将显示结果送向打印机。

#### DIR命令的各种形式

  - DIR \*.\*<Enter>显示当前盘当前目录的全部目录清单
  - DIR A:\\<Enter> 显示A盘根目录的目录清单
  - DIR \\<Enter> 显示当前盘根目录的清单
  - DIR ..<Enter> 显示当前盘当前目录的上级目录的目录清单
  - DIR \*.EXE<Enter> 显示当前盘当前目录下扩展名为.EXE的全部文件清单
  - DIR B:SUB/S<Enter> 显示B盘当前目录下子目录SUB下的目录清单，及SUB下所有子目录（包括各级下级子目录）下的目录清单
  - DIR .EXE/p<Enter> 以分屏方式显示当前盘当前目录下扩展名为.EXE的全部文件清单
  - DIR \*.\*\>PRN<Enter> 显示当前盘当前目录的全部目录清单同时打印

### copy

複製或合并文件

语法：COPY \[/D\]\[/V\]\[/N\]\[/Y|/-Y\]\[/Z\]\[/A|/B\] 命令形式：COPY source \[/A|/B\]\[+source \[/A|/B\][+ ...](https://zh.wikipedia.org/wiki/+_... "wikilink") \[destination \[/A|/B\]\] 　 方括号括起来的是可选部分，不是必须部分。 比如：copy c:\\source.exe c:\\destination.exe //就是把source.exe 复制到destination.exe,不论destination.exe存在与否，扩展名可以使其它

/D 允许解密要创建的目标文件 /V 验证新文件写入是否正确。 /N 复制带有非8dot3名称的文件 /Y |/-Y 使用确认是否要覆盖现有目标文件的提示 /Z可重新启动模式复制已联网的文件 \[/A|/B\]表示ASCII文本文件和二进位文件

要附加文件，用通配符或 file1+file2+file3 格式 source 指定要复制的文件;destination 为新文件指定目录和/或文件名。

### ren 或 rename

重命名文件或者一个子目录

语法

RENAME \[drive:\]\[path\]filename1 filename2 例如：rename d:\\soft\\setup.exe setup123.exe REN \[drive:\]\[path\]filename1 filename2

### cd 或 chdir

显示或者更改当前路径

语法 CHDIR \[/D\] \[drive:\]\[path\] CHDIR \[..\] CD \[/D\] \[drive:\]\[path\] CD \[..\]

### md 或 mkdir

新建一个目录

语法 MKDIR \[drive:\]path
MD \[drive:\]path

### rd 或 rmdir

删除一个空目录

语法
RMDIR \[/S\] \[/Q\] \[drive:\]path
RD \[/S\] \[/Q\] \[drive:\]path
在使用过程中要记住的是，这个命令若未加\[/S\]的參數時，只能够删除空子目录。

參數說明：
\[/S\]：除目錄樹，即刪除目錄及目錄下的所有子目錄和文件
\[/Q\]：在進行刪除時，取消系統詢問刪除與否的確認訊息。

### del 或 erase

删除一个或者多个文件

语法
ERASE \[/P\] \[/F\] \[/S\] \[/Q\] \[/A\[\[:\]attributes|:\]attributes\]\] names
DEL \[/P\] \[/F\] \[/S\] \[/Q\] \[/A\[\[:\]attributes|:\]attributes\]\] names

參數說明：

  - /F 強制刪除唯讀文件。
  - /S 從所有子目錄刪除指定文件。
  - /Q 安靜模式。刪除時，不要求確認。
  - /A 根據屬性選擇要刪除的文件。

範例：

  - del /f /s /q /a c:\\\*.bak
  - 就是刪除所有在 c 槽的 \*.bak 檔

假如是一個目錄的話就

  - del /q c:\\folder\\\*.bak

### type

显示文件内容 type *<檔案名>*

### set

显示、设置、删除环境变量。如时间，提示符等。
从Windows 2000起，通过添加/P参数，set命令可以用来接收命令行的输入。
例如：
Set /P Choice = Type your text.
echo You typed: "%choice%"

### path

设置可执行文件的搜索路径

在硬碟中建立樹狀目录结构，虽然方便了文件的分门别类整理，但是却带来了另一方面的问题：如何共同各目录中的文件？每当执行外部命令或批次檔时，首先要找到该檔案的目录，指出相应的路径，总是感到操作繁琐，于是DOS提供了PATH命令，以解决文件的共用问题。

1.  功能：设置可执行文件的搜索路径，只对.COM、.EXE及.BAT文件有效。
2.  类型：内部命令。
3.  格式 PATH\[;\]\[盘符1\]\[路径1\]\[;\]\[盘符2\]\[路径2\]\[;...\]
4.  使用说明

:\# PATH命令可用来设置可执行文件（仅包括：.COM、.EXE及.BAT文件）的搜索路径。当您執行一个可执行文件时，DOS会先在当前目录中搜索该文件，若找到则运行之；若找不到该文件，则根据PATH命令所设置的路径，顺序逐条地到各目录中搜索该文件；

:\# PATH命令中的路径，若有两条以上，各路径之间以一个分号“；”隔开；

:\# PATH命令有三种使用方法：

::\# PATH 盘符：路径1；盘符：路径2;...（设定可执行文件的搜索路径）

::\# PATH ；（取消所有路径）

::\# PATH（显示目前所设的路径）

### help

显示当前版本DOS的帮助信息

语法 HELP \[command\]

### ver

显示当前DOS版本信息。

## 外部命令

### tree

显示目录的树状结构。

TREE 命令自 DOS 2.0 系統開始支援[子目錄以後提供](https://zh.wikipedia.org/wiki/子目錄 "wikilink")，用以讓用戶得知磁碟或硬碟目錄的樹狀結構。

### more

分屏显示文件，文件内容可通过命令行参数指定，若未指定则使用 stdin（管道）。例：

more a.txt

dir | more

### move

移动文件，或重命名一个文件或子目录。

### attrib

修改文件的 [S](https://zh.wikipedia.org/wiki/系统文件 "wikilink")/[H](https://zh.wikipedia.org/wiki/隐藏文件 "wikilink")/[R](https://zh.wikipedia.org/wiki/只读文件 "wikilink")/[A](https://zh.wikipedia.org/wiki/归档文件 "wikilink") 等属性。 无法更改 NTFS 的 ACL。

### deltree

删除目录树。

### xcopy

复制文件或子目录。XCOPY意指*extended copy*\[1\]。

XCOPY 指令由 DOS 3.2 開始提供，用以提供一個更快捷及穩定的檔案抄寫模式。傳統 DOS 的內部指令在抄寫檔案時，會利用標準 DOS 呼叫把檔案逐一由源路徑複制往目的路徑；但 XCOPY 會先把要抄的內容抄往記憶作暫存，待記憶填滿了，再寫往目的路徑。由於磁碟動作減少了，所以抄寫動作得以大幅提高。

如果全路径名的长度超过254个字符，则Xcopy报"insufficient memory"错误。\[2\]如果move大文件但未使用"/j"选项（Windows Server 2008R2开始使用），可能会耗尽所有可用内存。\[3\]对于未使用FILE_SHARE_READ选项被其它进程打开的文件，Xcopy不能打开这个文件；Windows Volume Shadow Copy服务可用于此种情形，但Xcopy没有用它。所以Xcopy不能用于备份live操作系统的文件。

虽然[Windows 10中还有Xcopy](../Page/Windows_10.md "wikilink")，但它已经过时，应该使用更强有力的[Robocopy](https://zh.wikipedia.org/wiki/Robocopy "wikilink")。\[4\]

### format

格式化软盘或硬盘分区（高级格式化）。

### diskcopy

复制整张软盘。

### diskcomp

比较整张软盘。

### undelete

恢复删除的文件（如果可能的话）。

### unformat

恢复格式化的磁盘（如果可能的话）。

### fdisk

硬盘分区。

有些时候需要重置 [MBR](../Page/主引导记录.md "wikilink") 的信息（例如卸载掉 Linux 的启动菜单等），这时候可以使用这个命令： fdisk /mbr

## 參考資料

[Category:磁盘操作系统](https://zh.wikipedia.org/wiki/Category:磁盘操作系统 "wikilink") [Category:软件列表](https://zh.wikipedia.org/wiki/Category:软件列表 "wikilink")

1.
2.
3.
4.