> 本文内容由[SKI组合子演算](https://zh.wikipedia.org/wiki/SKI组合子演算)转换而来。


**SKI组合子演算**是一个计算系统，它是对无类型版本的[Lambda演算的简约](https://zh.wikipedia.org/wiki/Lambda演算 "wikilink")。这个系统声称在Lambda演算中所有运算都可以用三个组合子**S**、**K**和**I**来表达。

在这个系统中的所有[函数](../Page/函数.md "wikilink")可以只使用**S**、**K**、**I**的字母表和圆括号（分组符号）来表达。通常假定组合子是[左结合的](https://zh.wikipedia.org/wiki/结合性 "wikilink")，从而在不影响执行次序的情况下精简表达式中的圆括号。

## 非形式定义

非正式的说，在这个系统中的组合子定义如下（x, y和z表示从函数**S**, **K**, **I**与规定值制作的表达式）:

**I**接受一个参数并返回：

  -
    **I**x → x

**K**接受两个参数，丢弃第二个，返回第一个：

  -
    **K**xy → x

**S**是代换运算。它接受三个参数，把第一个参数应用于第三个，接着把它应用于把第二个应用于第三个的结果，返回最终的结果。更加清晰的：

  -
    **S**xyz → xz(yz)

注意从这些定义可以证实SKI演算不是完全进行Lambda演算的计算的最小化系统，因为**I**可以用**S**和**K**来表达。这可以通过比较下列表达式和上面的**I**的定义来证明：

  -
    **SKK**x → **K**x(**K**x) → x

事实上，只使用一个组合子定义一个完备的系统是可能的。一个例子是Chris Barker的[\(\iota\)](https://web.archive.org/web/20060428062101/http://ling.ucsd.edu/~barker/Iota/)组合子，定义如下：

  -
    **ι**x = x**SK**

## 形式定义

在系统中的项和推导可以被形式定义：

**项**: 项的集合T用如下规则递归的定义。

1.  **S**、**K**和**I**是项。
2.  如果τ<sub>1</sub>和τ<sub>2</sub>是项，则 (τ<sub>1</sub>τ<sub>2</sub>)是项。
3.  不是由前两个规则得到的东西都不是项。

**推导**: 推导是用下列规则递归定义的项的有限序列（这里的所有希腊字母表示有效的项或带有完全平衡的圆括号的表达式）:

1.  如果Δ是结束于形如α(**I**β)ι的表达式的一个推导，则Δ尾随着项αβι是一个推导。
2.  如果Δ是结束于形如α((**K**β)γ)ι的表达式的一个推导，则Δ尾随着项αβι是一个推导。
3.  如果Δ是结束于形如α(((**S**β)γ)δ)ι的表达式的一个推导，则Δ尾随着项α((βδ)(γδ))ι是一个推导。

假定一个序列本来是一个有效的推导，则可以使用这些规则来扩展它。[1](http://people.cs.uchicago.edu/~odonnell/Teacher/Lectures/Formal_Organization_of_Knowledge/Examples/combinator_calculus/)

## SKI表达式

### 自应用和递归

**SII**是接受一个参数并应用这个参数于自身的表达式：

  -
    **SII**α → **I**α(**I**α) → αα

这个表达式的一个有趣的性质是它使表达式**SII**(**SII**)不可归约：

  -
    **SII**(**SII**) → **I**(**SII**)(**I**(**SII**)) → **I**(**SII**)(**SII**) → **SII**(**SII**)

这个表达式的另一个结果是它允许你写应用某个东西到其他某个东西的自应用的函数：

  -
    (**S**(**K**α)(**SII**))β → **K**αβ(**SII**β) → α(**SII**β) → α(ββ)

这个函数可以用来完成[递归](../Page/递归.md "wikilink")。如果\(\beta\)是应用\(\alpha\)到其他某个东西的自应用的函数，则自应用\(\beta\)在\(\beta\beta\)上递归的进行\(\alpha\)。更加明确的，如果：

  -
    β = **S**(**K**α,**SII**)则：
    **SII**β → ββ → α(ββ) → α(α(ββ))→…

### 反转表达式

**S**(**K**(**SI**))**K**反转随后的两项：

  -
    **S**(**K**(**SI**))**K**αβ →
    **K**(**SI**)α(**K**α)β →
    **SI**(**K**α)β →
    **I**β(**K**αβ) →
    **I**βα → βα

### 布尔逻辑

SKI组合子演算还可以用if-then-else结构的形式实现[布尔逻辑](../Page/布尔逻辑.md "wikilink")。if-then-else结构由要么为**T**（真）要么为**F**（假）的一个布尔表达式和两个参数组成，使得：

  -
    **T**xy → x

和

  -
    **F**xy → y

关键在这两个布尔表达式的定义之中。第一个表现如同我们的基本组合子之一：

  -
    **T** = **K**
    **K**xy → x

第二个也非常简单：

  -
    **F** = **KI**
    **KI**xy → **I**y → y

一旦定义了真和假，所有布尔逻辑都可以用if-then-else结构的形式来实现。

布尔运算NOT（它返回给定布尔值的对立值）表现如同带有假和真作为第二个和第三个值的if-then-else结构，所以可以实现为后缀运算：

  -
    NOT = (**F**)(**T**) =(**KI**,**K**)如果把它们放入if-then-else结构中，可以证实它有预期的结果：
    (**T**)NOT=**T**(**F**)(**T**)=**F**
    (**F**)NOT=**F**(**F**)(**T**)=**T**

布尔运算OR（如果围绕它的两个布尔值任何一个为真则它返回真）表现如同带有真作为第二个参数的if-then-else结构，所以可以实现为中缀运算：

  -
    OR = **T** = **K**

如果把它放入if-then-else结构中，可以证实它有预期的结果：

  -
    (**T**)OR(**T**)=**T**(**T**)(**T**)=**T**
    (**T**)OR(**F**)=**T**(**T**)(**F**)=**T**
    (**F**)OR(**T**)=**F**(**T**)(**T**)=**T**
    (**F**)OR(**F**)=**F**(**T**)(**F**)=**F**

布尔运算AND（如果围绕它的两个布尔值两个都为真则它返回真）表现如同带有假作为第三个参数的if-then-else结构，所以它可以实现为后缀运算：

  -
    AND = **F** = **KI**

如果把它放入if-then-else结构中，可以证实它有预期的结果：

  -
    (**T**)(**T**)AND=**T**(**T**)(**F**)=**T**
    (**T**)(**F**)AND=**T**(**F**)(**F**)=**F**
    (**F**)(**T**)AND=**F**(**T**)(**F**)=**F**
    (**F**)(**F**)AND=**F**(**F**)(**F**)=**F**

因为如此以SKI符号的方式定义了真，假，NOT（作为后缀运算符），OR（作为中缀运算符），AND（作为后缀运算符），这证明了SKI系统可以完全的表达布尔逻辑。

### 直覺邏輯

組合子**K**和**S**對應於兩個周知的[命題邏輯公理](https://zh.wikipedia.org/wiki/命題邏輯 "wikilink")：

  -
    **AK**: A →(B → A)
    **AS**:(A →(B → C))→((A → B) →(A → C))函數應用對應於[肯定前件規則](https://zh.wikipedia.org/wiki/肯定前件 "wikilink")：

**MP**：從A和A → B推出B。

公理**AK**和**AS**和規則**MP**對于[直覺邏輯的蘊含片段是完備的](https://zh.wikipedia.org/wiki/直覺邏輯 "wikilink")。

## 参见

  - [函数式编程](../Page/函数式编程.md "wikilink")
  - [组合子逻辑](../Page/组合子逻辑.md "wikilink")
  - [B,C,K,W系统](../Page/B,C,K,W系统.md "wikilink")
  - [邱奇數](https://zh.wikipedia.org/wiki/邱奇數 "wikilink")

## 外部链接

  - [S and K Combinators](http://c2.com/cgi/wiki?EssAndKayCombinators)
  - [The SKI Combinator Calculus as a Universal System](http://people.cs.uchicago.edu/~odonnell/Teacher/Lectures/Formal_Organization_of_Knowledge/Examples/combinator_calculus/)
  - [Javascript SKI combinator interpreter](http://pnetz.org/ski)

[Category:Lambda演算](https://zh.wikipedia.org/wiki/Category:Lambda演算 "wikilink")