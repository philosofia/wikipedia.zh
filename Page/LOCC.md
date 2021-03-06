> 本文内容由[LOCC](https://zh.wikipedia.org/wiki/LOCC)转换而来。


**LOCC** 是 Local Operations（局域操作）and Classical Communications（經典通訊）的縮寫，它是一種用在[量子信息](../Page/量子信息.md "wikilink")上、對量子態進行操作的方法。簡單的說，當一個量子系統被分成許多部份，每個部份的測量和操作只限制在該部分上，各個部分之間允許經典通訊，例如：打電話。許多[量子信息](../Page/量子信息.md "wikilink")的工作必須藉由 **LOCC** 來完成，例如：假設某次實驗室製備了一個，但是卻不能確定這個是 \(|\psi_1\rangle\) 還是 \(|\psi_2\rangle\)，其中 \(|\psi_1\rangle\) 和 \(|\psi_2\rangle\) 是

[LOCC.png](https://zh.wikipedia.org/wiki/File:LOCC.png "fig:LOCC.png")

\[|\psi_1\rangle = \frac{1}{\sqrt{2}}\left(|0\rangle_A\otimes|0\rangle_B + |1\rangle_A\otimes|1\rangle_B\right)\]

\[|\psi_2\rangle = \frac{1}{\sqrt{2}}\left(|0\rangle_A\otimes|1\rangle_B + |1\rangle_A\otimes|0\rangle_B\right)\] A和B兩個[量子位元](../Page/量子位元.md "wikilink")是分隔兩地的，並且由*愛麗絲*對[量子位元](../Page/量子位元.md "wikilink")A進行操作，由*鲍勃*對[量子位元](../Page/量子位元.md "wikilink")B進行操作。首先*愛麗絲*測量[量子位元](../Page/量子位元.md "wikilink")A並得到結果0，此時我們仍不知道當初實驗室製備的是 \(|\psi_1\rangle\) 還是 \(|\psi_2\rangle\)。這時候*愛麗絲*藉由打電話把結果告訴*鲍勃*，接著*鲍勃*對[量子位元](../Page/量子位元.md "wikilink")B進行測量並得到結果0，現在*鲍勃*得知[波函數塌縮成](https://zh.wikipedia.org/wiki/波函數 "wikilink") \(|0\rangle_A\otimes|0\rangle_B\)，所以推得實驗室製備的是 \(|\psi_1\rangle\)。

## 糾纏轉換

將一個量子系統分成兩部分，利用 **LOCC** 操作，把一個糾纏態轉換成另一個糾纏態。 舉例說明：*愛麗絲*和*鲍勃*分別擁有一個糾纏態(純態)的一部分，例如 \(\frac{1}{\sqrt{2}}(\mid\uparrow\downarrow\rangle-\mid\downarrow\uparrow\rangle )\)。*愛麗絲*和*鲍勃*都只能對各自的自旋進行操作，也就是Local Operation的意思。當然這個操作也包含測量，當*愛麗絲*進行S<sub>z</sub>的測量後，得到本征值+ħ/2，波函數塌縮成 \(\mid\uparrow\downarrow\rangle\)，然後*愛麗絲*透過電話告訴*鲍勃*結果，這就是Classical Communications，*鲍勃*知道結果後也相應做了一個Local Operation，現在*鲍勃*做σ<sub>x</sub>操作，於是波函數變為 \(\mid\uparrow\uparrow\rangle\)。如果剛才*愛麗絲*測得本征值-ħ/2，波函數塌縮成 \(\mid\downarrow\uparrow\rangle\)，則*愛麗絲*立即進行σ<sub>x</sub>操作，然後經由電話告訴*鲍勃*，要求*鲍勃*不做任何操作，結果仍然可將波函數透過利用LOCC轉換成 \(\mid\uparrow\uparrow\rangle\)。

顯然利用 LOCC 把某個態 \(|\psi\rangle\) 轉換成 \(|\phi\rangle\)，A與B之間的糾纏只能變小或維持不變。但是並不是只要 \(|\phi\rangle\) 的[糾纏熵比](https://zh.wikipedia.org/wiki/糾纏熵 "wikilink") \(|\psi\rangle\) 的[糾纏熵還小就必定能透過](https://zh.wikipedia.org/wiki/糾纏熵 "wikilink") LOCC 作轉換。要判斷可不可轉，首先，可以把 \(|\psi\rangle\) 和 \(|\phi\rangle\) 分別做：

\[|\psi\rangle=\sum_{i=1}^D\sqrt{\omega_i}|a_i\rangle |b_i\rangle\]

\[|\phi\rangle=\sum_{i=1}^D\sqrt{\omega_i'}|a_i'\rangle |b_i'\rangle\] 將Schmidt值由大至小排列然後進行比較。尼爾森(Nielsen)在1999年提出定理\[1\]:

  -

      -
        若Majorization
        \[\sum_{i=1}^k\omega_i\le\sum_{i=1}^k\omega_i'\],
        對於所有 \(k\) 都成立，則 \(|\psi\rangle\) 可利用LOCC轉換成 \(|\phi\rangle\)。

然而若上述條件不成立，並不表示 LOCC 轉換必定不成立。如果允許引入**催化態**，LOCC 轉換仍有可能的。

### 催化轉換

Jonathan 和 Plenio 在尼爾森定理發表不久即給出一個催化轉換的例子\[2\]：考慮

\[|\psi\rangle=\sqrt{0.4}|00\rangle+\sqrt{0.4}|11\rangle+\sqrt{0.1}|22\rangle+\sqrt{0.1}|33\rangle\]

\[|\phi\rangle=\sqrt{0.5}|00\rangle+\sqrt{0.25}|11\rangle+\sqrt{0.25}|22\rangle\]

\[|c\rangle=\sqrt{0.6}\mid\uparrow\uparrow\rangle+\sqrt{0.4}\mid\downarrow\downarrow\rangle\] 以上三個態已經過且係數皆由大至小排列，以下進行 \(|\psi\rangle\) 和 \(|\phi\rangle\) 驗算係數的前 \(k\) 項之和：

  -

      -
        {| class="wikitable"

|- | \(k\) || \(|\psi\rangle\) || \(|\phi\rangle\) |- style="background: green; color: white" | 0 || 0.4 || 0.5 |- style="background: red; color: white" | 1 || 0.8 || 0.65 |- style="background: green; color: white" | 2 || 0.9 || 1.0 |- | 3 || 1.0 || 1.0 |} 以上表格中，若「\(|\psi\rangle\) 的前 \(k\) 項之和」比「\(|\phi\rangle\) 的前 \(k\) 項之和」小的話，填入綠色；大的話，填入紅色；相等則是留下白色。如此一來，**觀察 \(k\) 方向的顏色**便一目了然。如果所有顏色皆為綠色，則表示 \(|\psi\rangle\) 可經由LOCC轉換成 \(|\phi\rangle\)；如果所有顏色皆為紅色，則表示 \(|\phi\rangle\) 可經由LOCC轉換成 \(|\psi\rangle\)；如果顏色既有紅色又有綠色，則說明若無催化態便不可轉換。

那麼什麼是「催化轉換」和「催化態」呢？我們考慮直積態 \(|\psi\rangle |c\rangle\) 和 \(|\phi\rangle |c\rangle\)：

\[\begin{align}|\psi\rangle |c\rangle &=
\sqrt{0.24}|00\rangle\mid\uparrow\uparrow\rangle+\sqrt{0.24}|11\rangle\mid\uparrow\uparrow\rangle+
\sqrt{0.16}|00\rangle\mid\downarrow\downarrow\rangle+\sqrt{0.16}|11\rangle\mid\downarrow\downarrow\rangle\\
&+\sqrt{0.06}|22\rangle\mid\uparrow\uparrow\rangle+\sqrt{0.06}|33\rangle\mid\uparrow\uparrow\rangle+
\sqrt{0.04}|22\rangle\mid\downarrow\downarrow\rangle+\sqrt{0.04}|33\rangle\mid\downarrow\downarrow\rangle\end{align}\]

\[\begin{align}|\phi\rangle |c\rangle &=
\sqrt{0.30}|00\rangle\mid\uparrow\uparrow\rangle+\sqrt{0.20}|00\rangle\mid\downarrow\downarrow\rangle+
\sqrt{0.15}|11\rangle\mid\uparrow\uparrow\rangle+\sqrt{0.15}|22\rangle\mid\uparrow\uparrow\rangle\\
&+\sqrt{0.10}|11\rangle\mid\downarrow\downarrow\rangle+\sqrt{0.10}|22\rangle\mid\downarrow\downarrow\rangle\end{align}\] 以上各項已按照由大至小排列，接著同樣進行製作表格計算前 \(k\) 項之和：

  -

      -
        {| class="wikitable"

|- | \(k\) || \(|\psi\rangle |c\rangle\) || \(|\phi\rangle |c\rangle\) |- style="background: green; color: white" | 0 || 0.24 || 0.30 |- style="background: green; color: white" | 1 || 0.48 || 0.50 |- style="background: green; color: white" | 2 || 0.64 || 0.65 |- | 3 || 0.80 || 0.80 |- style="background: green; color: white" | 4 || 0.86 || 0.90 |- style="background: green; color: white" | 5 || 0.92 || 1.00 |- style="background: green; color: white" | 6 || 0.96 || 1.00 |- | 7 || 1.00 || 1.00 |} 表格做完馬上看出所有顏色皆為綠色，因此根據尼爾森定理，\(|\psi\rangle |c\rangle\) 透過LOCC轉換成 \(|\phi\rangle |c\rangle\) 是可以的。由於 \(|c\rangle\) 只是從直積態中直接加入然後轉換完畢便可取走，很像化學反應中的[催化劑](https://zh.wikipedia.org/wiki/催化劑 "wikilink")，因此可稱 \(|c\rangle\) 是催化態。

### 塔庫定理

2007年塔庫（Turgut）證明了定理\[3\]

### 糾纏轉換和量子多體系統

\[4\] \[5\] \[6\]

## 參考文獻

[Category:量子信息](https://zh.wikipedia.org/wiki/Category:量子信息 "wikilink")

1.  M. A. Nielsen, Phys. Rev. Lett. **83**, 436 - 439 (1999)
2.  D. Jonathan and M. B. Plenio, Phys. Rev. Lett. **83**, 3566 (1999)
3.  S. Turgut, J. Phys. A: Math. Theor. **40**, 12185 (2007)
4.  J. Cui, M. Gu, *et al.* Quantum phases with differing computational power. [Nat. Commun. **3**, 812 (2012)](http://dx.doi.org/10.1038/ncomms1809).
5.  F. Franchini, J. Cui, . Amico, H. Fan, M. Gu, V. Korepin, L. C. Kwek, and V. Vedral, Local Convertibility and the Quantum Simulation of Edge States in Many-Body Systems, [Phys. Rev. X **4**, 041028 (2014)](http://dx.doi.org/10.1103/PhysRevX.4.041028)
6.  Y.-C. Tzeng, L. Dai, *et al.* Entanglement convertibility by sweeping through the quantum phases of the alternating bonds XXZ chain. [Sci. Rep. **6**, 26453 (2016)](http://dx.doi.org/10.1038/srep26453).