[微軟視窗操作系统是以](https://zh.wikipedia.org/wiki/Microsoft_Windows "wikilink")[事件驅動做為程式設計的基礎](../Page/事件驅動程式設計.md "wikilink")。程式的執行緒会从作業系統获取訊息。應用程式會不斷循环呼叫GetMessage函式（或是PeekMessage函式）來接收這些訊息，這個循环稱之為“**事件迴圈**”。基本上事件迴圈的程式碼如下所示（[C語言](https://zh.wikipedia.org/wiki/C語言 "wikilink") / [C++](../Page/C++.md "wikilink")程式語言）：

``` cpp
MSG msg; //用于存储一条消息
BOOL bRet;

//从UI线程消息队列中取出一条消息
while( (bRet = GetMessage( &msg, NULL, 0, 0 )) != 0)
{
   if (bRet == -1)
   {
       //错误处理代码，通常是直接退出程序
    }
    else
    {
       TranslateMessage(&msg); //按键消息转换为字符消息
       DispatchMessage(&msg); //分发消息给相应的窗体
     }
}
```

雖然在程序上並沒有很嚴格的規定與要求，但是一般來說，它的事件迴圈通常會呼叫TranslateMessage函式與DispatchMessage函式，這兩個函式會傳遞訊息給回呼函式，以及调用相应視窗的消息处理函数。

現在的繪圖介面架構程式設計，例如[Visual Basic與](../Page/Visual_Basic.md "wikilink")[Qt基本上是不會要求應用程式直接拥有視窗程式的訊息迴圈](https://zh.wikipedia.org/wiki/Qt_\(toolkit\) "wikilink")，但是會以鍵盤與滑鼠的按鍵動作來作為事件的處理機制。在這些架構底下，訊息迴圈的痕迹還是可以被找到的。

注意：在上述的原始碼裡，尤其在while迴圈*大於零*的條件。即使GetMessage函式的傳回值型態是英文字大寫的BOOL，但是在Win32視窗程式裡，它是被定義成int整數型態，它有兩個值，TRUE是整數的1，FALSE是整數的0。整數 -1代表error（例如第二个参数为输出的窗口句柄但取不到值的时候），整數0值当GetMessage获取到WM_QUIT訊息。假如有其他訊息，那麼非零值會當成傳回值（有訊息的傳回值通常是正值，但是有些程式設計的說明文件不一定會說明的很詳細\[1\]\[2\]）。

## 历史

16位Windows系统为非抢先单线程模式，应用程序没有发送消息队列，向窗口发送一个消息总是按同步方式执行，也即发送程序要在接受消息的窗口完全处理完消息之后才能继续运行。这通常是一个所期望的特性。但是，如果接收消息的窗口花很长的时间来处理消息或者出现挂起，则发送程序就不能再执行。这意味着系统是不强壮的。\[3\]如果应用程序消息队列（只用于存放投寄的消息）为空，由于没有虚拟输入消息队列，SendMessage或PeekMessage函数访问系统事件队列查取可用的鼠标或键盘输入消息。如果系统队列中没有需要处理的事件，SendMessage或PeekMessage函数扫描所有窗口以处理需要修改重绘的区域。如果没有需要重绘的区域，则交出CPU控制权。恢复CPU控制权时，查看是否有定时器过期。至此如果没有消息可返回，SendMessage进入睡眠，直至被输入事件唤醒；PeekMessage如果没有设置PM_NOYIELD标记，则会让出CPU控制权，但不会让线程休眠，重新获得CPU后PeekMessage将控制权返回到线程，并返回一个空值指出这个线程没有要处理的消息了。

本文主要关注Win32系统的消息处理机制。

## 背景

### UI线程

Windows系统规定，窗口和钩子（hook）这两种[User对象分别由建立窗口和安装钩子的线程所拥有](../Page/Windows对象管理.md "wikilink")，一旦该线程结束，操作系统会自动删除窗口或卸载钩子。而其他的User对象（图标icon、光标cursor、窗口类WndClass、菜单、加速键表等）则归进程所有，进程结束时操作系统会自动删除这些对象。

建立窗口的线程必须就是处理窗口所有消息的线程，即**UI线程**（User Interface Thread）创建了窗体及窗体上的各种控件，系统为UI线程分配一个消息队列用于窗口消息的派送（dispatch）。为了使窗口处置这些消息，线程必须有它自己的“消息循环”。只有当一个线程调用[Windows API中的GDI](../Page/Windows_API.md "wikilink")（Graphics Device Interface）和User函数时，操作系统才会将其看成是一个UI线程，并为它分配一些另外的资源，创建一套线程消息队列；否则，操作系统把**非UI线程**视作普通工作线程（Workhorse），不会为它创建消息队列。因此，调用PostThreadMessage前，这个线程必须是UI线程从而有投寄消息的队列，通常可在该线程中调用一次PeekMessage函数以达到这个目的。

如果一个UI线程结束运行，操作系统会自动回收它所创建的所有窗体。

### 窗体过程

窗体过程（Window Procedure）是一个函数，每个窗体有一个窗体过程，负责处理该窗体的所有消息。

UI[控件](../Page/控件.md "wikilink")也是独立的“Window”，拥有自己的“窗体过程”。

### 消息队列

Windows操作系统的内核空间中有一个系统消息队列（system message queue），在内核空间中还为每个UI线程分配各自的线程消息队列(Thread message queue)。在发生输入事件之后，Windows操作系统的输入设备驱动程序将输入事件转换为一个「消息」投寄到系统消息队列；操作系统的一个专门线程从系统消息队列取出消息，分发到各个UI线程的输入消息队列中。

每个UI线程的线程信息块TIB分配一个THREADINFO的结构，该结构包含一族成员变量，包括：\[4\]

  - 发送消息队列（send-message queue）指针：其他发起线程通过SendMessage、SendMessageTimeout、SendMessageCallback、SendNotifyMessage、ReplyMessage等函数产生的消息放入该队列，发起的线程阻塞（挂起）在该队列上（对于SendMessageCallback、SendNotifyMessage不被阻塞）直至消息处理完或者超时返回。
  - 投寄消息队列（posted-message queue）指针：其他线程通过PostMessage函数或PostThreadMessage函数投寄的消息；
  - 虚拟输入消息队列（virtualized-input queue）指针：键盘与鼠标事件。该队列最多只保存一个键盘消息，仅当应用程序处理完这个键盘消息，Windows才会从操作系统消息队列取出下一个键盘消息放入线程的虚拟输入消息队列。这种方式至少有两点用途：一是如果用户的键盘输入速度快于应用程序处理键盘消息的速度，并且特定按键会使输入焦点从一个窗口切换到另一个窗口，随后的按键就应该是另一个窗口的输入；二是Windows API函数`TranslateMessage`把按键消息转化为字符消息，如WM_KEYDOWN转化为WM_CHAR，然后放入线程的虚拟输入消息队列中，成为下一个待处理的键盘消息。
  - 回复消息队列（reply-message queue）指针：调用SendMessage函数的线程在这个函数上阻塞后，实际上仍可能被系统使用该线程执行其他处理，因此SendMessage函数的目标线程把窗口函数的返回值登记到这个队列作为SendMessage的返回值，以便SendMessage函数从阻塞状态恢复时能取到该返回值（16位Windows系统是单线程的，因此不可能存在这种需求）。另外一种使用情形是SendMessageCallback函数（给所有重叠（overlapped）窗口广播）时，总是调用后立即返回并继续执行，因此接收了此消息的线程把窗口函数执行结果登记到发起线程的回复消息队列，在发起线程下一次调用GetMessage、PeekMessage、WaitMessage或某个SendMessage挂起时从回复消息队列中取出该msg并执行登记的ResultCallBack函数。
  - nExitCode：由PostQuitMessage函数设置该成员，作为线程的退出码。
  - 唤醒标志（wake flage）
  - 局部输入状态变量
      - QS_POSTMESSAGE位：投寄消息队列是否为空；
      - QS_QUIT位：由PostQuitMessage函数给该标志置位。
      - QS_SENDMESSAGE位：发送消息队列是否为空；
      - QS_KEY：有按键消息
      - QS_MOUSE：有鼠标消息
      - QS_PAINT：有WM_PAINT
      - QS_TIMER：有WM_TIMER

应用程序的每个UI线程中有一段称之为“消息循环”的代码，通过**GetMessage**系统调用（或是**PeekMessage**系统调用）访问系统空间中的对应的UI线程的消息队列，并依照下述**次序**处理：

  - QS_SENDMESSAGE置位：则对发送消息队列中的每个消息，依次调用各个发送消息的窗口函数直接处理，**GetMessage不返回**；直至所有发送消息队列中的消息处理完毕。
  - QS_POSTMESSAGE置位：则填充GetMessage函数参数的MSG结构为相应的投寄消息，GetMessage返回为真。该消息通过DispatchMessage系统调用把消息分发给相应窗口的消息处理函数。
  - QS_QUIT置位：则填充GetMessage函数参数的MSG结构为WM_QUIT，QS_QUIT复位，GetMessage返回为假。
  - QS_INPUT置位：则填充GetMessage函数参数的MSG结构为相应的输入消息，GetMessage返回为真。该消息通过DispatchMessage系统调用把消息分发给相应窗口的消息处理函数。
  - 再一次检查QS_SENDMESSAGE置位，如是则处理发送消息队列中的每个消息。
  - QS_PAINT置位：则填充GetMessage函数参数的MSG结构为WM_PAINT，GetMessage返回为真。GetMessage不从队列中删除WM_PAINT消息（即不对QS_PAINT复位）。
  - QS_TIMER置位：则填充GetMessage函数参数的MSG结构为WM_TIMER，QS_TIMER复位，GetMessage返回为真。如果QS_TIMER复位状态，则当前线程挂起（hung）。

需要注意的是，GetMessage如果在应用程序消息队列未获取消息，则GetMessage调用不返回，该线程挂起，CPU使用权交给操作系统。即GetMessage为阻塞调用。

由此可见，Windows的事件驱动模式，并不是操作系统把消息主动分发给应用程序；而是由应用程序的每个UI线程通过“消息循环”代码从UI线程消息队列获取消息。

## Windows消息类别

  - 键盘消息：
      - 按键消息：WM_SYSKEYDOWN、WM_SYSKEYUP、WM_KEYDOWN、WM_KEYUP等消息。
          - wParam包含虚拟键码（virtual-key code），表示按下或释放的键
          - lParam包含按键6个字段信息：
              - 重复按键次数（Repeat Count，0～15 位）：通常设为1。大于1说明按键速度大于程序处理能力。可以根据实际需要忽略或处理。
              - OEM扫描码(scan code，16～23位)：硬件产生的代码。
              - 扩充键标志（extended key，24位）：如果为扩充键（如右侧的Alt键或Ctrl键）按下时为1，否则为0。
              - 保留位（25～28位）：保留位是系统缺省保留的，一般不用。
              - 上下文代码（context code，29位）：如同时按下ALT，标志为1；否则为0。WM_SYSKEYUP或WM_SYSKEYDOWN常为1。WM_KEYUP或WM_KEYDOWN常为0。当所有程序都最小化时，没有窗口具有输入焦点，Windows仍将发送键盘消息给活动窗口；所有的按键都会产生WM_SYSKEYUP与WM_SYSKEYDOWN消息，此情况下如果没按下ALT，该字段为0，这样使最小化的活动窗口不处理这些按键。对于一些非英文键盘，有些字符是shift等组合键产生的，这时内容代码为1，但是其是非系统按键。
              - 键先前状态（previous key state，位30）：键此前是释放的，则为0，还则为1。很明显UP为1，DOWN可以为1或0，为1表示该键自动重复。
              - 转换状态（transition state，31位）：键被按下为0，键被松开时为1。如UP为1，DOWN为零。
          - SYSKEY：按下(将激活菜单条)或者按下后再按下别的键，或者没有窗口具有键盘输入焦点（WM_SETFOCUS指示窗口得到输入焦点，WM_KILLFOCUS指示窗口失去输入焦点）时的按键，为SYSKEY。lParam的第29位为context code，如果为1表示被按下，如果为0表示WM_SYSKEYDOWN发出时没有窗口具有键盘输入焦点。无论用户处理与否，必须传送给Windows默认窗口过程处理此类按键消息。
          - 其他情形为普通按键。除Print键之外都有“按下”消息；所有键都存在“弹起”消息。
      - 字符消息：按键消息WM_SYSKEYDOWN、WM_KEYDOWN被Windows API函数`TranslateMessage`处理后该函数在线程消息队列投寄(post)相应的字符消息，wParam参数是ASCII或Unicode的character code；这取决于RegisterClass函数是A或W版；IsWindowUnicode函数判断窗口过程会接受哪种编码。产生字符消息的按键有：任何字符键、回退键（BACKSPACE）、回车键（carriage return）、ESC、SHIFT + ENTER（linefeed换行）、TAB。因为TranslateMessage函数从WM_KEYDOWN和WM_SYSKEYDOWN消息产生了字符消息，所以字符消息是夹在按键消息之间传递给窗口消息处理程序的。如果使用者按住一个键不放，会自动重复产生一系列的WM_KEYDOWN消息；对每条WM_KEYDOWN消息，都会得到一条字符消息。如果某些WM_KEYDOWN消息的重复计数大于1，那么相应的WM_CHAR消息将具有同样的重复计数。
          - WM_SYSCHAR：按下后再按下别的键的WM_SYSKEYDOWN消息被翻译，
          - WM_CHAR：WM_KEYDOWN消息被翻译为WM_CHAR消息。
          - WM_DEADCHAR：`TranslateMessage`函数处理“[死键](https://zh.wikipedia.org/wiki/死键 "wikilink")”（dead key）的WM_KEYUP消息，向具有输入焦点的窗口投寄（post）出WM_DEADCHAR消息。死键是产生[附加符号](../Page/附加符号.md "wikilink")的按键。例如在德语键盘，[锐音符被按下](https://zh.wikipedia.org/wiki/锐音符 "wikilink")、释放后，再按下，将获得字母á的WM_CHAR。如果在死键之后跟有不能带此附件符号的字母（例如[锐音符后跟](https://zh.wikipedia.org/wiki/锐音符 "wikilink")「s」），那么将接收到两条WM_CHAR消息：前一个消息的wParam等于附加符号本身的ASCII码（与传递到WM_DEADCHAR消息的wParam值相同），第二个消息的wParam等于字母的ASCII代码。
          - WM_SYSDEADCHAR：按下时又按下了“死键”的WM_SYSKEYUP消息。
  - 鼠标消息：
      - 客户区鼠标消息：WM_MOUSEMOVE及鼠标按键的DOWN、UP、DBLCLK消息。双击事件的处理只有窗口类定义接收（CS_DBLCLKS）时，才起作用，这时接收到的鼠标消息顺序为：DOWN、UP、DBLCLK、UP。鼠标消息发送给被单击的窗口或鼠标经过的窗口，即使该窗口处于非活动或不带输入焦点；例外情况有“捕获鼠标”时或模式对话框处于活动状态时。消息参数wParam(指出那个鼠标按钮、Shift键、Ctrl键被按下；lParam的低位表示x坐标，高位表示y坐标的鼠标位置。
      - 非客户区鼠标消息：为WM_NC\*形式。
          - 击中测试消息：WM_NCHITTEST。Windows利用此消息来产生其他所有的鼠标消息。
      - WM_MOUSEWHEEL发送给具有焦点的窗口（注意不一定是鼠标下面的窗口）
  - 定时器消息
  - 控件消息
  - 跨进程发送数据的消息：WM_SETTEXT、WM_GETTEXT、WM_COPYDATA，系统自动分配使用可在进程间共享的[内存映射文件](../Page/内存映射文件.md "wikilink")来传递数据。

键盘输入时需要明确插入符位置，相关API函数为：CreateCaret、SetCaretPos、ShowCaret、HideCaret、DestroyCaret、GetCaretPos、GetCaretBlinkTime、SetCaretBlinkTime。

3个获得键状态的函数：GetKeyState、GetAsyncKeyState、GetKeyboardState。

对于自定义的控件，当单击子窗口时，父窗口会得到焦点。但对于标准子窗口控件，单击时会自动获得焦点（子窗口过程在WM_LBUTTONDOWN中实现了SetFocus(hwnd)）。如果一个子窗口拥有输入焦点，鼠标单击另一个兄弟子窗口，则兄弟子窗口获得输入焦点。

## 同步与阻塞

[Windows API函数SendMessage是个](../Page/Windows_API.md "wikilink")[同步调用](../Page/同步_\(计算机科学\).md "wikilink")，即它发出的Windows消息没被处理完之前这个函数就不返回。但这个函数不是阻塞的。分两种情形：\[5\]

  - 如果被指定的窗口是发起调用SendMessage的线程创建的，则该线程立即执行窗口过程（window procedure）；
  - 如果被指定的窗口不是发起调用SendMessage的线程创建的，操作系统切换到该窗口所属的线程执行相应的窗口过程。消息处理完之前，发送线程不从调用SendMessage处返回，但发送线程这期间可以处理非队列消息（nonqueued message）。这是“同步非阻塞”。

异步发送或投寄消息的函数，如PostMessage、SendMessageCallback、SendNotifyMessage，消息参数中不能使用指针，否则函数调用失败。

## GetMessage伪算法

``` cpp
BOOL GetMessage(MSG *lpMsg, HWND hWnd , UINT wMsgFilterMin, UINT wMsgFilterMax)
{
         //查看QS_SENDMESSAGE标志，如果有的话循环处理，直到没有消息位置
         DWORD dwRetVal = 0;
         ThreadInfo threadInfo;

FLAG_SENDPROCLOOP:
         GetThreadInfo(GetCurrentThreadId(), &threadInfo);
         while (threadInfo.QS_SENDMESSAGE == QS_SIGNALSET) {
                   //从发送消息队列中获取消息
                   dwReturnVal = GetMsgFromQueue(QUEUE_SEND, lpMsg, hWnd,wMsgFilterMin, wMsgFilterMax);
                   //判断是否取到消息,有则调用窗口函数，无则复为QS_SENDMESSAGE标志
                   If (dwReturnVal == GETMESSAGE_HASMESSAGE) {
                            //调用指定窗口的窗口函数
                            CallWindowProc(hWnd, &threadInfo, lpMsg);
                   }
                   else {
                            QS_SENDMESSAGE = QS_SIGNALRESET;
                            break;
                   }
         }
         //在继续处理之前再次检查发送消息队列
         if (threadInfo.QS_SENDMESSAGE == QS_SIGNALSET) goto FLAG_SENDPROCLOOP;
         //检查发送消息队列, 如果有消息则取发送消息
         //判断是否还有发送消息，没有了则复位QS_POSTMESSAGE标志
         if (threadInfo.QS_POSTMESSAGE == QS_SIGNALSET) {
                   dwReturnVal = GetMsgFromQueue(QUEUE_POST, lpMsg, hWnd, wMsgFilterMin, wMsgFilterMax);
                   if (dwReturnVal == GETMESSAGE_LASTMESSAGE)
                            threadInfo.QS_POSTMESSAGE = QS_SIGNALRESET;

                   return TRUE;
         }

         //如果退出标志被置位
         if (threadInfo.QS_QUIT == QS_SIGNALSET) {
                   threadInfo.QS_QUIT = QS_SIGNALRESET;
                   FillMessage(lpMsg, MESSAGE_QUIT);
                   return FALSE;
         }

         //检查输入消息队列
         if (threadInfo.QS_INPUT == QS_SIGNALSET) {
                   DWORD dwRetVal = GetMessageFromQueue(QUEUE_INPUT, lpMsg, hWnd, wMsgFilterMin, wMsgFilterMax);
                   //检查是否有键盘，鼠标消息
                   if (Test(dwRetVal, QS_KEY) == QS_LASTMOUSEKEYMESSAGE)
                            threadInfo.QS_KEY = QS_SIGNALRESET;
                   if (Test(dwRetVal, QS_MOUSEBUTTON) == QS_LASTMOUSEMESSAGE)
                            threadInfo.QS_MOUSEBUTTON = QS_SIGNALRESET;

                   return TRUE;
         }

         //测试QS_PAINT
         if (threadInfo.QS_PAINT == QS_SIGNALSET) {
                   //填充MSG，如果没有窗口过程确认窗口，则复位QS_PAINT标志
                   //...
                   //返回TRUE
                   threadInfo.QS_PAINT = QS_SIGNALRESET;
                   return TRUE;
         }

         if (threadInfo.QS_TIMER == QS_SIGNALSET) {
                   //填充MSG，如果没有定时器报时，则复位QS_TIMER标志
                   //...
                   //返回TRUE
                   return TRUE;
         }

         //等待有消息到达
         dwRetVal = MsgWaitForMultipleObjectsEx(...);
         if (...)
                   goto FLAG_SENDPROCLOOP;

         //等待失败
         return FALSE;
}
```

## 參考資料

<div class="references-small">

<references />

</div>

## 相關條目

  - [C語言](https://zh.wikipedia.org/wiki/C語言 "wikilink")
  - [C++](../Page/C++.md "wikilink")

## 外部連結

  - [Meandering Through the Maze of MFC Message and Command Routing](https://web.archive.org/web/20091228154216/http://www.microsoft.com/msj/0795/dilascia/dilascia.aspx)
  - \[<http://msdn.microsoft.com/en-us/library/ms632590(VS.85>).aspx Platform SDK: Message and Message Queue Overviews\]
  - [Platform SDK: Windows API: Entering the Message Loop](http://msdn2.microsoft.com/en-us/library/aa383682.aspx)
  - [GetMessage function](http://msdn2.microsoft.com/en-us/library/ms644936.aspx)
  - [PeekMessage function](http://msdn2.microsoft.com/en-us/library/ms644943.aspx)

[Category:事件_(计算机)](https://zh.wikipedia.org/wiki/Category:事件_\(计算机\) "wikilink") [Category:微軟API](https://zh.wikipedia.org/wiki/Category:微軟API "wikilink") [Category:Microsoft_Windows](https://zh.wikipedia.org/wiki/Category:Microsoft_Windows "wikilink") [Category:Windows_API](https://zh.wikipedia.org/wiki/Category:Windows_API "wikilink")

1.  [GetMessage function](http://msdn2.microsoft.com/en-us/library/ms644936.aspx)
2.  [PeekMessage function](http://msdn2.microsoft.com/en-us/library/ms644943.aspx)
3.  Bob Gunderson：《GetMessage and PeekMessage Internals》，Microsoft Developer Network Technology Group，December 11, 1992
4.  （美）Jeffrey Richter：Programming Applications for Microsoft Windows, Microsoft Press，2000，Fourth edition，“第26章 窗口消息”，《Windows核心编程》中文版，机械工业出版社2008年5月1日。 ISBN：9787111237914.
5.  \[<https://msdn.microsoft.com/en-us/library/windows/desktop/ms644950(v=vs.85>).aspx MSDN:SendMessage function\]