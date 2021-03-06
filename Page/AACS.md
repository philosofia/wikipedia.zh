> 本文内容由[AACS](https://zh.wikipedia.org/wiki/AACS)转换而来。


**高级内容访问系统**（）是内容分发、[数字版权管理](../Page/数字版权管理.md "wikilink")标准，用来限制访问和复制光盘DVD内容。该规范于2005年4月公开发布，该标准已被用作[HD DVD和](../Page/HD_DVD.md "wikilink")[Blu ray Disc](../Page/藍光光碟.md "wikilink")（BD）的访问限制方案。它是由AACS授权管理开发有限责任公司（AACS LA）开发。这个公司包括迪士尼、英特尔、微软、松下、华纳兄弟公司、IBM、东芝和索尼等公司。AACS一直是一个“临时协议”，因为最终的规范（包括拷贝管理规定）尚未最后确定。自从2006年后，几个AACS解密密钥已被从软件播放器中提取并公布在网上，导致破解者可以使用未授权的软件解密内容。

## 简介

AACS使用[密码学](../Page/密码学.md "wikilink")方法限制数字媒体的使用。它使用[高级加密标准](../Page/高级加密标准.md "wikilink")（AES）在一个或多个主密钥下加密内容。使用媒体密钥和媒体的卷id（例如，嵌入在预先记录的磁盘上的物理序列号）组合来解密主密钥。

### AACS的优势

AACS和[CSS这两款用于DVD和CD的](https://zh.wikipedia.org/wiki/CSS_\(消歧義\) "wikilink")[DRM](../Page/数字版权管理.md "wikilink")（数字版权管理）系统之间的主要区别，在于设备如何解密密钥和组织秘钥。在CSS中，一个给定的型号的所有播放器被提供相同的主密钥。内容在头指定的密钥下进行加密，该密钥本身在每个型号的密钥下加密。因此，每个光盘包含几百个加密密钥的集合，每个獲得许可的播放器型号都有一个自己的秘钥。 原则上，这种方法可以让版权方具有“撤销”一个特定的播放器型号的播放能力的权力——停止使用该播放器的主密钥加密内容头秘钥。然而在实践中，取消所有的特定播放器型号的播放的代價是昂贵的，因为它使许多用户失去播放能力。此外，在许多播放器中加入共享密钥使得关键泄密更可能发生，正如90年代中期的一些泄密所证明的那样。AACS使每个播放器具有单独的秘钥。这种方法允许版权方“撤销”任何单独的播放器的播放权，或者更具体地说，与播放器相关的解密密钥。因此，如果一个播放器的密钥被攻破，AACS LA可以撤销在未来的内容中的那些秘钥，使该秘钥、播放器无法解密新内容中的头秘钥。AACS还集成了叛徒追踪技术。该标准允许一个电影的短片段的多个版本用不同的密钥分别进行加密，而一个给定的播放器只能解密每个部分的一个版本。制造商将在每一部分中加入不同的数字水印，从而盗版版本泄露的密钥可以被识别从而被撤销和追踪。（此功能称为AACS规格序列键）。\[1\]\[2\]

### 卷ID

卷ID是在特定硬件上预先存储的磁盘上存储的唯一标识符或序列号。它们不能被消费者复制到可记录的媒体上。这样做的目的是防止简单的逐位拷贝，因为卷ID被用于解码内容，而复制过程不能复制此ID。蓝光光盘上的卷ID存储在BD-ROM标记中。

要读取卷ID、被AACS LA所签署的秘钥（私人主机密钥）是必需的。然而，这已被修改固件的HD DVD光驱和Blu ray光驱所破解。

### 解密过程

要查看电影，播放器必须首先解密光盘上的内容。解密过程有点复杂。光盘包含4项信息：媒体密钥块（MKB），卷ID、加密头密钥和被加密加密的内容。MKB使用了有差异的加密子集树方法。本质上，一组密钥被树状安排，这样任何给定的密钥都可以用来查找除其父密钥之外的所有其他密钥。这种方式下MKB只需要与设备关联的母密钥加密即可。

一旦MKB被解密，它提供了媒体秘钥。媒体秘钥是结合卷ID（只能通过由证书认证的驱动器所读取，如上面所描述的）在一个单向加密方案（aes-g）生产的唯一键（kvu）。kvu用来解密加密的头秘钥，这是用来解密加密的内容的。

## 模拟落日条款

为防止模拟输出设备被用来录取影音，AACS规定在2010年12月31日以后生产销售的BD播放机，播放受AACS保护的BD影片时，将不允许通过模拟图像输出端子（如色差端子、D端子等）输出高分辨率（1080i/720p/1080p）图像，只能输出标准分辨率（480i）图像。

2013年12月31日以后生产销售的BD播放机，将全面禁止模拟图像输出。

## 专利纠纷

2007年5月30日，加拿大Certicom加密服务供应商状告索尼称其旗下的AACS侵犯了他的两项专利：“加强公钥协议”和“智能卡上的数字签名”。这些专利分别在1999年和2001年申请，且[美国国家安全局](../Page/美国国家安全局.md "wikilink")在2003年支付25万美元来使用certicom的26项专利，其中包括其认为索尼侵犯的两项。

## 参考文献

[Category:电脑安全](https://zh.wikipedia.org/wiki/Category:电脑安全 "wikilink") [Category:數位版權管理](https://zh.wikipedia.org/wiki/Category:數位版權管理 "wikilink")

1.
2.