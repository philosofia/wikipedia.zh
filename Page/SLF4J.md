> 本文内容由[SLF4J](https://zh.wikipedia.org/wiki/SLF4J)转换而来。


**JAVA簡易日誌門面**（Simple Logging Facade for Java，縮寫SLF4J），是一套包裝[Logging 框架的介面程式](https://zh.wikipedia.org/wiki/Logging_框架 "wikilink")，以[外觀模式](../Page/外觀模式.md "wikilink")實现。可以在軟體部署的時候決定要使用的 Logging 框架，目前主要支援的有[Java Logging API](https://zh.wikipedia.org/wiki/Java_Logging_API "wikilink")、[log4j及](https://zh.wikipedia.org/wiki/log4j "wikilink")[logback等框架](https://zh.wikipedia.org/wiki/logback "wikilink")。以[MIT 授權方式發佈](https://zh.wikipedia.org/wiki/MIT_授權 "wikilink")。

SLF4J 的作者就是 log4j 的作者 Ceki Gülcü，他宣稱 SLF4J 比 log4j 更有效率，而且比 [Apache Commons Logging](https://zh.wikipedia.org/wiki/Apache_Commons_Logging "wikilink") (JCL) 簡單、穩定。

## 與 log4j 的比較

  - log4j 提供 TRACE, DEBUG, INFO, WARN, ERROR 及 FATAL 六種紀錄等級，但是 SLF4J 認為 ERROR 與 FATAL 並沒有實質上的差別，所以拿掉了 FATAL 等級，只剩下其他五種。
  - 大部分人在程序里面会去写logger.error(exception),其实这个时候log4j会去把这个exception tostring。真正的写法应该是logger(message.exception);而slf4j就不会使得程序员犯这个错误。
  - log4j间接的在鼓励程序员使用string相加的写法，而slf4j就不会有这个问题 ,你可以使用logger.error("{} is+serviceid",serviceid);
  - 使用slf4j可以方便的使用其提供的各种集体的实现的jar。（类似commons-logger）
  - 从commons--logger和log4j merge非常方便，slf4j也提供了一个swing的tools来帮助大家完成这个merge。
  - 提供字串內容替換的功能，會比較有效率，說明如下：

<!-- end list -->

    // 传统的字符串产生方式，如果没有要记录Debug等级的信息，就会浪费时间在产生不必要的信息上
    logger.debug("There are now " + count + " user accounts: " + userAccountList);

    // 为了避免上述问题，我们可以先检查是不是开启了Debug信息记录功能，只是程序的编码会比较复杂
    if (logger.isDebugEnabled()) {
        logger.debug("There are now " + count + " user accounts: " + userAccountList);
    }

    // 如果Debug等级没有开启，则不会产生不必要的字符串，同时也能保持程序编码的简洁
    logger.debug("There are now {} user accounts: {}", count, userAccountList);

  - SLF4J 只支持 MDC，不支持 NDC。

[Category:Java](https://zh.wikipedia.org/wiki/Category:Java "wikilink") [Category:用Java編程的自由軟體](https://zh.wikipedia.org/wiki/Category:用Java編程的自由軟體 "wikilink")