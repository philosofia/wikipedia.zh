> 本文内容由[JAXM](https://zh.wikipedia.org/wiki/JAXM)转换而来。


JAXM（Java API for XML Messaging简称JAXM）是为Java平台上的应用程序定义的API，用以通过[XML](../Page/XML.md "wikilink")(以及[SOAP](https://zh.wikipedia.org/wiki/SOAP "wikilink"))发送和接收消息，支持同步消息和异步消息。JAXR API是在JCP下开发的，代号JSR 67。

## 基本概念

JAXM的基本概念包括消息，连接，消息提供者以及JAXM客户端和JAXM服务

### 消息（Message）

JAXM的消息使用SOAP消息标准，包括或不包括附件。

### 连接（Connection）

JAXM有两种连接：

  - 直接连接，由消息发送者直接发送给消息的接收者的连接。
  - 间接连接，消息发送者通过消息提供者发送给消息接收者的连接。

### 消息提供者（Messaging Provider）

消息提供者是中介服务，负责为消息发送者处理消息的传送和路由。消息提供者也会提供一些服务，如可靠消息。

### JAXM客户端

JAXM客户端向接收者发送消息。最终的接收者一般是服务。 JAXM客户端可以直接发送消息给服务，也可以发送给一个中介提供者，被称为JAXM消息提供者。取决于客户端和接收者是如何配置的。

### JAXM服务

JAXM服务端JAXM客户端发送的消费XML消息。服务读取和处理客户端的消息。服务对客户端的反应取决于两者之间所建立的消息交换的类型。这部分取决于发送消息的客户端是单独的JAXM客户端还是使用消息提供者的JAXM客户端。

## 消息交换模式

JAXM消息在客户端，发送者，和最末端的服务，接收者之间交换。JAXM的消息交换主要有两种类型：同步通讯或异步通讯。

  - 异步交换（单向），消息发送者向接收者发送一条消息，并不等待接收者返回的响应消息。发送消息后就继续处理。一旦接收者接收消息，将会读取和处理消息。如果需要响应消息，消息接收者将向发送者发送一条响应消息。原发送者可能需要处理响应消息。
  - 同步交换（请求-响应）消息发送者向消息接收者发送一条消息，然后等待直至消息接收者的应答。消息接收者必须处理该消息并向消息发送者发送一条确认消息或其他消息。响应消息取消发送者的阻塞，发送者才能继续处理其他工作。连接失败也可以取消阻塞发送者。

## 编程模型

JAXM的API包包括：

  - javax.xml.messaging，提供发送和接收消息的接口和类，包括连接和监听器。
  - javax.xml.soap，对SOAP消息的封装，包括SOAP头消息，消息体等。

### 客户端

客户端发送消息的过程包括：

1.  获取连接，可以获取点对点连接或者获取与消息提供者的连接
2.  创建消息
3.  填充消息内容
4.  发送消息
5.  读取响应消息，并进行处理

### 服务

服务接收和处理消息的过程包括：

1.  实现onMessage，读取消息
2.  进行业务处理
3.  创建响应消息
4.  填充响应消息
5.  返回响应消息

## 参见

  - [JAX-RPC](https://zh.wikipedia.org/wiki/JAX-RPC "wikilink")
  - [JAX-WS](../Page/JAX-WS.md "wikilink")
  - [SOAP](https://zh.wikipedia.org/wiki/SOAP "wikilink")
  - [SAAJ](../Page/SAAJ.md "wikilink")

## 外部链接

  - [Java API for XML Messaging (JAXM)](http://java.sun.com/javaee/5/docs/api/javax/xml/soap/package-summary.html)

[Category:Java_API_for_XML](https://zh.wikipedia.org/wiki/Category:Java_API_for_XML "wikilink") [Category:基于XML的标准](https://zh.wikipedia.org/wiki/Category:基于XML的标准 "wikilink") [Category:Java](https://zh.wikipedia.org/wiki/Category:Java "wikilink") [Category:Java规范请求](https://zh.wikipedia.org/wiki/Category:Java规范请求 "wikilink")