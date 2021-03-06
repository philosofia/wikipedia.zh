> 本文内容由[PLY](https://zh.wikipedia.org/wiki/PLY)转换而来。


**PLY**是一種電腦檔案格式，全名為**多邊形檔案（Polygon File Format）**或 **史丹佛三角形檔案（Stanford Triangle Format）**。

[David_von_Michelangelo.jpg](https://zh.wikipedia.org/wiki/File:David_von_Michelangelo.jpg "fig:David_von_Michelangelo.jpg")的 [The Digital Michelangelo Project](http://graphics.stanford.edu/projects/mich/)計畫採用PLY格式儲存極高解析度之[米開朗基羅的作品](https://zh.wikipedia.org/wiki/米開朗基羅 "wikilink")"[大衛](https://zh.wikipedia.org/wiki/大衛 "wikilink")"雕塑。\]\]

該格式主要用以儲存立體掃描結果的三維數值，透過多邊形片面的集合描述三維物體，與其他格式相較之下這是較為簡單的方法。它可以儲存的資訊包含顏色、透明度、表面法向量、材質座標與資料可信度，並能對多邊形的正反兩面設定不同的屬性。

在檔案內容的儲存上PLY有兩種版本，分別是純文字（ASCII）版本與二元碼（binary）版本，其差異在儲存時是否以ASCII編碼表示元素資訊。

## 檔案格式

（本文並未提供完整的格式描述，以下僅介紹PLY的基本概念與格式）

每個PLY檔都包含檔頭（header），用以設定網格模型的「元素」與「屬性」，以及在檔頭下方接著一連串的元素「數值資料」。一般而言，網格模型的「元素」就是[頂點](../Page/頂點_\(電腦圖學\).md "wikilink")（vertices）、面（faces），另外還可能包含有邊（edges）、深度圖樣本（samples of range maps）與三角帶（triangle strips）等元素。無論是純文字與二元碼的PLY檔，檔頭資訊都是以ASCII編碼編寫，接續其後的數值資料才有編碼之分。PLY檔案以此行：

` ply`

開頭作為PLY格式的識別。接著第二行是版本資訊，目前有三種寫法：

` format ascii 1.0`
` format binary_little_endian 1.0`
` format binary_big_endian 1.0`

其中ascii, binary_little_endian, binary_big_endian是檔案儲存的編碼方式，而1.0是遵循的標準版本（現階段僅有PLY 1.0版）。在檔頭中可使用'comment'作為一行的開頭以編寫註解，例如：

` comment This is a comment!`

描述元素及屬性，必須使用'element'及'property'的關鍵字，一般的格式為element下方接著屬性列表，例如:

` element `<element name>` `<number in file>
` property `<data_type>` <property name 1>`
` property `<data_type>` <property name 2>`
` property `<data_type>` <property name 3>`

'property'不僅定義了資料的型態，其出現順序亦定義了資料的順序。內定的資料形態有兩種寫法：一種是*char uchar short ushort int uint float double*,另外一種是具有位元長度的*int8 uint8 int16 uint16 int32 uint32 float32 float64*。 例如，描述一個包含12個**頂點**的物體，每個頂點使用3個單精度浮點數 (x,y,z）代表點的座標，使用3個unsigned char代表[頂點顏色](../Page/頂點_\(電腦圖學\).md "wikilink")，顏色順序為 (B, G, R),則檔頭的寫法為：

` element vertex 12`
` property float x`
` property float y`
` property float z`
` property uchar blue`
` property uchar green`
` property uchar red`

其中vertex是內定的元素類型，接續的6行property描述構成vertex元素的數值欄位順序代表的意義，及其資料形態。

另一個常使用的元素是**面**。由於一個面是由3個以上的頂點所組成，因此使用一個「頂點列表」即可描述一個面, PLY格式使用一個特殊關鍵字'property list'定義之。 例如，一個具有10個面的物體，其PLY檔頭可能包含：

` element face 10`
` property list uchar int vertex_indices`

'property list'表示該元素face的特性是由一行的頂點列表來描述。列表開頭以uchar型態的數值表示列表的項目數，後面接著資料型態為int的頂點索引值（vertex_indices），頂點索引值從0開始。

最後，標頭必須以此行結尾：

` end_header`

檔頭後接著的是元素資料（端點座標、拓樸連結等）。在ASCII格式中各個端點與面的資訊都是以獨立的一行描述，而二元編碼格式則連續儲存這些資料，載入時須以'element'定義的元素數目以及'property'中設定的資料形態計算各筆欄位的長度。

## 範例

一個典型的PLY檔案結構分成三部分：

` 檔頭 (從ply開始到end_header）`
` 頂點元素列表`
` 面元素列表`

其中的**頂點元素列表**一般以x y z方式排列，形態如檔頭所定義；而**面元素列表**是以下列格式表示。

` `<組成面的端點數N>` <端點#1的索引> <端點#2的索引> ... <端點#N的索引>`

例如畫出一個有4個頂點，4個面的[四面體](../Page/四面體.md "wikilink")，檔案內容為:

` ply`
` format ascii 1.0`
` comment這是一個正四面體`
` element vertex 4`
` property float x`
` property float y`
` property float z`
` element face 4`
` property list uchar int vertex_index`
` end_header`
` 0 3 0`
` 2.449 -1.0 -1.414`
` 0 -1 2.828`
` -2.449 -1.0 -1.414`
` 3 0 1 3`
` 3 0 2 1`
` 3 0 3 2`
` 3 1 2 3`

其中1\~10行是檔頭, 11\~14行是**頂點元素列表**, 15\~18行則是**面元素列表**。

## 歷史

PLY格式發展於90年代中期，在史丹佛大學圖學實驗室的Marc Levoy教授指導下，由及其他成員開發出來。PLY格式受[Wavefront .obj格式的啟發](../Page/Wavefront_.obj文件.md "wikilink")，但改進了Obj格式所缺少的對任意屬性及群組的擴充性。因此PLY格式發明了"property"及"element"這兩個關鍵詞，來概括「頂點、面、相關資訊、群組」的概念。

## 參見

  - [Blender](../Page/Blender.md "wikilink"):免費而功能強大3D編輯工具，可以用來匯入PLY檔案
  - [MeshLab](../Page/MeshLab.md "wikilink"):在Windows、Mac OS X與Linux平台上開放原始碼的網格編修與展示工具，可用來編輯轉換PLY檔案

## 外部連結

  - [Greg Turk撰寫的PLY格式文件](http://www.cs.virginia.edu/~gfx/Courses/2001/Advanced.spring.01/plylib/Ply.txt)
  - [PLY - Polygon File Format](http://paulbourke.net/dataformats/ply/)（內含格式範例檔）
  - [一些支援PLY的工具](http://www.cc.gatech.edu/projects/large_models/ply.html)
  - [讀取、寫入PLY檔的函式庫](https://web.archive.org/web/20081203195143/http://www.cs.princeton.edu/~diego/professional/rply/)
  - [以PLY格式儲存的大量三維模型](http://graphics.stanford.edu/data/3Dscanrep/)

[分類:三維計算機圖形學](https://zh.wikipedia.org/wiki/分類:三維計算機圖形學 "wikilink") [分類:文件格式](https://zh.wikipedia.org/wiki/分類:文件格式 "wikilink") [分類:CAD文件格式](https://zh.wikipedia.org/wiki/分類:CAD文件格式 "wikilink") [分類:圖形文件格式](https://zh.wikipedia.org/wiki/分類:圖形文件格式 "wikilink")

[Category:電腦圖學](https://zh.wikipedia.org/wiki/Category:電腦圖學 "wikilink")