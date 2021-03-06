**NTLDR**（*NT loader*的[缩写](https://zh.wikipedia.org/wiki/缩写 "wikilink")）是[微软](../Page/微软.md "wikilink")的[Windows NT系列](../Page/Windows_NT.md "wikilink")[操作系统](../Page/操作系统.md "wikilink")（直至[Windows XP和](../Page/Windows_XP.md "wikilink")[Windows Server 2003](../Page/Windows_Server_2003.md "wikilink")）的引导程序。NTLDR可以从[硬盘](../Page/硬盘.md "wikilink")以及[CD-ROM](../Page/CD-ROM.md "wikilink")、[U盘等移动存储器运行并引导Windows](https://zh.wikipedia.org/wiki/U盘 "wikilink") NT系统的启动。如果要用NTLDR启动其他操作系统，则需要将该操作系统所使用的[启动扇区代码保存为一个文件](https://zh.wikipedia.org/wiki/启动扇区 "wikilink")，NTLDR可以从这个文件加载其它[引导程序](https://zh.wikipedia.org/wiki/引导程序 "wikilink")。 [Windows_Advanced_Options_menu.png](https://zh.wikipedia.org/wiki/File:Windows_Advanced_Options_menu.png "fig:Windows_Advanced_Options_menu.png") NTLDR主要由两个文件组成，这两个文件必须放在系统分区（根据微软的定义，为在MBR中标识为活动分区的分区，一般为第一个分区/C分区）：

  - `NTLDR`，这是引導程序本身
  - NTDETECT.COM，用于检测基础硬件信息，以便系统正常启动

boot.ini也是比较重要的文件。它是引導程序的組態檔。当boot.ini丢失时，NTLDR会启动第一块硬盘第一个分区上的\\Windows目录中的系统。

在安装、维护Windows NT系统时，可以使用`format`命令会在[卷引导记录中写入启动NTLDR引导程序的代码](https://zh.wikipedia.org/wiki/卷引导记录 "wikilink")。

[Windows Vista](../Page/Windows_Vista.md "wikilink")、[Windows Server 2008及以后版本的操作系统中](../Page/Windows_Server_2008.md "wikilink")，NTLDR被[BOOTMGR替代](https://zh.wikipedia.org/wiki/BOOTMGR "wikilink")。

## 结构

NTLDR由两个可执行文件构成：

  - 第一部分是一个标准二进制文件，用于切换系统至[保护模式](https://zh.wikipedia.org/wiki/保护模式 "wikilink")，使得系统能识别并运行[可移植可执行](../Page/可移植可执行.md "wikilink")（PE）文件，并运行第二部分。一般被称为STPBOOT.BIN
  - 第二部分是一个可移植可执行文件，被称为OSLOADER.EXE

使用WinHex或者类似的二进制处理软件，在NTLDR中搜索“MZ”，并将其前的部分截去，即可以获得OSLOADER.EXE。在Windows安装文件中也可以找到压缩后的OSLOADER.EX_文件。

Windows NT最初是为ARC（一类[RISC系统架构](https://zh.wikipedia.org/wiki/RISC "wikilink")）设计的，因此只有OSLOADER.EXE，即系统加载器，通过接受指定的系统文件路径和其他启动参数引导对应目录下的Windows NT系统，而指定这些参数的工作交给ARC自带的启动管理器进行。x86架构缺乏启动管理器：BIOS只会调用第一启动设备的MBR中列明的活动分区的卷引导记录。因此启动管理器的功能被包括在OSLOADER部分中，直至微软在2003年引入了自己的启动管理器。ARC的启动管理器的保护模式切换和PE文件识别运行功能则交给STPBOOT完成。boot.ini中的列表项也被设计为类似于ARC的格式，以便直接传给OSLOADER.EXE。

## 启动步骤

1.  与一般的系统启动进程一致，[BIOS](../Page/BIOS.md "wikilink")调用[MBR](https://zh.wikipedia.org/wiki/MBR "wikilink")，然后调用活动分区的卷引导记录，该卷引导记录被设计为搜索NTLDR，并执行之。
2.  NTLDR的第一部分被调用。此时系统进入保护模式，并可以识别并运行PE格式的可执行文件。
3.  NTLDR的第二部分，OSLOADER.EXE被调用。OSLOADER.EXE中内嵌有[FAT](../Page/FAT.md "wikilink")、[NTFS](../Page/NTFS.md "wikilink")和[ISO 9660三种文件系统的驱动](../Page/ISO_9660.md "wikilink")，启动管理器，以及INI文件读取器的CAB文件解压缩器。OSLOADER中附带的文件系统驱动通过[BIOS中断直接访问磁盘](../Page/BIOS中斷呼叫.md "wikilink")，因为内核和HAL此时都没有被载入。此时系统可以访问磁盘内的文件。
4.  如果Windows被置于[休眠模式](../Page/休眠_\(電腦\).md "wikilink")，读取hiberfil.sys中的内容并将其写入内存，然后恢复系统的运行。
5.  OSLOADER使用内置的INI文件读取器，试图读取boot.ini文件的内容，并配置启动菜单。如果boot.ini不存在，OSLOADER将视为boot.ini中有且仅有一个指向multi(0)disk(0)rdisk(0)partition(1)\\WINDOWS且没有参数的启动项目。如果boot.ini中只存在一个启动项目，则忽略timeout的时间设置（视为0）。
6.  向用户显示启动菜单，并按照timeout的时间设置倒计时。如果用户按下按键，则停止倒计时。（这样即使只有一个启动项目，当用户在自检结束后狂按F8键，也可以进入進階開機選單）
7.  如果一个非NT的系统被选择，OSLOADER加载列表项中指定的启动扇区代码文件，并移交控制权。此时系统回到[实模式](https://zh.wikipedia.org/wiki/实模式 "wikilink")。如果没有指定文件（常见于Windows 9x和Windows NT共存），则加载bootsect.dos，然后移交控制权，由其搜索并加载IO.SYS。
8.  如果一个NT系统被选择，OSLOADER调用NTDETECT.COM。NTDETECT将检测系统硬件相关的信息，并交给OSLOADER。
9.  OSLOADER调用列表项中指定的文件夹中的[NTOSKRNL.EXE](https://zh.wikipedia.org/wiki/Ntoskrnl.exe "wikilink")，将NTDETECT检测到的硬件信息交给NTOSKRNL，并移交控制权。\[1\]

## boot.ini

在确认系统为冷启动，即非休眠模式后，NTLDR所做的第一件事为读取boot.ini。\[2\]

### 示例

以下是boot.ini的一个示例：

``` ini
[boot loader]
timeout=30
default=multi(0)disk(0)rdisk(0)partition(1)\WINDOWS
[operating systems]
multi(0)disk(0)rdisk(0)partition(1)\WINDOWS="Microsoft Windows XP Professional" /fastdetect
C:\grldr="Ubuntu"
C:\="Previous Version of Windows"
```

#### 解释

  - \[boot loader\]节：配置启动菜单的细节。
  - timeout=30：timeout选项控制启动菜单显示的时间长度，单位为秒，最短为0，此时启动菜单不显示。
  - default=multi(0)disk(0)rdisk(0)partition(1)\\WINDOWS：default选项控制启动菜单的默认选项。
  - \[operating systems\]节：列举启动项目。
  - multi(0)disk(0)rdisk(0)partition(1)\\WINDOWS="Microsoft Windows XP Professional" /fastdetect：基于Windows NT的系统的启动项目。
      - multi(0)disk(0)rdisk(0)partition(1)\\WINDOWS：对于基于Windows NT的系统，系统文件路径由ARC路径给出。
      - "Microsoft Windows XP Professional"：启动项目的友好名称，即显示在启动菜单中的名称。
      - /fastdetect：指定默认的引导参数。使用高级引导菜单启动系统会覆盖引导参数的设置。
          - /fastdetect：不检测串行接口的鼠标。\[3\]
          - /noexecute=optin：在Windows XP SP2后默认安装的系统会有该引导参数，意为为基本Windows程序和服务启用[数据执行保护](https://zh.wikipedia.org/wiki/数据执行保护 "wikilink")（DEP）。\[4\]
  - C:\\grldr="Ubuntu"：基于非Windows NT的系统的启动项目。
      - C:\\grldr：对于基于非Windows NT的系统，引导扇区文件路径由DOS路径给出。
      - “grldr”是[GRUB4DOS的默认引导扇区文件名](../Page/Grub4Dos.md "wikilink")。[Ubuntu](../Page/Ubuntu.md "wikilink")曾使用[Wubi](../Page/Wubi.md "wikilink")提供在Windows下安装Ubuntu的解决方案。
  - C:\\="Previous Version of Windows"
      - C:\\：对于基于MS-DOS的系统，在非三方启动（DOS、Windows 9x、Windows NT共存）、非启动到[恢复控制台的情况下](https://zh.wikipedia.org/wiki/復原主控台 "wikilink")，引导扇区文件名称可以省略，此时视为“C:\\bootsect.dos”。
      - 在三方启动情况下，需要进行一些特殊操作，比如“/WIN95”和“/WIN95DOS”参数用来模拟单系统状况，且引导扇区文件名称不可省略。\[5\]\[6\]
      - 恢复控制台对应的启动项目一般为：C:\\CMDCONS\\BOOTSECT.DAT="Microsoft Windows Recovery Console" /cmdcons

## 多语言支持

NTLDR不支援多語言，如果[中日韓版本的Windows](https://zh.wikipedia.org/wiki/中日韓 "wikilink") NT 5.x NTLDR找不到BOOTFONT.BIN字型檔案，會自動顯示英語代替。[Windows Boot Manager支援多語言](https://zh.wikipedia.org/wiki/Windows_Boot_Manager "wikilink")。

## 常见問題

NTLDR的問題常见于使用者不慎将该文件删除，这样會导致Windows NT系列系统无法启動，开机时将以黑屏白字显示错误信息："NTLDR is missing, Press CTRL+ALT+DEL to restart." 当用户重启后又将出现上述信息，这样就无法进入系统。

解决该问题需要向[光驱内放入一张相应的Windows安装光碟](https://zh.wikipedia.org/wiki/光驱 "wikilink")，开机时先将[BIOS](../Page/BIOS.md "wikilink")设置为从光盘启动，进入系统安装菜单后再选择进入故障恢复台，按屏幕相关说明进入命令行模式，然后将光盘根目录下i386文件夹内的“ntldr”文件和“ntdetect.com”拷贝至系统分区根目录下，重新启动后将BIOS设置回复为硬盘启动即可\[7\]。

## 参考来源

<references/>

[Category:Windows组件](https://zh.wikipedia.org/wiki/Category:Windows组件 "wikilink") [Category:引导程序](https://zh.wikipedia.org/wiki/Category:引导程序 "wikilink")

1.
2.  [Rick Maybury](https://zh.wikipedia.org/wiki/Rick_Maybury "wikilink"), *[Startup and Shutdown Problems, part 1](http://www.pctoptips.co.uk/Bootcamp/2009/559.htm) *, Bootcamp, 2009, accessed 25 April 2012
3.
4.
5.
6.
7.  [NTLDR文件丢失的解决方案](http://www.piaoyi.org/computer/NTLDR-is-missing.html)