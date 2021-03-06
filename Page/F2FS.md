> 本文内容由[F2FS](https://zh.wikipedia.org/wiki/F2FS)转换而来。


**F2FS**（）是一種[快閃記憶體檔案系統](../Page/快閃記憶體檔案系統.md "wikilink")，主要由[金載極](https://zh.wikipedia.org/wiki/金載極 "wikilink")（）在[三星集团研發](https://zh.wikipedia.org/wiki/三星集团 "wikilink")，适合[Linux内核](../Page/Linux内核.md "wikilink")使用\[1\]。

此檔案系統起初是為了[NAND闪存的存储设备設計](../Page/闪存.md "wikilink")（诸如[固态硬盘](../Page/固态硬盘.md "wikilink")、[eMMC和](../Page/多媒體記憶卡.md "wikilink")[SD卡](../Page/SD卡.md "wikilink")），这些设备广泛存在于自[移动设备](../Page/移动设备.md "wikilink")至[服务器](../Page/服务器.md "wikilink")领域。

三星應用了日誌結構檔案系統的概念，使它更適合用於儲存設備。

## 特性

  - 多头日志（Multi-head logging）

  - 对目录项的多层哈希表

  - 静态/动态冷热数据分离

  - 自适应记录方案

  - 可配置操作单元

  - 双检查点

  - 回滚和前滚恢复

  - Heap-style块分配

  - [TRIM/FITRIM支持](../Page/Trim命令.md "wikilink")\[2\]

  - 联机的文件系统/文件\[3\]

  - 内联xattrs\[4\]/数据\[5\]/目录\[6\]

  - 脱机（检查和修复不一致）\[7\])

  - [线性一致性](../Page/线性一致性.md "wikilink")\[8\]

  - \[9\]

  - 脱机调整大小\[10\]

  - 内部定期数据刷新\[11\]

  - 范围缓存\[12\]

## 设计

### 磁盘上布局

F2FS将整个卷分成多个段（segment），每个段固定为2 MB。一个节（section）由连续的段组成，一个区（zone）由一组节组成。默认情况下，节与区被设置为相同的大小，但用户可以用`mkfs`轻松修改大小。

F2FS将整个卷划分为六个区域，除了超级块（superblock）以外的所有区都由多个段组成，如下所述。

  - 超级块（Superblock，SB）
    超级块位于分区起始处，共有两个副本以避免文件系统损坏。它包含基本的分区信息和一些默认的F2FS参数。
  - 检查点（Checkpoint，CP）
    检查点包含文件系统信息，有效NAT/SIT集的位图，孤立inode列表，以及当前活动段的摘要条目。
  - 段信息表（SIT）
    段信息表包含主区域块的有效块数量和有效位图。
  - 节点地址表（NAT）
    节点信息表主区域节点块的地址表。
  - 段摘要区（SSA）
    段摘要区包含的条目包含主区域数据和节点块的所有者信息。
  - 主区域（Main Area）
    主区域包含文件和目录数据及其索引（indices）。

为了避免文件系统与闪存之间的对齐错误，F2FS将CP的起始块地址与段大小对齐。它还通过在SSA区域中预留一些段来将“主区”起始块地址与区的大小对齐。

### 元数据结构

F2FS使用检查点方案来维护文件系统的完整性。在挂载时，F2FS首先尝试扫描CP区域来查找最后的有效检查点数据。为了缩短扫描时间，F2FS只使用CP的两个副本。其中一个总是指示最后的有效数据，这被称为影子副本机制。除了CP之外，NAT和SIT也使用影子副本机制。为了保证文件系统的一致性，每个CP指向的NAT和SIT副本都是有效的。

### 索引结构

关键的数据结构是“节点”。与传统的文件结构类似，F2FS有三种类型的节点：inode，直接节点，间接节点。F2FS将4 KB分配给一个inode块，其中包含923个数据块索引（data block indices），两个直接节点指针，两个间接节点指针，以及一个double间接节点指针，如下所述。一个直接节点块包含1018个数据块索引，而间接节点块包含1018个节点块索引。因此，一个inode块（即一个文件）涵盖：

`4 KB × (923 + 2×1018 + 2×1018`<sup>`2`</sup>` + 1018`<sup>`3`</sup>`) = 3.94 TB`

注意，所有节点块都经NAT映射，因此每个节点的位置都经NAT转换。为了缓解漫游树问题，F2FS能够切断叶数据写入引起的节点更新传播。

### 目录结构

一个目录条目（dentry）占用11个字节，由以下属性组成。

| hash | 文件名的散列值                                |
| :--- | :------------------------------------- |
| ino  | [Inode](../Page/Inode.md "wikilink")号码 |
| len  | 文件名长度                                  |
| type | 文件类型，如目录、符号链接等。                        |

目录条目结构

一个目录条目块由及文件名组成。有一个位图用于记录每个目录条目是否有效。一个目录条目块占用4 KB，结构如下：

`目录条目块 (4 K) = 位图 (27 字节) + 保留 (3 字节) +`
`                      目录项 (11 * 214 字节) + 文件名 (8 * 214 字节)`

F2FS为目录结构实现了多级散列表，每一级有一个包含专用散列桶数的散列表，如下所示。“A(2B)”表示桶包含2个数据块。

  - 项
    A表示桶（bucket）
    B表示块（block）
    N表示目录散列最大深度（MAX_DIR_HASH_DEPTH）

<!-- end list -->

    level #0    A(2B)
    level #1    A(2B) - A(2B)
    level #2    A(2B) - A(2B) - A(2B) - A(2B)
        ...
    level #N/2  A(2B) - A(2B) - A(2B) - A(2B) - A(2B) - ... - A(2B)
        ...
    level #N    A(4B) - A(4B) - A(4B) - A(4B) - A(4B) - ... - A(4B)

当F2FS在一个目录中找一个文件名时，首先计算出该文件名的散列值，然后F2FS扫描级别\#0的散列表一查找由文件名及其inode编号组成的目录条目。如果未找到，F2FS继续查找级别\#1的散列表。F2FS通过此方法逐级扫描由1至N的每层散列表。在每一层中，F2FS只需扫描由以下等式确定的一个桶（bucket），因此展现出 O(log(\# of files)) 的复杂度。

` 级别#n中要扫描的桶（bucket）数 = (散列值) % (级别#n中的桶数)`

在创建文件时，F2FS找到一个能涵盖文件名的空的连续槽。F2FS以同样的方式由1至N查找各级散列表中的空槽。

### 默认的块分配

在运行时，F2FS在“主要区域：”内管理六个活动日志：热/暖/冷节点和热/暖/冷数据。

| 热节点 | 包含直接的目录节点块。      |
| :-- | :--------------- |
| 暖节点 | 包含除热节点块以外的直接节点块。 |
| 冷节点 | 包含间接节点块。         |
| 热数据 | 包含目录条目块。         |
| 暖数据 | 包含除冷热数据块以外的数据块。  |
| 冷数据 | 包含多媒体数据或迁移的数据块。  |

块分配策略

基于日志的文件系统（LFS）有两种空闲空间管理方案：穿插记录（threaded log）与复制并压缩（copy-and-compaction）。后者也称为清理（cleaning），很适合有良好顺序写入性能的设备，因为空闲空间总用于写入新数据。但它会在发生高利用率时遭遇“清理”的开销。穿插记录则受到随机写入性能的影响，但没有“清理”过程。F2FS采用混合方案，默认采用“复制并压缩”，但根据文件系统的状态将策略动态变更为“穿插记录”方案。

为使F2FS与基于闪存的存储保持一致，F2FS以一个节（section）为单位分配一个段（segment）。F2FS预期节的大小与FTL中的垃圾收集单元大小相同。为考虑FTL中的映射粒度，F2FS将活动日志的每个节分配给尽可能多的不同区域。 FTL可以根据其映射粒度将活动日志数据写入一个分配单元。

### 清理流程

F2FS在需要时和后台闲置时进行清理。按需清理在没有足够的空闲分段（segments）服务VFS调用时触发。后台清理器由一个内核线程执行，在系统空闲时触发清理作业。

F2FS支持两种受者选择策略：贪婪、成本效益算法。在贪婪算法中，F2FS选择有最小有效块数的受者段。在成本效益算法中，F2FS根据段的年龄和有效块数量选择受者段，以解决贪婪算法中存在的日志块抖动问题。F2FS使用贪婪算法进行按需清理，后台清理器则使用成本效益算法。

为识别受者段中的数据是否有效，F2FS管理了一个位图，其中用一个[位元](../Page/位元.md "wikilink")表示一个块的有效性，覆盖主区域所有块的位元流组成了该位图。

## 相關條目

  - [文件系统的对比](../Page/文件系统的对比.md "wikilink")
  - [文件系统列表](../Page/文件系统列表.md "wikilink")

## 參考資料

## 外部链接

  - [F2FS文档于kernel.org](https://www.kernel.org/doc/Documentation/filesystems/f2fs.txt)

[Category:快閃記憶體檔案系統](https://zh.wikipedia.org/wiki/Category:快閃記憶體檔案系統 "wikilink") [Category:嵌入式Linux](https://zh.wikipedia.org/wiki/Category:嵌入式Linux "wikilink") [Category:Linux檔案系統](https://zh.wikipedia.org/wiki/Category:Linux檔案系統 "wikilink")

1.  [f2fs: introduce flash-friendly file system](https://lwn.net/Articles/518718/) by Kim Jaegeuk
2.
3.
4.
5.
6.
7.
8.
9.
10.
11.
12.