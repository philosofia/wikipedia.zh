> 本文内容由[LWA](https://zh.wikipedia.org/wiki/LWA)转换而来。


**LTE-WLAN aggregation** (**LWA**) 為[3GPP](../Page/3GPP.md "wikilink")所制定的新規格. 在LWA運作下, 當一台有[LTE](../Page/長期演進技術.md "wikilink") 與 [Wi-Fi](../Page/Wi-Fi.md "wikilink") 能力的行動手持裝置可以在被網路端配置後, 同時使用LTE與Wi-Fi傳輸資料. 它提供的方法有別於另外一種技術,  可以被佈署而"不用"更換網路端硬體的基礎建設與行動裝置, 但LWA同時卻提供了與LAA相似的效能.

對於一般使用者而言, LWA提供了[LTE](../Page/長期演進技術.md "wikilink") 與 [Wi-Fi](../Page/Wi-Fi.md "wikilink")的無縫(seamless)接合同時實質上的提高了效能. 對營運商而言, LWA只需佈署[Wi-Fi](../Page/Wi-Fi.md "wikilink")後, 即可增進系統效能並且減少網路營運與管理成本. LWA可以以所謂的"collocated manner"佈署, 這種情況eNB與[Wi-Fi](../Page/Wi-Fi.md "wikilink") AP或AC(原文應該是想表示AP Controller)是被整合在同一台實體終端上. 另外一種"non-collocated manner"佈署方式, eNB與[Wi-Fi](../Page/Wi-Fi.md "wikilink") AP或AC則是用標準的接口所連接(參考Xw reference point). 後者的佈署方案特別適合於需要支援大區域的Wi-Fi範圍, 而這些Wi-Fi服務是第三方所提供(例如是一間大學校園)而並非某個營運商.

LWA是在3GPP Release-13所標準化. Release-14改進為Enhanced LWA (eLWA), 增加支援60Ghz 頻帶 (802.11ad and 802.11ay aka WiGig)與2.16Ghz 頻寬, 上傳聚合(uplink aggregation), 移動性增進與其他改進.

## 背景

行動網路被設計於使用授權頻譜(licensed spectrum). 然而, 近年用途模式改變, 從原本以語音為中心變成了資料, 並且資料的使用量激增, 營運商開始嘗試尋找免授權頻譜(unlicensed spectrum)的機會. 使用WLAN不只讓營運商增加峰值資料量, 也可以提供服務給非蜂巢服務的裝置, 例如筆記型電腦.

為迎合營運商的胃口, 3GPP在LTE-WLAN inter-working上制定了許多版本, 從Non-Seamless WLAN Offload (NSWO)到一些不嚴謹的方法如S2b, 至更先進的技術如LTE WLAN Radio Level Integration with IPsec Tunnel (LWIP), 到目前的LTE-WLAN Aggregation (LWA).

靠著LWA, WLAN終於可以完全的被融入蜂巢網路的世界裡.

## 深入LWA

從網路層面來看, 大致上有兩種選擇來彈性的佈署LWA - collocated 與 non-collocated.

LWA主要設計是遵照3GPP Release 12 LTE Dual Connectivity (DC) 架構\[3\], 其中允許UE(User Equipment)同時的連接至多個基站(base stations). 在U-plan(user plane)層面, LTE與WLAN是被聚合於Packet Data Convergence Protocol(PDCP)層.

## LWA 效能

## LWA 佈署研議

## 技術比較 (LTE-U, LAA, S2B, LWIP)

## 佈署

2016 8月19日, Nokia聲稱M1誕生了新加坡第一家商運HetNet(Heterogeneous Network), 其中包含LWA. 藉著尖端的 LTE-WiFi Aggregation (LWA)技術, M1希望2017年提供超過1Gbps的最大下載速度.

2017 2月23日, 台灣中華電信, 中磊, HTC(U Play), 搭配聯發科(Helio Pro 處理器)晶片, 發表全球首發 LWA 服務, 在會場現場實測下載/上傳速度可達413.1Mbps/45.9Mbps

## 參見

  - M1, "[M1, Nokia announce Singapore’s first commercial nationwide HetNet rollout](https://www.m1.com.sg/AboutM1/NewsReleases/2016/M1%20Nokia%20announce%20Singapore%20first%20commercial%20nationwide%20HetNet%20rollout.aspx)"

## 延伸閱讀

  - 5G Americas , "[LTE Aggregation & Unlicensed Spectrum](https://web.archive.org/web/20151106085720/http://www.4gamericas.org/files/1214/4648/2397/4G_Americas_LTE_Aggregation__Unlicensed_Spectrum_White_Paper_-_November_2015.pdf)"
  - The Ruckus Room, "[Getting Engaged: LTE and Wi-Fi Fall in Love](http://www.theruckusroom.net/2015/04/getting-engaged-lte-and-wi-fi-falling-in-love.html)"
  - Qualcomm, "[Improving LTE and Wi-Fi integration with PDCP aggregation](https://www.qualcomm.com/invention/research/projects/lte-advanced/lte-wi-fi-interworking)"
  - [点对点协议](../Page/点对点协议.md "wikilink")（Multiclass PPP、Multilink PPP）
  - [链路聚合](../Page/链路聚合.md "wikilink")（Link Aggregation）

## 外部連結

  - [Section 22A in Evolved Universal Terrestrial Radio Access (E-UTRA) and Evolved Universal Terrestrial Radio Access Network (E-UTRAN); Overall description; Stage 2](http://www.3gpp.org/dynareport/36300.htm)
  - [Evolved Universal Terrestrial Radio Access Network (E-UTRAN) and Wireless LAN (WLAN); Xw application protocol (XwAP)](http://www.3gpp.org/DynaReport/36463.htm)
  - [Evolved Universal Terrestrial Radio Access Network (E-UTRAN) and Wireless LAN (WLAN); Xw data transport](http://www.3gpp.org/DynaReport/36464.htm)
  - [Evolved Universal Terrestrial Radio Access Network (E-UTRAN) and Wireless LAN (WLAN); Xw interface user plane protocol](http://www.3gpp.org/DynaReport/36465.htm)

[Category:移动技术](https://zh.wikipedia.org/wiki/Category:移动技术 "wikilink") [Category:移动通信标准](https://zh.wikipedia.org/wiki/Category:移动通信标准 "wikilink") [Category:电信](https://zh.wikipedia.org/wiki/Category:电信 "wikilink")