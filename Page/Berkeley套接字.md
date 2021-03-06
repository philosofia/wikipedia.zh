> 本文内容由[Berkeley套接字](https://zh.wikipedia.org/wiki/Berkeley套接字)转换而来。


[InternetSocketBasicDiagram_zhtw.png](https://zh.wikipedia.org/wiki/File:InternetSocketBasicDiagram_zhtw.png "fig:InternetSocketBasicDiagram_zhtw.png") **伯克利套接字**（） ，又稱為**BSD 套接字**()是一種[应用程序接口](../Page/应用程序接口.md "wikilink")（API），用於[网络套接字](https://zh.wikipedia.org/wiki/网络套接字 "wikilink")（ socket）與[Unix域套接字](https://zh.wikipedia.org/wiki/Unix域套接字 "wikilink")，包括了一个用[C语言写成的应用程序开发库](https://zh.wikipedia.org/wiki/C语言 "wikilink")，主要用于实现[进程间通讯](https://zh.wikipedia.org/wiki/进程间通讯 "wikilink")，在[计算机网络](../Page/计算机网络.md "wikilink")通讯方面被广泛使用。

Berkeley套接字（也作BSD套接字应用程序接口）刚开始是4.2BSD Unix操作系统（于1983发布）的一套应用程序接口。然而，由于[AT\&T](../Page/AT&T.md "wikilink")的专利保护着[UNIX](https://zh.wikipedia.org/wiki/UNIX操作系统 "wikilink")，所以只有在1989年[伯克利大学才能自由地发布自己的](https://zh.wikipedia.org/wiki/伯克利大学 "wikilink")[操作系统](../Page/操作系统.md "wikilink")和网络库。

Berkeley套接字应用程序接口形成了事实上的网络套接字的标准精髓。 大多数其他的编程语言使用与这套用C语言写成的应用程序接口\[1\] 类似的接口。 这套应用程序接口也被用于[Unix域套接字](https://zh.wikipedia.org/wiki/Unix域套接字 "wikilink")（Unix domain sockets），后者可以在单机上为[进程间通讯](https://zh.wikipedia.org/wiki/进程间通讯 "wikilink")（IPC）的接口。

这种基于流的传输层接口（TLI）为套接字应用程序接口提供了一种选择。 不过，最近提供TLI应用程序接口的的系统同时也提供Berkeley套接字应用程序接口。

## Berkeley套接字接口

**Berkeley套接字接口**，一个应用程序接口（API），使用一个Internet套接字的概念，使主机间或者一台计算机上的进程间可以通讯。 它可以在很多不同的输入/输出设备和驱动之上运行，尽管这有赖于操作系统的具体实现。 接口实现用于TCP/IP协议，因此它是维持Internet的基本技术之一。 它是由加利福尼亚的伯克利大学开发，最初用于Unix系统。 如今，所有的现代操作系统都有一些源于Berkeley套接字接口的实现，它已成为连接Internet的标准接口。

套接字接口的接入有三个不同的级别，最基础的也是最有效的就是raw socket级别接入。 很少的应用程序需要在外向通讯控制的这个级别接入，所以raw socket级别是只为了用于开发计算机Internet相关技术的。 最近几年，大多数的操作系统已经实现了对它的全方位支持，包括Windows XP。

## 使用Berkeley套接字的系统

由于Berkeley套接字是第一个socket，大多数程序员很熟悉它们，所以大量系统把伯克利套接字作为其主要的网络API。一个不完整的列表如下：

  - Windows Sockets (Winsock) ，和Berkeley Sockets很相似，最初是为了便于移植Unix程序。
  - Java Sockets
  - Python sockets
  - Perl sockets

## 头文件

Berkeley套接字接口的定义在几个头文件中。这些文件的名字和内容与具体的实现之间有些许的不同。 大体上包括：

:; `<sys/socket.h>`

  -

      -
        核心BSD套接字核心函数和数据结构。
        AF_INET、AF_INET6 地址集和它们相应的协议集PF_INET、PF_INET6. 广泛用于Internet，这些包括了IP地址和TCP、UDP端口号。

:; `<netinet/in.h>`

  -

      -
        AF_INET 和AF_INET6 地址家族和他们对应的协议家族 PF_INET 和 PF_INET6。在互联网编程中广泛使用，包括IP地址以及TCP和UDP端口号。

:; `<sys/un.h>`

  -

      -
        PF_UNIX/PF_LOCAL 地址集。用于运行在一台计算机上的程序间的本地通信，不用于网络通讯。

:; `<arpa/inet.h>`

  -

      -
        处理数值型IP地址的函数。

:; `<netdb.h>`

  -

      -
        将协议名和主机名翻译为数值地址的函数。搜索本地数据以及DNS。

## 套接字API函数

这个列表是一个Berkeley套接字API库提供的函数或者方法的概要：

  - `socket()` 创建一个新的确定类型的套接字，类型用一个整型数值标识（[文件描述符](../Page/文件描述符.md "wikilink")），并为它分配系统资源。
  - `bind()` 一般用于服务器端，将一个套接字与一个套接字地址结构相关联，比如，一个指定的本地端口和IP地址。
  - `listen()` 用于服务器端，使一个绑定的TCP套接字的tcp状态由CLOSE转至LISTEN；操作系统内核为此监听socket所对应的tcp服务器建立一个pending socket队列和一个established socket队列；参数backlog指定pending socket队列的长度，0表示长度可以无限大。pending socket，就是某客户端三次握手的syn包到达，内核为这个syn包对应的tcp请求生成一个socket（状态为SYN_RECV），但三次握手还没有完成时的socket。
  - `connect()` 用于客户端，为一个套接字分配一个自由的本地端口号。 如果是TCP套接字的话，它会试图获得一个新的TCP连接。
  - `accept()` 用于服务器端。 它接受一个从远端客户端发出的创建一个新的TCP连接的接入请求，创建一个新的套接字，与该连接相应的套接字地址相关联。
  - `send()`和`recv()`,或者`write()`和`read()`,或者`recvfrom()`和`sendto()`, 用于往/从远程套接字发送和接受数据。
  - `close()` 用于系统释放分配给一个套接字的资源。 如果是TCP，连接会被中断。
  - `gethostbyname()`和`gethostbyaddr()` 用于解析主机名和地址。
  - `select()` 用于修整有如下情况的套接字列表： 准备读，准备写或者是有错误。
  - `poll()` 用于检查套接字的状态。 套接字可以被测试，看是否可以写入、读取或是有错误。
  - `getsockopt()` 用于查询指定的套接字一个特定的套接字选项的当前值。
  - `setsockopt()` 用于为指定的套接字设定一个特定的套接字选项。

更多的细节如下给出。

### socket()

`socket()` 为通讯创建一个端点，为套接字返回一个[文件描述符](../Page/文件描述符.md "wikilink")。 socket() 有三个参数：

  - <var>domain</var> 为创建的套接字指定协议集（或称做地址族 address family)。 例如：
      - `AF_INET` 表示[IPv4](../Page/IPv4.md "wikilink")网络协议
      - `AF_INET6` 表示[IPv6](../Page/IPv6.md "wikilink")
      - `AF_UNIX` 表示本地套接字（使用一个文件）
  - <var>type</var>（socket类型）如下：
      - `SOCK_STREAM` （可靠的面向流服务或[流套接字](https://zh.wikipedia.org/wiki/流套接字 "wikilink")）
      - `SOCK_DGRAM` （数据报文服务或者[数据报文套接字](https://zh.wikipedia.org/wiki/数据报文套接字 "wikilink")）
      - `SOCK_SEQPACKET` （可靠的连续数据包服务）
      - `SOCK_RAW` (在网络层之上自行指定运输层协议头，即[原始套接字](../Page/原始套接字.md "wikilink"))
  - <var>protocol</var> 指定实际使用的传输协议。 最常见的就是[`IPPROTO_TCP`](../Page/传输控制协议.md "wikilink")、[`IPPROTO_SCTP`](https://zh.wikipedia.org/wiki/SCTP "wikilink")、[`IPPROTO_UDP`](../Page/用户数据报协议.md "wikilink")、[`IPPROTO_DCCP`](https://zh.wikipedia.org/wiki/DCCP "wikilink")。这些协议都在\<netinet/in.h\>中有详细说明。 如果该项为“`0`”的话，即根据选定的domain和type选择使用缺省协议。

如果发生错误，函数返回值为-1。 否则，函数会返回一个代表新分配的描述符的整数。

  - 原型：

<!-- end list -->

``` c
int socket(int domain, int type, int protocol);
```

„”

### bind()

`bind()` 为一个套接字分配地址。当使用`socket()`创建套接字后，只赋予其所使用的协议，并未分配地址。在接受其它主机的连接前，必须先调用bind()</code>为套接字分配一个地址。`bind()`有三个参数：

  - `sockfd`, 表示使用bind函数的套接字描述符
  - `my_addr`, 指向sockaddr结构（用于表示所分配地址）的指针
  - `addrlen`, 用socklen_t字段指定了sockaddr结构的长度

如果发生错误，函数返回值为-1，否则为0。

  - 原型:

<!-- end list -->

``` c
int bind(int sockfd, const struct sockaddr *my_addr, socklen_t addrlen);
```

### listen()

当socket和一个地址绑定之后，`listen()`函数会开始监听可能的连接请求。然而，这只能在有可靠数据流保证的时候使用，例如：数据类型(`SOCK_STREAM`, `SOCK_SEQPACKET`)。

listen()函数需要两个参数：

  - `sockfd`, 一个socket的描述符.
  - `backlog`, 完成三次握手、等待accept的全连接的队列的最大长度上限。对于AF_INET类型的socket，全连接数量为：min(backlog, somaxconn)。当队列满时，新的全连接会返回错误。somaxconn默认为128.半连接队列的最大长度可通过sysctl函数设置tcp_max_syn_backlog，默认值为256。Linux Kernel 2.2之后，全连接队列与半连接队列分别叫做accept queue与syns queue。根据/proc/sys/net/ipv4/tcp_abort_on_overflow里的值为0表示如果三次握手第三步的时候全连接队列满了，那么server扔掉client发过来的ack，server过一段时间再次发送syn+ack给client（也就是重新走握手的第二步），如果client超时等待比较短，就很容易异常；tcp_abort_on_overflow为1表示第三次握手时如果全连接队列满了，server发送一个reset包给client，表示废掉这个握手过程和这个连接。

一旦连接被接受，返回0表示成功，错误返回-1。

**原型**:

``` c
int listen(int sockfd, int backlog);
```

### accept()

当应用程序监听来自其他主机的面对数据流的连接时，通过事件（比如Unix select()系统调用）通知它。必须用 `accept()`函数初始化连接。 Accept() 为每个连接创立新的套接字并从监听队列中移除这个连接。它使用如下参数：

  - `sockfd`,监听的套接字描述符
  - `cliaddr`, 指向sockaddr 结构体的指针，客户机地址信息。
  - `addrlen`,指向 `socklen_t`的指针，确定客户机地址结构体的大小 。

返回新的套接字描述符，出错返回-1。进一步的通信必须通过这个套接字。

Datagram 套接字不要求用accept()处理，因为接收方可能用监听套接字立即处理这个请求。

  - 函数原型：

<!-- end list -->

``` c
int accept(int sockfd, struct sockaddr *cliaddr, socklen_t *addrlen);
```

### connect()

`connect()`系统调用为一个套接字设置连接，参数有文件描述符和主机地址。

某些类型的套接字是无连接的，大多数是UDP协议。对于这些套接字，连接时这样的：默认发送和接收数据的主机由给定的地址确定，可以使用 send()和 recv()。 返回-1表示出错，0表示成功。

  - 函数原型：

<!-- end list -->

``` c
int connect(int sockfd, const struct sockaddr *serv_addr, socklen_t addrlen);
```

### select()

`int select (int nfds, fd_set FAR * readfds, fd_set FAR * writefds, fd_set FAR * exceptfds, const struct timeval FAR * timeout); `

  - 第一个参数nfds：沒有用，仅仅为与伯克利Socket兼容而提供。
  - 第二个参数readfds：指定一個Socket数组，select检查该数组中的所有Socket。如果成功返回，则readfds中存放的是符合‘可读性’条件的数组成员（如缓冲区中有可读的数据）。
  - 第三个参数writefds：指定一个Socket数组，select检查该数组中的所有Socket。如果成功返回，则writefds中存放的是符合‘可写性’条件的数组成员（包括连接成功）。
  - 第四个参数exceptfds：指定一个Socket数组，select检查该数组中的所有Socket。如果成功返回，则cxceptfds中存放的是符合‘有异常’条件的数组成员（包括连接接失败）。
  - 第五个参数timeout：指定select执行的最长时间，如果在timeout限定的时间内，readfds、writefds、exceptfds中指定的Socket沒有一个符合要求，就返回0。

### getsockname() 和 getpeername ()

`int getsockname (SOCKET s, struct sockaddr *name, int* namelen);`

getsockname函数获取已绑定（可能是未调用bind的系统自动绑定）的套接口本地协议地址。

`int getpeername (SOCKET s, struct sockaddr *name, int* namelen);`

getpeername函数获得与指定套接口连接的远程信息（IP:PORT）。

### gethostbyname() 和 gethostbyaddr()

`gethostbyname()` 和 `gethostbyaddr()`函数是用来解析主机名和地址的。可能会使用DNS服务或者本地主机上的其他解析机制（例如查询/etc/hosts）。返回一个指向 <var>struct hostent</var>的指针，这个结构体描述一个[IP主机](https://zh.wikipedia.org/wiki/IP "wikilink")。函数使用如下参数：

  - <var>name</var> 指定主机名。例如 www.wikipedia.org
  - <var>addr</var> 指向 <var>struct in_addr</var>的指针，包含主机的地址。
  - <var>len</var> 给出 <var>addr</var>的长度，以字节为单位。
  - <var>type</var> 指定地址族类型 （比如 AF_INET）。

出错返回NULL指针，可以通过检查 <var>h_errno</var> 来确定是临时错误还是未知主机。正确则返回一个有效的 <var>struct hostent \*</var>。

这些函数并不是伯克利套接字严格的组成部分。这些函数可能是过时了，只能处理IPv4地址。在IPv6中，替代的新函数是 [getaddrinfo() and getnameinfo()](https://zh.wikipedia.org/wiki/getaddrinfo "wikilink"), 这些新函数是基于[*addrinfo*数据结构](https://zh.wikipedia.org/wiki/getaddrinfo#struct_addrinfo "wikilink")。参考\<Ws2tcpip.h\>。

  - 函数原型：

<!-- end list -->

``` c
struct hostent *gethostbyname(const char *name);
struct hostent *gethostbyaddr(const void *addr, int len, int type);
```

### setsockopt()

`int setsockopt(int sockfd, int level, int optname, void *optval, socklen_t *optlen);  --设置套接字选项`

参数：

  - sockfd: 套接字
  - level: 协议层 SOL_SOCKET/IPPROTO_IP/IPPRO_TCP
  - optname: 选项名 每一个协议层都有其固定的选项名
  - optval: 缓冲区 set是指向将要存放的地址, get是指向目前存放信息的地址
  - optlen: 缓冲区大小长度

在socket层, 有以下一些选项:

  - SO_BROADCAST 允许发送广播数据 int
  - SO_DEBUG　　　　　　　　允许调试　　　　　　　　　　　　　　　　int
  - SO_DONTROUTE　　　　　　不查找路由　　　　　　　　　　　　　　　int
  - SO_ERROR　　　　　　　　获得套接字错误　　　　　　　　　　　　　int
  - SO_KEEPALIVE　　　　　　保持连接　　　　　　　　　　　　　　　　int
  - SO_LINGER　　　　　　　 延迟关闭连接　　　　　　　　　　　　　　struct linger
  - SO_OOBINLINE　　　　　　带外数据放入正常数据流　　　　　　　　　int
  - SO_RCVBUF　　　　　　　 接收缓冲区大小　　　　　　　　　　　　　int
  - SO_SNDBUF　　　　　　　 发送缓冲区大小　　　　　　　　　　　　　int
  - SO_RCVLOWAT　　　　　　 接收缓冲区下限　　　　　　　　　　　　　int
  - SO_SNDLOWAT　　　　　　 发送缓冲区下限　　　　　　　　　　　　　int
  - SO_RCVTIMEO　　　　　　 接收超时　　　　　　　　　　　　　　　　struct timeval
  - SO_SNDTIMEO　　　　　　 发送超时　　　　　　　　　　　　　　　　struct timeval
  - SO_REUSERADDR　　　　　 允许重用本地地址和端口　　　　　　　　　int
  - SO_TYPE　　　　　　　　 获得套接字类型　　　　　　　　　　　　　int
  - SO_BSDCOMPAT　　　　　　与BSD系统兼容　　　　　　　　　　　　　 int

### ioctlsocket

`int ioctlsocket(_In_ SOCKET s,  _In_ long   cmd,   _Inout_ u_long *argp);`

根据第二个参数的取值，设置socket I/O模式：

  - FIONBIO：允许设置socket为阻塞或非阻塞：当第三个参数argp为0是阻塞模式，为非0则为非阻塞模式。如果已对一个套接口进行了WSAAsynSelect() 操作，则任何用ioctlsocket()来把套接口重新设置成阻塞模式的试图将以WSAEINVAL失败。为了把套接口重新设置成阻塞模式，应用程序必须首先用WSAAsynSelect()调用（IEvent参数置为0）来禁至WSAAsynSelect(), 或者通过设置lNetworkEvents参数为0来调用WSAEventSelect。
  - FIONREAD：返回套接字s下一次自动读入的数据量的大小。用来确定（determin）悬挂（pending）在网络输入缓冲区中，能从socket s中读取的数据总数。返回单次recv函数能读取的数据的总数
  - SIOCATMARK：返回所有的“紧急”（带外）数据是否都已被读入。仅适用于SOCK_STREAM类型的套接口，且该套接口已被设置为可以在线接收带外数据（SO_OOBINLINE）

### inet_pton与inet_ntop

inet_pton与inet_ntop两个函数，在ASCII字符描述的IP地址与网络字节序的4字节IP地址之间转换。 字母"n"与"p"，分别是numerical与presentation的缩写。

## 协议和地址

套接字API是Unix网络的通用接口，允许使用各种网络协议和地址。

下面列出了一些例子，在现在的 [Linux](../Page/Linux.md "wikilink") 和 [BSD](../Page/BSD.md "wikilink") 中一般都已经实现了。

`PF_LOCAL, PF_UNIX, PF_FILE`
`                Local to host (pipes and file-domain)`
`PF_INET         IP protocol family`
`PF_AX25         Amateur Radio AX.25`
`PF_IPX          Novell Internet Protocol`
`PF_APPLETALK    Appletalk DDP`
`PF_NETROM       Amateur radio NetROM`
`PF_BRIDGE       Multiprotocol bridge`
`PF_ATMPVC       ATM PVCs`
`PF_X25          Reserved for X.25 project`
`PF_INET6        IP version 6`
`PF_ROSE         Amateur Radio X.25 PLP`
`PF_DECnet       Reserved for DECnet project`
`PF_NETBEUI      Reserved for 802.2LLC project`
`PF_SECURITY     Security callback pseudo AF`
`PF_KEY          PF_KEY key management API`
`PF_NETLINK, PF_ROUTE`
`                routing API`
`PF_PACKET       Packet family`
`PF_ASH          Ash`
`PF_ECONET       Acorn Econet`
`PF_ATMSVC       ATM SVCs`
`PF_SNA          Linux SNA Project`
`PF_IRDA         IRDA sockets`
`PF_PPPOX        PPPoX sockets`
`PF_WANPIPE      Wanpipe API sockets`
`PF_BLUETOOTH    Bluetooth sockets`

socket的通用address描述结构sockaddr是一个16字节大小的结构（2+14），sa_family可以认为是socket address family的缩写。另外的14字节是用来描述地址。当指定sa_family=AF_INET之后，sa_data的形式也就被固定了下来：最前端的2字节用于记录16位的端口，紧接着的4字节用于记录32位的IP地址，最后的8字节清空为零。

``` c
struct sockaddr
{
    unsigned short sa_family;
    char sa_data[14];
};

struct sockaddr_in //means socket address internet
{
    unsigned short sin_family; //sin means socket (address) internet
    unsigned short sin_port;
    struct in_addr sin_addr;
    char sin_zero[8];
};

struct in_addr
{
    unsigned long s_addr; // means source address
};
```

## 使用TCP的服务器客户机举例

### 服务器

设置一个简单的TCP服务器涉及下列步骤：

  - 调用socket函数建立套接字，应当使用的参数参见例程。
  - 调用bind函数把套接字绑定到一个监听端口上。注意bind函数需要接受一个sockaddr_in结构体作为参数，因此在调用bind函数之前, 程序要先声明一个 sockaddr_in结构体,用memset函数将其清零，然后将其中的sin_family设置为AF_INET，接下来，程序需要设置其sin_port成员变量，即监听端口。需要说明的是，sin_port中的端口号需要以网络[字节序](../Page/字节序.md "wikilink")存储，因此需要调用htons函数对端口号进行转换（函数名是"host to network short"的缩写）。
  - 调用listen函数，使该套接字成为一个处在监听状态的套接字。
  - 接下来，服务器可以通过accept函数接受客户端的连接请求。若没有收到连接请求，accept函数将不会返回并阻塞程序的执行。接收到连接请求后，accept函数会为该连接返回一个套接字描述符。accept函数可以被多次调用来接受不同客户端的连接请求，而且之前的连接仍处于监听状态——直到其被关闭为止。
  - 现在，服务器可以通过对send，recv或者对write，read等函数的调用来同客户端进行通信。
  - 对于一个不再需要的套接字，可以使用close函数关闭它。 Note that if there were any calls to `fork()`, each process must close the sockets it knew about (the kernel keeps track of how many processes have a descriptor open), and two processes should not use the same socket at once.

<!-- end list -->

``` c
  /* Server code in C */

  #include <sys/types.h>
  #include <sys/socket.h>
  #include <netinet/in.h>
  #include <arpa/inet.h>
  #include <stdio.h>
  #include <stdlib.h>
  #include <string.h>
  #include <unistd.h>

  int main(void)
  {
    struct sockaddr_in stSockAddr;
    int SocketFD = socket(PF_INET, SOCK_STREAM, IPPROTO_TCP);

    if(-1 == SocketFD)
    {
      perror("can not create socket");
      exit(EXIT_FAILURE);
    }

    memset(&stSockAddr, 0, sizeof(struct sockaddr_in));

    stSockAddr.sin_family = AF_INET;
    stSockAddr.sin_port = htons(1100);
    stSockAddr.sin_addr.s_addr = INADDR_ANY;

    if(-1 == bind(SocketFD,(const struct sockaddr *)&stSockAddr, sizeof(struct sockaddr_in)))
    {
      perror("error bind failed");
      close(SocketFD);
      exit(EXIT_FAILURE);
    }

    if(-1 == listen(SocketFD, 10))
    {
      perror("error listen failed");
      close(SocketFD);
      exit(EXIT_FAILURE);
    }

    for(;;)
    {
      int ConnectFD = accept(SocketFD, NULL, NULL);

      if(0 > ConnectFD)
      {
        perror("error accept failed");
        close(SocketFD);
        exit(EXIT_FAILURE);
      }

     /* perform read write operations ... */

      shutdown(ConnectFD, SHUT_RDWR);

      close(ConnectFD);
    }

    close(SocketFD);
    return 0;
  }
```

Python实现：

``` python
from socket import *
from time import ctime
HOST=''
PORT=1100
BUFSIZ=1024
ADDR=(HOST, PORT)
sock=socket(AF_INET, SOCK_STREAM)
sock.bind(ADDR)
sock.listen(5)
while True:
    print('waiting for connection')
    tcpClientSock, addr=sock.accept()
    print('connect from ', addr)
    while True:
        try:
            data=tcpClientSock.recv(BUFSIZ)
        except:
            print(e)
            tcpClientSock.close()
            break
        if not data:
            break
        s='Hi,you send me :[%s] %s' %(ctime(), data.decode('utf8'))
        tcpClientSock.send(s.encode('utf8'))
        print([ctime()], ':', data.decode('utf8'))
tcpClientSock.close()
sock.close()
```

### 客户机

建立一个客户机连接涉及以下步骤：

  - 调用 `socket()`建立套接字。
  - 用`connect()`连接到服务器,类似服务器端的操作，将一个sin_family设为AF_INET,sin_port设为服务器的监听端口（依然要以网络[字节序](../Page/字节序.md "wikilink")）,sin_addr设为服务器IP地址的（还是要用网络字节序）的sockaddr_in作为参数传入。
  - 用`send()` 和 `recv()` 或者 `write()` 和 `read()`进行通信。
  - 用`close()`终止连接。如果调用`fork()`, 每个进程都要用`close()`。

<!-- end list -->

``` c
  /* Client code in C */

  #include <sys/types.h>
  #include <sys/socket.h>
  #include <netinet/in.h>
  #include <arpa/inet.h>
  #include <stdio.h>
  #include <stdlib.h>
  #include <string.h>
  #include <unistd.h>

  int main(void)
  {
    struct sockaddr_in stSockAddr;
    int Res;
    int SocketFD = socket(PF_INET, SOCK_STREAM, IPPROTO_TCP);

    if (-1 == SocketFD)
    {
      perror("cannot create socket");
      exit(EXIT_FAILURE);
    }

    memset(&stSockAddr, 0, sizeof(struct sockaddr_in));

    stSockAddr.sin_family = AF_INET;
    stSockAddr.sin_port = htons(1100);
    Res = inet_pton(AF_INET, "192.168.1.3", &stSockAddr.sin_addr);

    if (0 > Res)
    {
      perror("error: first parameter is not a valid address family");
      close(SocketFD);
      exit(EXIT_FAILURE);
    }
    else if (0 == Res)
    {
      perror("char string (second parameter does not contain valid ipaddress");
      close(SocketFD);
      exit(EXIT_FAILURE);
    }

    if (-1 == connect(SocketFD, (const struct sockaddr *)&stSockAddr, sizeof(struct sockaddr_in)))
    {
      perror("connect failed");
      close(SocketFD);
      exit(EXIT_FAILURE);
    }

    /* perform read write operations ... */

    shutdown(SocketFD, SHUT_RDWR);

    close(SocketFD);
    return 0;
  }
```

Python实现：

``` python
from socket import *

HOST='192.168.1.3'
PORT=1100
BUFSIZ=1024
ADDR=(HOST, PORT)
client=socket(AF_INET, SOCK_STREAM)
client.connect(ADDR)
while True:
    data=input('>')
    if not data:
        break
    client.send(data.encode('utf8'))
    data=client.recv(self.BUFSIZ)
    if not data:
        break
    print(data.decode('utf8'))
```

## 使用UDP的服务器客户机举例

用户数据报协议（UDP）是一个不保证正确传输的无连接协议。 UDP数据包可能会乱序到达，多次到达或者直接丢失。但是设计的负载比TCP小。

UDP地址空间，也即是UDP端口，和TCP端口是没有关系的。

### 服务器

Code may set up a UDP server on port 7654 as follows:

``` c

#include <stdio.h>
#include <errno.h>
#include <string.h>
#include <sys/socket.h>
#include <sys/types.h>
#include <netinet/in.h>
#include <unistd.h> /* for close() for socket */
#include <stdlib.h>

int main(void)
{
  int sock = socket(PF_INET, SOCK_DGRAM, IPPROTO_UDP);
  struct sockaddr_in sa;
  char buffer[1024];
  ssize_t recsize;
  socklen_t fromlen;

  memset(&sa, 0, sizeof(sa));
  sa.sin_family = AF_INET;
  sa.sin_addr.s_addr = INADDR_ANY;
  sa.sin_port = htons(7654);

  if (-1 == bind(sock,(struct sockaddr *)&sa, sizeof(struct sockaddr)))
  {
    perror("error bind failed");
    close(sock);
    exit(EXIT_FAILURE);
  }

  for (;;)
  {
    printf ("recv test....\n");
    recsize = recvfrom(sock, (void *)buffer, 1024, 0, (struct sockaddr *)&sa, &fromlen);
    if (recsize < 0)
      fprintf(stderr, "%s\n", strerror(errno));
    printf("recsize: %d\n ",recsize);
    sleep(1);
    printf("datagram: %s\n",buffer);
  }
}
```

上面的无限循环用`recvfrom()`接收给UDP端口7654的数据包。使用如下参数：

  - 指向缓存数据指针
  - 缓存大小
  - 标志
  - 地址
  - 地址结构体大小

同样功能的Python实现：

``` python
import socket
port=7654
s=socket.socket(socket.AF_INET,socket.SOCK_DGRAM)
#从指定的端口，从任何发送者，接收UDP数据
s.bind(('',port))
print('正在等待接入...')
while True:
    #接收一个数据
    data,addr=s.recvfrom(1024)
    print('Received:',data,'from',addr)
```

### 客户机

用UDP数据包发送一个"[Hello World\!](https://zh.wikipedia.org/wiki/Hello_World! "wikilink")" 给地址127.0.0.1（[回环地址](https://zh.wikipedia.org/wiki/回环地址 "wikilink")），端口 7654 。

``` c
#include <stdlib.h>
#include <stdio.h>
#include <errno.h>
#include <string.h>
#include <sys/socket.h>
#include <sys/types.h>
#include <netinet/in.h>
#include <unistd.h> /* for close() for socket */

int main(int argc, char *argv[])
{
  int sock;
  struct sockaddr_in sa;
  int bytes_sent, buffer_length;
  char buffer[200];

  buffer_length = snprintf(buffer, sizeof(buffer), "Hello World!");

  sock = socket(PF_INET, SOCK_DGRAM, IPPROTO_UDP);
  if (-1 == sock) /* if socket failed to initialize, exit */
    {
      printf("Error Creating Socket");
      exit(EXIT_FAILURE);
    }

  memset(&sa, 0, sizeof(sa));
  sa.sin_family = AF_INET;
  sa.sin_addr.s_addr = htonl(0x7F000001);
  sa.sin_port = htons(7654);

  bytes_sent = sendto(sock, buffer, buffer_length, 0,(struct sockaddr*)&sa, sizeof (struct sockaddr_in));
  if (bytes_sent < 0)
    printf("Error sending packet: %s\n", strerror(errno));

  close(sock); /* close the socket */
  return 0;
}
```

`buffer`指定要发送数据的指针, `buffer_length`指定缓存内容的大小。

同样功能的Python实现：

``` python
import socket
port=7654
host='localhost'
s=socket.socket(socket.AF_INET,socket.SOCK_DGRAM)
s.sendto(b'Hello World!',(host,port))
```

## 参见

  - [计算机网络](../Page/计算机网络.md "wikilink")
  - [Winsock](../Page/Winsock.md "wikilink")

## 参考资料

<references />

The "de jure" standard definition of the Sockets interface is contained in the POSIX standard, known as:

  - [IEEE](https://zh.wikipedia.org/wiki/IEEE "wikilink") Std. 1003.1-2001 Standard for Information Technology—Portable Operating System Interface (POSIX).
  - Open Group Technical Standard: Base Specifications, Issue 6, December 2001.
  - ISO/IEC 9945:2002

Information about this standard and ongoing work on it is available from [the Austin website](http://www.opengroup.org/austin/).

The IPv6 extensions to the base socket API are documented in RFC 3493 and RFC 3542.

## 外部連結

  - [手册页](../Page/手册页.md "wikilink")
      - [accept(2)](http://www.die.net/doc/linux/man/man2/accept.2.html)
      - [connect(2)](http://www.die.net/doc/linux/man/man2/connect.2.html)
  - [Beej's Guide to Network Programming](http://beej.us/guide/bgnet/) - 2007
      - [Beej's Guide to Network Programming 正體中文版（zh-tw）](http://beej-zhtw.netdpi.net) - 2014
      - [Beej's Guide to Network Programming 简体中文版（zh-cn）](http://beej-zhcn.netdpi.net) - 2014
  - [UnixSocket FAQ](http://www.developerweb.net/forum/forumdisplay.php?f=70)
  - [Get system IP list - C++ Example](https://web.archive.org/web/20090402130431/http://xzdev.com/random_ip_cpp.html)
  - [quick TCP-IP NetIntro with C examples](http://heather.cs.ucdavis.edu/~matloff/Networks/Intro/NetIntro.pdf)
  - [Porting Berkeley Socket programs to Winsock](http://msdn2.microsoft.com/en-us/library/ms740096.aspx) - Microsoft's documentation.
  - [Programming UNIX Sockets in C - Frequently Asked Questions](http://www.softlab.ntua.gr/facilities/documentation/unix/unix-socket-faq/unix-socket-faq.html) - 1996
  - [Linux network programming](http://www.linuxjournal.com/article/2333) - *[Linux Journal](https://zh.wikipedia.org/wiki/Linux_Journal "wikilink")*, 1998

[Category:网络软件](https://zh.wikipedia.org/wiki/Category:网络软件 "wikilink") [Category:应用程序接口](https://zh.wikipedia.org/wiki/Category:应用程序接口 "wikilink")

1.