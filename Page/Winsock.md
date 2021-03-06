> 本文内容由[Winsock](https://zh.wikipedia.org/wiki/Winsock)转换而来。


**Windows Sockets API (WSA)**, 简短记为**Winsock**, 是[Windows的](https://zh.wikipedia.org/wiki/Microsoft_Windows "wikilink")[TCP/IP网络编程接口](https://zh.wikipedia.org/wiki/TCP/IP "wikilink")（API）。兼容于[Berkeley socketsAPI在函数名字](https://zh.wikipedia.org/wiki/Berkeley_sockets "wikilink")。实际上，Winsock的实现库(winsock.dll)使用的是长名字。

Winsock是一种能使Windows程序通过任意网络传输协议发送数据的API。Winsock中有几个只支持TCP/IP协议的函数（例如gethostbyaddr()），但是在Winsock 2中新增了所有这些函数的通用版本，以允许开发者使用其它的传输协议。

## 历史

MS-DOS与早期版本的Microsoft Windows使用的网络协议是[NetBIOS](../Page/NetBIOS.md "wikilink"). 因此，各方提供了各自的MS-DOS上的TCP/IP实现。由于各种解决方案的API函数名并不统一，使得软件开发者难以下决心转到TCP/IP协议上。

1991年10月，以Martin Hall, Mark Towfiq, Geoff Arnold, Henry Sanders为首在[CompuServe](../Page/CompuServe.md "wikilink") [BBS](../Page/BBS.md "wikilink")上讨论形成了Windows Sockets API规范(specification)并且版权属于这五人。

### 规范版本

  - Version 1.0 (1992年6月) 虽然不限于TCP/IP, 但TCP与UDP是仅有被明确提到的网络协议。
  - Version 1.1 (1993年1月) 很多小的修正与澄清。Winsock以[Windows消息的形式发送通知](https://zh.wikipedia.org/wiki/Windows消息 "wikilink")，使程序无需担心并发性。
  - Winsock 2 [向后兼容Winsock](https://zh.wikipedia.org/wiki/向后兼容 "wikilink") 1.1，还增加了协议独立的名字解析，异步操作（基于事件通知与完成过程(completion routine))， [多播](../Page/多播.md "wikilink"), [QoS](https://zh.wikipedia.org/wiki/QoS "wikilink"). 明文支持了多协议，包括[IPX/SPX与](https://zh.wikipedia.org/wiki/IPX/SPX "wikilink"). 增加了(SPI)与[分层协议实现](https://zh.wikipedia.org/wiki/Layered_Service_Provider "wikilink").
      - Versions 2.0.x (1994年5月)草案没有正式公开发布。
      - Version 2.1.0 (1996年1月)是Winsock 2首次公开的规范。定义了两种接口：一是应用程序接口（API），这种接口将开发者和底层隔离开；二是服务提供接口（SPI），这种接口允许对Winsock协议栈的扩展。对多种传输协议的官方支持。Winsock 2的规范中写入了对OSI、Novell IPX/SPX和Digital DECNet的官方支持。也添加了对一些诸如服务质量（QoS）、广播等技术创新的支持。[重叠I/O机制下工作](https://zh.wikipedia.org/wiki/重叠I/O "wikilink")。
      - Version 2.2.0 (1996年5月)包含很多小的矫正与澄清，并且不再支持16位Windows应用程序.
      - Version 2.2.1 (1997年5月)与Version 2.2.2 (1997年8月)增加小的新功能。

[Windows 95 OSR2以后版本的Windows操作系统均支持Windows](../Page/Windows_95.md "wikilink") Sockets version 2.2。此外，Windows 95 with the Windows Socket 2 Update也支持WinSock 2.2。

Windows 95、[Windows NT 3.51及更早版本的Windows操作系统](https://zh.wikipedia.org/wiki/Windows_NT_3.51 "wikilink")，最高支持Windows Sockets version 1.1。

## 技术

WinSock编程时，可选择下述编程模型之一：

  - 同步阻塞模型：直接使用recv()与send()收发数据，是最直观与最基本的IO模型；
  - select模型，可以阻塞/非阻塞/超时返回等方式查询socket的状态；
  - WSAAsyncSelect函数把socket绑定到一个窗口句柄，socket的若干事件绑定到一个窗口消息（如WM_SOCKET_NOTIFY），来异步响应的模型；
  - WSAEventSelect函数把socket与其若干事件绑定到一个操作系统的同步event上，来异步响应的模型；配套的API函数有：WSACreateEvent、WSAResetEvent、WSAWaitForMultiEvents、WSAEnumNewWorkEvents
  - [Overlapped I/O事件通知模型](https://zh.wikipedia.org/wiki/Overlapped_I/O "wikilink")：使用WSA_FLAG_OVERLAPPED标志通过WSASocket创建一个套接字；使用WSASend、WSASendTo、WSARecv、WSARecvFrom、WSAIoctl、AcceptEx、TransmitFile等函数带一个WSAOVERLAPPED结构参数来发起重叠IO操作。WSACreateEvent函数创建所需要的事件对象。WSAWaitForMultipleEvents函数来等待该事件对象。再调用WSAGetOverlappedResult函数判断重叠IO操作是否成功完成。
  - [Overlapped I/O完成例程模型](https://zh.wikipedia.org/wiki/Overlapped_I/O "wikilink"),使用完成例程来通知socket事件；使用ReadFileEx和WriteFileEx，或WSARecv/WSASend，指定完成例程。
  - [完成端口模型](../Page/IOCP.md "wikilink")：首先使用CreateCompletionPort创建一个完成端口对象，然后把任意数量的socket或IO句柄绑定到该完成端口对象（通过CreateCompletionPort函数）。然后创建一批工作者线程，每个线程通过GetQueuedCompletionStatus就把自己绑定到完成端口对象。IO完成包在完成端口对象先进先出，挂在完成端口对象上的工作者线程按照后进先出调度执行以减少线程切换的代价。

Windows Sockets API规范包含两种接口：

  - API,用于应用程序开发者。

  - (SPI), 用于增加新的协议模块到操作系统。实际上，现在Windows上实现TCP/IP以外的网络协议并没有什么用途.

Windows Sockets的代码与设计是基于[Berkeley sockets](https://zh.wikipedia.org/wiki/Berkeley_sockets "wikilink")，此外还提供了额外的功能使得API遵从Windows编程模式（如[重叠I/O](https://zh.wikipedia.org/wiki/重叠I/O "wikilink")）. API函数名字都以前缀`WSA`开始, 例如`WSASend()`.

为了便于从[Unix向Windows移植网络程序的源代码](https://zh.wikipedia.org/wiki/Unix "wikilink")，Winsock提供了很多便利. 例如，[Unix应用程序能使用](https://zh.wikipedia.org/wiki/Unix "wikilink")记录网络错误与C运行时错误。Windows Sockets引入了专门的函数`WSAGetLastError()`以获取错误信息. 但很多[TCP/IP应用程序使用了](https://zh.wikipedia.org/wiki/TCP/IP "wikilink")[Unix的特性](https://zh.wikipedia.org/wiki/Unix "wikilink"), 如与。这使得源代码移植非常困难。

### 回复Ack的延时

当Microsoft TCP栈接收到一个数据包时，会启动一个200毫秒的计时器。当ACK确认数据包发出之后，计时器会复位。接收到下一个数据包时，会再次启动200毫秒的计时器。这称为TCP确认延迟机制(TCP Delayed acknowledge)，作用是接收到数据后延迟ACK的发送，使得TCP协议栈有机会合并多个ACK以提高性能。Microsoft TCP栈使用了下面的策略来决定在接收到数据包后什么时候发送ACK确认数据包：

1.  如果在200毫秒的计时器超时之前，接收到下一个数据包，则立即发送ACK确认数据包。
2.  如果当前恰好有数据包需要发给ACK确认信息的接收端，则把ACK确认信息附带在数据包上立即发送。
3.  当计时器超时，ACK确认信息立即发送。

### 发送小尺寸数据时默认采用Nagle算法拼接为大数据包

为了避免小数据包拥塞网络，Microsoft TCP栈默认启用了[納格算法](../Page/納格算法.md "wikilink")，这个算法能够将应用程序多次调用Send发送的小尺寸的数据拼接起来，一块封包发送。Nagle算法规定的特殊情况：

1.  如果Microsoft TCP栈拼接起来的数据超过了MSS值，这个数据会立即发送，而不等待前一个数据包的ACK确认信息。以太网MTU(Maximum Transmission Unit)是1460字节。
2.  如果以前发送的数据都收到了回复的Ack，那么当前的数据会立即发送，而没有延迟。
3.  如果等待超时（例如200ms）仍然没有拼成一个MSS的数据包，当前的数据会被发送。
4.  如果设置了TCP_NODELAY选项，就会禁用Nagle算法，应用程序调用Send发送的数据包会立即被投递到网络，而没有延迟。

### Winsock的内核发送缓冲区与send函数的实现

为了在应用层优化性能，Winsock把应用程序调用Send发送的数据从应用程序的缓冲区复制到Winsock内核缓冲区。Microsoft TCP栈利用类似Nagle算法的方法，决定什么时候才实际地把数据投递到网络。内核缓冲区的默认大小是8K，使用SO_SNDBUF选项，可以改变Winsock内核缓冲区的大小。如果有必要的话，Winsock能缓冲大于SO_SNDBUF缓冲区大小的数据。在绝大多数情况下，应用程序完成Send调用仅仅表明数据 被复制到了Winsock内核缓冲区，并不能说明数据就实际地被投递到了网络上。例外情况：通过设置SO_SNDBUT为0禁用了Winsock内核缓冲区。

Winsock使用下面的规则来向应用程序表明一个Send调用的完成：

1.  如果socket仍然在SO_SNDBUF限额内，Winsock复制应用程序要发送的数据到内核缓冲区，完成Send调用。
2.  如果Socket超过了SO_SNDBUF限额并且先前只有一个被缓冲的发送数据在内核缓冲区，Winsock复制要发送的数据到内核缓冲区，完成Send调用。
3.  如果Socket超过了SO_SNDBUF限额并且内核缓冲区有不只一个被缓冲的发送数据，Winsock复制要发送的数据到内核缓冲区，然后投递数据到网络，直到Socket降到SO_SNDBUF限额内或者只剩余一个要发送的数据，才完成Send调用。

## 实现

### Microsoft实现

  - Microsoft未提供Winsock 1.0实现.
  - Version 1.1作为插件包(称为Wolverine)用于Windows for Workgroups (代号**Snowball**). 它是Windows 95与[Windows NT](../Page/Windows_NT.md "wikilink") 3.5版以后的组成部分。
  - Version 2.1是Windows 95的插件包. 它是[Windows 98](../Page/Windows_98.md "wikilink"), [Windows NT 4.0及其以后版本的组成部分](../Page/Windows_NT_4.0.md "wikilink")。 Microsoft不提供Windows 3.x或Windows NT 3.x的Winsock 2实现。

Winsock1.1 API，需要声明\#include \<winsock.h\>并链接wsock32.lib，使用wsock32.dll。

Winsock2 API，需要声明\#include \<winsock2.h\>，链接ws2_32.lib，在Winsock2_32.dll中实现。 其下是两种服务提供者接口（Service Provider Interface）：

  - Transport SPI: 提供建立连接、数据传输、QoS、错误处理等功能。rsvpsp.dll实现了RSVP QoS；mswsock.dll实现了Winsock core。
  - NameSpace SPI：名字解析，如getXXXbyYYY等函数。支持TCP/IP、NT DS、NLA等命名空间。

可通过ws2spi.h中的两对API函数来安装/卸载服务提供者接口：WSCInstallProvider、WSCDeinstallProvider、WSCInstallNameSpace、WSCUnInstallNameSpace。

SPOrder.dll中提供了重排序服务提供者：WSCWriteNameSpaceOrder、WSCWriteProviderOrder。

大部分Winsock2 API函数被映射到SPI函数，由当前安装的服务提供者实现其功能。一条简单规则是根据提供者链顺序从WSA\*函数名映射为WSP\*函数名（Winsock Service Provider, 用于传输服务提供者函数）。下述函数不在SPI中实现：

  - 事件处理函数与等待函数，直接映射到Windows API:
      - WSACreateEvent,
      - WSACloseEvent,
      - WSASetEvent,
      - WSAResetEvent
      - WSAWaitForMultipleEvents
  - 名字服务函数:
      - 特定IP名字转换函数与名字解析函数：Winsock 1.1的GetXXXByYYY以及WSAAsyncGetXXXbyYYY, WSACancelAsyncRequest, gethostname等。
      - 支持（support）函数： ntohs, ntohl, htonl, htons
      - IP转换函数：inet_XtoY, inet_addr, ...
  - 错误处理函数：WSAGetLastError, WSASetLastError
  - 其他函数
      - WSAEnumProtocols
      - WSAIsBlocking,
      - WSASetBlockingHook,
      - WSAUnhookBlockingHook

WSP前缀（Winsock Service Provider）的函数是传输服务提供者函数。例如WSPStartup函数用于初始化分层服务提供者。

WPU前缀（Winsock Provider Upcall）的函数是被服务提供者调用的ws2_32.dll中的函数，

WSC前缀(WinSock Configuration)的函数名是LSP安装程序调用的ws2_32.dll中的函数，如：WSCInstallProvider， WSCWriteProviderOrder。

NSP前缀（NameSpace Provider）的函数名用于命名空间提供者。

service provider interface (SPI)是各种功能的具体实施者。允许插入第三方厂商写的 service providers 而无需改变Winsock 2 的API与DLL（ws2_32.dll）；从而应用程序开发人员写的基于Winsock的代码也无需改变 。

Winsock 2 SPI 有两种类型的 service providers —— transport 和 namespace。Transport providers（通常称之为协议栈）提供建立连接、传输数据、进行流控制和差错控制等功能。Namespace providers 提供网络协议的寻址属性、协议无关的名字解析。

SPI transport service providers细分为两类 —— base service providers 和 layered service providers。Base service providers 实现了传输协议的实际细节：建立连接、传送数据、流控制和差错控制。Layered service providers 仅实现了高层的自定义的通讯功能，而且依赖于已有的下层的 base provider 来与远程端进行实际的数据交换。也就是说，LSP是做什么的，就是做一些附件的高端的可选的功能。如在 base TCP/IP 栈的顶端实现一个带宽管理器。 而base service providers提供必需的基础的功能。

Winsock 2不允许 namespace providers 的LSP。虽然可以使用 Winsock 2 SPI 来实现一个新的 namespace provider，但是不能改变或扩展已有 namespace provider 的命名、注册和查询行为。

layered transport service provider一般由高层应用开发；而 base transport providers 和 namespace providers 一般由操作系统厂商和协议栈厂商开发。

编写 service provider的就是标准的DLL，其导出函数只有运输服务的WSPStartup 或名字服务的 NSPStartup。WSPStartup 和 NSPStartup通过输出参数lpProcTable作为LSP的dispatch table，提供了约30个可用的函数的地址，这些函数原型在WS2spi.h中声明。WSPStartup的另外一个参数UpcallTable为LSP提供了ws2_32.dll中的15个函数的地址表，这些函数原型也在WS2spi.h中声明。如果ws2_32.dll提供了额外的函数，就需要在WSPStartup通过GetProcAddress获取函数地址，目前仅有一个例子WPUCompleteOverlappedResult。

LSP可以形成一个链，通过调用下层LSP的WSPStartup函数，下层LSP由上层LSP装入。最上层的LSP被ws2_32.dll装入。WSPStartup函数参数lpProtocolInfo指向一个WSAPROTOCOL_INFOW结构组成的链表。链表最底层是base provider。 WSPStartup与WSPCleanup使用引用计数来加载/清除。

### 其他实现

遵从Winsock规范的TCP/IP与UDP/IP协议栈有：[3Com](../Page/3Com.md "wikilink"), Beame & Whiteside, DEC, Distinct, [FTP Software](https://zh.wikipedia.org/wiki/FTP_Software "wikilink"), Frontier, [IBM](../Page/IBM.md "wikilink"), Microdyne, , [Novell](../Page/Novell.md "wikilink"), [Sun Microsystems](https://zh.wikipedia.org/wiki/Sun_Microsystems "wikilink"), Trumpet Software International\[1\].

## 例子

### 列出所有服务提供者

``` cpp
/**
* Winsock 2 API Protocol Enumerator -
*/
#ifndef WIN32_LEAN_AND_MEAN
#define WIN32_LEAN_AND_MEAN
#endif
#define WINSOCK_API_LINKAGE
#include <winsock2.h>
#include <ws2spi.h>
#include <wtypes.h>
#include <assert.h>
#include <winnt.h>
#include <stdlib.h>
#include <stdio.h>
#pragma comment(lib,"Ws2_32.lib")
char *ExpandServiceFlags(DWORD serviceFlags)
{
    /* A little utility function to make sense of all those bit flags */
    /* The following code leaks. Yeah, I know.. Go find Buffer 0v3rfl0w$ :-) */
    char *serviceFlagsText = (char *)malloc(2048);
    memset(serviceFlagsText, '\0', 2048);
    char *strip_comma;
    /* Hey - it's only for printing and demo purposes.. */
    if (serviceFlags & XP1_CONNECTIONLESS)
    {
        strcat(serviceFlagsText, "Connectionless, ");
    }
    if (serviceFlags & XP1_GUARANTEED_ORDER)
    {
        strcat(serviceFlagsText, "Guaranteed Order, ");
    }
    if (serviceFlags & XP1_GUARANTEED_DELIVERY)
    {
        strcat(serviceFlagsText, "Message Oriented, ");
    }
    if (serviceFlags & XP1_CONNECT_DATA)
    {
        strcat(serviceFlagsText, "Connect Data, ");
    }
    if (serviceFlags & XP1_DISCONNECT_DATA)
    {
        strcat(serviceFlagsText, "Disconnect Data, ");
    }
    if (serviceFlags & XP1_SUPPORT_BROADCAST)
    {
        strcat(serviceFlagsText, "Broadcast Supported, ");
    }
    if (serviceFlags & XP1_EXPEDITED_DATA)
    {
        strcat(serviceFlagsText, "Urgent Data, ");
    }
    if (serviceFlags & XP1_QOS_SUPPORTED)
    {
        strcat(serviceFlagsText, "QoS supported, ");
    }
    /*
    * While we're quick and dirty, let's get as dirty as possible..
    */
    strip_comma = strrchr(serviceFlagsText, ',');
    if (strip_comma)
        *strip_comma = '\0';
    return (serviceFlagsText);
}
void PrintProtocolInfo(LPWSAPROTOCOL_INFOW prot)
{
    wprintf(L"Protocol Name: %s\n", prot->szProtocol); /* #%^@$! UNICODE...*/
    printf("\tServiceFlags1:  %d (%s)\n",
        prot->dwServiceFlags1,
        ExpandServiceFlags(prot->dwServiceFlags1));
    printf("\tProvider Flags: %d\n", prot->dwProviderFlags);
    printf("\tNetwork Byte Order: %s\n",
        (prot->iNetworkByteOrder == BIGENDIAN) ? "Big Endian" : "Little Endian");
    printf("\tVersion: %d\n", prot->iVersion);
    printf("\tAddress Family: %d\n", prot->iAddressFamily);
    printf("\tSocket Type: ");
    switch (prot->iSocketType)
    {
    case SOCK_STREAM:
        printf("STREAM\n");
        break;
    case SOCK_DGRAM:
        printf("DGRAM\n");
        break;
    case SOCK_RAW:
        printf("RAW\n");
        break;
    default:
        printf(" Some other type\n");
    }
    printf("\tProtocol: ");
    switch (prot->iProtocol)
    {
    case IPPROTO_TCP:
        printf("TCP/IP\n");
        break;
    case IPPROTO_UDP:
        printf("UDP/IP\n");
        break;
    default:
        printf("some other protocol\n");
    }
}
int _cdecl main(int argc, char** argv)
{
    LPWSAPROTOCOL_INFOW  bufProtocolInfo = NULL;
    DWORD                dwSize = 0;
    INT                  dwError;
    INT                  iNumProt;
    /*
    * Enum Protocols - First, obtain size required
    */
    printf("Sample program to enumerate Protocols\n");
    WSCEnumProtocols(NULL,                     // lpiProtocols
        bufProtocolInfo,          // lpProtocolBuffer
        &dwSize,                 // lpdwBufferLength
        &dwError);               // lpErrno
    bufProtocolInfo = (LPWSAPROTOCOL_INFOW)malloc(dwSize);
    if (!bufProtocolInfo) {
        fprintf(stderr, "SHOOT! Can't MALLOC!!\n");
        exit(1);
    }
    /* Now, Enum */
    iNumProt = WSCEnumProtocols(
        NULL,                    // lpiProtocols
        bufProtocolInfo,         // lpProtocolBuffer
        &dwSize,                 // lpdwBufferLength
        &dwError);
    if (SOCKET_ERROR == iNumProt)
    {
        fprintf(stderr, "Darn! Can't Enum!!\n");
        exit(1);
    }
    printf("%d Protocols detected:\n", iNumProt);
    for (int i = 0;
    i < iNumProt;
        i++)
    {
        PrintProtocolInfo(&bufProtocolInfo[i]);
        printf("-------\n");
    }
    printf("Done");
    return(0);
}
```

### 阻塞式程序

``` cpp
    int nPort =65000;//指定通信端口
    WSADATA wsaData;
    WSAStartup( MAKEWORD( 2, 2 ), &wsaData );

     // 创建监听套接字，绑定本地端口，开始监听
    SOCKET sListen = socket( AF_INET,SOCK_STREAM, 0 );
    SOCKADDR_IN addr;
    addr.sin_family = AF_INET;
    addr.sin_port = htons( nPort );
    addr.sin_addr.S_un.S_addr = INADDR_ANY;
    bind( sListen, (sockaddr *)&addr, sizeof( addr ) );
    listen( sListen, 5 );

    SOCKADDR_IN saRemote;
    int nRemoteLen = sizeof( saRemote );
    SOCKET sRemote = accept( sListen, (sockaddr *)&saRemote, &nRemoteLen );
```

### 优雅关闭

TCP连接的关闭过程有两种：

  - 优雅关闭（graceful close）如果发送缓存中还有数据未发出则其发出去，并且收到所有数据的ACK之后，发送FIN包，开始关闭过程
  - 强制关闭（hard close或abortive close）如果缓存中还有数据，则这些数据都将被丢弃，然后发送RST包，直接重置TCP连接。

<!-- end list -->

``` cpp
    shutdown(clntSock, SD_SEND);  //数据发送完毕，断开输出流，向客户端发送FIN包
    recv(clntSock, buffer, BUF_SIZE, 0);  //阻塞，等待客户端接收完毕后closesocket，这将导致本方的recv从阻塞状态返回
    fclose(fp);  //释放资源
    closesocket(clntSock);
    closesocket(servSock);  //也要关闭用于listen/accept的socket
    WSACleanup();
```

调用 close()/closesocket() 函数意味着完全断开连接，即不能发送数据也不能接收数据，这种“生硬”的方式有时候会显得不太“优雅”。使用 shutdown() 函数和WSASendDisconnect函数可以优雅关闭连接，其函数原型为

`int shutdown(SOCKET s, int howto);  //Windows  `

howto 在 Windows 下有以下取值：

  - SD_RECEIVE：关闭接收操作，也就是断开输入流。
  - SD_SEND：关闭发送操作，也就是断开输出流。
  - SD_BOTH：同时关闭接收和发送操作。

确切地说，close() / closesocket() 用来关闭套接字，将套接字描述符（或句柄）从内存清除，之后再也不能使用该套接字。应用程序关闭套接字后，与该套接字相关的连接和缓存也失去了意义，TCP协议会自动触发关闭连接的操作。shutdown() 用来关闭连接，而不是套接字；套接字依然存在，直到调用 close() / closesocket() 将套接字从内存清除。调用 close()/closesocket() 关闭套接字时，或调用 shutdown() 关闭输出流时，都会向对方发送 FIN 包。FIN 包表示数据传输完毕，对端收到 FIN 包就知道不会再有数据传送过来了。默认情况下，close()/closesocket() 会立即向网络中发送FIN包，不管输出缓冲区中是否还有数据，而shutdown() 会等输出缓冲区中的数据传输完毕再发送FIN包。也就意味着，调用 close()/closesocket() 将丢失输出缓冲区中的数据，而调用 shutdown() 不会。

shutdown()并不实际关闭socket，而是仅仅改变其可用性。shutdown是一种优雅地单方向或者双方向关闭socket的方法。 如果有多个进程共享一个socket，shutdown影响所有进程，而close只影响本进程。shutdown本身并不影响底层，也即此前发出的异步send/recv不会返回。在所有已发送的包被对端确认后，本方会发送FIN包给client，开始TCP四次挥手过程。 对端收到FIN报文后，并不知道server端以何种方式shutdown，甚至不知道server端是shutdown还是close。

若本方发送FIN报文后没有收到对端的FIN-ACK，会两次重传FIN报文，若一直收不到对端的FIN-ACK，则会给对端发送RST信号，关闭socket并释放资源。对端收到FIN信号后，再调用read函数会返回0；因为接收了FIN，表明以后再无数据可以接收。

对端收到RST报文后，行为如下：

  - 阻塞模型下，内核无法主动通知应用层出错，只有应用层主动调用read()或者write()这样的IO系统调用时，内核才会利用出错来通知应用层已经收到RST报文
  - 非阻塞模型下，select或者epoll会返回sockfd可读,应用层对其进行读取时，read()会报RST错误。

收到RST报文的情况下，再做任何read write都是毫无意义。

调用调用close()，根据参数设置不同，会出现如下两种情况：

  - l_onoff为非0，l_linger为0： 向对端发送一个RST报文，丢弃本地缓冲区的未读数据，关闭socket并释放相关资源，此种方式为强制关闭。
  - l_onoff 为非0，l_linger为非0：向对端发送一个FIN报文，收到对端FIN-ACK后，进入了FIN_WAIT_2阶段，参考TCP四次挥手过程，此种方式为优雅关闭。如果在l_linger的时间内仍未完成四次挥手，则强制关闭。

当l_onoff值设置为0时，closesocket会立即返回，并关闭用户socket句柄。如果此时缓冲区中有未发送数据，则系统会在后台将这些数据发送完毕后关闭TCP连接，是一个优雅关闭过程，但是这里有一个副作用就是socket的底层资源会被保留直到TCP连接关闭，这个时间用户应用程序是无法控制的。

当l_onoff值设置为非0值，而l_linger也设置为0，那么closesocket也会立即返回并关闭用户socket句柄，但是如果此时缓冲区中有未发送数据，TCP会发送RST包重置连接，所有未发数据都将丢失，这是一个强制关闭过程。

当l_onoff值设置为非0值，而l_linger也设置为非0值时，同时如果socket是阻塞式的，此时如果缓冲区中有未发送数据，如果TCP在l_linger表明的时间内将所有数据发出，则发完后关闭TCP连接，这时是优雅关闭过程；如果如果TCP在l_linger表明的时间内没有将所有数据发出，则会丢弃所有未发数据然后TCP发送RST包重置连接，此时就是一个强制关闭过程了。

另外还有一个socket选项SO_DONTLINGER，它的参数值是一个bool类型的，如果设置为true，则等价于SO_LINGER中将l_onoff设置为0。

注意SO_LINGER和SO_DONTLINGER选项只影响closesocket的行为，而与shutdown函数无关，shutdown总是会立即返回的。

## 参见

  - [Berkeley sockets](https://zh.wikipedia.org/wiki/Berkeley_sockets "wikilink")
  - [分层服务提供者](../Page/分层服务提供者.md "wikilink") (Winsock LSP)

## 参考文献

## 外部链接

  - [MSDN - Winsock2 Reference](http://msdn2.microsoft.com/en-us/library/ms741416.aspx)
  - [MSDN - Winsock2 Home](http://msdn2.microsoft.com/en-us/library/ms740673.aspx)
  - [Sockets FAQ](http://www.faqs.org/faqs/windows/winsock-faq) - Windows Sockets FAQ
  - [Client / Server Programming with TCP/IP Sockets](https://web.archive.org/web/20110124193213/http://devmentor.org/articles/network/Socket%20Programming%28v2%29.pdf) - Winsock C++ Programming
  - [Porting Berkley Socket programs to Winsock](http://msdn2.microsoft.com/en-us/library/ms740096.aspx)
  - [Windows Network Development blog](http://blogs.msdn.com/wndp/) — Microsoft developer blog covering Winsock, WSK, WinINet, Http.sys, WinHttp, QoS and System.Net, with a focus on features being introduced in [Windows Vista](../Page/Windows_Vista.md "wikilink")
  - [Brief History of Microsoft on the Web](http://www.microsoft.com/misc/features/features_flshbk.htm)
  - [Winsock error codes list](https://web.archive.org/web/20160922213937/http://winsock-error.danielclarke.com/) with descriptions
  - [WinSock Development Information](http://www.sockets.com/)
  - [Winsock Programmer's FAQ](http://tangentsoft.net/wskfaq/)

[Category:Windows_API](https://zh.wikipedia.org/wiki/Category:Windows_API "wikilink")

1.  [Trumpet Winsock v5.0](http://www.trumpet.com.au/index.php/downloads.html)