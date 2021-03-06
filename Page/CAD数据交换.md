> 本文内容由[CAD数据交换](https://zh.wikipedia.org/wiki/CAD数据交换)转换而来。


**CAD 数据交换**包括许多将数据从一种[CAD系统转换到另外一种](https://zh.wikipedia.org/wiki/CAD "wikilink")[CAD文件格式的软件技术及方法](https://zh.wikipedia.org/wiki/CAD文件格式 "wikilink")。[产品生命周期管理要求](https://zh.wikipedia.org/wiki/产品生命周期管理 "wikilink") [OEM](https://zh.wikipedia.org/wiki/OEM "wikilink") 厂商之间以及他们的供应商之间要进行良好的产品开发协作。

其中主要的问题议题就是几何元素如[网格](https://zh.wikipedia.org/wiki/网格模型 "wikilink")、[曲面以及](https://zh.wikipedia.org/wiki/自由曲面造型 "wikilink")[实体造型](../Page/实体造型.md "wikilink")之间的转换，以及如属性、[元数据](../Page/元数据.md "wikilink")、[装配结构以及](https://zh.wikipedia.org/wiki/装配建模 "wikilink")[特征数据的转换](https://zh.wikipedia.org/wiki/基于参数化特征的建模 "wikilink")。

## 转换的方法

总地来说有三种方法可以进行 [CAD](https://zh.wikipedia.org/wiki/CAD "wikilink") 软件之间的数据转换。

  - CAD 系统直接输出／输入
  - 第三方的直接转换
  - 采用中间的数据交换格式

### 内部直接格式转换

一些 CAD 系统通过简单地打开、另存选项就可以直接读写其它一些 CAD 格式。由于大部分的 CAD 文件格式都不是公开的，只有是同一个公司的产品或者是擅自破译竞争对手的文件格式才有可能采用这种方式。

### 外部直接格式转换

许多专注于 CAD 数据转换的公司提供将一种 CAD 数据格式转换成另外一种 CAD 系统的数据格式。这些系统有它们自己的预处理中间格式，一些系统还可以审查转换过程中的数据。其中一些可以独自工作，另外一些由于 CAD 系统的编程接口所以需要在同一机器上安装两个 CAD 的软件包以读写数据。

### 数据转换格式

一种常用的转换格式是使用中间格式。一个 CAD 系统输出这种格式，另外一个 CAD 则读取这种格式。 其中有一些格式是标准化组织定义的独立于 CAD 厂商的格式，另外更多的却是被当作业界标准的公司私有的格式。

示例格式

  - [IGES](https://zh.wikipedia.org/wiki/IGES "wikilink")
  - STEP – [ISO 10303](https://zh.wikipedia.org/wiki/ISO_10303 "wikilink")
  - [VDA-FS](https://zh.wikipedia.org/wiki/VDA-FS "wikilink")
  - [DXF](https://zh.wikipedia.org/wiki/AutoCAD_DXF "wikilink")
  - [Parasolid XT](https://zh.wikipedia.org/wiki/Parasolid "wikilink")
  - [JT](https://zh.wikipedia.org/wiki/JT_\(visualization_format\) "wikilink")

## 数据转换的细致程度

由于每一种 CAD 系统都有自己数学上以及结构上定义的几何形状，因此在从一种 CAD 数据格式转换到另外一种时都不可避免地会有一些信息的丢失。另外中间文件格式还受制于它们能够描述的数据格式，在不同的发送、接受系统上其解释可能会有所不同。

因此在不同的系统之间进行数据转换的时候首先要确定哪些需要进行转换。

如果自顶向下设计过程中只需要三维模型，那么就只需要转换模型的描述信息。但是，仍然有细节程度的问题需要考虑。例如，线框数据、曲面或者实体是否需要转换；是否需要拓扑信息（或称[边界表示](https://zh.wikipedia.org/wiki/边界表示 "wikilink")[BREP](https://zh.wikipedia.org/wiki/BREP "wikilink")）；在随后的修改中是不是要维持面与边的编号不变；特性信息以及历史信息是否需要保留在不同的系统之中；以及[产品制造信息是否需要进行转换](https://zh.wikipedia.org/wiki/产品制造信息 "wikilink")。

对于产品模型来说，可能需要保留装配信息。

当需要转换图纸的时候，通常线框几何信息容易表示，但是文本、尺寸以及其它的注释信息可能会成为问题，尤其是字体及其格式更是这样。

无论需要转换什么样的信息，都需使如图形的颜色、层面以等属性及文件中的文本信息等保持不变。

根据所用转换方法的不同，在不同的 CAD 系统之间进行转换的能力也有所不同。

## 外部链接

  - [Data Formats for AEC Software](http://www.bridgeart.net/software_database/browse_by_data_format.php)
  - [Data Formats for AEC Software](http://www.bridgeart.net/software_database/browse_by_data_format.php)
  - [Official Parasolid web page](http://www.ugs.com/products/open/parasolid/)
  - [Official JT Open web page](http://www.jtopen.com/)

[Category:计算机辅助设计](https://zh.wikipedia.org/wiki/Category:计算机辅助设计 "wikilink") [Category:CAD文件格式](https://zh.wikipedia.org/wiki/Category:CAD文件格式 "wikilink")