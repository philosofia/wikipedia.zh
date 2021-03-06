> 本文内容由[SC-FDMA](https://zh.wikipedia.org/wiki/SC-FDMA)转换而来。


**SC-FDMA**（Single-carrier Frequency-Division Multiple Access，单载波[频分多址](https://zh.wikipedia.org/wiki/频分多址 "wikilink")），是[LTE的上行链路的主流多址技术](https://zh.wikipedia.org/wiki/LTE "wikilink")\[1\]\[2\]\[3\]。因为SC-FDMA在传统的OFDMA处理过程之前有一个额外的DFT（离散傅立叶变换）处理，SC-FDMA也被叫做线性预编码[OFDMA技术](https://zh.wikipedia.org/wiki/OFDMA "wikilink")。

相比OFDMA，SC-FDMAOFDMA的[PAPR](https://zh.wikipedia.org/wiki/PAPR "wikilink")（峰值/平均功率比，peak-to-average power ratio）比较低，可以提高移动终端的功率发射效率，延长电池的使用时间，降低终端成本。

## Transmitter and Receiver Structure of LP-OFDMA/SC-FDMA

SC-FDMA技术和OFDMA十分类似。每个用户的数据流比特被映射到星座图符号（比如BPSK符号、QPSK符号 或者M-QAM符号）。系统给不同的用户分配不同的傅立叶系数。傅立叶系数的分配在映射单元和逆映射单元内 完成。发射端在IFFT之前插入傅立叶沉默系数，接收端则在FFT之后去除这个系数。

SC-FDMA的特征是输出单载频发射信号，而OFDMA输出的是多载频信号。

OFDMA中，数据符号被独立地调制到每一个子载波，因此在任何一个时点，每个子载波的振幅取决于数字信 号调制方案的星座点。而在SC-FDMA，调制到特定子载波上的某个时点的所有数据符号的线性组合。

SC-FDMA信号可以在时域生成，也可以在频域生成。处于和下行链路的兼容考虑，LTE选择了在频域生成 SC-FDMA技术，即DFT-S-OFDM（Discrete Fourier Transform-Spread OFDM）技术。该技术是在 OFDM的IFFT调制之前对信号进行DFT扩展，这样系统发射的是时域信号，从而可以避免OFDM系统发送频域信号 带来的PAPR问题。

LTE上行链路物理层的相关参数是：子帧（Subframe）长度1ms， 每个子帧包含2个时隙,即时隙（Slot） 长度0.5ms;SC-FDMA符号长度66.67µs；如果是普通前缀（CP）,则每个slot包括7个符号，第一个符号前的 CP长度为5.2µs，后面6个符号之前的CP长度为4.69µs；如果是扩展前缀（CP），则每个slot包括6个符号， 符号前的CP长度是16.67µs；每个资源块（RB）包含12个子载波；每个子载波的带宽是15KHz。

对于一个20MHz的LTE系统，能够提供1200个子载波，即100个资源块（RB）。

## 參見

  - [OFDMA](https://zh.wikipedia.org/wiki/OFDMA "wikilink")

## 参考资料

<references />

[Category:頻道存取方式](https://zh.wikipedia.org/wiki/Category:頻道存取方式 "wikilink")

1.  Hyung G. Myung, Junsung Lim, and David J. Goodman, “[Single Carrier FDMA for Uplink Wireless Transmission](http://hgmyung.googlepages.com/SingleCarrierFDMA_VTmagSep06.pdf)”, IEEE Vehicular Technology Magazine, vol. 1, no. 3, Sep. 2006, pp. 30–38
2.  H. Ekström, A. Furuskär, J. Karlsson, M. Meyer, S. Parkvall, J. Torsner, and M. Wahlqvist, “Technical Solutions for the 3G Long-Term Evolution,” IEEE Commun. Mag., vol. 44, no. 3, March 2006, pp. 38–45
3.  3rd Generation Partnership Project (3GPP); Technical Specification Group Radio Access Network; Physical Layer Aspects for Evolved UTRA, <http://www.3gpp.org/ftp/Specs/html-info/25814.htm>