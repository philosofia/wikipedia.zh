> 本文内容由[Microsoft Azure 虛擬機器服務](https://zh.wikipedia.org/wiki/Microsoft_Azure_虛擬機器服務)转换而来。


**Microsoft Azure 虛擬機器服務** 是 Microsoft Azure 平台的基礎建設服務之一，且是運算類服務的核心，由微軟資料中心的實體伺服器[虛擬化](../Page/虛擬化.md "wikilink")後產生的虛擬機器提供，雖然虛擬機器會供應 Microsoft Azure 平台內所有需要運算資源的服務 (如 Cloud Service、Web App、Service Fabric 以及其他類型服務)，但虛擬機器服務會開放足夠的管理與控制權給系統管理人員或網路管理人員，讓他們有權力操作整台虛擬機器。

虛擬機器服務自 2012 年 Spring Release 階段正式推出，目前已是 Microsoft Azure 平台上使用率最高的服務。

## 服務類型

虛擬機器服務是由[Azure 雲端服務的](../Page/Microsoft_Azure_雲端服務.md "wikilink") VM Role 所發展出來的服務，將機器的管理權與控制權交給系統管理人員自行維運，以獲得較大的可控制與相容性，虛擬機器會使用到如[虛擬網路以及](../Page/Microsoft_Azure_虛擬網路服務.md "wikilink")[儲存服務](../Page/Microsoft_Azure_儲存體.md "wikilink") 等資源來支援網路通訊與資料儲存功能。

Azure將虛擬機器分為兩種類型，一種是標準型的虛擬機器 (Standard)，擁有完整的虛擬機器服務功能，如負載平衡 (Load Balancing) 與自動擴展 (Auto Scale) 的能力，另一種是基本型的虛擬機器 (Basic)，基本層無法使用負載平衡與自動擴展能力，但其他功能與標準型相同，基本層也只能使用 A0\~A4 (Extra Small, Small, Medium, Large, Extra Large) 五種等級的虛擬機器，標準型則可使用全部的虛擬機器類型。

虛擬機器的計費方式是以分計費，計算基準為虛擬機器啟動時到虛擬機器被停止 (或刪除) 並釋放出資源時為止。

## 虛擬機器類型

Azure 虛擬機器依照運算能力區分為數種類型 \[1\]，共分為一般性運算能量的 A 類型、經效能提升的 D 類型以及擁有最強運算效能的 G 類型，未來也會推出使用[GPU運算的](https://zh.wikipedia.org/wiki/GPU "wikilink") N 類型。

### Azure 計算單元

Azure 計算單元 (Azure Compute Unit, ACU) 是一個可用於比較 Azure 虛擬機器之運算效能的方法，現階段是以 Standard_A1 虛擬機等級為標準，數值為 100。

### A 類型

A 類型是 Azure 一開始就提供的標準虛擬機器類型，使用 [AMD](https://zh.wikipedia.org/wiki/AMD "wikilink") 的 CPU 以及傳統 [SATA](../Page/SATA.md "wikilink") 介面的硬碟，提供最標準不需太高運算能量的應用，早期是以五種規格推出，分別是 Extra Small (XS)、Small (S)、Medium (M)、Large (L) 以及 Extra Large (XL) 五種，除了 XS 記憶體使用 0.75GB 記憶體外，其他是以 1.75GB 記憶體，每晉一級就會加倍，可作為衡量運算資源與成本的標準之一。不過在虛擬機器種類愈來愈多的情況下，A 類型也做了擴充，現在除了原有的五類外，還多加了 A5\~A7、A8\~A11等七種規格。

A5\~A7 與 A8\~A11 均使用 Intel Xeon E5 系列 CPU，但 A5\~A7 的記憶體量比 A2\~A4 高；A8\~A9 與 A10\~A11 規格相同，但 A8\~A9 有支援 HPC 的 InfiniBand 網路介面與 RDMA 技術，A10\~A11 則無。

A0\~A7 系列的 ACU 為 50\~100，A8 以上的 ACU 為 225。

| 規格            | CPU核心數 | 記憶體量   | 暫存硬碟大小 (SATA) | 可用網卡數 | 可用資料磁碟數 | 最高[IOPS](../Page/IOPS.md "wikilink") | 說明                   |
| ------------- | ------ | ------ | ------------- | ----- | ------- | ------------------------------------ | -------------------- |
| Standard_A0  | 1      | 0.75GB | 20GB          | 1     | 1       | 1x500                                | Extra Small          |
| Standard_A1  | 1      | 1.75GB | 70GB          | 1     | 2       | 2x500                                | Small                |
| Standard_A2  | 2      | 3.5GB  | 135GB         | 1     | 4       | 4x500                                | Medium               |
| Standard_A3  | 4      | 7GB    | 285GB         | 2     | 8       | 8x500                                | Large                |
| Standard_A4  | 8      | 14GB   | 605GB         | 4     | 16      | 16x500                               | Extra Large          |
| Standard_A5  | 2      | 14GB   | 135GB         | 1     | 4       | 4x500                                |                      |
| Standard_A6  | 4      | 28GB   | 285GB         | 2     | 8       | 8x500                                |                      |
| Standard_A7  | 8      | 56GB   | 605GB         | 4     | 16      | 16x500                               |                      |
| Standard_A8  | 8      | 56GB   | 382GB         | 2     | 16      | 16x500                               | 支援 InfiniBand 與 RDMA |
| Standard_A9  | 16     | 112GB  | 382GB         | 4     | 16      | 16x500                               | 支援 InfiniBand 與 RDMA |
| Standard_A10 | 8      | 56GB   | 382GB         | 2     | 16      | 16x500                               |                      |
| Standard_A11 | 16     | 112GB  | 382GB         | 4     | 16      | 16x500                               |                      |

Av2 系列的 ACU 為 100。

| 規格                | CPU核心數 | 記憶體量 | 暫存硬碟大小 (SSD) | 可用網卡數 | 可用資料磁碟數 | 最高[IOPS](../Page/IOPS.md "wikilink") | 說明 |
| ----------------- | ------ | ---- | ------------ | ----- | ------- | ------------------------------------ | -- |
| Standard_A1_v2  | 1      | 2GB  | 10GB         | 2     | 2       | 2x500                                |    |
| Standard_A2_v2  | 2      | 4GB  | 20GB         | 2     | 4       | 4x500                                |    |
| Standard_A4_v2  | 4      | 8GB  | 40GB         | 4     | 8       | 8x500                                |    |
| Standard_A8_v2  | 8      | 16GB | 80GB         | 8     | 16      | 16x500                               |    |
| Standard_A2m_v2 | 2      | 16GB | 200GB        | 2     | 4       | 4x500                                |    |
| Standard_A4m_v2 | 4      | 32GB | 40GB         | 4     | 8       | 8x500                                |    |
| Standard_A8m_v2 | 8      | 64GB | 80GB         | 8     | 16      | 16x500                               |    |

### D 類型

D 類型是 Azure 在 2013 年推出的類型，它使用比 A 類型更好的 CPU，並且在實體伺服器上使用固態硬碟 ([SSD](https://zh.wikipedia.org/wiki/SSD "wikilink"))，以加速在本地運算時的 I/O 速度，另外，為滿足提升虛擬機器本身的 I/O 量的需求，微軟開發了高階儲存體 (Premium Storage) 用來保存虛擬機使用的 VHD (稱為 OS Disk)，而使用高階儲存體的 D 類型虛擬機器，稱為 DS 類型。

D 與 DS 類型的 ACU 為 160。

<table>
<thead>
<tr class="header">
<th><p>規格</p></th>
<th><p>CPU核心數</p></th>
<th><p>記憶體量</p></th>
<th><p>暫存硬碟大小 (SSD)</p></th>
<th><p>可用網卡數</p></th>
<th><p>可用資料磁碟數</p></th>
<th><p>最高<a href="../Page/IOPS.md" title="wikilink">IOPS</a></p></th>
<th><p>最高<a href="../Page/IOPS.md" title="wikilink">IOPS</a> (DS類型)</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Standard_D1<br />
Standard_DS1</p></td>
<td><p>1</p></td>
<td><p>3.5GB</p></td>
<td><p>50GB</p></td>
<td><p>1</p></td>
<td><p>2</p></td>
<td><p>2x500</p></td>
<td><p>3,200</p></td>
</tr>
<tr class="even">
<td><p>Standard_D2<br />
Standard_DS2</p></td>
<td><p>2</p></td>
<td><p>7GB</p></td>
<td><p>100GB</p></td>
<td><p>2</p></td>
<td><p>4</p></td>
<td><p>4x500</p></td>
<td><p>6,400</p></td>
</tr>
<tr class="odd">
<td><p>Standard_D3<br />
Standard_DS3</p></td>
<td><p>4</p></td>
<td><p>14GB</p></td>
<td><p>200GB</p></td>
<td><p>4</p></td>
<td><p>8</p></td>
<td><p>8x500</p></td>
<td><p>12,800</p></td>
</tr>
<tr class="even">
<td><p>Standard_D4<br />
Standard_DS4</p></td>
<td><p>8</p></td>
<td><p>28GB</p></td>
<td><p>400GB</p></td>
<td><p>8</p></td>
<td><p>16</p></td>
<td><p>16x500</p></td>
<td><p>25,600</p></td>
</tr>
<tr class="odd">
<td><p>Standard_D11<br />
Standard_DS11</p></td>
<td><p>2</p></td>
<td><p>14GB</p></td>
<td><p>100GB</p></td>
<td><p>2</p></td>
<td><p>4</p></td>
<td><p>4x500</p></td>
<td><p>6,400</p></td>
</tr>
<tr class="even">
<td><p>Standard_D12<br />
Standard_DS12</p></td>
<td><p>4</p></td>
<td><p>28GB</p></td>
<td><p>200GB</p></td>
<td><p>4</p></td>
<td><p>8</p></td>
<td><p>8x500</p></td>
<td><p>12,800</p></td>
</tr>
<tr class="odd">
<td><p>Standard_D13<br />
Standard_DS13</p></td>
<td><p>8</p></td>
<td><p>56GB</p></td>
<td><p>400GB</p></td>
<td><p>8</p></td>
<td><p>16</p></td>
<td><p>16x500</p></td>
<td><p>25,600</p></td>
</tr>
<tr class="even">
<td><p>Standard_D14<br />
Standard_DS14</p></td>
<td><p>16</p></td>
<td><p>112GB</p></td>
<td><p>800GB</p></td>
<td><p>8</p></td>
<td><p>32</p></td>
<td><p>32x500</p></td>
<td><p>50,000</p></td>
</tr>
</tbody>
</table>

2015年，微軟利用新的 Intel Xeon E5-2673 v3 CPU 的伺服器組建了 D 類型的第二版，稱為 Dv2，可獲取 D 類型虛擬機高 35% 的效能。

Dv2 的 ACU 為 210\~250。

| 規格                | CPU核心數 | 記憶體量  | 暫存硬碟大小 (SSD) | 可用網卡數 | 可用資料磁碟數 | 最高[IOPS](../Page/IOPS.md "wikilink") | 說明 |
| ----------------- | ------ | ----- | ------------ | ----- | ------- | ------------------------------------ | -- |
| Standard_D1_v2  | 1      | 3.5GB | 50GB         | 1     | 2       | 2x500                                |    |
| Standard_D2_v2  | 2      | 7GB   | 100GB        | 2     | 4       | 4x500                                |    |
| Standard_D3_v2  | 4      | 14GB  | 200GB        | 4     | 8       | 8x500                                |    |
| Standard_D4_v2  | 8      | 28GB  | 400GB        | 8     | 16      | 16x500                               |    |
| Standard_D5_v2  | 16     | 56GB  | 800GB        | 8     | 32      | 32x500                               |    |
| Standard_D11_v2 | 2      | 14GB  | 100GB        | 2     | 4       | 4x500                                |    |
| Standard_D12_v2 | 4      | 28GB  | 200GB        | 4     | 8       | 8x500                                |    |
| Standard_D13_v2 | 8      | 56GB  | 400GB        | 8     | 16      | 16x500                               |    |
| Standard_D14_v2 | 16     | 112GB | 800GB        | 8     | 32      | 32x500                               |    |

DSv2 類型的 ACU 為 210\~250。

| 規格                 | CPU核心數 | 記憶體量  | 暫存硬碟大小 (SSD) | 可用網卡數 | 可用資料磁碟數 | 最高[IOPS](../Page/IOPS.md "wikilink") | 說明           |
| ------------------ | ------ | ----- | ------------ | ----- | ------- | ------------------------------------ | ------------ |
| Standard_DS1_v2  | 1      | 3.5GB | 7GB          | 2     | 2       | 4,000                                |              |
| Standard_DS2_v2  | 2      | 7GB   | 14GB         | 2     | 4       | 8,000                                |              |
| Standard_DS3_v2  | 4      | 14GB  | 28GB         | 4     | 8       | 16,000                               |              |
| Standard_DS4_v2  | 8      | 28GB  | 56GB         | 8     | 16      | 32,000                               |              |
| Standard_DS5_v2  | 16     | 56GB  | 112GB        | 8     | 32      | 64,000                               |              |
| Standard_DS11_v2 | 2      | 14GB  | 28GB         | 2     | 4       | 8,000                                |              |
| Standard_DS12_v2 | 4      | 28GB  | 56GB         | 4     | 8       | 16,000                               |              |
| Standard_DS13_v2 | 8      | 56GB  | 112GB        | 8     | 16      | 32,000                               |              |
| Standard_DS14_v2 | 16     | 112GB | 224GB        | 8     | 32      | 64,000                               |              |
| Standard_DS15_v2 | 20     | 140GB | 280GB        | 8     | 40      | 80,000                               | 部署至單一客戶專屬的硬體 |

微軟於 Build 2017 研討會上宣布，Dv3 將於今年推出，並支援巢狀虛擬化。

### G 類型

G 類型是 Azure 擁有最強運算與 I/O 能量的虛擬機器，它使用 [Intel Xeon](https://zh.wikipedia.org/wiki/Intel_Xeon "wikilink") E5 v3 系列 CPU，並且配備較大量的記憶體，可用於需要大量又高速的運算需求，例如資料庫或是科學運算。與 D 類型相同，G 類型也可利用高階儲存體來加速 I/O，使用高階儲存體的 G 類型虛擬機器，稱為 GS 類型。

G/GS 系列的 ACU 為 180\~240。

<table>
<thead>
<tr class="header">
<th><p>規格</p></th>
<th><p>CPU核心數</p></th>
<th><p>記憶體量</p></th>
<th><p>暫存硬碟大小 (SSD) (G類型/GS類型)</p></th>
<th><p>可用網卡數</p></th>
<th><p>可用資料磁碟數</p></th>
<th><p>最高<a href="../Page/IOPS.md" title="wikilink">IOPS</a> (G類型/GS類型)</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Standard_G1<br />
Standard_GS1</p></td>
<td><p>2</p></td>
<td><p>28GB</p></td>
<td><p>384GB/56GB</p></td>
<td><p>1</p></td>
<td><p>4</p></td>
<td><p>4x500/10,000</p></td>
</tr>
<tr class="even">
<td><p>Standard_G2<br />
Standard_GS2</p></td>
<td><p>4</p></td>
<td><p>56GB</p></td>
<td><p>768GB/112GB</p></td>
<td><p>2</p></td>
<td><p>8</p></td>
<td><p>8x500/20,000</p></td>
</tr>
<tr class="odd">
<td><p>Standard_G3<br />
Standard_GS3</p></td>
<td><p>8</p></td>
<td><p>112GB</p></td>
<td><p>1,536GB/224GB</p></td>
<td><p>4</p></td>
<td><p>16</p></td>
<td><p>16x500/40,000</p></td>
</tr>
<tr class="even">
<td><p>Standard_G4<br />
Standard_GS4</p></td>
<td><p>16</p></td>
<td><p>224GB</p></td>
<td><p>3,072GB/448GB</p></td>
<td><p>8</p></td>
<td><p>32</p></td>
<td><p>32x500/80,000</p></td>
</tr>
<tr class="odd">
<td><p>Standard_G5<br />
Standard_GS5</p></td>
<td><p>32</p></td>
<td><p>448GB</p></td>
<td><p>6,144GB/896GB</p></td>
<td><p>8</p></td>
<td><p>64</p></td>
<td><p>64x500/160,000</p></td>
</tr>
</tbody>
</table>

註：GS5等級會部署到單一客戶專用的硬體。

### N 類型

N 類型是 Azure 在 2015 年宣佈的新虛擬機器類型，包含兩種類型：

  - NC 使用 NVIDIA 的 Tesla K80 GPU 卡，可用於能源探勘應用程式、當機模擬、光線追蹤轉譯、深入學習等，K80 提供 4,992 個 CUDA 核心。
  - NV 使用 NVIDIA 的 Tesla M60 GPU 卡，可用於桌面加速應用程式和虛擬桌面，可供客戶從中將其資料或模擬視覺化，也適用於編碼與轉譯，M60 提供 4096 個 CUDA 核心，最多可供 36 個 1080p H.264 的串流能力。

| 規格      | Standard_NV6 | Standard_NV12 | Standard_NV24 | Standard_NC6 | Standard_NC12 | Standard_NC24 | Standard_NC24r |
| ------- | ------------- | -------------- | -------------- | ------------- | -------------- | -------------- | --------------- |
| CPU 核心數 | 6             | 12             | 24             | 6             | 12             | 24             | 24              |
| 記憶體     | 56GB          | 112GB          | 224GB          | 56GB          | 112GB          | 224GB          | 224GB           |
| SSD硬碟大小 | 380GB         | 680GB          | 1,440GB        | 380GB         | 680GB          | 1,440GB        | 1,440GB         |
| GPU     | 1             | 2              | 4              | 1             | 2              | 4              | 4               |

2017 年即將推出新的 ND 系列與 NC v2 系列，搭載 NVIDIA Tesla P40 與 P100 GPU \[2\]。

註 1: 1 GPU = 1/2 M60 (NV) 或 1/2 K80 (NC) 註 2: Standard_NC24r 支援 RDMA 運算

### F 類型

F 類型是以 Intel Xeon 2673 v3 (Haswell) 等級的 CPU 為基礎，提供高效能運算的服務，與 D 等級第二版 (Dv2) 的 CPU 相同，但價格較便宜。 F 類型適用於需要高速 CPU，但不需要太多記憶體或本機 SSD 的工作負載。 Fs 類型是輕量化的 F 類型，但仍提供 F 類型的所有優點。

F/Fs類型的 ACU 為 210\~250。

<table>
<thead>
<tr class="header">
<th><p>規格</p></th>
<th><p>CPU核心數</p></th>
<th><p>記憶體量</p></th>
<th><p>暫存硬碟大小 (SSD) (Fs/F)</p></th>
<th><p>可用網卡數</p></th>
<th><p>可用資料磁碟數</p></th>
<th><p>最高<a href="../Page/IOPS.md" title="wikilink">IOPS</a> (Fs類型)</p></th>
<th><p>最高<a href="../Page/IOPS.md" title="wikilink">IOPS</a> (F類型)</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Standard_F1s<br />
Standard_F1</p></td>
<td><p>1</p></td>
<td><p>2GB</p></td>
<td><p>4GB/16GB</p></td>
<td><p>2</p></td>
<td><p>2</p></td>
<td><p>4,000</p></td>
<td><p>2x500</p></td>
</tr>
<tr class="even">
<td><p>Standard_F2s<br />
Standard_F2</p></td>
<td><p>2</p></td>
<td><p>4GB</p></td>
<td><p>8GB/32GB</p></td>
<td><p>2</p></td>
<td><p>4</p></td>
<td><p>8,000</p></td>
<td><p>4x500</p></td>
</tr>
<tr class="odd">
<td><p>Standard_F4s<br />
Standard_F4</p></td>
<td><p>4</p></td>
<td><p>8GB</p></td>
<td><p>16GB/64GB</p></td>
<td><p>4</p></td>
<td><p>8</p></td>
<td><p>16,000</p></td>
<td><p>8x500</p></td>
</tr>
<tr class="even">
<td><p>Standard_F8s<br />
Standard_F8</p></td>
<td><p>8</p></td>
<td><p>16GB</p></td>
<td><p>32GB/128GB</p></td>
<td><p>8</p></td>
<td><p>16</p></td>
<td><p>32,000</p></td>
<td><p>16x500</p></td>
</tr>
<tr class="odd">
<td><p>Standard_F16s<br />
Standard_F16</p></td>
<td><p>16</p></td>
<td><p>32GB</p></td>
<td><p>64GB/256GB</p></td>
<td><p>8</p></td>
<td><p>32</p></td>
<td><p>64,000</p></td>
<td><p>32x500</p></td>
</tr>
</tbody>
</table>

### L 類型

L 類型適用於需低延遲本機儲存體的工作負載，例如 NoSQL 資料庫 (如 Cassandra, MongoDB, Cloudera 與 Redis)，使用 Intel Xeon E5 v3 處理器，等同於 G/GS 類型的 CPU 效能。

L 系列為 ACU 為 180\~240。

| 規格             | CPU核心數 | 記憶體量  | 暫存硬碟大小 (SSD) | 可用網卡數 | 可用資料磁碟數 | 最高[IOPS](../Page/IOPS.md "wikilink") |
| -------------- | ------ | ----- | ------------ | ----- | ------- | ------------------------------------ |
| Standard_L4s  | 1      | 32GB  | 678GB        | 2     | 8       | 5,000                                |
| Standard_L8s  | 2      | 64GB  | 1,388GB      | 4     | 16      | 10,000                               |
| Standard_L16s | 4      | 128GB | 2,807GB      | 8     | 32      | 20,000                               |
| Standard_L32s | 8      | 256GB | 5,630GB      | 8     | 64      | 40,000                               |

### H 類型

H 類型是以高端運算需求為目標設計，使用 Intel Haswell E5-2667 v3 CPU、DDR4 記憶體、SSD 與 RDMA 來加速運算，適用於如分子建模及運算流體力學等。

H 系列的 ACU 為 290\~300。

| 規格                       | CPU核心數 | 記憶體量  | 暫存硬碟大小 (SSD) | 可用網卡數 | 可用資料磁碟數 | 最高[IOPS](../Page/IOPS.md "wikilink") |
| ------------------------ | ------ | ----- | ------------ | ----- | ------- | ------------------------------------ |
| Standard_H8             | 8      | 56GB  | 1,000GB      | 2     | 16      | 16x500                               |
| Standard_H16            | 16     | 112GB | 2,000GB      | 4     | 32      | 32x500                               |
| Standard_H8m            | 8      | 112GB | 1,000GB      | 2     | 16      | 16x500                               |
| Standard_H16m           | 16     | 224GB | 2,000GB      | 4     | 32      | 32x500                               |
| Standard_H8r (RDMA支援)   | 8      | 112GB | 2,000GB      | 4     | 32      | 32x500                               |
| Standard_H16mr (RDMA支援) | 16     | 224GB | 2,000GB      | 4     | 32      | 32x500                               |

## 作業系統類型

Azure 虛擬機器支援 [Windows](https://zh.wikipedia.org/wiki/Windows "wikilink") 與 [Linux](../Page/Linux.md "wikilink") 作業系統，並且依 Azure 與其協力廠商或夥伴的合作關係，提供有預先搭載軟體的虛擬機器映像 (Image)。

### Linux

Azure 支援下列 Linux 作業系統：

  - [OpenLogic](https://zh.wikipedia.org/wiki/OpenLogic "wikilink") [CentOS](../Page/CentOS.md "wikilink") 6.3+, 7.0+
  - [CoreOS](../Page/CoreOS.md "wikilink") 494.4.0+
  - [Debian](../Page/Debian.md "wikilink") 7.9+, 8.2+
  - [Oracle Linux](../Page/Oracle_Linux.md "wikilink") 6.4+, 7.0+
  - [Red Hat Enterprise Linux](../Page/Red_Hat_Enterprise_Linux.md "wikilink") 6.7+, 7.1+
  - [SUSE](../Page/SUSE.md "wikilink") Linux Enterprise 11 SP3+, 12+, SLES for SAP 11.3+
  - [OpenSUSE](../Page/OpenSUSE.md "wikilink") 13.1+
  - [Ubuntu](../Page/Ubuntu.md "wikilink") 12.04, 14.04, 15.04, 15.10

### Windows

Azure 支援下列 Windows 作業系統:

  - [Windows Server 2008 R2](../Page/Windows_Server_2008_R2.md "wikilink") SP1
  - [Windows Server 2012](../Page/Windows_Server_2012.md "wikilink")
  - [Windows Server 2012 R2](https://zh.wikipedia.org/wiki/Windows_Server_2012_R2 "wikilink")
  - [Windows Server 2016](../Page/Windows_Server_2016.md "wikilink")
  - [Windows 7](https://zh.wikipedia.org/wiki/Windows_7 "wikilink")、[Windows 8](https://zh.wikipedia.org/wiki/Windows_8 "wikilink")、[Windows 8.1](../Page/Windows_8.1.md "wikilink")、[Windows 10](../Page/Windows_10.md "wikilink") 等用戶端作業系統 (僅有 MSDN 訂閱戶才能使用)

### 預載軟體

Azure 除了提供標準作業系統的映像外，也有提供數種已經預載合作廠商或微軟自家產品的虛擬機器映像，讓管理人員一開始就能擁有已設定好的虛擬機器，不過此類虛擬機器的費用會比僅有標準作業系統的虛擬機器要高，因為費用已內含授權費。企業也可以利用授權可攜性 (License Mobility) 將企業內已採購的授權移到 Azure 虛擬機器使用，而微軟的虛擬機器也可以另製成映像下載到地端使用，但當映像下載到地端時，其軟體的版權就必須自負。

  - Red Hat Enterprise Linux
  - SQL Server 2014
  - BizTalk Server 2013
  - SharePoint Server 2013
  - Oracle (有 Oracle Database 與 Oracle WebLogic Server)

除了 Azure 入口網內提供的映像外，在 Azure Marketplace 內也有其他預載軟體的虛擬機器，其費用以標準作業系統類型計算，但內含的軟體授權必須自行準備。

## 磁碟類型

一台已部署完成的 Azure 虛擬機器，其初始的磁碟有兩個，一個是作業系統本身的磁碟機 (C:\\ 或 /dev/sda)，這個磁碟機是保存在 [Microsoft Azure 儲存體](../Page/Microsoft_Azure_儲存體.md "wikilink") 內的 VHD，又稱為 **作業系統磁碟 (OS Disk)**，最大容量 127GB，Azure 供應的標準作業系統都是採用這個規格建置，若是由企業自行使用 [Hyper-V](https://zh.wikipedia.org/wiki/Hyper-V "wikilink") 製作的映像，則視當時製作時使用的大小決定，但不可超過 127GB (這是 VHD 的技術限制)。

另一個是虛擬機器所在的實體伺服器上的硬碟 (D:\\ 或 /dev/sdb)，依虛擬機器的類型不同，可以是 SATA 磁碟機 (A 類型) 或是 SSD 磁碟機 (D 與 G 類型)，但它們的共通點是，它們都只適合用來暫存資料，因此被稱為**暫存磁碟機 (Temporary Disk)**，這是基於 Azure 平台會自主偵測虛擬機器健康狀態，當 Azure 發現虛擬機器沒有回應時，就會啟動復原機制，將虛擬機移到另一台實體伺服器啟動，這時原本存在暫存磁碟機的資料並不會跟隨移動過去，所以暫存磁碟機不能用來儲存持久性資料，而是用來處理應用程式所產生的暫存性資料，或是作為緩衝區使用。

若需要在虛擬機器上保存永久性資料，則應該另外建置**資料磁碟 (Data Disk)**並附掛到虛擬機器內 (E:\\ 起，或是 /dev/sdc 起)，不同等級的虛擬機器可掛的資料磁碟有限制，從 1 台到 16 台不等，資料磁碟是建置於 Azure 儲存體之上，所以具有可持久的保存能力，而且也享有 Azure 儲存體所提供的 SLA 水準。

## 網路功能

Azure 虛擬機器的網路功能是依賴[虛擬網路服務的網路連線能力](../Page/Microsoft_Azure_虛擬網路服務.md "wikilink")，早期 Azure 虛擬機器是由 Azure 自行管理的大型虛擬網路組態所供應，但 2014 年起，微軟配合 Resource Group 管理模式的導入，強制要求 Azure 虛擬機器必須部署在由使用者自行建置的 Azure 虛擬網路內，其內部的 IP 管理亦由 Azure 虛擬網路負責。

虛擬機器對 Internet 的網路有兩種模式，一種是由 Azure 負載平衡器 (Azure Load Balancer) 提供，早期 Azure 虛擬機器對外的 IP 資源是一開始就會配給，而這也是 Azure 的計費基準之一，稱為 Azure Public IP (公用 IP)，虛擬機器一開機就會配給，一關機就會釋放，所以 IP 位址不穩定，若要讓 IP 穩定，就需要使用保留 IP (Reserved IP)，保留 IP 需特別建立並設定給虛擬機器。DNS 名稱則是由 [Azure 雲端服務](../Page/Microsoft_Azure_雲端服務.md "wikilink") 提供，Azure 雲端服務會在 Azure 負載平衡器上註冊 DNS (\*.cloudapp.net)，所有與此雲端服務關聯的虛擬機器都使用這個 DNS 連入，同時 Azure 負載平衡器上的通訊埠也是由Azure 雲端服務管理。

2015年，在 Resource Group 的管理模式下，虛擬機器的網路資源被拆分出來，IP、負載平衡器、網路安全群組、網路卡 (NIC) 等個別的負責各自的工作。

  - 網路卡：負責虛擬機器與網路的聯繫，一台虛擬機器可配置的網路卡數量依其等級決定。
  - 負載平衡器: 由網路卡決定要連線的負載平衡器，可以是 Azure 負載平衡器或是內部的負載平衡器。
  - 網路安全群組: 負責網路的通訊埠存取控制表管理。
  - IP: 配置在網路卡上，可以是內部虛擬網路的 IP 或是公用 IP，且可以不配置公用 IP。

## 管理方式

虛擬機器建置完成後，可採用遠端桌面 (Remote Desktop) 或是 [SSH](https://zh.wikipedia.org/wiki/SSH "wikilink") 的連線方式連至虛擬機器進行管理。

對虛擬機器的組態，則有幾個管道能進行:

  - Azure PowerShell 的虛擬機器管理指令 (AzureRM.Compute)
  - Azure CLI 的虛擬機器管理指令
  - Azure Portal
  - Azure RDFE API，外部工具都是使用這個管道，例如 System Center Virtual Machine Manager (SCVMM) 或 System Center App Controller 等。

## 高可用度與擴展

為達成高可用度 (High Availability)，Azure 虛擬機器採用了可用集 (Availability Set) 的概念 \[3\]，可用集規範了虛擬機器的失效域配置 (Fault Domain)，當虛擬機器部署在同一個可用集時，其實體的部署就不會放在同一個機架 (Rack) 的伺服器內，而是會分散配置，以避免因為機架出問題導致的單點失效問題。系統管理人員可依需求設定一個或多個可用集來配置虛擬機器，以提升可用度。同時，若需要實作跨區域的高可用度，系統管理人員也可以利用[Azure站台復原](https://zh.wikipedia.org/wiki/Azure站台復原 "wikilink") (Azure Site Recovery) 備援服務處理虛擬機器雲端對雲端的備援工作。

Azure 虛擬機器支援橫向 (Scale Out/In) 自動擴展 (Auto Scale)，與手動的縱向擴展 (Scale Up/Down)，縱向擴展可用指令或是在 Azure Portal 操作，橫向擴展則需要由系統管理人員事先部署好相同等級規格的虛擬機器後，利用 Azure Portal 進行設定。但為了要簡化此類部署的時間與成本，微軟開發了新一代的部署技術，稱為虛擬機器擴展集 (VM Scale Set)\[4\]，利用資源範本的能力，讓系統管理員預先設定好具相同規範 (虛擬機器本身的組態與網路組態等) 的虛擬機器群，等待需要擴展時，再由制定好的規範產生虛擬機器即可。

## 參考

<references />

[Category:微軟](https://zh.wikipedia.org/wiki/Category:微軟 "wikilink") [Category:Microsoft_Azure](https://zh.wikipedia.org/wiki/Category:Microsoft_Azure "wikilink")

1.  [虛擬機器的大小](https://azure.microsoft.com/zh-tw/documentation/articles/virtual-machines-size-specs/)
2.  [More GPUs, more power, more intelligence](https://azure.microsoft.com/zh-tw/blog/more-gpus-more-power-more-intelligence/)
3.  [管理虛擬機器的可用性](https://azure.microsoft.com/zh-tw/documentation/articles/virtual-machines-manage-availability/)
4.  [虛擬機器調整集概觀](https://azure.microsoft.com/zh-tw/documentation/articles/virtual-machines-vmss-overview/)