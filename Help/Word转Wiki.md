> 本文内容由[Help:Word转Wiki](https://zh.wikipedia.org/wiki/Help:Word转Wiki)转换而来。


## Microsoft Word

### Word2MediaWikiPlus

以下的扩展自2007年释出，至2014年未有更新，但仍然可以工作： [Word2MediaWikiPlus](http://www.mediawiki.org/wiki/Extension:Word2MediaWikiPlus) 经[Office 365](../Page/Office_365.md "wikilink") Word测试，有部分出错。

下载地址： <http://sourceforge.net/projects/word2mediawikip/files/word2MediaWikiPlus/1.0.0/Word2MediaWikiPlus-1.0.0.zip/download>

### 微软插件解决方案

[微软公司发布了一个插件](https://zh.wikipedia.org/wiki/微软公司 "wikilink")，支持用户在[Microsoft Office Word 2007以及之后版本的软件将word文档另存为MediaWiki格式的文本](https://zh.wikipedia.org/wiki/Word "wikilink")。

1.  从微软下载中心（Microsoft Download Center）下载“[Microsoft Office Word Add-in For MediaWiki](http://www.microsoft.com/downloads/en/details.aspx?FamilyID=8e519637-afb0-4134-a91f-7b0ebea8d933)”并安装于本地电脑。
2.  启动Office Word打开或新建一个word文档并将其另存为“MediaWiki (\*.txt)”文件格式。
3.  将(\*.txt) 文件中的代码拷贝至wiki页面。

#### 可能出现的问题

  - 此插件仅支持[Windows](https://zh.wikipedia.org/wiki/Windows "wikilink")[系统环境下使用](../Page/操作系统.md "wikilink")，[Mac OS X系统下不支持](https://zh.wikipedia.org/wiki/Mac_OS_X "wikilink")。
  - 此插件不支持处理图像并会报错。
  - 此插件不支持转换页眉页脚和脚注，包含这些元素的文档在转换时将会报错。

:\* 如果您尝试通过插入<ref>标签来解决上面不能处理脚注的问题，转换后<和>将会取代尖括号。

  - 部分文本将被和标签包围。
  - 此插件在[Microsoft Office Word 2013默认情况下不能正常工作](https://zh.wikipedia.org/wiki/Microsoft_Office_2013 "wikilink")，但是可以通过更改注册表来启用。具体参见[这里](http://answers.microsoft.com/en-us/office/forum/office_2010-word/using-microsoft-office-word-add-in-for-mediawiki/449726c2-6d08-45e1-919a-4b5082ab4b5b?rtAction=1403289479743)或[这里](http://answers.microsoft.com/en-us/office/forum/office_2013_release-word/word-add-in-for-mediawiki-not-supported-in-word/b8b9c71d-de69-4fe7-900e-00f6fae40556)。

## 从Word到MediaWiki的两步转换

以下两种方法进行：`Word -> HTML -> MediaWiki`。

### 手动转换

1.  在Word中打开您的文档，“另存为”HTML文件。
2.  在文本编辑器中打开一个HTML文件，将剪贴板中的HTML源代码复制到其中。
3.  将HTML源代码到[HTML wiki](https://tools.wmflabs.org/magnustools/html2wiki.php)页面标有“原始HTML”的大文本框中。
4.  点击“转换为HTML到wiki标记”按钮。
5.  选择“MediaWiki标记”文本框中的文本，并将其复制到剪贴板。
6.  将文本粘贴到维基百科的文章中。

### 自动脚本

该转换还可以使用的两个脚本和两个软件包的组合完成的。

1.  下面的两个软件包必须安装：
      - [wvHtml Word to HTML converter](http://wvware.sourceforge.net/)——“wvWare”Word查看库的组件(*Note*: wvHtml is deprecated and the site recommends using `AbiWord --to=html` instead. AbiWord can be obtained at [abisource.com](http://www.abisource.com/).)
      - \[<https://metacpan.org/module/HTML>::WikiConverter HTML::WikiConverter\] - a Perl module to convert HTML to wiki markup language.
2.  编写bash脚本“doc2mw”，以及perl脚本“html2mw”，如以下所示。
3.  Call doc2mw passing the word document as parameter。如：

`> doc2mw my_word.doc`

**doc2mw**：

    <nowiki> #!/bin/bash
     #       doc2mw - Word to MediaWiki converter

     FILE=$1
     TMP="$$-${FILE}"

     if [ -x "./html2mw" ]; then
             HTML2MW='./html2mw'
     else
             HTML2MW='html2mw'
     fi

     wvHtml --targetdir=/tmp "${FILE}" "${TMP}"
     # but see also AbiWord: http://www.abisource.com/help/en-US/howto/howtoexporthtml.html

     # Remove extra divs
     perl -pi -e "s/\<div[^\>]+.\>//gi;" "/tmp/${TMP}"

     ${HTML2MW} "/tmp/${TMP}"
     rm "/tmp/${TMP}"
    </nowiki>

**html2mw**：

    <nowiki>
     #!/usr/bin/perl
     #       html2mw - HTML to MediaWiki converter

     use HTML::WikiConverter;

     my $b;
     while (<>) { $b .= $_; }

     my $w = new HTML::WikiConverter( dialect => 'MediaWiki' );

     my $p = $w->html2wiki($b);

     # Substitutions to get rid of nasty things we don't need
     $p =~ s/<br \/>//g;
     $p =~ s/\&nbsp\;//g;
     print $p;
    </nowiki>

<i>免责声明：这些脚本可能并不是最合适的方法，仅仅是一个可能可行的方案。请随时加以改进。</i>

## OpenOffice或LibreOffice

[LibreOffice支持导出Word文档为MediaWiki格式的文本文档](https://zh.wikipedia.org/wiki/LibreOffice "wikilink")（.txt）

1.  LibreOffice打开Word文档。
2.  选择“文件”——“导出”。
3.  选择“保存类型”为“MediaWiki（.txt）(\*.txt)”并保存。
4.  将(\*.txt) 文件中的代码拷贝至wiki页面。

[OpenOffice](../Page/OpenOffice.org_Writer.md "wikilink")3.3及以后的版本支持直接将Word文档发送至MediaWiki服务器，但目前Windows 7下工作不稳定。（至少德文版[OpenOffice](https://zh.wikipedia.org/wiki/OpenOffice "wikilink") 3.3.0需要先安装‘[Sun Wiki Publisher](http://extensions.services.openoffice.org/de/project/wikipublisher)’）

1.  用OpenOffice或LibreOffice Writer打开Word文档。
2.  文件 \>发送 \> 至MediaWiki或文件 \> 导出 \> 文件另存为: Mediawiki
3.  选择您的MediaWiki-server（或者点击“添加……”来添加一个站点）
4.  Select a title and summary for your article, check the box if it's a minor revision.
5.  点击发送按钮。

## 另见

  - [Commons: Convert tables and charts to wiki code or image files](https://zh.wikipedia.org/wiki/commons:Commons:Convert_tables_and_charts_to_wiki_code_or_image_files "wikilink")