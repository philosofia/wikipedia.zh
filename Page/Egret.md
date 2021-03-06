> 本文内容由[Egret](https://zh.wikipedia.org/wiki/Egret)转换而来。


**Egret Engine**白鹭引擎是一套开源免费的完整的HTML5游戏开发解决方案，用于构建二维游戏、演示程序和其他图形界面交互应用等。白鹭引擎是一个基于[TypeScript](../Page/TypeScript.md "wikilink")语言开发的HTML5游戏引擎。当游戏开发完成后，可将程序发布到[Web](https://zh.wikipedia.org/wiki/Web "wikilink")、[iOS](https://zh.wikipedia.org/wiki/iOS "wikilink")、[Android](../Page/Android.md "wikilink")、[Windows Phone](../Page/Windows_Phone.md "wikilink")、[PC](../Page/PC.md "wikilink")等平台，实现[跨平台特性](https://zh.wikipedia.org/wiki/跨平台 "wikilink")。

白鹭引擎不仅仅是一个基于HTML5技术的游戏引擎，完整的产品线中除了白鹭引擎还提供了很多辅助游戏开发的工具。开发者可以使用Egret提供的相关工具搭建属于自己的游戏开发工作流。

白鹭引擎分为2D版本和3D版本，白鹭引擎2D版本已更新至5.0，白鹭引擎3D版本已发布。\[1\]

## 白鹭引擎迭代历史

2017年7月，白鹭发布白鹭引擎3D版本，支持 [WebAssembly](../Page/WebAssembly.md "wikilink") 技术，拥有强大的 3D 编辑器系统，支持 [Unity](https://zh.wikipedia.org/wiki/Unity "wikilink") 工作流导出。 

2017年5月，白鹭发布了5.0版本，支持WASM 极速模式和 JS 兼容模式智能切换成为业界首个双核H5引擎。

2016年12月，白鹭引擎发布4.0版本，改善资源管理框架。

2016年5月，白鹭引擎发布3.0版本，引入的[WebGL](../Page/WebGL.md "wikilink")。

2015年9月，白鹭引擎发布2.5版本，调整局部渲染技术。

2015年5月，白鹭引擎发布2.0版本，并发布业界首个H5工作流。

## 白鹭引擎特点

**开源免费** 基于BSD开源协议的白鹭引擎，用户可自由的使用白鹭引擎创作自己的游戏。

**优秀的设计思想** 白鹭引擎的设计思想借鉴了2D动画软件Flash的一些设计思想。在引擎的设计中，白鹭引擎底层使用了弹性跑道模型，显示列表，脏矩阵，事件模型等技术。在这些技术基础之上，白鹭封装了对用户友好的API。开发者在开发游戏时，无需考虑底层渲染逻辑，只关心游戏逻辑即可。

**高效的渲染模块** 在图形图像渲染中，白鹭引擎完全使用HTML5标准中的canvas技术。帮助开发者使用白鹭引擎开发的游戏在各个浏览器上的兼容性。同时，为了给玩家更好的游戏体验，我们提供了CPU渲染和 WebGL 渲染模式。同时，支持 WebAssembly（又名wasm） 技术。 wasm是由谷歌、苹果、微软和Mozilla的工程师合力创建的新技术，这是能够运用在未来浏览器中承诺可带来20倍更快性能的字节码（bytecode）。wasm项目创造全新的字节码（一种机器可读的指令集，能够更快为浏览器加载高级语言），让桌面和移动端浏览器相比较网页或者应用的整体源代码变得更加高效。

**完善的配套工具** 白鹭引擎提供的配套工具极大简化了游戏开发流程。从游戏的代码编写，UI制作，地图拼接，关卡制作到最终游戏上线，研发过程中都有大量工具支撑。

**灵活的工作流** 白鹭引擎不限制开发工具的使用，我们也为一些优秀的第三方工具提供了相关插件。让用户在不改变开发习惯的情况下无缝迁移到Egret。

**社区支持** 白鹭引擎为用户建立了用户社区，如果在使用白鹭引擎过程中遇到了哪些问题，可以直接在用户社区中得到答案。同时，我们也为用户提供了大量文档手册，方便用户学习。

## 白鹭引擎主要功能

白鹭引擎继承了Flash的优点，同时更加针对游戏开发，主要包括如下功能：

  - 显示列表：将游戏中的可视化元素抽象为视觉模型，通过显示列表可以灵活的控制游戏中可视化元素
  - 精灵：一种轻量级显示容器
  - 事件机制：提供了一套生成和处理事件消息的标准方法
  - 纹理集合：将大量图片汇集为一张纹理图进行处理
  - 矢量绘图：封装了方便简单的矢量绘图功能
  - 网络加载：封装了常用的网络通讯协议
  - 位图字体：可通过位图字体方式显示文本
  - 性能监控：可在游戏中快速开启性能监控面板
  - 反射：对TypeScript增加了反射机制，方便模块化开发
  - XML处理：提供标准的XML格式解析生成功能
  - 骨骼动画：支持业内最优骨骼动画解决方案DragonBones
  - 资源加载：提供了整套资源加载方案，优化网络加载功能
  - EUI：提供大量组件，可快速开发游戏中的UI控件
  - 脏矩形渲染：可以手动控制渲染过程中的脏矩形区域
  - WebSocket支持：可以使用内置的WebSocket

## 模块

  - 物理系统：内置物理系统模块，可以制作逼真的物理碰撞效果，模拟真实世界效果

<!-- end list -->

  - 屏幕适配模块：提供4中屏幕适配策略，可以方便进行切换，使用不同分辨率手机屏幕

<!-- end list -->

  - 三种渲染模式无缝切换：可以在DOM、Canvas和WebGL模式下渲染

<!-- end list -->

  - 粒子库系统：可以制作精美的粒子效果

## 白鹭产品家族

除了核心引擎Egret Engine（白鹭引擎）外，白鹭时代已构建起一条完整的专业工作流, Egret Runtime（白鹭加速器）, Egret Wing（可视化编辑器）, DragonBones（骨骼动画工具）等10余款工具可让开发者简单、高效的开发出移动游戏。   **白鹭引擎3D**：业内首款 真3D HTML5 游戏引擎。白鹭引擎3D版本拥有强大的 3D 编辑器系统，支持 Unity 工作流导出，高性能和小巧包体满足H5 3D游戏在PC、APP、H5 三端齐发。白鹭引擎3D支持 GPU 骨骼动画、高级灯光烘焙、可编程渲染管线、泛光、环境光效果、高级纹理、基于Web Audio音频引擎和完善的实时通信网络模块，以及大型网络游戏必须的延迟渲染技术。除此以外 白鹭引擎3D还支持全功能后期特效处理，包括后期材质、抗锯齿、融合、景深等功能。 

**骨骼动画（DragonBones）**：DragonBones是国内首款支持HTML5动漫国际标准的创作工具。它是白鹭时代推出的面向设计师的动画与动漫创作平台。包含了可创作骨骼动画、帧动画和可交互动态漫画的集成式创作工具DragonBones Pro、Flash动画导出插件，并支持各大平台主流引擎的运行库。2017年7月，DragonBones5.3版正式上线。

**白鹭加速器（Egret Runtime）**：这是一款支持3D的HTML5游戏加速器，主要解决解决低端机对HTML5标准支持不佳、体验差的弊端，通过Runtime适配不同的系统让HTML5游戏效果媲美原生游戏。截止到2017年，Runtime已累计接入设备5亿台。

**可视化编辑器（Egret Wing）**：可视化编辑器（Egret Wing）是白鹭时代推出的一款强大而智能的记成开发环境（IDE），支持主流开发语言与技术。通过可视化编辑器，提高游戏开发效率。支持Node.js开发扩展插件，更好地定制化自由内容。使用Egret Wing可以更快速的编写Web相关项目及快速实现Egret可视化内容。

**Lakeshore**：是一款无需编程的免费游戏创作工具，使用Lakeshore的强大功能每个人都可以快速创作效果炫酷的游戏。借助Egret引擎，Lakeshore创作的游戏能够在安卓、iOS和Windows Phone平台上运行。

**Egret Native**：可以将您基于Egret开发的HTML5游戏转换为Android App 和 iOS APP。转换后的APP效率更加接近原生游戏性能，Egret Native通过对QuickSDK的支持，可使你一键生成所有渠道包，更加专注游戏品质。

**Egret Feather**：是一款粒子编辑器，各个参数的组合塑造出千变万化的效果，为游戏添姿添彩。全程可视化编辑操作，屏蔽所有底层复杂的参数设置。所见即所得的操作模式，让即使毫无编程技能的美术人员也可快速上手，立即制作出精美的粒子效果。编辑器可以自动导出配置文件供程序开发使用。

**EgretVS**：是一款 Visual Studio 插件，致力于提高 Egret 引擎在 Visual Studio 中的使用体验。

**Texture Merger**：是一款纹理集打包和动画转换工具。它能将零散的小图合并为大图纹理集，提高资源加载速度和游戏性能。在游戏研发过程中，开发者可以使用小图开发，等到产品发布时再对资源进行合并，完全不用修改代码Texture Merger 可以方便的将 GIF 和 SWF 动画转换为 Egret 支持的动画格式。

**Egret Conversion**：是白鹭时代推出的一款重要产品，可以快速的将现有的Flash项目转换到Egret HT ML5项目。界面友好易用，无需其他工具的辅助。功能强大可扩展，支持AS3各种复杂语法特性，涵盖绝大部分的Flash API，并且支持swf资源的直接转换。

**Egret Inspector**：是一款 供Chrome 开发者使用的插件，能够帮助开发者可视化地调试 Egret 项目。

**ResDepot**：是 Egret游戏的可视化资源管理工具。它能轻松高效地管理大量游戏素材和配置文件资源.帮您快速制作生成 Egret 游戏中所需的资源配置文件，轻松定制灵活的分组加载规则。通过可视化的拖拽操作，快速完成资源配置文件。\[1\] 

## 参考资料

## 参见

## 外部链接

  - [egret](https://www.egret.com/en/)

[Category:電子遊戲開發軟件](https://zh.wikipedia.org/wiki/Category:電子遊戲開發軟件 "wikilink")

1.