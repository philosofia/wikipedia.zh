> 本文内容由[Paxos算法](https://zh.wikipedia.org/wiki/Paxos算法)转换而来。


**Paxos算法**是[莱斯利·兰伯特](https://zh.wikipedia.org/wiki/莱斯利·兰伯特 "wikilink")（，[LaTeX中的](https://zh.wikipedia.org/wiki/LaTeX "wikilink")「La」）于1990年提出的一种基于消息传递且具有高度容错特性的共识（consensus）算法。\[1\]

需要注意的是，Paxos常被误称为“一致性算法”。但是“[一致性（consistency）](../Page/线性一致性.md "wikilink")”和“共识（consensus）”并不是同一个概念。Paxos是一个共识（consensus）算法。\[2\]

## 问题和假设

分布式系统中的节点通信存在两种模型：[共享内存](https://zh.wikipedia.org/wiki/共享内存 "wikilink")（Shared memory）和[消息传递](https://zh.wikipedia.org/wiki/消息传递 "wikilink")（Messages passing）。基于消息传递通信模型的分布式系统，不可避免的会发生以下错误：进程可能会慢、被杀死或者重启，消息可能会延迟、丢失、重复，在基础 Paxos 场景中，先不考虑可能出现消息篡改即[拜占庭错误的情况](../Page/拜占庭将军问题.md "wikilink")。Paxos 算法解决的问题是在一个可能发生上述异常的[分布式系统中如何就某个值达成一致](../Page/分布式计算.md "wikilink")，保证不论发生以上任何异常，都不会破坏决议的共识。一个典型的场景是，在一个分布式数据库系统中，如果各节点的初始状态一致，每个节点都执行相同的操作序列，那么他们最后能得到一个一致的状态。为保证每个节点执行相同的命令序列，需要在每一条指令上执行一个「共识算法」以保证每个节点看到的指令一致。一个通用的共识算法可以应用在许多场景中，是分布式计算中的重要问题。因此从20世纪80年代起对于共识算法的研究就没有停止过。

为描述Paxos算法，Lamport虚拟了一个叫做Paxos的[希腊城邦](https://zh.wikipedia.org/wiki/希腊城邦 "wikilink")，这个岛按照议会民主制的政治模式制订法律，但是没有人愿意将自己的全部时间和精力放在这种事情上。所以无论是议员，议长或者传递纸条的服务员都不能承诺别人需要时一定会出现，也无法承诺批准决议或者传递消息的时间。但是这里假设没有[拜占庭将军问题](../Page/拜占庭将军问题.md "wikilink")（Byzantine failure，即虽然有可能一个消息被传递了两次，但是绝对不会出现错误的消息）；只要等待足够的时间，消息就会被传到。另外，Paxos岛上的议员是不会反对其他议员提出的决议的。

对应于分布式系统，议员对应于各个节点，制定的法律对应于系统的状态。各个节点需要进入一个一致的状态，例如在独立[Cache的](https://zh.wikipedia.org/wiki/Cache "wikilink")[对称多处理器系统中](https://zh.wikipedia.org/wiki/对称多处理器 "wikilink")，各个处理器读内存的某个字节时，必须读到同样的一个值，否则系统就违背了一致性的要求。一致性要求对应于法律条文只能有一个版本。议员和服务员的不确定性对应于节点和消息传递通道的不可靠性。

## 算法

### 算法的提出与证明

首先将议员的角色分为 proposers，acceptors，和 learners（允许身兼数职）。proposers 提出提案，提案信息包括提案编号和提议的 value；acceptor 收到提案后可以接受（accept）提案，若提案获得多数派（majority）的 acceptors 的接受，则称该提案被批准（chosen）；learners 只能「学习」被批准的提案。划分角色后，就可以更精确的定义问题：

1.  决议（value）只有在被 proposers 提出后才能被批准（未经批准的决议称为「提案（proposal）」）；
2.  在一次 Paxos 算法的执行实例中，只批准（chosen）一个 value；
3.  learners 只能获得被批准（chosen）的 value。

`在 Leslie Lamport 之后发表的paper中将 majority 替换为更通用的 quorum 概念，但在描述classic paxos的论文  `[`Paxos``   ``made``   ``simple`](https://lamport.azurewebsites.net/pubs/paxos-simple.pdf)` 中使用的还是majority的概念。`

另外还需要保证 progress。这一点以后再讨论。

作者通过不断加强上述3个约束（主要是第二个）获得了 Paxos 算法。

批准 value 的过程中，首先 proposers 将 value 发送给 acceptors，之后 acceptors 对 value 进行接受（accept）。为了满足只批准一个 value 的约束，要求经「多数派（majority）」接受的 value 成为正式的决议（称为「批准」决议）。这是因为无论是按照人数还是按照权重划分，两组「多数派」至少有一个公共的 acceptor，如果每个 acceptor 只能接受一个 value，约束2就能保证。

于是产生了一个显而易见的新约束：

`P1：一个 acceptor 必须接受（accept）第一次收到的提案。`

注意 P1 是不完备的。如果恰好一半 acceptor 接受的提案具有 value A，另一半接受的提案具有 value B，那么就无法形成多数派，无法批准任何一个 value。

约束2并不要求只批准一个提案，暗示可能存在多个提案。只要提案的 value 是一样的，批准多个提案不违背约束2。于是可以产生约束 P2：

`P2：一旦一个具有 value v 的提案被批准（chosen），那么之后批准（chosen）的提案必须具有 value v。`

注：通过某种方法可以为每个提案分配一个编号，在提案之间建立一个全序关系，所谓“之后”都是指所有编号更大的提案。

如果 P1 和 P2 都能够保证，那么约束2就能够保证。

批准一个 value 意味着多个 acceptor 接受（accept）了该 value。因此，可以对 P2 进行加强：

`P2a：一旦一个具有 value v 的提案被批准（chosen），那么之后任何 acceptor 再次接受（accept）的提案必须具有 value v。`

由于通信是异步的，P2a 和 P1 会发生冲突。如果一个 value 被批准后，一个 proposer 和一个 acceptor 从休眠中苏醒，前者提出一个具有新的 value 的提案。根据 P1，后者应当接受，根据 P2a，则不应当接受，这种场景下 P2a 和 P1 有矛盾。于是需要换个思路，转而对 proposer 的行为进行约束：

`P2b：一旦一个具有 value v 的提案被批准（chosen），那么以后任何 proposer 提出的提案必须具有 value v。`

由于 acceptor 能接受的提案都必须由 proposer 提出，所以 P2b 蕴涵了 P2a，是一个更强的约束。

但是根据 P2b 难以提出实现手段。因此需要进一步加强 P2b。

假设一个编号为 m 的 value v 已经获得批准（chosen），来看看在什么情况下对任何编号为 n（n\>m）的提案都含有 value v。因为 m 已经获得批准（chosen），显然存在一个 acceptors 的多数派 C，他们都接受（accept）了v。考虑到任何多数派都和 C 具有至少一个公共成员，可以找到一个蕴涵 P2b 的约束 P2c：

`P2c：如果一个编号为 n 的提案具有 value v，那么存在一个多数派，要么他们中所有人都没有接受（accept）编号小于 n `
`的任何提案，要么他们已经接受（accept）的所有编号小于 n 的提案中编号最大的那个提案具有 value v。`

可以用[数学归纳法](../Page/数学归纳法.md "wikilink")证明 P2c 蕴涵 P2b：

假设具有value v的提案m获得批准，当n=m+1时，采用反证法，假如提案n不具有value v，而是具有value w，根据P2c，则存在一个多数派S1，要么他们中没有人接受过编号小于n的任何提案，要么他们已经接受的所有编号小于n的提案中编号最大的那个提案是value w。由于S1和通过提案m时的多数派C之间至少有一个公共的acceptor，所以以上两个条件都不成立，导出矛盾从而推翻假设，证明了提案n必须具有value v；

若（m+1）..（N-1）所有提案都具有value v，采用反证法，假如新提案N不具有value v，而是具有value w',根据P2c，则存在一个多数派S2，要么他们没有接受过m..（N-1）中的任何提案，要么他们已经接受的所有编号小于N的提案中编号最大的那个提案是value w'。由于S2和通过m的多数派C之间至少有一个公共的acceptor，所以至少有一个acceptor曾经接受了m，从而也可以推出S2中已接受的所有编号小于n的提案中编号最大的那个提案的编号范围在m..（N-1）之间，而根据初始假设，m..（N-1）之间的所有提案都具有value v，所以S2中已接受的所有编号小于n的提案中编号最大的那个提案肯定具有value v，导出矛盾从而推翻新提案n不具有value v的假设。根据数学归纳法，我们证明了若满足P2c，则P2b一定满足。

P2c是可以通过消息传递模型实现的。另外，引入了P2c后，也解决了前文提到的P1不完备的问题。

### 算法的内容

要满足P2c的约束，proposer提出一个提案前，首先要和足以形成多数派的acceptors进行通信，获得他们进行的最近一次接受（accept）的提案（prepare过程），之后根据回收的信息决定这次提案的value，形成提案开始投票。当获得多数acceptors接受（accept）后，提案获得批准（chosen），由acceptor将这个消息告知learner。这个简略的过程经过进一步细化后就形成了Paxos算法。

在一个paxos实例中，每个提案需要有不同的编号，且编号间要存在全序关系。可以用多种方法实现这一点，例如将序数和proposer的名字拼接起来。如何做到这一点不在Paxos算法讨论的范围之内。

如果一个没有chosen过任何proposer提案的acceptor在prepare过程中回答了一个proposer针对提案n的问题，但是在开始对n进行投票前，又接受（accept）了编号小于n的另一个提案（例如n-1），如果n-1和n具有不同的value，这个投票就会违背P2c。因此在prepare过程中，acceptor进行的回答同时也应包含承诺：不会再接受（accept）编号小于n的提案。这是对P1的加强：

`P1a：当且仅当acceptor没有回应过编号大于n的prepare请求时，acceptor接受（accept）编号为n的提案。`

现在已经可以提出完整的算法了。

#### 决议的提出与批准

通过一个决议分为两个阶段：

1.  prepare阶段：
    1.  proposer选择一个提案编号n并将prepare请求发送给acceptors中的一个多数派；
    2.  acceptor收到prepare消息后，如果提案的编号大于它已经回复的所有prepare消息(回复消息表示接受accept)，则acceptor将自己上次接受的提案回复给proposer，并承诺不再回复小于n的提案；
2.  批准阶段：
    1.  当一个proposer收到了多数acceptors对prepare的回复后，就进入批准阶段。它要向回复prepare请求的acceptors发送accept请求，包括编号n和根据P2c决定的value（如果根据P2c没有已经接受的value，那么它可以自由决定value）。
    2.  在不违背自己向其他proposer的承诺的前提下，acceptor收到accept请求后即批准这个请求。

这个过程在任何时候中断都可以保证正确性。例如如果一个proposer发现已经有其他proposers提出了编号更高的提案，则有必要中断这个过程。因此为了优化，在上述prepare过程中，如果一个acceptor发现存在一个更高编号的提案，则需要通知proposer，提醒其中断这次提案。

#### 实例

用实际的例子来更清晰地描述上述过程：

有A1, A2, A3, A4, A5 5位议员，就税率问题进行决议。议员A1决定将税率,因此它向所有人发出一个草案。这个草案的内容是：

`现有的税率是什么?如果没有决定，我来决定一下. 提出时间：本届议会第3年3月15日;提案者：A1`

在最简单的情况下，没有人与其竞争;信息能及时顺利地传达到其它议员处。

于是, A2-A5回应：

`我已收到你的提案，等待最终批准`

而A1在收到2份回复后就发布最终决议：

`税率已定为10%,新的提案不得再讨论本问题。`

这实际上退化为[二阶段提交](../Page/二阶段提交.md "wikilink")协议。

现在我们假设在A1提出提案的同时, A5决定将税率定为20%:

`现有的税率是什么?如果没有决定，我来决定一下.时间：本届议会第3年3月16日;提案者：A5`

草案要通过侍从送到其它议员的案头. A1的草案将由4位侍从送到A2-A5那里。现在，负责A2和A3的侍从将草案顺利送达，负责A4和A5的侍从则不上班. A5的草案则顺利的送至A4和A3手中。

现在, A1, A2, A3收到了A1的提案; A4, A3, A5收到了A5的提案。按照协议, A1, A2, A4, A5将接受他们收到的提案，侍从将拿着

`我已收到你的提案，等待最终批准`

的回复回到提案者那里。

而A3的行为将决定批准哪一个。

在讨论之前我们要明确一点，提案是全局有序的。在这个示例中，是说每个提案提出的日期都不一样。即第3年3月15日只有A1的提案；第3年3月16日只有A5的提案。不可能在某一天存在两个提案。

##### 情况一

假设A1的提案先送到A3处，而A5的侍从决定放假一段时间。于是A3接受并派出了侍从. A1等到了两位侍从，加上它自己已经构成一个多数派，于是税率10%将成为决议. A1派出侍从将决议送到所有议员处：

`税率已定为10%,新的提案不得再讨论本问题。`

A3在很久以后收到了来自A5的提案。由于税率问题已经讨论完毕，开始讨论某些议员在第3年3月17日提出的议案。因此这个3月16日提出的议案他不去理会。他自言自语地抱怨一句：

`这都是老问题了，没有必要讨论了。`

##### 情况二

依然假设A1的提案先送到A3处，但是这次A5的侍从不是放假了，只是中途耽搁了一会。这次, A3依然会将"接受"回复给A1.但是在决议成型之前它又收到了A5的提案。则：

1.如果A5提案的提出时间比A1的提案更晚一些，这里确实满足这种情况，因为3月16日晚于3月15日。，则A3回复：

`我已收到您的提案，等待最终批准，但是您之前有人提出将税率定为10%,请明察。`

于是, A1和A5都收到了足够的回复。这时关于税率问题就有两个提案在同时进行。但是A5知道之前有人提出税率为10%.于是A1和A5都会向全体议员广播：

` 税率已定为10%,新的提案不得再讨论本问题。`

共识到了保证。

2\. 如果A5提案的提出时间比A1的提案更早一些。假设A5的提案是3月14日提出，则A3直接不理会。

` A1不久后就会广播税率定为10%.`

#### 决议的发布

一个显而易见的方法是当acceptors批准一个value时，将这个消息发送给所有learners。但是这个方法会导致消息量过大。

由于假设没有Byzantine failures，learners可以通过别的learners获取已经通过的决议。因此acceptors只需将批准的消息发送给指定的某一个learner，其他learners向它询问已经通过的决议。这个方法降低了消息量，但是指定learner失效将引起系统失效。

因此acceptors需要将accept消息发送给learners的一个子集，然后由这些learners去通知所有learners。

但是由于消息传递的不确定性，可能会没有任何learner获得了决议批准的消息。当learners需要了解决议通过情况时，可以让一个proposer重新进行一次提案。注意一个learner可能兼任proposer。

#### Progress的保证

根据上述过程当一个proposer发现存在编号更大的提案时将终止提案。这意味着提出一个编号更大的提案会终止之前的提案过程。如果两个proposer在这种情况下都转而提出一个编号更大的提案，就可能陷入活锁，违背了Progress的要求。一般活锁可以通过 **随机睡眠-重试** 的方法解决。这种情况下的解决方案是选举出一个leader，仅允许leader提出提案。但是由于消息传递的不确定性，可能有多个proposer自认为自己已经成为leader。Lamport在[The Part-Time Parliament](http://research.microsoft.com/users/lamport/pubs/lamport-paxos.pdf)一文中描述并解决了这个问题。

## Multi-Paxos

Paxos的典型部署需要一组连续的被接受的值（value），作为应用到一个分布式状态机的一组命令。如果每个命令都通过一个Basic Paxos算法实例来达到一致，会产生大量开销。

如果Leader是相对稳定不变的，第1阶段就变得不必要。 这样，系统可以在接下来的Paxos算法实例中，跳过的第1阶段，直接使用同样的Leader。

为了实现这一目的，在同一个Leader执行每轮Paxos算法时，提案编号 I 每次递增一个值，并与每个值一起发送。Multi-Paxos在没有故障发生时，将消息延迟(从propose阶段到learn阶段)从4次延迟降低为2次延迟。

### Multi-Paxos中消息流的图形表示

#### Multi-Paxos 没有失败的情况

在下面的图中，只显示了基本Paxos协议的一个实例(或“执行”)和一个初始Leader(Proposer)。注意，Multi-Paxos使用几个Basic Paxos的实例。

    Client   Proposer      Acceptor     Learner
       |         |          |  |  |       |  | --- First Request ---
       X-------->|          |  |  |       |  |  Request
       |         X--------->|->|->|       |  |  Prepare(N)
       |         |<---------X--X--X       |  |  Promise(N,I,{Va,Vb,Vc})
       |         X--------->|->|->|       |  |  Accept!(N,I,V)
       |         |<---------X--X--X------>|->|  Accepted(N,I,V)
       |<---------------------------------X--X  Response
       |         |          |  |  |       |  |

式中V = (Va, Vb, Vc) 中最新的一个。

#### 跳过阶段1时的Multi-Paxos

在这种情况下，Basic Paxos的后续实例(由I+1表示)使用相同的Leader，因此，包含在Prepare和Promise的阶段1(Basic Paxos协议的这些后续实例)将被跳过。注意，这里要求Leader应该是稳定的，即它不应该崩溃或改变。

    Client   Proposer       Acceptor     Learner
       |         |          |  |  |       |  |  --- Following Requests ---
       X-------->|          |  |  |       |  |  Request
       |         X--------->|->|->|       |  |  Accept!(N,I+1,W)
       |         |<---------X--X--X------>|->|  Accepted(N,I+1,W)
       |<---------------------------------X--X  Response
       |         |          |  |  |       |  |

## Fast-Paxos

Fast-Paxos将Basic-Paxos进行了推广，以减少端到端消息延迟。在Basic-Paxos中，从客户端发起请求开始，到Learn阶段结束的消息延迟是3个消息延迟。而Fast-Paxos允许2个消息延迟，但要求：

(1)系统由*3f+ 1*个Acceptor组成，以容忍最多*f*个错误(而不是Basic-Paxos的*2f+1*)；

(2)客户端需要直接将请求发送到多个目标。

直观上，如果Leader没有提议任何value，那么客户可以直接发送*Accept*消息到向接收方发。Acceptor会像Basic-Paxos一样运行，向Leader和每个Learner发送*Accepted*的消息，从而实现从客户端到Learner的两消息延迟。

如果Leader检测到冲突，它通过发起新一轮投票，并发送*Accept*消息来解决冲突，通常是一个*Accepted*消息。这种有协调者参与的冲突恢复机制需要4个从客户端到Learner的消息延迟。

如果Leader提前指定了一种冲突恢复机制，就可以实现另一种优化，它允许Acceptors自己执行冲突恢复。因此，无协调的冲突恢复可能实现三个消息延迟(如果所有的Learner都是接收者，那么只有两个消息延迟)。

### 消息流: Fast-Paxos，无冲突

    Client    Leader         Acceptor      Learner
       |         |          |  |  |  |       |  |
       |         X--------->|->|->|->|       |  |  Any(N,I,Recovery)
       |         |          |  |  |  |       |  |
       X------------------->|->|->|->|       |  |  Accept!(N,I,W)
       |         |<---------X--X--X--X------>|->|  Accepted(N,I,W)
       |<------------------------------------X--X  Response(W)
       |         |          |  |  |  |       |  |

### 消息流:Fast-Paxos，冲突的建议

有协调这参与的冲突恢复。注意:协议没有指定如何处理被丢弃的客户端请求。

    Client   Leader      Acceptor     Learner
     |  |      |        |  |  |  |      |  |
     |  |      |        |  |  |  |      |  |
     |  |      |        |  |  |  |      |  |  !! Concurrent conflicting proposals
     |  |      |        |  |  |  |      |  |  !!   received in different order
     |  |      |        |  |  |  |      |  |  !!   by the Acceptors
     |  X--------------?|-?|-?|-?|      |  |  Accept!(N,I,V)
     X-----------------?|-?|-?|-?|      |  |  Accept!(N,I,W)
     |  |      |        |  |  |  |      |  |
     |  |      |        |  |  |  |      |  |  !! Acceptors disagree on value
     |  |      |<-------X--X->|->|----->|->|  Accepted(N,I,V)
     |  |      |<-------|<-|<-X--X----->|->|  Accepted(N,I,W)
     |  |      |        |  |  |  |      |  |
     |  |      |        |  |  |  |      |  |  !! Detect collision & recover
     |  |      X------->|->|->|->|      |  |  Accept!(N+1,I,W)
     |  |      |<-------X--X--X--X----->|->|  Accepted(N+1,I,W)
     |<---------------------------------X--X  Response(W)
     |  |      |        |  |  |  |      |  |

无协调者参与的相冲突恢复：

    Client   Leader      Acceptor     Learner
     |  |      |        |  |  |  |      |  |
     |  |      X------->|->|->|->|      |  |  Any(N,I,Recovery)
     |  |      |        |  |  |  |      |  |
     |  |      |        |  |  |  |      |  |  !! Concurrent conflicting proposals
     |  |      |        |  |  |  |      |  |  !!   received in different order
     |  |      |        |  |  |  |      |  |  !!   by the Acceptors
     |  X--------------?|-?|-?|-?|      |  |  Accept!(N,I,V)
     X-----------------?|-?|-?|-?|      |  |  Accept!(N,I,W)
     |  |      |        |  |  |  |      |  |
     |  |      |        |  |  |  |      |  |  !! Acceptors disagree on value
     |  |      |<-------X--X->|->|----->|->|  Accepted(N,I,V)
     |  |      |<-------|<-|<-X--X----->|->|  Accepted(N,I,W)
     |  |      |        |  |  |  |      |  |
     |  |      |        |  |  |  |      |  |  !! Detect collision & recover
     |  |      |<-------X--X--X--X----->|->|  Accepted(N+1,I,W)
     |<---------------------------------X--X  Response(W)
     |  |      |        |  |  |  |      |  |

### 消息流:无协调者的冲突恢复、角色崩溃的Fast-Paxos

(合并的Acceptor/Learner)

    Client         Servers
     |  |         |  |  |  |
     |  |         X->|->|->|  Any(N,I,Recovery)
     |  |         |  |  |  |
     |  |         |  |  |  |  !! Concurrent conflicting proposals
     |  |         |  |  |  |  !!   received in different order
     |  |         |  |  |  |  !!   by the Servers
     |  X--------?|-?|-?|-?|  Accept!(N,I,V)
     X-----------?|-?|-?|-?|  Accept!(N,I,W)
     |  |         |  |  |  |
     |  |         |  |  |  |  !! Servers disagree on value
     |  |         X<>X->|->|  Accepted(N,I,V)
     |  |         |<-|<-X<>X  Accepted(N,I,W)
     |  |         |  |  |  |
     |  |         |  |  |  |  !! Detect collision & recover
     |  |         X<>X<>X<>X  Accepted(N+1,I,W)
     |<-----------X--X--X--X  Response(W)
     |  |         |  |  |  |

## 应用 

[微软公司为简化的Paxos算法申请了](https://zh.wikipedia.org/wiki/微软公司 "wikilink")[专利](../Page/专利.md "wikilink")\[3\]。但专利中公开的技术和本文所描述的不尽相同。

[谷歌公司](https://zh.wikipedia.org/wiki/谷歌公司 "wikilink")（Google公司）在其中应用了Multi-Paxos算法\[4\]。Chubby lock应用于[大表](https://zh.wikipedia.org/wiki/大表 "wikilink")（Bigtable），后者在[谷歌公司所提供的各项服务中得到了广泛的应用](https://zh.wikipedia.org/wiki/谷歌公司 "wikilink")\[5\]。

[谷歌公司](https://zh.wikipedia.org/wiki/谷歌公司 "wikilink")（Google公司）在其分布式数据库spanner中使用Multi-Paxos作为分布式共识保证的基础组件 \[6\]

[Apache ZooKeeper](../Page/Apache_ZooKeeper.md "wikilink") 使用一个类Multi-Paxos的共识算法作为底层存储协同的机制。

## 参考文献

<references />

## 外部链接

  - [The Part-Time Parliament](http://research.microsoft.com/users/lamport/pubs/lamport-paxos.pdf) ── Lamport于1998年发表在ACM Transactions on Computer Systems。

<!-- end list -->

  -
    註：这是该算法第一次公开发表。

<!-- end list -->

  - [Paxos Made Simple](http://research.microsoft.com/users/lamport/pubs/paxos-simple.pdf)，2001年。

<!-- end list -->

  -
    註：Lamport觉得同行无法接受他的幽默感，于是用容易接受的方法重新表述了一遍。

<!-- end list -->

  - [Pinewiki对Paxos算法的介绍](https://web.archive.org/web/20070811172059/http://pine.cs.yale.edu/pinewiki/Paxos)

[Category:分布式计算](https://zh.wikipedia.org/wiki/Category:分布式计算 "wikilink") [Category:算法](https://zh.wikipedia.org/wiki/Category:算法 "wikilink")

1.  Lamport本人在http://research.microsoft.com/users/lamport/pubs/pubs.html\#lamport-paxos 中描写了他用9年时间发表这个算法的前前后后
2.  [Lamport L. Paxos made simple\[J\]. ACM Sigact News, 2001, 32(4): 18-25.](http://www.cs.utexas.edu/users/lorenzo/corsi/cs380d/past/03F/notes/paxos-simple.pdf)
3.  [中国专利局的相关页面](http://search.sipo.gov.cn/sipo/zljs/hyjs-yx-new.jsp?recid=CN200410082196.X&leixin=fmzl&title=%BC%F2%BB%AF%B5%C4Paxos%CB%E3%B7%A8&ipc=G06F9/46)
4.  [The Chubby lock service for loosely-coupled distributed systems](http://labs.google.com/papers/chubby-osdi06.pdf)
5.  [Bigtable: A Distributed Storage System for Structured Data](http://labs.google.com/papers/bigtable-osdi06.pdf)
6.  [Spanner: Google's Globally-Distributed Database](https://ai.google/research/pubs/pub39966)