> 本文内容由[OTA位图](https://zh.wikipedia.org/wiki/OTA位图)转换而来。


**OTA位图**（**OTA Bitmap**）是[诺基亚](../Page/诺基亚.md "wikilink")（Nokia）为手机上的黑白图像定义的一个规范。

## 引入

OTA或Over The Air位图由[诺基亚](../Page/诺基亚.md "wikilink")公司在其（Smart Messaging）规范中定义，用以通过一条或多条[串接的](https://zh.wikipedia.org/wiki/串接 "wikilink")[SMS文本消息发送图片](https://zh.wikipedia.org/wiki/SMS "wikilink")。该格式所支持的最大尺寸为255x255像素。OTA位图主要为72x28像素（图片消息）或72x14/72x13像素（[运营商标志](https://zh.wikipedia.org/wiki/运营商标志 "wikilink")）。该规范包含标示多色图像的数据字节，这是为未来准备，但因为[多媒體短訊的出现](https://zh.wikipedia.org/wiki/多媒體短訊 "wikilink")，它从未被实现。

## 基本格式描述

**OTA位图**格式为每位元一个像素的单色、未压缩格式。该格式是为手机设计，而不是标准的计算机格式。它可以存储为[二进制文件](https://zh.wikipedia.org/wiki/二进制文件 "wikilink")，或者以十六进制格式（通常无空格）存储在文本文件中。可辨识[文件扩展名](../Page/文件扩展名.md "wikilink")为**.otb**。

## 格式版权

该格式的版权属于[诺基亚](../Page/诺基亚.md "wikilink")公司。

## 数据头

该图像本身有一个头部标识。标头宽度为四个字节。典型例子为：`00 48 1C 01`。含义如下：

`  00  “信息字段”（始终保持为00）。`
`  48  位图宽度。此例为72像素（48为72的`[`十六进制`](../Page/十六进制.md "wikilink")格式`）。`
`  1C  位图高度。此例为28像素（1C为28的十六进制格式）。`
`  01  颜色数（始终为1）。`

其他可能性为 `00 48 0E 01`（72x14像素位图），`00 48 0D 01`（72x13像素位图）。

## 像素编码

标头之后为图像本身。下面的例子将使用下列72x28像素图像。 最初的8个像素从左上角向右，先是白色（0），其次是七个黑色（1111111）。[二进制格式的首个](https://zh.wikipedia.org/wiki/二进制 "wikilink")[字节](../Page/字节.md "wikilink")为01111111。

将[二进制格式的](https://zh.wikipedia.org/wiki/二进制 "wikilink")01111111转换到[十六进制](../Page/十六进制.md "wikilink")格式后，首个表示像素的字节将是7F。接下来是8个黑色（1​​1111111或FF）等等。

当顶行的所有像素都被编码时，只需移动到下一行。没有用于指示新行的标记，该信息包含在标头中。

在OTA位图的宽度非8个像素的倍数时，一个字节将存储两行的信息（例如，来自第一行的两个像素和来自第二行的六个像素）。在其他格式中不是这样，因此在OTA和其他格式（例如）之间进行转换时请务必小心。

## 组合体

下列是该图像转换为OTA的结果。

`  00 48 1C 01  //标头`
`  7F FF EF FF EF FF FB FF FE //第一行`
`  40 3F E8 38 2F FF FB FF FE //第二行`
`  48 3F A8 38 2F 9F FB FF FE //第三行`
`  4C FF A9 FF 2F 8F FA DA DA //第四行`
`  4E FF 29 01 2F 80 FA 52 52`
`  5E 7F 69 31 2F BF 7B 07 06`
`  4F FF 69 79 2F BE FB 77 76`
`  47 FF 69 79 2F BE 7B 07 06`
`  47 FE EF 7D EF BE 7B FF FE`
`  47 FC EF 7D E7 BC F1 FF FC`
`  40 F0 EF 7D E7 7C F1 ED BC`
`  21 E7 C9 79 27 98 F1 E5 3C`
`  21 E7 C9 39 27 C8 F1 F0 7C`
`  16 6F 89 39 23 E6 E0 F7 78`
`  15 2F 88 82 23 F3 E0 F0 78`
`  08 3F 04 44 43 D7 E0 FF F8`
`  04 3E 02 28 81 EF C0 7F F0`
`  02 3C 01 39 00 FF 80 3F E0`
`  01 38 00 BA 00 7F 00 1F C0`
`  00 F0 00 7C 00 3E 00 0F 80`
`  FF C0 00 38 00 1C 00 07 FF`
`  55 FF FF FF FF FF FF FF AA`
`  2A F3 87 87 3F 1E 67 0F 54`
`  15 F3 93 9F 3E 4E 27 27 A8`
`  2A F3 87 8F 3E 4E 07 27 54`
`  55 F3 93 9F 3E 0E 47 27 AA`
`  FF F3 9B 87 0E 4E 67 0F FF  //倒数第二行`
`  00 FF FF FF FF FF FF FF 00  //最后一行`

## 应用程序支持

### 读写支持

  - [ImageMagick](../Page/ImageMagick.md "wikilink")\[1\]
  - [XnView](../Page/XnView.md "wikilink")

注意：XnView中不支持OTA格式的写入。

## 参见

  -
## 参考资料

  - Nokia Smart Messaging Specification v3.0.0

## 外部链接

  - [Forum Nokia](https://web.archive.org/web/20080120155220/http://www.forum.nokia.com/#navi) - 诺基亚开发者网站

[Category:诺基亚](https://zh.wikipedia.org/wiki/Category:诺基亚 "wikilink") [Category:位图](https://zh.wikipedia.org/wiki/Category:位图 "wikilink")

1.