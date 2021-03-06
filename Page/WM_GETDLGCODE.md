> 本文内容由[WM GETDLGCODE](https://zh.wikipedia.org/wiki/WM_GETDLGCODE)转换而来。


**WM_GETDLGCODE**，是[Windows操作系统内建的一种标准Windows消息](https://zh.wikipedia.org/wiki/Windows操作系统 "wikilink")。\[1\]如果使用[Windows API函数IsDialogMessage来过滤Windows消息](../Page/Windows_API.md "wikilink")，操作系统在下述情形会发送一条WM_GETDLGCODE消息给对话框或窗体内的控件：\[2\]

  - 确定控件是否会处理特定类型输入。
  - 确定编辑框控件（edit control）的内容是否被选中，如果用户按了TAB键使得这个编辑框控件收到了输入焦点（input focus）。
  - 确定按钮（button）类型。

## 參數

WM_GETDLGCODE消息的参数的含义：

  - wParam：按键输入的虚拟键码（virtual key）。
  - lParam：MSG数据结构的指针或者为NULL（如果系统执行一个查询）。

## 返回碼

每个预定义控件的窗口过程对WM_GETDLGCODE消息返回1个或多个下述值，可用布尔OR运算符组合：

| 返回码                   | 解释                                                                             |
| --------------------- | ------------------------------------------------------------------------------ |
| DLGC_BUTTON          | Control is a button (of any kind).                                             |
| DLGC_DEFPUSHBUTTON   | Control is a default push button.                                              |
| DLGC_HASSETSEL       | Windows will send an EM_SETSEL message to the control to select its contents. |
| DLGC_RADIOBUTTON     | Control is an option (radio) button.                                           |
| DLGC_STATIC          | Control is a static control.                                                   |
| DLGC_UNDEFPUSHBUTTON | Control is a push button but not the default push button.                      |
| DLGC_WANTALLKEYS     | Control processes all keyboard input.                                          |
| DLGC_WANTARROWS      | Control processes arrow keys.                                                  |
| DLGC_WANTCHARS       | Control processes WM_CHAR messages.                                           |
| DLGC_WANTMESSAGE     | Control processes the message in the MSG structure that lParam points to.      |
| DLGC_WANTTAB         | Control processes the TAB key.                                                 |

上述返回值也可用于用户定义控件或者[子类化](https://zh.wikipedia.org/wiki/子类化 "wikilink")（subclassing）的预定义控件。子类化一个预定义控件，应该先调用预定义控件的窗口过程，然后修改返回码的必要的位元。

## 範例

如果控件处理WM_GETDLGCODE消息时返回某个DLGC_WANT位元組，控件将处理指定的消息类型而Windows将对该类型的消息不会做任何默认处理。

例如，下拉列表控件（list box）处理WM_GETDLGCODE消息返回码包含了DLGC_WANTARROWS位，指示下拉列表控件将会处理方向键。如果下拉列表控件有输入焦点且用户按下了“向下方向键”, Windows发送WM_GETDLGCODE消息给下拉列表控件。由于返回值包含了DLGC_WANTARROWS值， Windows允许下拉列表控件处理方向键且操作系统不会做任何处理。如果返回值不包含DLGC_WANTARROWS值， Windows将继续处理方向键并且把输入焦点转移为下一个控件。

另一个例子，编辑框控件返回值包含DLGC_WANTCHARS码而按钮控件返回值则不包含。因此如果一个按钮控件有输入焦点且用户按下了一个有效的控件助记符（mnemonic character，显示为控件标签中的加了底划线的字母）, Windows将设置输入焦点到该控件上。如果一个编辑框控件有输入焦点且用户输入了一个助记符， Windows不会把输入焦点改到别的控件因为编辑框控件会自行处理WM_CHAR消息。

一个控件处理WM_GETDLGCODE 消息时，如果返回值包含了DLGC_WANTMESSAGE码，表明应用程序不希望系统默认处理lParam参数中包含的消息。这些消息可以是WM_KEYDOWN, WM_SYSCHAR, WM_CHAR.

下述代码示例，对检查框控件（check box ）子类化，处理WM_GETDLGCODE消息，当用户按下"X"键则选中检查框，如果按下"O"键则清除检查框。

``` cpp
   case WM_GETDLGCODE:
      // Call the check box window procedure first
      lRet = CallWindowProc(lpCheckProc, hWnd, wMessage, wParam,
                            lParam);

      // If lParam points to an MSG structure
      if (lParam)
      {
         lpmsg = (LPMSG)lParam;
         if (lpmsg->message == WM_CHAR)
         {
            if (lpmsg->wParam == 'x' || lpmsg->wParam == 'X')
            {
               // Select the check box when user presses "X"
               SendMessage(hWnd, BM_SETCHECK, TRUE, 0);
               lRet |= DLGC_WANTMESSAGE;
            }
            else if (lpmsg->wParam == 'o' || lpmsg->wParam == 'O')
            {
               // Clear the check box when user presses "O"
               SendMessage(hWnd, BM_SETCHECK, FALSE, 0);
               lRet |= DLGC_WANTMESSAGE;
            }
         }
      }
      return lRet;
```

上述代码使得Windows对X, x, O, o字符的WM_CHAR消息不会做进一步处理，因为WM_GETDLGCODE返回值包含了DLGC_WANTMESSAGE码。上例中，控件返回值也可以用DLGC_WANTCHARS代替DLGC_WANTMESSAGE。

下例代码子类化编辑框控件，禁止其通过Tab键获得输入焦点时默认地全部选中编辑框内的文本。

``` cpp
     // In the subclass procedure
   case WM_GETDLGCODE:
      // Call the original edit control window procedure
      lRet = CallWindowProc(lpEditProc, hWnd, wMessage, wParam,
                            lParam);

      // Clear the DLGC_HASSETSEL bit from the return value
      lRet &= ~DLGC_HASSETSEL;

      return lRet;
```

## 参考文献

<references/>

[Category:Microsoft_Windows](https://zh.wikipedia.org/wiki/Category:Microsoft_Windows "wikilink")

1.  \[<https://msdn.microsoft.com/en-us/library/windows/desktop/ms645425(v=vs.85>).aspx MSDN:WM_GETDLGCODE message\]
2.  [How To Use the WM_GETDLGCODE Message](https://support.microsoft.com/en-us/help/83302/how-to-use-the-wm-getdlgcode-message)