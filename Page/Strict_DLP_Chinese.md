**Strict DLP Chinese**（英文缩写：或)，是一个基于[eMule Xtreme Mod的](https://zh.wikipedia.org/wiki/eMule_Xtreme_Mod "wikilink")[官方DLP库的严格的版本](https://zh.wikipedia.org/wiki/动态反吸血驴保护#官方DLP库 "wikilink")，可用于Xtreme等[eMule Mod的](https://zh.wikipedia.org/wiki/eMule_Mod "wikilink")[动态反吸血驴保护](../Page/动态反吸血驴保护.md "wikilink")（DLP）功能。SDC在官方DLP库基础上，将[VeryCD公司开发的](https://zh.wikipedia.org/wiki/上海维西公司 "wikilink")[VeryCD Mod和](https://zh.wikipedia.org/wiki/eMule_VeryCD_Mod "wikilink")[easyMule加入了SoftBan](https://zh.wikipedia.org/wiki/easyMule "wikilink")（软性吸血客户端）列表\[1\]，原因是违反GNU [GPL开源协议](https://zh.wikipedia.org/wiki/GPL "wikilink")、私有化[eDonkey网络和](https://zh.wikipedia.org/wiki/eDonkey网络 "wikilink")[滥用社区加分等](https://zh.wikipedia.org/wiki/吸血驴#定义 "wikilink")。

SDC制作的目标是“以更加严格的检测手段来维护eDonkey网络的纯净与高效”\[2\]，它根据用户在反吸血力度上的不同要求，推出了各种版本。

## 历史

自2003年以来，[VeryCD公司相继推出了其在官方](https://zh.wikipedia.org/wiki/VeryCD公司 "wikilink")[eMule基础上修改或类似eMule的](https://zh.wikipedia.org/wiki/eMule "wikilink")[VeryCD Mod](https://zh.wikipedia.org/wiki/eMule_VeryCD_Mod "wikilink")、[easyMule](https://zh.wikipedia.org/wiki/easyMule "wikilink") 1.0、easyMule 2.0、[miniMule](https://zh.wikipedia.org/wiki/miniMule "wikilink")。其中没有开放[源代码](../Page/源代码.md "wikilink")的[easyMule](https://zh.wikipedia.org/wiki/easyMule "wikilink") 2.0涉嫌抄袭[aMule违反GNU](https://zh.wikipedia.org/wiki/aMule "wikilink") [GPL开源协议](https://zh.wikipedia.org/wiki/GPL "wikilink")\[3\]，协议存在问题而软件也缺乏维护 \[4\]；miniMule则删除了eMule的主动文件共享功能和eD2k/Kad搜索功能\[5\]彻底成为吸血客户端；而[VeryCD Mod和](https://zh.wikipedia.org/wiki/eMule_VeryCD_Mod "wikilink")[easyMule则没有开放其自带](https://zh.wikipedia.org/wiki/easyMule "wikilink")[DLP库的源代码且多次误封其它](https://zh.wikipedia.org/wiki/动态反吸血驴保护#DLP库 "wikilink")[eMule Mod](https://zh.wikipedia.org/wiki/eMule_Mod "wikilink")。同时，一些用户也对[强制默认昵称列表](https://zh.wikipedia.org/wiki/easyMule#问题 "wikilink")、VeryCD客户端的社区加分、其公司的混淆性宣传等行为不满\[6\]。于是有用户在[SourceForge](../Page/SourceForge.md "wikilink")上建立了**Strict DLP Chinese（SDC）**开源项目\[7\]，并成立了SDC Team\[8\]负责更新与管理。

  - 2010年6月30日，Xtreme官方DLP库升级到42版本时将miniMule加入到硬性吸血骡（HardBan）列表中彻底屏蔽\[9\]，而SDC则已经在发布39005\[10\]时加入此侦测。

<!-- end list -->

  - 2010年12月20日，Xtreme官方DLP库升级到43版本时将easyMule 2.0加入到硬性吸血骡（HardBan）列表中彻底屏蔽\[11\]，而SDC则已经在发布39004\[12\]时加入此侦测。

## 支持状况

目前支持[官方DLP库的](https://zh.wikipedia.org/wiki/动态反吸血驴保护#官方DLP库 "wikilink")[eMule Mod](https://zh.wikipedia.org/wiki/eMule_Mod "wikilink")，如[Xtreme](https://zh.wikipedia.org/wiki/eMule_Xtreme_Mod "wikilink")、[MagicAngel](https://zh.wikipedia.org/wiki/eMule_MagicAngel_Mod "wikilink")、[ScarAngel](https://zh.wikipedia.org/wiki/eMule_ScarAngel_Mod "wikilink")、[Mephisto](https://zh.wikipedia.org/wiki/eMule_Mephisto_Mod "wikilink")、[X-Ray](https://zh.wikipedia.org/wiki/eMule_X-Ray_Mod "wikilink")、[StulleMule](https://zh.wikipedia.org/wiki/eMule_StulleMule_Mod "wikilink")、[NeoMule](https://zh.wikipedia.org/wiki/eMule_NeoMule_Mod "wikilink")、[CN](https://zh.wikipedia.org/wiki/eMule_CN_Mod "wikilink")、[Dreamule等](https://zh.wikipedia.org/wiki/eMule_Dreamule_Mod "wikilink")，一般都支持SDC。

但也有部分用户反映SDC可能存在[BUG而导致部分对DLP库支持不佳的eMule](https://zh.wikipedia.org/wiki/BUG "wikilink") Mod出现崩溃，此类eMule Mod加载SDC后也可能会触发其它未知的误伤和漏检\[13\]。同时SDC的Develop版本和Beta版本也曾经出现误伤正规eMule Mod的情况，不过均已经在最新的Beta版本中得以解决\[14\]。

## 使用

用户可以手动下载最新的SDC库文件**antiLeech.dll.new**用以更新\[15\]。

## 版本

  - SDC原来分Base和Develop版本，现已合并成为一个正式版本\[16\]，并会在有需要的时候发布Beta版本供紧急修复漏检以及新的吸血骡检测方式的测试使用\[17\]。

<!-- end list -->

  - 根据使用环境可分为[x86](https://zh.wikipedia.org/wiki/x86 "wikilink")（用于[32位操作系统的版本](https://zh.wikipedia.org/wiki/32位操作系统 "wikilink")）和[x64](https://zh.wikipedia.org/wiki/x64 "wikilink")（用于[64位操作系统的版本](https://zh.wikipedia.org/wiki/64位操作系统 "wikilink")）。

<!-- end list -->

  - 根据用途可分为\[18\]\[19\]：
      - 侦测所有VeryCD客户端的All-VeryCD版；
      - 侦测VeryCD强制默认昵称的VeryCD-NickName版；
      - 侦测所有easyMule的easyMule版；
      - 修正官方DLP库问题并修补官方DLP库漏检的Lite版\[20\]。
      - 基于All-VeryCD版制作并可侦测所有带有VeryCD Tag的客户端的All-VeryCD-Mod\&VeryCD-Tag版

## 软性硬性吸血列表

SDC将不同[吸血骡客户端分为软性和硬性](https://zh.wikipedia.org/wiki/吸血骡 "wikilink")，软性吸血骡对应减分模式（排队积分按比例减少），硬性吸血骡对应屏蔽模式，对方将被踢出排队列表。

## 参见

  - [动态反吸血驴保护](../Page/动态反吸血驴保护.md "wikilink")
  - [吸血驴](../Page/吸血驴.md "wikilink")

## 参考资料与注释

## 外部链接

  - [Strict DLP Chinese 的 GitHub 项目页](https://github.com/chengr28/specialdlp)

  - [Strict DLP Chinese 的 SourceForge 项目页](https://sourceforge.net/projects/specialdlp)

  -
  - [电骡爱好者](https://emulefans.com)

[Category:应用程序接口](https://zh.wikipedia.org/wiki/Category:应用程序接口 "wikilink") [Category:自由软件](https://zh.wikipedia.org/wiki/Category:自由软件 "wikilink") [Category:EMule](https://zh.wikipedia.org/wiki/Category:EMule "wikilink")

1.
2.
3.  [aMule的开发者和一些用户指出easyMule](https://zh.wikipedia.org/wiki/aMule "wikilink")2使用了[GPL软件aMule的代码却未开源](https://zh.wikipedia.org/wiki/GPL "wikilink")，VeryCD公司方面则否认其使用aMule代码。另也有用户称easyMule2对eMule代码也有使用。见：。官方[eMule的维护者Some](https://zh.wikipedia.org/wiki/eMule "wikilink") Support和[Xtreme](https://zh.wikipedia.org/wiki/eMule_Xtreme_Mod "wikilink")、[ScarAngel等Mods的维护者Stulle也均对easyMule](https://zh.wikipedia.org/wiki/eMule_ScarAngel_Mod "wikilink")2的“完全自主开发”表示质疑。见：
4.  参见Xtreme官方DLP库源代码中antiLeech.cpp的第491行
5.
6.
7.
8.
9.
10.
11.
12.
13.
14.
15.
16.
17.
18.
19. 参见SDC的ReadMe
20.