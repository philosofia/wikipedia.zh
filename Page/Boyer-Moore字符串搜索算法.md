在[计算机科学](../Page/计算机科学.md "wikilink")里，**Boyer-Moore字符串搜索算法**是一种非常高效的[字符串搜索算法](https://zh.wikipedia.org/wiki/字符串搜索算法 "wikilink")。它由[Bob Boyer和](https://zh.wikipedia.org/wiki/Bob_Boyer "wikilink")[J Strother Moore设计于](https://zh.wikipedia.org/wiki/J_Strother_Moore "wikilink")1977年。此[算法](../Page/算法.md "wikilink")仅对搜索目标[字符串](https://zh.wikipedia.org/wiki/字符串\(计算机科学\) "wikilink")（关键字）进行[预处理](https://zh.wikipedia.org/wiki/预处理 "wikilink")，而非被搜索的字符串。虽然Boyer-Moore算法的执行时间同样线性依赖于被搜索字符串的大小，但是通常仅为其它算法的一小部分：它不需要对被搜索的字符串中的字符进行逐一比较，而会跳过其中某些部分。通常搜索关键字越长，算法速度越快。它的效率来自于这样的事实：对于每一次失败的匹配尝试，算法都能够使用这些信息来排除尽可能多的无法匹配的位置。

## 定义

  - S\[i\]为字符串S从1开始排列的第i个字符
  - S\[i..j\]为字符串S的一个子串，始于i，终于j。
  - S的前缀定义为S\[1..i\],1\<i\<n，n为字符串S的长度。
  - S的后缀定义为S\[i..n\],1\<i\<=n，小于字符串S的长度。
  - 检索的字符串称为**pattern**，用符号**P**表示。
  - 被检索字符称为**text**，用符号**T**表示。
  - **P**的长度为n
  - **T**的长度为m
  - *k*表示**P**的**最后一个字符在**T'''中的位置。
  - 当匹配发生时，**P**在**T**中的位置为***T\[(k-n+1)..k\]***。

## 原理

不同于朴素模式（brute-force search）的逐个字符对比，Boyer-Moore充分使用预处理**P**的信息来尽可能跳过更多的字符。通常，我们比较一个字符串都是从首字母开始，逐个比较下去。一旦发现有不同的字符，就需要从头开始进行下一次比较。这样，就需要将字串中的所有字符一一比较。Boyer-Moore算法的关键在于，当**P**的最后一个字符被比较完成后，我们可以决定跳过一个或更多个字符。如果最后一个字符不匹配，那么就没必要继续比较前一个字符。如果最后一个字符未在**P**中出现，那么我们可以直接跳过**T**的n个字符，比较接下来的n个字符，n为**P**的长度（见定义）。如果最后一个字符出现在**P**中，那么跳过的字符数需要进行计算（也就是将**P**整体往后移），然后继续前面的步骤来比较。通过这种字符的移动方式来代替逐个比较是这个算法如此高效的关键所在。

形式化的表述方式为，从k=n开始，也就是**P**从**T**的最开始进行比较。紧接着，**P**的第n个字符和**T**的第k个字符开始：字符串依次从**P**的最后一个字符到最开始的字符。结束条件是当比较到达P的最开始（此时匹配完成），或按照规则移动后的字符部匹配发生时。然后，在新的对齐位置重新开始比较，如此反复，直到到达**T**的结尾。

移动规则是一张间恒定的查找表，通过对**P**的预处理产生的。

## 移动规则

移动字符数是通过两条规则决定的：坏字符规则和好后缀规则。实际移动为通过这两条规则计算出的最大移动个数。

### 坏字符规则

#### 原理

<div class="thumb tright" style="width:160px;">

<div>

|    |    |                                      |    |                                      |    |    |   |    |    |    |
| -- | -- | ------------------------------------ | -- | ------------------------------------ | -- | -- | - | -- | -- | -- |
| \- | \- | \-                                   | \- | X                                    | \- | \- | K | \- | \- | \- |
| A  | N  | P                                    | A  | <span style="color:#FF0000">N</span> | M  | A  | N | A  | M  | \- |
| \- | N  | <span style="color:#008000">N</span> | A  | A                                    | M  | A  | N | \- | \- | \- |
| \- | \- | \-                                   | N  | <span style="color:#008000">N</span> | A  | A  | M | A  | N  | \- |

<div class="thumbcaption" style="width:160px;">

Demonstration of bad character rule with pattern **NNAAMAN**.

</div>

</div>

</div>

当**T**中有字符不匹配时，如果**T**中的这个不匹配的字符出现在对应**P**中当前位置的左侧，那么**P**移动位置将这两个在字符对齐。如果**T**中这个不匹配字符不在P中当前位置的左侧，那么将当前位置左侧的所有字符均移到该不匹配字符后。右侧的例子中，X位置发生了不匹配，我们检查P中的不匹配字符N（对应T中字符A）在P当前位置（X）的左侧存在，因此，将最靠近该不匹配字符位置的N与**P**中的X位置的N对齐，也就是向右移动两位。

#### 处理

当我们发现不匹配字符时，假设这个字符在**T**中为**c**，位置在**T**的i。字符**c**在**P**中出现的最靠近i位置，假设为j，j\<i或j=-1（如果**P**不存在字符c）。那么移动位数为i - j，复杂度是O(1)。i，j的起点为P在T中位置的开始***T\[(k-n+1)..k\]***的***(k-n+1)。*** 大多网站都只建立一个一维坏字符数组来保存，但事实这只能保存最靠左或最靠右的字符c，明显与英文的wikipedia里面要求一个二维数组来保存信息的不一样。

### 好后缀规则

#### 原理

好后缀规则要更复杂一点。

假设有**P**和**T**，**T**中字串t匹配到了**P**的一个后缀，但在比较位置i时发生不匹配。设匹配到的好后缀在**T**中为t，在**P**中为t'（t = t'）。

分两种情况来讨论：

1，在**P**中i位置的左侧最靠近i位置查找字串t'使得t'=t（此时t'不是P的后缀，实际上也就是查找匹配到的字串除了在P的后缀中存在，是否在P的其他位置存在），若存在，则移动相应的位数将找到的t'与T中的t对齐。

2，如果t'不存在，那我们继续查找**t的某一个后缀是否为P的前缀**，若存在，则移动相应的位将P的前缀与t的后缀位置对齐。否则，将**P**向后移动n个字符。

**好后缀规则的实质是，将不匹配位置右侧匹配到的字符串t的所有字符后缀组合，用于查找它们在P的不匹配位置左侧是否存在。**

通俗的理解是，最长的好后缀t是否存在于i的左侧（情况1），其他后缀组合中是否存在与P的前缀相同的情况（情况2）。

#### 处理

## 举例

假设被检索文字列是“1234567890”，檢索文字列是“MOORE”。简单的比较需要执行十次才得到结论不匹配。被检索文字列：1234567890

`  第一次比较：M....         （M和1比较，不匹配）`
`  第二次比较：M....        （M和2比较，不匹配）`
`  第三次比较：  M....       （M和3比较，不匹配）`
`        ...`
`  第十次比较：         M....（M和0比较，不匹配）`

※未参与比较的文字用【.】占位。

BM算法只需要2次比较。

被检索文字列：1234567890

`  第一次比较：....E        （E和5比较，不匹配，并且5不是MOORE中任何文字）`
`  第二次比较：     ....E   （E和0比较，不匹配，并且0不是MOORE中任何文字）`

第一次从检索文字的末尾开始，因为如果被检索文字的第5文字位置不是E，则无论前4个文字是什麽，都绝不可能匹配了。这一点比较容易理解。

那么，为什么不用E和6比较呢？

这是BM算法又一处精妙之处。在E和5进行比较的时候不仅知道他们不相等，而且还知道了5不和检索文字MOORE中的任何一个文字相等，这使得下面这些比较都可以省略掉。

被检索文字列：....5......

`不需要的比较：...R.       （E和5比较时也同时发现5不等于R，于是这个比较是不必要的）`
`不需要的比较：  ..O..      （E和5比较时也同时发现5不等于O，于是这个比较是不必要的）`
`不需要的比较：   .O...     （E和5比较时也同时发现5不等于O，于是这个比较是不必要的）`
`不需要的比较：    M....    （E和5比较时也同时发现5不等于M，于是这个比较是不必要的）`

## 另见

  - [克努斯-莫里斯-普拉特算法](../Page/克努斯-莫里斯-普拉特算法.md "wikilink")
  - [后缀树](https://zh.wikipedia.org/wiki/后缀树 "wikilink")

## 参考资料

<references />

## 外部链接

  - [String Searching Applet animation](http://www.cs.pitt.edu/~kirk/cs1501/animations/String.html)
  - [Original article](http://www.cs.utexas.edu/~moore/publications/fstrpos.pdf)
  - [An example of the Boyer-Moore algorithm](http://www.cs.utexas.edu/users/moore/best-ideas/string-searching/fstrpos-example.html) from the homepage of [J Strother Moore](https://zh.wikipedia.org/wiki/J_Strother_Moore "wikilink"), co-inventor of the algorithm
  - [An explanation of the algorithm (with sample C code)](http://www-igm.univ-mlv.fr/%7Elecroq/string/node14.html)
  - [Cole et al., Tighter lower bounds on the exact complexity of string matching](http://www.cs.nyu.edu/cs/faculty/cole/papers/CHPZ95.ps)
  - [An implementation of the algorithm in Ruby](http://github.com/jashmenn/boyermoore)
  - [Scala functional implementation](http://blog.aunndroid.com/2011/11/learning-scala-boyermoore-search-1.html) with [source code](https://gist.github.com/1376820)
  - [字符串匹配的Boyer-Moore算法](http://www.ruanyifeng.com/blog/2013/05/boyer-moore_string_search_algorithm.html)

[Category:字符串匹配算法](https://zh.wikipedia.org/wiki/Category:字符串匹配算法 "wikilink")