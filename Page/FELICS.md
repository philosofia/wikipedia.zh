> 本文内容由[FELICS](https://zh.wikipedia.org/wiki/FELICS)转换而来。


## FELICS（快速高效无损图像压缩系统）

FELICS 是一个无损图像压缩算法，它比工作在无损模式下的 JPEG 快 5 倍，并且能够达到同样的[压缩率](https://zh.wikipedia.org/wiki/压缩率 "wikilink")。

## 历史

它是由分别工作在布朗大学与杜克大学计算机系的 P. G. Howard 与 J. S. Vitter 共同发明并在 1993 年提交到了犹他州 Snowbird 举办的数据压缩会议。

## 原理

FELICS 与其它用熵编码器针对经过去相关的图像进行压缩的无损图像压缩算法类似，去相关表示为 \(\Delta = H - L\) ，其中 \(H=max(P1,P2)\)，\(L=min(P1,P2)\)， 其中 \(P1,P2\) 是用于对当前像素 \(P\) 进行编码提供相关信息的两个相邻的像素（[因果](https://zh.wikipedia.org/wiki/因果 "wikilink") 在解码器中已经进行编码并且已知）。

P 可以在区间 \[L,H\] 之内、也可以大于 H 或者小于 L，第一种情况用 1 位表示，第二种情况用 2 位表示。下面的图示表示像素的直方图、沿 x 轴的亮度值以及在 y 轴上的出现频率。

当 P 落在区间 \[L,H\] 中时，使用修正的二进制编码进行编码在这个区间中心 \((L+H)/2\) 处有一个小的峰值。这里所用的修正二进制编码类似于标准的 P 的二进制表示，只是有一些小的改动。

当 P 落在区间之外的时候使用 [Rice code](https://zh.wikipedia.org/wiki/Rice_code "wikilink") 进行编码，参数是自适应选择的，这是因为出现的概率是按照指数分布的。

对于最后在 *区间(L,H)* 中不再摆动的区域（dead-beat zone）, FELICS 使用[修正的二进制编码对余数进行编码](https://zh.wikipedia.org/wiki/修正的二进制编码 "wikilink")。这种使用上下文关系的形式是[后向自适应量化](https://zh.wikipedia.org/wiki/后向自适应量化 "wikilink")，它可以避免[前向自适应量化中多余的标志从而实现更大的压缩](https://zh.wikipedia.org/wiki/前向自适应量化 "wikilink")。

对于指数分布的尾数使用传统的 [Golomb Rice code](https://zh.wikipedia.org/wiki/Golomb_Rice_code "wikilink") 进行编码。

## 改进

FELICS 的改进包括根据前面的数据块搜索 Rice 的参数 k 的方法以及当 L=H 的时候编码动态区间的改进。

## 参考文献

1.  P. G. Howard and J. S. Vitter. \`\`Fast and Efficient Lossless Image Compression,'' Proceedings of the 1993 IEEE Data Compression Conference (DCC '93), Snowbird, UT, April 1993. \[<http://ieeexplore.ieee.org/search/srchabstract.jsp?arnumber=253114&isnumber=6456&punumber=452&k2dockey=253114@ieeecnfs&query=%28%28felics%29%3Cin%3Emetadata%29&pos=2>. IEEExplore Abstract\]
2.
## 参见

1.  [JPEG-LS](https://zh.wikipedia.org/wiki/JPEG-LS "wikilink")
2.  \[<http://www.compression-links.info/Link/1321_FELICS_Fast_and_Efficient_Lossless_Image_Compression.htm>, Compression-Links.Info\]。

[Category:无损压缩算法](https://zh.wikipedia.org/wiki/Category:无损压缩算法 "wikilink") [Category:有损压缩算法](https://zh.wikipedia.org/wiki/Category:有损压缩算法 "wikilink")