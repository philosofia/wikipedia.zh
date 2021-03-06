> 本文内容由[Floyd判圈算法](https://zh.wikipedia.org/wiki/Floyd判圈算法)转换而来。


**Floyd判圈算法**(**Floyd Cycle Detection Algorithm**)，又称**龟兔赛跑算法**(**Tortoise and Hare Algorithm**)，是一个可以在[有限状态机](../Page/有限状态机.md "wikilink")、[迭代函数](../Page/迭代函数.md "wikilink")或者[链表](../Page/链表.md "wikilink")上判断是否存在[环](https://zh.wikipedia.org/wiki/環_\(圖論\) "wikilink")，求出该环的起点与长度的算法。该算法据[高德纳](../Page/高德纳.md "wikilink")称由美国科学家[罗伯特·弗洛伊德](../Page/罗伯特·弗洛伊德.md "wikilink")发明，但这一算法并没有出现在[罗伯特·弗洛伊德](../Page/罗伯特·弗洛伊德.md "wikilink")公开发表的著作中[1](https://en.wikipedia.org/wiki/Cycle_detection#Tortoise_and_hare)。

如果有限状态机、迭代函数或者链表上存在环，那么在某个环上以不同速度前进的2个[指针必定会在某个时刻相遇](https://zh.wikipedia.org/wiki/指針_\(信息學\) "wikilink")。同时显然地，如果从同一个起点(即使这个起点不在某个环上)同时开始以不同速度前进的2个指针最终相遇，那么可以判定存在一个环，且可以求出2者相遇处所在的环的起点与长度。

## 算法

### 算法描述

如果有限状态机、迭代函数或者链表存在环，那么一定存在一个起点可以到达某个环的某处(这个起点也可以在某个环上)。

初始状态下，假设已知某个起点[节点为节点S](https://zh.wikipedia.org/wiki/节点 "wikilink")。现设两个指针t和h，将它们均指向S。

接着，同时让t和h往前推进，但是二者的速度不同：t每前进1步，h前进2步。只要二者都可以前进而且没有相遇，就如此保持二者的推进。当h无法前进，即到达某个没有[后继的节点时](https://zh.wikipedia.org/wiki/后继 "wikilink")，就可以确定从*S*出发不会遇到环。反之当t与h再次相遇时，就可以确定从S出发一定会进入某个环，设其为环C。

如果确定了存在某个环，就可以求此环的起点与长度。

上述算法刚判断出存在环C时，显然t和h位于同一节点，设其为节点M。显然，仅需令h不动，而t不断推进，最终又会返回节点M，统计这一次t推进的步数，显然这就是环C的长度。

为了求出环C的起点，只要令h仍均位于节点M，而令t返回起点节点S，此时h与t之间距为环C长度的整数倍。随后，同时让t和h往前推进，且保持二者的速度相同：t每前进1步，h前进1步。持续该过程直至t与h再一次相遇，设此次相遇时位于同一节点P，则节点P即为从节点S出发所到达的环C的第一个节点，即环C的一个起点。

### 伪代码

` 1  `*`t`*` := `**`&`***`S`*
` 2  `*`h`*` := `**`&`***`S`*`                                        //令指針`*`t`*`和`*`h`*`均指向起點節點`*`S`*`。`
` 3  `**`repeat`**
` 4     `*`t`*` := `*`t`*`->next`
` 5     `*`h`*` := `*`h`*`->next`
` 6     `**`if`**` `*`h`*` is not NULL                                //要注意這一判斷一般不能省略`
` 7         `*`h`*` := `*`h`*`->next`
` 8  `**`until`**` `*`t`*` = `*`h`*` `**`or`**` `*`h`*` = NULL`
` 9  `**`if`**` `*`h`*` != NULL                                       //如果存在環的話`
` 10    `*`n`*` := 0`
` 11    `**`repeat`**`                                              //求環的度`
` 12        `*`t`*` := `*`t`*`->next`
` 13        `*`n`*` := `*`n`*`+1`
` 14    `**`until`**` `*`t`*` = `*`h`*
` 15    `*`t`*` := `**`&`***`S`*`                                     //求環的一個起點`
` 16    `**`while`**` `*`t`*` != `*`h`*
` 17        `*`t`*` := `*`t`*`->next`
` 18        `*`h`*` := `*`h`*`->next`
` 19    `*`P`*` := `**`*`***`t`*

### 算法复杂度

#### 时间复杂度

注意到当指针t到达环C的一个起点节点P时(此时指针h显然在环C上)，之后指针t最多仅可能走1圈。若设节点S到P距离为\(m\)，环C的长度为\(n\)，则时间复杂度为\(O(m+n)\)，是[线性时间的算法](https://zh.wikipedia.org/wiki/线性 "wikilink")。[2](http://www.siafoo.net/algorithm/10)

#### 空间复杂度

仅需要创立指针t、指针h，保存环长n、环的一个起点P。空间复杂度为\(O(1)\)，是[常数空间的算法](https://zh.wikipedia.org/wiki/常数 "wikilink")。[3](http://www.siafoo.net/algorithm/10)

## 应用

对于有限状态机与链表，可以判断从某个起点开始是否会返回到访问过运行过程中的某个[状态和节点](https://zh.wikipedia.org/wiki/状态 "wikilink")。

对于迭代函数，可以判断其是否存在[周期](https://zh.wikipedia.org/wiki/周期 "wikilink")，以及求出其[最小正周期](https://zh.wikipedia.org/wiki/最小正周期 "wikilink")。

## 相关算法

虽然Floyd判圈算法已经达到了线性时间复杂度和常数空间复杂度，但是[Brent判圈算法将减小时间复杂度的常数系数](https://zh.wikipedia.org/wiki/Brent判圈算法 "wikilink")，平均消耗时间比Floyd判圈算法少36%。[4](http://www.siafoo.net/algorithm/11)

## 参考链接

  - [Floyd's Cycle Detection Algorithm (The Tortoise and the Hare)](http://www.siafoo.net/algorithm/10)
  - [Brent's Cycle Detection Algorithm (The Teleporting Turtle)](http://www.siafoo.net/algorithm/11)
  - [Floyd's cycle-finding algorithm](https://en.wikipedia.org/wiki/Cycle_detection#Tortoise_and_hare)

[Category:图论算法](https://zh.wikipedia.org/wiki/Category:图论算法 "wikilink")