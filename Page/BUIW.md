> 本文内容由[BUIW](https://zh.wikipedia.org/wiki/BUIW)转换而来。


**BREW UI Widget**（BUIW），原名為**BREW UI Toolkit**（BUIT），是美國[Qualcomm公司於](https://zh.wikipedia.org/wiki/Qualcomm "wikilink")2004年以後致力發展的一套全新的UI-package，用以替代早期的[BREW關於GUI](https://zh.wikipedia.org/wiki/BREW "wikilink") 設計。

最早BREW GUI只提供少數的GUI元件，如：IMenuCrl, ITextCtl，這些簡單的Controls遠遠不敷開發廠商的需求，許多廠商必須自行負責UI的設計開發。後來Qualcomm接續推出兩套較為完整的BREW GUI Packages，即code-based的BUIW，以及XML-based的[uiOne](https://zh.wikipedia.org/wiki/uiOne "wikilink")。TrigML和BUIW是uiOne的核心。TrigML負責UI的描述，BUIW負責UI的建構。

BUIW較原來的BREW UI設計新增兩大特色，一是階層（layer）的觀念，這是早期BREW GUI所缺乏的；二是提供客製化（customize）的概念，有了客製化的機制，廠商可以自行替換這些元件。BUIW大量使用了設計模式，如[MVC模式](https://zh.wikipedia.org/wiki/Model-view-controller "wikilink")，Decorator模式。

## Container

  - IPropContainer,
      - ImageStaticWidget
      - SoftkeyWidget
  - ICardContainer：Tab Control之實作。
  - IConstraintContainer,
  - IIDecorator：裝飾介面，用於裝飾Container。像ScrollbarWidget, BorderWidget, BlendWidget, TabWidget都是繼承自IDecorator interface。

## Widget

  - TextWidget,
  - StaticWidget,
  - CheckWidget,
  - RadioWidget,
  - ScrollWidget,
  - SliderWidget,
  - ProgressWidget,
  - BitmapWidget,
  - ImageWidget,
  - ImageStaticWidget,
  - TabWidget,
  - ListWidget,
  - BorderWidget,
  - BlendWidget,
  - CursorWidget,
  - ViewportWidget

## Model

  - IValueModel
  - IInterfaceModel
  - IMenuModel
  - ITextModel
  - IListModel
      - IArrayModel
      - IVectorModel

[Category:移动通信标准](https://zh.wikipedia.org/wiki/Category:移动通信标准 "wikilink")