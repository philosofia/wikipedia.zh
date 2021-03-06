**XCF**是*eXperimental Computing Facility*\[1\]的简称，是 [GIMP](../Page/GIMP.md "wikilink")（GNU图像处理程序）保存的图像源文件，具有很多诸如图层的额外特性。也是[GNU自由文档许可证](../Page/GNU自由文档许可证.md "wikilink")与[维基共享资源](../Page/维基共享资源.md "wikilink")所允许的透明影像格式之一。

该格式类似[Adobe Photoshop的PSD文件](../Page/Adobe_Photoshop.md "wikilink")，支持[图层](https://zh.wikipedia.org/wiki/图层 "wikilink")，通道，透明，路径等的储存，不支持撤销历史记录。对保存的图像数据使用简单的[RLE算法压缩](https://zh.wikipedia.org/wiki/RLE "wikilink")。

XCF文件可以[向后兼容](https://zh.wikipedia.org/wiki/向后兼容 "wikilink")。例如，GIMP 2.0能够文本作为文本图层保存，而GIMP 1.2不能，但GIMP 1.2可以把GIMP 2.0保存的XCF文件中的文字图层当作普通图像层处理。

GIMP开发者不推荐使用XCF作为数据交换格式\[2\]，是因为这一格式反应了GIMP的内部架构，而且在将来的版本中会有细微的调整。另外，GIMP开发者和[Krita](../Page/Krita.md "wikilink")开发者之间的合作成果是进行中的光栅文件格式，以[OpenDocument格式为蓝本](https://zh.wikipedia.org/wiki/OpenDocument "wikilink")，会在这两个应用程序未来的版本中使用。

从GIMP 2.8版本起图像以XCF格式存取。GIMP仅支持以XCF格式保存，其他格式改由“导出”对话框保存。

## 支持此格式的软件

除了在GIMP中作为源文件，XCF还可被另外一些软件，如某些图像阅览器与图像转换软件中被读取、使用、导出：

  - 是个[Mac OS X上基于GIMP的轻量级图像处理软件](https://zh.wikipedia.org/wiki/Mac_OS_X "wikilink")。

  - [ImageMagick](../Page/ImageMagick.md "wikilink") 有个XCF模块，但仅可读取其单层未索引图像。

  - [Inkscape](../Page/Inkscape.md "wikilink") 在0.44版后支持导出XCF。\[3\]

  - [XnView](../Page/XnView.md "wikilink") 可以显示XCF的单层未索引图像。

  - [Imagine](https://zh.wikipedia.org/wiki/Imagine_\(绘图软件\) "wikilink") 可以显示XCF的单层未索引图像。

## 注釋

## 外部連結

  - [XCF檔案格式技術資-{}-料](https://git.gnome.org/browse/gimp/tree/devel-docs/xcf.txt)

[分類:圖形文件格式](https://zh.wikipedia.org/wiki/分類:圖形文件格式 "wikilink")

1.
2.
3.