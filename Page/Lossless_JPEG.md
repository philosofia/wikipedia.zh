> 本文内容由[Lossless JPEG](https://zh.wikipedia.org/wiki/Lossless_JPEG)转换而来。


**Lossless JPEG**是一種無失真的圖像壓縮標準，在1993年由組織創建和維護，但是現在也可以用來代表Joint Photographic Experts Group所創建的無失真壓縮，包含了[JPEG 2000還有JPEG](../Page/JPEG_2000.md "wikilink")-LS。

Lossless JPEG在1993年被建立並加入了[JPEG](../Page/JPEG.md "wikilink")的標準之中，JPEG的壓縮方式通常是破壞性資料壓縮（lossy compression），意即在壓縮過程中圖像的品質會遭受到可見的破壞，Lossless JPEG則是用了與傳統的JPEG完全不同的方法來壓縮，採用無失真的壓縮方式，但並沒有受到廣泛的支援。

Lossless JPEG使用了一個預測的系統，從與目標最近的三個方格（通常為上方，左方，以及左上方）來預測，並且在預測誤差中使用熵編碼（entropy coding），Lossless JPEG在醫學影像中很受歡迎，也被用在數位負片（Digital Negative）的格式中，以及一些數位相機中用來壓縮圖片，但是在其他方面並沒有廣泛的應用。

## 無失真的操作模式

Lossless JPEG實際上是JPEG的一種操作模式，因為JPEG是使用離散餘弦變換（Discrete cosine transform）來壓縮圖片，而Lossless JPEG的模式會存在是因為離散餘弦逆變換（Inverse discrete cosine transform）沒有被嚴謹的規定，所以無法保證編碼器（encoder）的輸入會剛好與解碼器（decoder）的輸出相符合，Lossless JPEG跟使用離散餘弦變換（Discrete cosine transform）的失真壓縮模式不同，無失真的壓縮使用了一個簡單的預期性編碼模型（predictive coding model），稱為離散脈衝編碼調變（differential pulse code modulation）。

離散脈衝編碼調變是一種使用圖片中目標樣本周圍的樣本中已經編碼完成的樣本來預測目標樣本的調變，預測通常是取目標樣本的上方以及左方的樣本進行平均，離散脈衝編碼調變會將預測樣本的誤差編碼，而不是將每個樣本編碼，通常在圖片中，一個樣本與相鄰的樣本差異會接近0，傳統的離散脈衝編碼調變的編碼器如圖片一所示。[有框](https://zh.wikipedia.org/wiki/File:DPCM_concept.svg "fig:有框") [有框](https://zh.wikipedia.org/wiki/File:Lossless_encode.svg "fig:有框") [有框](https://zh.wikipedia.org/wiki/File:Pixel-prediction.svg "fig:有框")

無失真的操作模式的步驟如圖片二所示，在預測的過程中，使用了圖片三的A、B、C三個附近的樣本，以做出目標樣本X的預測，A、B、C三個樣本必須為已經預測且編碼過的樣本，在下面的表格中，有八個預測值可以用來預測目標樣本X\[1\]。

  - 數值1、2以及3是一維的預測
  - 數值4、5、6以及7是二維的預測
  - 數值0只能用在差別編碼（differential coding）的分級操作模式

一旦所有的樣本都有了預測值，樣本間的差值可以使用霍夫曼編碼（Huffman coding）或算術編碼（arithmetic coding）等等方法得到無失真的編碼。

| 數值 | 預測值           |
| -- | ------------- |
| 0  | 無             |
| 1  | A             |
| 2  | B             |
| 3  | C             |
| 4  | A + B – C     |
| 5  | A + (B – C)/2 |
| 6  | B + (A – C)/2 |
| 7  | (A + B)/2     |

一般來說，使用無失真的操作模式來壓縮彩色圖片，可以達到2:1左右的壓縮比，這個操作模式在醫學影像中很受歡迎，也被定義為數位負片（Digital Negative）的標準之一，但是因為複雜度所以不被廣泛的使用。

## JPEG-LS

**JPEG-LS**是一個無失真/接近無失真的連續調（continuous-tone）圖片壓縮標準，這個標準可以被分為兩個部分，分別為在1998年獲得了ISO 14495-1認定的核心技術，以及在2002年獲得了ISO 14495-2認定的擴增技術的部分，JPEG-LS是一個簡單且有效率的演算法，包含了兩個獨立且獨特的層級，分別為建模（modeling）與編碼（encoding），JPEG-LS是為了可以提供比lossless JPEG更有效的無失真/接近無失真的圖片壓縮而被創建出來，因為當時使用霍夫曼編碼的JPEG lossless以及其他的標準壓縮效果並沒有很好，這些壓縮方法並沒有辦法達成很好的去相關（decorrelation）效果，然而JPEG-LS可以得到很好的去相關（decorrelation）的效果，JPEG-LS的核心技術是LOCO-I演算法，此演算法使用了對殘餘項（residuals）的預測、建模、以及前文參考編碼（context-based coding），因為將殘餘項當成雙邊幾何分布（two-sided geometric distribution），又稱為離散拉普拉斯分布（discrete Laplace distribution），以及Golomb-like碼（Golomb-like codes）的使用，所以能有較低的複雜度，除了無失真壓縮，透過控制絕對值誤差（maximum absolute）的最大值，JPEG-LS也提供了失真壓縮的選擇，JPEG-LS的壓縮速度也比JPEG 2000以及原本的lossless JPEG標準還要快上許多。

### LOCO-I演算法\[2\]

在編碼前，有2個必須要做的步驟：去相關（decorrelation）以及誤差建模（error modeling）

#### 去相關（decorrelation）

在LOCO-I演算法中，垂直或水平的邊界偵測（edge detection）可以透過檢查目標像素（pixel）X的周圍像素，如圖片三所示，像素B是垂直的邊界，而像素A是水平的邊界，這個簡單的預測式稱為Median Edge Detection預測式，或稱為LOCO-I預測式，像素X透過LOCO-I預測式，像素X透過 In the LOCO-I algorithm, primitive edge可以做出以下假設：

\(X =
\begin{cases}
min(A,B),  & \mbox{if } \mbox{ C≥max(A,B)} \\
max(A,B), & \mbox{if } \mbox{ C≤min(A,B)} \\
A+B-C, & \mbox{otherwise }
\end{cases}\)

所以會有以下三種情況：

  - 當X左邊有個垂直的邊界，會挑B

<!-- end list -->

  - 當X上面有個水平的邊界，會挑A

<!-- end list -->

  - 如果都沒有，會挑A+B-C

#### 前文建模（Context modeling）

JEPG-LS的演算法估計了預測誤差（prediction errors）的條件期望值\(E\left\{\ e|Ctx \right\}\)，前文建模（Context modeling）的目的是要利用圖片中結構相似的部分來對預測誤差做編碼，前文（Context）是由已知的鄰近樣本的差異決定，可以用坡度（gradient）來表示：

\(\begin{array}{lcl}
g_1        & = & D-B \\
g_2        & = & B-C \\
g_3        & = & C-A
\end{array}\)

坡度反映了周圍樣本的平滑度（smoothness）及銳利度（edginess）等資訊，這些差異對預測誤差以及統計特性有相當大的影響，從上面的式子中找出的差值都會被量化，以JPEG-LS來說，差值會被量化成9個不同區域，分別以-4\~4代表，量化的目的是要使目前樣本的值與前文（Context）的互信息（Mutual Information）最大化，我們可以從以下的假設獲得前文：

\(P(e|Ctx=[q_1,q_2,q_3])=P(-e|Ctx=[-q_1,-q_2,-q_3])\)

在合併了正號與負號之後，可以得到前文有365個，在LOCO-I演算法是一個改進後的演算法，加法和減法的次數已經減少很多，division-free bias的計算過程可以從\[\]得到論證，可以透過這些反饋機制減少預測的偏差，進而得到較為精確的預測

#### 相同的區域可做遊程編碼（Run-length encoding）

在JPEG-LS的一般模式，使用了Golomb–Rice碼（Golomb–Rice codes）來做非負遊程（non-negative run lengths）的編碼，但Golomb–Rice碼做低熵的編碼很沒有效率，因為編碼的速率至少要1位元/符元（one bit per symbol），所以常常會造成許多冗餘（redundancy），為了避免產生太多多餘的碼，可以使用字元擴充（alphabet extension）的方法。

### JPEG-LS優點

#### 可選擇無失真/接近無失真壓縮模式

透過控制絕對值誤差可以選擇不同模式。

#### 壓縮速度較快

JPEG-LS的壓縮速度比起JPEG 2000以及原本的lossless JPEG標準還要快上許多。

#### 複雜度較低

JPEG-LS特別適合低複雜度的硬體，因為複雜度不會太高，卻可以得到不錯的無失真壓縮效果。

## JPEG 2000

JPEG 2000有一個無失真模式，是基於小波轉換的圖像壓縮，但是JPEG 2000的無失真 模式編碼速度較JPEG-LS慢，也常常在人為或合成的圖片上有較差的壓縮比，但JPEG 2000也是比較可擴展的，更進步的，且較廣泛被使用的一種壓縮格式。

## 外部連結

<http://www.jpeg.org/jpegls/index.html>

<http://www.jpeg.org/jpeg2000/index.html>

## 參考來源

[Category:图像压缩](https://zh.wikipedia.org/wiki/Category:图像压缩 "wikilink")

1.  ITU-T. ISO DIS 10918-1 Digital compression and coding of continuous-tone still images (JPEG). Recommendation T.81
2.  Marcelo J. Weinberger, Senior Member, IEEE, Gadiel Seroussi, Fellow, IEEE, and Guillermo Sapiro, Member, IEEE.*The LOCO-I Lossless Image Compression Algorithm:Principles and Standardization into JPEG-LS*IEEE TRANSACTIONS ON IMAGE PROCESSING, VOL. 9, NO. 8, AUGUST 2000