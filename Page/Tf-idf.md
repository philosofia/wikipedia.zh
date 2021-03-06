> 本文内容由[Tf-idf](https://zh.wikipedia.org/wiki/Tf-idf)转换而来。


**tf-idf**（）是一種用於[資訊檢索與](https://zh.wikipedia.org/wiki/資訊檢索 "wikilink")[文本挖掘](../Page/文本挖掘.md "wikilink")的常用加權技術。tf-idf是一種統計方法，用以評估一字詞對於一個文件集或一個[語料庫中的其中一份](https://zh.wikipedia.org/wiki/語料庫 "wikilink")[文件的重要程度](https://zh.wikipedia.org/wiki/文件 "wikilink")。字詞的重要性隨著它在文件中出現的次數成[正比增加](https://zh.wikipedia.org/wiki/正比 "wikilink")，但同時會隨著它在語料庫中出現的頻率成反比下降。tf-idf加權的各種形式常被[搜索引擎](../Page/搜索引擎.md "wikilink")應用，作為文件與用戶查詢之間相關程度的度量或評級。除了tf-idf以外，互聯網上的搜尋引擎還會使用基於連結分析的評級方法，以確定文件在搜尋結果中出現的順序。

## 原理

在一份給定的文件裡，**詞頻**（term frequency，tf）指的是某一個給定的詞語在該文件中出現的频率。這個數字是对**词数**（term count）的归一化，以防止它偏向長的文件。（同一個詞語在長文件裡可能會比短文件有更高的詞数，而不管該詞語重要與否。）對於在某一特定文件裡的詞語\(t_{i}\)來說，它的重要性可表示為：

\[\mathrm{tf_{i,j}} = \frac{n_{i,j}}{\sum_k n_{k,j}}\]

以上式子中\(n_{i,j}\)是該詞在文件\(d_{j}\)中的出現次數，而分母則是在文件\(d_{j}\)中所有字詞的出現次數之和。

**逆向文件頻率**（inverse document frequency，idf）是一個詞語普遍重要性的度量。某一特定詞語的idf，可以由總文件數目除以包含該詞語之文件的數目，再將得到的商取以10为底的[對數得到](https://zh.wikipedia.org/wiki/對數 "wikilink")：

\[\mathrm{idf_{i}} =  \lg \frac{|D|}{|\{j: t_{i} \in d_{j}\}|}\]

其中

  - |D|：語料庫中的文件總數
  - \(|\{ j: t_{i} \in d_{j}\}|\)：包含詞語\(t_{i}\)的文件數目（即\(n_{i,j} \neq 0\)的文件數目）如果詞語不在資料中，就導致分母為零，因此一般情况下使用\(1 + |\{j : t_{i} \in d_{j}\}|\)

然後

\[\mathrm{tf{}idf_{i,j}} = \mathrm{tf_{i,j}} \times  \mathrm{idf_{i}}\]

某一特定文件內的高詞語頻率，以及該詞語在整個文件集合中的低文件頻率，可以產生出高權重的tf-idf。因此，tf-idf傾向於過濾掉常見的詞語，保留重要的詞語。

## 例子

有很多不同的[數學公式可以用來](https://zh.wikipedia.org/wiki/數學公式 "wikilink")[計算tf](https://zh.wikipedia.org/wiki/計算 "wikilink")-idf。這邊的例子以上述的數學公式來計算。詞頻（tf）是一詞語出現的次數除以該文件的總詞語數。假如一篇文件的總詞語數是100個，而詞語「母牛」出現了3次，那麼「母牛」一詞在該文件中的詞頻就是3/100=0.03。而計算文件頻率（IDF）的方法是以文件集的檔案總數，除以出現「母牛」一詞的檔案數。所以，如果「母牛」一詞在1,000份文件出現過，而文件總數是10,000,000份的話，其逆向文件頻率就是lg（10,000,000 / 1,000）=4。最後的tf-idf的分數為0.03 \* 4=0.12。

## 在向量空間模型裡的應用

tf-idf權重計算方法經常會和[餘弦相似性](https://zh.wikipedia.org/wiki/餘弦相似性 "wikilink")（cosine similarity）一同使用於[向量空間模型](../Page/向量空間模型.md "wikilink")中，用以判斷兩份文件之間的[相似性](https://zh.wikipedia.org/wiki/相似性 "wikilink")。

## tf-idf的理论依据及不足

tf-idf算法是建立在这样一个假设之上的：对区别文档最有意义的词语应该是那些在文档中出现频率高，而在整个文档集合的其他文档中出现频率少的词语，所以如果特征空间坐标系取tf词频作为测度，就可以体现同类文本的特点。另外考虑到单词区别不同类别的能力，tf-idf法认为一个单词出现的文本频数越小，它区别不同类别文本的能力就越大。因此引入了逆文本频度idf的概念，以tf和idf的乘积作为特征空间坐标系的取值测度，并用它完成对权值tf的调整，调整权值的目的在于突出重要单词，抑制次要单词。但是在本质上idf是一种试图抑制雜訊的加权，并且单纯地认为文本頻率小的单词就越重要，文本頻率大的单词就越无用，显然这并不是完全正确的。idf的简单结构并不能有效地反映单词的重要程度和特征词的分布情况，使其无法很好地完成对权值调整的功能，所以tf-idf法的精度并不是很高。

此外，在tf-idf算法中并没有体现出单词的位置信息，对于Web文档而言，权重的计算方法应该体现出HTML的结构特征。特征词在不同的标记符中对文章内容的反映程度不同，其权重的计算方法也应不同。因此应该对于处于网页不同位置的特征词分别赋予不同的系数，然后乘以特征词的词频，以提高文本表示的效果。

## 參考資料

  - Salton, G. and McGill, M. J. 1983 *Introduction to modern information retrieval*. McGraw-Hill, ISBN 0-07-054484-0.
  - Salton, G., Fox, E. A. and Wu, H. 1983 Extended Boolean information retrieval. *Commun. ACM* 26, 1022–1036.
  - Salton, G. and Buckley, C. 1988 Term-weighting approaches in automatic text retrieval. *Information Processing & Management* 24 (5): 513–523.

## 外部連結

  - [Term Weighting Approaches in Automatic Text Retrieval](http://portal.acm.org/citation.cfm?id=866292)
  - [Robust Hyperlinking](http://elib.cs.berkeley.edu/cgi-bin/pl_dochome?query_src=&format=html&collection=Wilensky_papers&id=3&show_doc=yes)：An application of tf–idf for stable document addressability.

[Category:情报检索](https://zh.wikipedia.org/wiki/Category:情报检索 "wikilink") [Category:人工智慧](https://zh.wikipedia.org/wiki/Category:人工智慧 "wikilink")