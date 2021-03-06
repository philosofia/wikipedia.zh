**Q.931**是[ITU-T](https://zh.wikipedia.org/wiki/ITU-T "wikilink") 制定的[ISDN網路層介面協議](https://zh.wikipedia.org/wiki/ISDN "wikilink")（ISDN network layer interface protocol）。

Q.931一般不進行數據運送。Q.931並沒有直接相當於在互聯網協議棧，但跟SIP相比,由于底层的协议被认为是可靠的协议并且电路交换网络的带宽调整是固定的方式, 所以Q.931不提供流量控制和重传机制.

Q.931是[ISDN相關的協議](https://zh.wikipedia.org/wiki/ISDN "wikilink"), Q.931最近被用來作為[H.323](../Page/H.323.md "wikilink")協議（即[H.225](../Page/H.225.md "wikilink")）的一部份，在某種形式的移動電話傳輸系統。H.323包括Q.931、[H.225](../Page/H.225.md "wikilink")、[H.245](../Page/H.245.md "wikilink")和[ASN.1](../Page/ASN.1.md "wikilink"), 為了提供呼叫資訊，H.323部份融合了H.225和Q.931標準。Q.931流程包括呼叫建立和拆除。

一個 Q.931 frame包含以下元素：

  - 協議鑑別器（Protocol discriminator, PD）-指定的信令協議是用於連接（如PD = 8為DSS1 ）
  - 呼叫參考值（Call reference value, CR） - 針對不同的連接，可以同時存在。 只有在實際連接的一段時間值有效。
  - 消息類型（message type, MT） - 指定的第3層消息類型的呼叫控制（如設置）設置在Q.931定義的消息類型。 有呼叫建立，呼叫釋放和通話功能的控制定義的消息。
  - 資訊元素（information element, IE） - 指定關聯到實際的消息的進一步資料。Q.931 分組（packet）包含多個稱為資訊單元的參數。一個 IE瀏覽器包括IE瀏覽器的名稱（如承載能力），其長度和變量字段的內容。

## 訊息示例

  - SETUP：指示建立一個連接
  - CALL PROCEEDING
  - ALERTING
  - CONNECT
  - RELEASE
  - RELEASE COMPLETE

## 中斷原因

| 十六進制  | 十進制           | 原因                                                                                                                                          |
| ----- | ------------- | ------------------------------------------------------------------------------------------------------------------------------------------- |
| 0x1   | 1             | 未分配或未指定的號碼                                                                                                                                  |
| 0x2   | 2             | 沒有路由到指定的運輸網絡 (Transit Network Identity)                                                                                                     |
| 0x3   | 3             | 沒有到目的地的路由                                                                                                                                   |
| 0x4   | 4             | 發送特殊信息                                                                                                                                      |
| 0x5   | 5             | Misdialled trunk prefix                                                                                                                     |
| 0x6   | 6             | 頻道不可接受                                                                                                                                      |
| 0x7   | 7             | Call awarded and being delivered in an established channel                                                                                  |
| 0x8   | 8             | Prefix 0 dialed, 但不允許                                                                                                                       |
| 0x9   | 9             | Prefix 1 dialed, 但不允許                                                                                                                       |
| 0xA   | 10            | Prefix 1 not dialed, 但需要                                                                                                                    |
| 0xB   | 11            | More digits received than allowed, call is proceeding                                                                                       |
| 0x10  | 16            | Normal call clearing                                                                                                                        |
| 0x11  | 17            | User busy                                                                                                                                   |
| 0x12  | 18            | No user responding                                                                                                                          |
| 0x13  | 19            | T.301 expired: - User Alerted, No answer from user                                                                                          |
| 0x15  | 21            | Call rejected                                                                                                                               |
| 0x16  | 22            | Number changed to number in diagnostic field.                                                                                               |
| 0x17  | 23            | Reverse charging rejected                                                                                                                   |
| 0x18  | 24            | Call suspended                                                                                                                              |
| 0x19  | 25            | Call resumed                                                                                                                                |
| 0x1A  | 26            | Non-selected user clearing                                                                                                                  |
| 0x1B  | 27            | Destination out of order                                                                                                                    |
| 0x1C  | 28            | Invalid number format or incomplete address                                                                                                 |
| 0x1D  | 29            | EKTS facility rejected by network                                                                                                           |
| 0x1E  | 30            | Response to STATUS ENQUIRY                                                                                                                  |
| 0x1F  | 31            | Normal, unspecified                                                                                                                         |
| 0x21  | 33            | Circuit out of order                                                                                                                        |
| 0x22  | 34            | No circuit/channel available                                                                                                                |
| 0x23  | 35            | Destination unattainable                                                                                                                    |
| 0x24  | 36            | Out of order                                                                                                                                |
| 0x25  | 37            | Degraded service                                                                                                                            |
| 0x26  | 38            | Network out of order                                                                                                                        |
| 0x27  | 39            | Transit delay range cannot be achieved                                                                                                      |
| 0x28  | 40            | Throughput range cannot be achieved                                                                                                         |
| 0x29  | 41            | Temporary failure                                                                                                                           |
| 0x2A  | 42            | Switching equipment congestion                                                                                                              |
| 0x2B  | 43            | Access information discarded                                                                                                                |
| 0x2C  | 44            | Requested circuit channel not available                                                                                                     |
| 0x2D  | 45            | Preempted                                                                                                                                   |
| 0x2E  | 46            | Precedence call blocked                                                                                                                     |
| 0x2F  | 47            | Resource unavailable, unspecified                                                                                                           |
| 0x31  | 49            | Quality of service unavailable                                                                                                              |
| 0x32  | 50            | Requested facility not subscribed                                                                                                           |
| 0x33  | 51            | Reverse charging not allowed                                                                                                                |
| 0x34  | 52            | Outgoing calls barred                                                                                                                       |
| 0x35  | 53            | Outgoing calls barred within CUG                                                                                                            |
| 0x36  | 54            | Incoming calls barred                                                                                                                       |
| 0x37  | 55            | Incoming calls barred within CUG                                                                                                            |
| 0x38  | 56            | Call waiting not subscribed                                                                                                                 |
| 0x39  | 57            | Bearer capability not authorized                                                                                                            |
| 0x3A  | 58            | Bearer capability not presently available                                                                                                   |
| 0x3F  | 63            | Service or option not available, unspecified                                                                                                |
| 0x41  | 65            | Bearer service not implemented                                                                                                              |
| 0x42  | 66            | Channel type not implemented                                                                                                                |
| 0x43  | 67            | Transit network selection not implemented                                                                                                   |
| 0x44  | 68            | Message not implemented                                                                                                                     |
| 0x45  | 69            | Requested facility not implemented                                                                                                          |
| 0x46  | 70            | Only restricted digital information bearer capability is available                                                                          |
| 0x4F  | 79            | Service or option not implemented, unspecified                                                                                              |
| 0x51  | 81            | Invalid call reference value                                                                                                                |
| 0x52  | 82            | Identified channel does not exist                                                                                                           |
| 0x53  | 83            | A suspended call exists, but this call identity does not                                                                                    |
| 0x54  | 84            | Call identity in use                                                                                                                        |
| 0x55  | 85            | No call suspended                                                                                                                           |
| 0x56  | 86            | Call having the requested call identity has been cleared                                                                                    |
| 0x57  | 87            | Called user not member of CUG                                                                                                               |
| 0x58  | 88            | Incompatible destination                                                                                                                    |
| 0x59  | 89            | Non-existent abbreviated address entry                                                                                                      |
| 0x5A  | 90            | Destination address missing, and direct call not subscribed                                                                                 |
| 0x5B  | 91            | Invalid transit network selection (national use)                                                                                            |
| 0x5C  | 92            | Invalid facility parameter 93 Mandatory information element is missing                                                                      |
| 0x5D  | 93            | Message type non-existent or not implemented                                                                                                |
| 0x5F  | 95            | Invalid message, unspecified                                                                                                                |
| 0x60  | 96            | Mandatory information element is missing                                                                                                    |
| 0x61  | 97            | Message type non-existent or not implemented                                                                                                |
| 0x62  | 98            | Message not compatible with call state or message type non-existent or not implemented                                                      |
| 0x63  | 99            | Information element nonexistent or not implemented                                                                                          |
| 0x64  | 100           | Invalid information element contents                                                                                                        |
| 0x65  | 101           | Message not compatible with call state                                                                                                      |
| 0x66  | 102           | Recovery on timer expiry                                                                                                                    |
| 0x67  | 103           | Parameter non-existent or not implemented - passed on                                                                                       |
| 0x6F  | 111           | Protocol error, unspecified                                                                                                                 |
| 0x7F  | 127           | Internetworking, unspecified                                                                                                                |
| 0x80+ | 128 or higher | Proprietary diagnostic code (not necessarily bad). Typically used to pass proprietary control or maintenance messages between multiplexers. |

## 限制

Q.931是基於原語（primitive）的，但Q.931並沒有規定原語的字義，Q.931和H.225都定義了呼叫資訊流程，但定義不充分，Q.931的原語缺乏充分的文字說明。另一方面, Q.931和H.225融合不夠好，H.225將Q.931中的消息標記成“禁用”，但卻沒有規定出新流程。Q.931介面是不可移植的, 這是因為H.225只提到原語而沒有提供包含參數的資訊，使得H.323的發展大受影響, [SIP有取代H](https://zh.wikipedia.org/wiki/SIP "wikilink").323的趨勢。

## Q.2931

Q.2931是Q.931修改和擴展B-ISDN的變種。

[Category:ITU-T标准](https://zh.wikipedia.org/wiki/Category:ITU-T标准 "wikilink")