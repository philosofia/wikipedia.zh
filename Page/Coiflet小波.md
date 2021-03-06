> 本文内容由[Coiflet小波](https://zh.wikipedia.org/wiki/Coiflet小波)转换而来。


[Wavelet_Coif1.svg](https://zh.wikipedia.org/wiki/File:Wavelet_Coif1.svg "fig:Wavelet_Coif1.svg") **Coiflet小波**是[英格麗·多貝西](https://zh.wikipedia.org/wiki/英格麗·多貝西 "wikilink")（Ingrid Daubechies）應Ronald Coifman的要求所設計的一種離散[小波](https://zh.wikipedia.org/wiki/小波 "wikilink")。Coiflet小波的調整函式（scaling function）及小波函式（wavelet function）能同時擁有高消失動量，且其波形接近對稱，常被用於[數位訊號處理](https://zh.wikipedia.org/wiki/數位訊號處理 "wikilink")。\[1\]

## 性質

  - 定義

<!-- end list -->

  -
    一個[正交小波](https://zh.wikipedia.org/wiki/正交小波 "wikilink")（orthogonal wavelet）系統若符合以下條件，則稱為Generalized Coiflet Wavelet(GOC)。

\[\begin{array}{lcl}
\\
\mathcal{M_\tilde{\psi}}(0,l] = 0   & \mbox{for }l\mbox{ =0,1,...,L-1} \\
\mathcal{M_\tilde{\phi}}(t_0,l] = \delta[l]   & \mbox{for }l\mbox{ =0,1,...,L-1} \\
\end{array}\]

  -
    其中\({\psi}\)為小波函式，\({\phi}\)為調整函式

<!-- end list -->

  - 濾波器長度與消失動量

<!-- end list -->

  -
    若\(N\)為濾波器長度，而\(L\)為系統消失動量，則最小的\(N\)為：
    :<math>N=\\begin{cases}

3L - 1, & \\mbox{if }L\\mbox{ is odd} \\\\ 3L, & \\mbox{if }L\\mbox{ is even} \\\\ \\end{cases}</math>

  - 近線性相位（Near-linear phase）濾波器

<!-- end list -->

  -
    當\(|w|\)夠小時，GOC的[低通濾波器的](https://zh.wikipedia.org/wiki/低通濾波器 "wikilink")[頻率響應擁有漸進型態](https://zh.wikipedia.org/wiki/頻率響應 "wikilink")（asymptotic form）：
    \[\angle{H(w)}=-t_0w+C\cdot{w^{L'}}+O(w^{L'+2})\]

<!-- end list -->

  -
    其中\(L'=2\left \lfloor L/2 \right \rfloor+1\)，\(C\)則為常數項。因此\(h\)具有漸近線性相位（asymptotic linear phase）的特性：
    \[\lim_{L \to \infty}\angle{H(w)}=-t_0w\]

## 應用

  -
    Coiflet小波除了被使用在[影像壓縮外](https://zh.wikipedia.org/wiki/影像壓縮 "wikilink")，目前也有被使用在電力系統訊號監測上\[2\]

## 係數

  -
    下表為coiflet小波調整函式C6\~30的係數，小波函式的係數可以藉由每兩個係數變換一次符號來推導(例如C6 wavelet = {−0.022140543057, 0.102859456942, 0.544281086116, −1.205718913884, 0.477859456942, 0.102859456942})

| k    | C6                   | C12                  | C18                  | C24                  | C30                  |
| ---- | -------------------- | -------------------- | -------------------- | -------------------- | -------------------- |
| \-10 |                      |                      |                      |                      | \-0.0002999290456692 |
| \-9  |                      |                      |                      |                      | 0.0005071055047161   |
| \-8  |                      |                      |                      | 0.0012619224228619   | 0.0030805734519904   |
| \-7  |                      |                      |                      | \-0.0023044502875399 | \-0.0058821563280714 |
| \-6  |                      |                      | \-0.0053648373418441 | \-0.0103890503269406 | \-0.0143282246988201 |
| \-5  |                      |                      | 0.0110062534156628   | 0.0227249229665297   | 0.0331043666129858   |
| \-4  |                      | 0.0231751934774337   | 0.0331671209583407   | 0.0377344771391261   | 0.0398380343959686   |
| \-3  |                      | \-0.0586402759669371 | \-0.0930155289574539 | \-0.1149284838038540 | \-0.1299967565094460 |
| \-2  | \-0.1028594569415370 | \-0.0952791806220162 | \-0.0864415271204239 | \-0.0793053059248983 | \-0.0736051069489375 |
| \-1  | 0.4778594569415370   | 0.5460420930695330   | 0.5730066705472950   | 0.5873348100322010   | 0.5961918029174380   |
| 0    | 1.2057189138830700   | 1.1493647877137300   | 1.1225705137406600   | 1.1062529100791000   | 1.0950165427080700   |
| 1    | 0.5442810861169260   | 0.5897343873912380   | 0.6059671435456480   | 0.6143146193357710   | 0.6194005181568410   |
| 2    | \-0.1028594569415370 | \-0.1081712141834230 | \-0.1015402815097780 | \-0.0942254750477914 | \-0.0877346296564723 |
| 3    | \-0.0221405430584631 | \-0.0840529609215432 | \-0.1163925015231710 | \-0.1360762293560410 | \-0.1492888402656790 |
| 4    |                      | 0.0334888203265590   | 0.0488681886423339   | 0.0556272739169390   | 0.0583893855505615   |
| 5    |                      | 0.0079357672259240   | 0.0224584819240757   | 0.0354716628454062   | 0.0462091445541337   |
| 6    |                      | \-0.0025784067122813 | \-0.0127392020220977 | \-0.0215126323101745 | \-0.0279425853727641 |
| 7    |                      | \-0.0010190107982153 | \-0.0036409178311325 | \-0.0080020216899011 | \-0.0129534995030117 |
| 8    |                      |                      | 0.0015804102019152   | 0.0053053298270610   | 0.0095622335982613   |
| 9    |                      |                      | 0.0006593303475864   | 0.0017911878553906   | 0.0034387669687710   |
| 10   |                      |                      | \-0.0001003855491065 | \-0.0008330003901883 | \-0.0023498958688271 |
| 11   |                      |                      | \-0.0000489314685106 | \-0.0003676592334273 | \-0.0009016444801393 |
| 12   |                      |                      |                      | 0.0000881604532320   | 0.0004268915950172   |
| 13   |                      |                      |                      | 0.0000441656938246   | 0.0001984938227975   |
| 14   |                      |                      |                      | \-0.0000046098383254 | \-0.0000582936877724 |
| 15   |                      |                      |                      | \-0.0000025243583600 | \-0.0000300806359640 |
| 16   |                      |                      |                      |                      | 0.0000052336193200   |
| 17   |                      |                      |                      |                      | 0.0000029150058427   |
| 18   |                      |                      |                      |                      | \-0.0000002296399300 |
| 19   |                      |                      |                      |                      | \-0.0000001358212135 |
|      |                      |                      |                      |                      |                      |

**Coiflets係數**

## Matlab程式

  -
    F = coifwavf(W)會回傳N=str2num(W)的coiflet小波的調整函式，其中N只能為1\~5的整數。\[3\]

## 雙正交Coiflet小波

  - 定義

<!-- end list -->

  -
    一個order為\((L,\tilde{L})\)的雙正交Coiflet小波需符合以下條件：
    :<math>

\\begin{array}{lcl} \\\\ \\mathcal{M_\\tilde{\\phi}}(0,l\] = \\delta\[l\] & \\mbox{for }l\\mbox{ =0,1,...,L-1} \\\\ \\mathcal{M_\\tilde{\\psi}}(0,l\] = 0 & \\mbox{for }l\\mbox{ =0,1,...,L-1} \\\\ \\mathcal{M_{\\phi}}(0,l\] = \\delta\[l\] & \\mbox{for }l\\mbox{ =0,1,...,L-1} \\\\ \\mathcal{M_{\\psi}}(0,l\] = 0 & \\mbox{for }l\\mbox{ =0,1,...,}\\tilde{L}\\mbox{-1} \\\\ \\end{array}</math>

  - 性質

<!-- end list -->

  -
    當\(L\)為偶數時，\(h\)會對稱於原點：\(h[n]=h[-n]\)。這讓雙正交coiflet在圖片壓縮方面能有較好的[峰值信噪比](../Page/峰值信噪比.md "wikilink")（PSNR）。

## 参考资料

[Category:小波分析](https://zh.wikipedia.org/wiki/Category:小波分析 "wikilink")

1.
2.
3.