**延伸顯示能力識別**（Extended display identification data，簡稱EDID）是指[螢幕解析度的資料](https://zh.wikipedia.org/wiki/螢幕解析度 "wikilink")，包括廠商名稱與序號。一般EDID存在於[顯示器的](https://zh.wikipedia.org/wiki/顯示器 "wikilink")[PROM或](https://zh.wikipedia.org/wiki/PROM "wikilink")[EEPROM內](https://zh.wikipedia.org/wiki/EEPROM "wikilink")。一般如要讀取EDID都是透過[I2C](https://zh.wikipedia.org/wiki/I2C "wikilink")，slave address是0x50\[1\]。目前[HDMI](../Page/HDMI.md "wikilink") 1.0 - 1.3c使用EDID結構1.3版。

許多現成的[套裝軟體都可以讀取並顯示EDID資訊](https://zh.wikipedia.org/wiki/套裝軟體 "wikilink")，像是read-edid\[2\] 和 Powerstrip\[3\] 可以使用於[Windows之上](https://zh.wikipedia.org/wiki/Windows "wikilink")，又如[XFree86](../Page/XFree86.md "wikilink") 〔將EDID 資料輸出到log檔, 如果 verbose logging 是在 (`startx -- -logverbose 6`)〕可以使用於Linux平台上，以及[BSD Unix](https://zh.wikipedia.org/wiki/BSD_Unix "wikilink")。在Linux平台上也可以看到raw EDID的十六進位格式，只要你執行 "xrandr --verbose"。[Mac OS X平台上可自然的讀取EDID資訊](https://zh.wikipedia.org/wiki/Mac_OS_X "wikilink") (見 /var/log/system.log or hold down Cmd-V on startup) 並加以程式化，像是 SwitchResX\[4\] 或 DisplayConfigX\[5\] 可以顯示其資訊。

## EDID 1.3 資料格式

    位元組序列
    0x00-0x13: 標頭資訊
      0x00–0x07: 標頭資訊 "00h FFh FFh FFh FFh FFh FFh 00h"
      0x08–0x09: 製造商ID。 這個識別碼是經由微軟來分配。
                  "00001=A”； “00010=B”； ... “11010=Z”，每個字元是5bits。 第7bit (位址 08h) 是0， 第一個字元(字母)
                  是位於bit 6 ~ 2 (位址 08h)， 第二個字元(字母)是位於bit 1和0 (位址 08h) 和 bit7 ~ 5
                  (位址 09h)，第三個字元(字母)是位於bit4 ~ 0 (位址 09h)。
                  Ex:
                     製造商ID : CEA -> 00011 00101 00001
                     EDID Byte 8~9: 0CA1

      0x0A–0x0B: 生產ID碼 (儲存方式是LSB開始)。 由製造商分配。
      0x0C–0x0F: 32位元序號。 非必需格式。 通常儲存由 LSB 優先。為了去維持和之前需求的相容性，假如一個ASCII
                  序號在詳細時脈部分被提供，這個欄位應該設定至少一個位元組不是零。
      0x10: 製造週。 這個由製造商改變。 法一是去計算一月的 1-7 當做第一週，一月 8-15 當做第二週並且以此
            類推。 一些計算是以星期幾(星期日-星期六)為基礎。有效範圍是 1-54。
      0x11: 製造年份。 加上1990才是確實的年份。
      0x12: EDID 版本號碼。 "01h"
      0x13: EDID 修訂版號碼。 "03h"

    0x14-0x18: 基本顯示參數
      0x14: 影像輸入定義
            位元 7： 0=類比, 1=數位
            假如 位元 7 是數位：
              位元 0： 1=相容DFP 1.x
            假如 位元 7 是類比：
              位元 6-5： 影像等級
               00=0.7, 0.3， 01=0.714, 0.286， 10=1, 0.4 11=0.7, 0
          bit 4: 白黑設定
          bit 3: 分離同步
          bit 2: 合成同步
          bit 1: 綠色同步
          bit 0: 鋸齒垂直同步
      0x15: 最大水平圖形尺寸 (單位為公分)。
      0x16: 最大垂直圖形尺寸 (單位為公分)。
      0x17: 顯示伽瑪。 除以100再加1才是真正的值。
      0x18: 電源管理和支援的特徵：
          bit 7： 待命
          bit 6： 暫停
          bit 5： 活躍關閉/低電源
          bit 4-3： 顯示型態
            00=黑白, 01=RGB 色彩, 10=非 RGB 多色彩, 11=未定義
          bit 2： 標準色彩空間
          bit 1： 偏好時脈模式
          bit 0： 預設 GTF 支援

    0x19-0x22: 色度調節
      0x19: 低有效位關於紅色 X1X0 (位元 7-6)， 紅色 Y1Y0 (位元 5-4)， 綠色 X1X0 (位元 3-2)，
            綠色 Y1Y0 (位元 1-0)。
      0x1A: 低有效位關於藍色 X1X0 (位元 7-6)， 藍色 Y1Y0 (位元 5-4)， 白色 X1X0 (位元 3-2)，
            白色 Y1Y0 (位元 1-0)。
      0x1B–0x22: 高有效位關於紅色 X9-2， 紅色 Y9-2， 綠色 X9-2， 綠色 Y9-2， 藍色 X9-2，
            藍色 Y9-2， 白色 X9-2， 白色 Y9-2。
      正確值是介於0.000和0.999，但編碼值是介於000h和3FFh。

    0x23: 建立時脈 I
          位元 7-0： 720×400@70 Hz， 720×400@88 Hz， 640×480@60 Hz， 640×480@67 Hz，
               640×480@72 Hz， 640×480@75 Hz， 800×600@56 Hz， 800×600@60 Hz

    0x24: 建立時脈 II
          位元 7-0： 800×600@72 Hz， 800×600@75 Hz， 832×624@75 Hz， 1024×768@87 Hz (交錯的)，
               1024×768@60 Hz， 1024×768@70 Hz， 1024×768@75 Hz， 1280×1024@75 Hz

    0x25: 製造商保留的時脈
          00h 是無
          位元 7： 1152x870 @ 75 Hz (麥金塔 II， 蘋果)

    0x24–0x35: 標準時脈識別。
                第一個位元組
                水平結果。  加上31，再乘上8， 得到正確值。
                第二個位元組
                  位元 7-6： 外觀比例。 正確的垂直結果依賴水平結果。
                  00=16：10， 01=4：3， 10=5：4， 11=16：9 (00=1:1 在v1.3之前)
                  位元 5-0： 垂直頻率。 加上 60 去得到正確的值。

    0x36–0x47: 詳細時脈描述 1
      0x36–0x37: 像素時脈 (單位為 10 kHz) 或 0  (55 MSB  54 LSB)
      假如像素時脈並非無效：
        0x38： 水平活躍 (單位為像素)
        0x39： 水平空白 (單位為像素)
        0x3A： 水平活躍高 (4 高位元)
               水平空白高 (4 低位元)
        0x3B： 垂直活躍 (單位為線)
        0x3C： 垂直空白 (單位為線)
        0x3D： 垂直活躍在高有效位 (4 高位元)
               垂直空白在高有效位 (4 低位元)
        0x3E： 水平同步偏移量 (單位為像素)
        0x3F： 水平同步脈沖寬度 (單位為像素)
        0x40： 垂直同步偏移量 (單位為線) (4 高位元)
               垂直同步脈沖寬度 (單位為線) (4 低位元)
        0x41： 高有效位關於水平同步偏移量 (位元 7-6)
               高有效位關於水平同步脈沖寬度 (位元 5-4)
               高有效位關於垂直同步偏移量 (位元 3-2)
               高有效位關於垂直同步脈沖寬度 (位元 1-0)
        0x42： 水平圖像尺寸 (單位為公釐)
        0x43： 垂直圖像尺寸 (單位為公釐)
        0x44： 高有效位關於水平圖像尺寸 (4 高位元)
               高有效位關於垂直圖像尺寸 (4 低位元)
        0x45： 水平邊界線 (單位為像素且只表示一邊)
        0x46： 垂直邊界線 (單位為線且只表示一邊)
        0x47： 交錯與否 (位元 7)
               立體與否 (位元 6-5) ("00" 表示否)
               分離同步與否 (位元 4-3)
               垂直同步正與否 (位元 2)
               水平同步正與否 (位元 1)
               立体模式 (位元 0) (若是6-5 是 00 則沒使用)
      假如像素時脈是無效：
        0x38： 0
        0x39： 區塊型態
               FFh=監視器序號， FEh=ASCII 字串， FDh=監視器變動限制， FCh=監視器名稱，
               FBh=色彩點資料， FAh， 標準時脈資料， F9h=現在未定義，
               0Fh=由製造商定義
        0x3A： 0
        0x3B–0x47: 區塊內容描述符。
               假如區塊型態是 FFh， FEh， 或 FCh， 整個區域是字串。
               假如區塊型態是 FDh：
                 0x3B–0x3F：
                   最小垂直頻率， 最大垂直頻率，
                   最小水平頻率 (單位為 kHz)， 最大水平頻率 (單位為 kHz)， 像素時脈
                   (單位為 MHz (正確值需乘上10))
                 0x40–0x41: 第二 GTF 觸發器
                   假如編碼值是 000A， 位元組 59-63 是使用。 假如編碼值是 0200，
                   位元組 67–71 是使用。
                 0x42： 開始水平頻率 (單位為 kHz)。  乘上2得到實際值。
                 0x43： C。 除以 2 得到實際值。
                 0x44-0x45： M (以LSB優先儲存)。
                 0x46： K
                 0x47： J。 除以 2 得到實際值。
               假如區塊型態是 FBh：
                 0x3B： W 索引 0。 假如設定成 0， 位元組 60-63 是沒使用。 假如設定成 1， 61–63 是
                        分配到白點索引 #1
                 0x40： W 索引 1。 假如設定成 0， 位元組 65-68 是沒使用。 假如設定成 2， 65–68 是
                        分配到白點索引 #2
                 白點索引結構：
                   第一個位元
                     位元 3-2： 低有效位關於白 X (位元 3-2)， 白 Y (位元 1-0)
                   第二到第三位元組： 高有效位關於白 X， 白 Y。
                   第四位元組： 伽瑪。 除以100， 再加上1得到實際值。
                   解碼白 X 和白 Y， 看位元組 25-34。
               假如區塊型態是 FAh：
                 0x3B–0x46： 標準時脈識別。  2 位元組對於每一個紀錄。
                              關於結構細節， 看位元組 38-53。

    0x48–0x59: 詳細時脈描述 2 或監視器描述符

    0x5A–0x6B: 詳細時脈描述 3 或監視器描述符

    0x6C–0x7D: 詳細時脈描述 4 或監視器描述符

    0x7E: 額外的旗標。 額外的數值採用這個區塊。
          在EDID 1.3之前， 這是被忽略的， 並且應該被設成 0。

    0x7F: 校驗和 - 這個位元組應該被程式化使得所有 128 位元組的加總等於 00h.

## 參見

  - [電腦標準列表](https://zh.wikipedia.org/wiki/電腦標準列表 "wikilink")

## 注釋

[Category:顯示科技](https://zh.wikipedia.org/wiki/Category:顯示科技 "wikilink")

1.  [DDC/CI specifications](http://www.boichat.ch/nicolas/ddcci/specs.html)
2.  [read-edid software for Linux and Windows](http://www.polypux.org/projects/read-edid/)
3.  [Powerstrip for Windows (Shareware)](http://www.entechtaiwan.com/util/ps.shtm)
4.  [SwitchResX for Mac OS X shows EDID and customizes display timings](http://www.madrau.com/)
5.  [DisplayConfigX for Mac OS X shows EDID and customizes display timings](http://www.3dexpress.de/)