---
title: 调试时映射调用堆栈上的方法
description: 了解如何创建代码图，以在调试时直观地跟踪调用堆栈。 此外，请了解你可以在地图上进行注释，以跟踪代码正在执行哪些工作。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
f1_keywords:
- vs.progression.debugwithcodemaps
dev_langs:
- FSharp
- VB
- CSharp
- C++
helpviewer_keywords:
- call stacks, code maps
- Call Stack window, mapping calls
- debugging [Visual Studio], diagramming the call stack
- call stacks, mapping
- Call Stack window, visualizing
- debugging code visually
- debugging [Visual Studio], mapping the call stack
- call stacks, visualizing
- debugging, code maps
- Call Stack window, tracing calls visually
- Call Stack window, show on code map
- debugging [Visual Studio], tracing the call stack visually
- debugging [Visual Studio], visualizing the call stack
author: mgoertz-msft
ms.author: mgoertz
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 08fa0ff028140ebad421dd43fdfa53cc36b77804
ms.sourcegitcommit: e3a364c014ccdada0860cc4930d428808e20d667
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2021
ms.locfileid: "112387484"
---
# <a name="map-methods-on-the-call-stack-while-debugging-in-visual-studio"></a>在 Visual Studio 中调试时映射调用堆栈上的方法

创建代码映射，以便在调试时对调用堆栈进行可视化跟踪。 你可以在图中进行标注以跟踪代码执行的操作，以便专注于查找 Bug。

 ![使用代码图上的调用堆栈调试](../debugger/media/debuggermap_overview.png)

 需要：

 ::: moniker range="vs-2017"

- [Visual Studio Enterprise](https://visualstudio.microsoft.com/vs/older-downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=vs+2017+download)

::: moniker-end

::: moniker range=">=vs-2019"

- [Visual Studio Enterprise](https://visualstudio.microsoft.com/downloads)

::: moniker-end

- 可以调试的代码，例如 Visual C#、Visual Basic、C++、JavaScript 或 X++

  请参阅：

- [视频：使用代码图调试器集成进行可视化调试 (第 9 频道) ](https://channel9.msdn.com/Series/Visual-Studio-2012-Premium-and-Ultimate-Overview/Visual-Studio-Ultimate-2012Debug-visually-with-Code-Map-debugger-integration)

- [映射调用堆栈](#MapStack)

- [记下代码](#MakeNotes)

- [使用下一个调用堆栈更新映射](#UpdateMap)

- [将相关代码添加到地图](#AddRelatedCode)

- [使用地图查找 bug](#FindBugs)

- [问答](#QA)

  有关在使用代码图时可以使用的命令和操作的详细信息，请参阅 [浏览和重新排列代码图](../modeling/browse-and-rearrange-code-maps.md)。

## <a name="map-the-call-stack"></a><a name="MapStack"></a>映射调用堆栈

1. 开始调试。  (键盘 **：F5**) 

2. 在应用进入中断模式或进入函数后，选择"代码 **映射"。**  (键盘 **：Ctrl**  +  **Shift**  +  **`**) 

     ![选择代码图以开始映射调用堆栈](../debugger/media/debuggermap_choosecodemap.png)

     当前的调用堆栈在新代码图上显示为橙色：

     ![查看代码图上的调用堆栈](../debugger/media/debuggermap_seeundocallstack.png)

     在你继续调试时，该代码图将自动更新。 请参阅 [使用下一个调用堆栈 更新映射](#UpdateMap)。

## <a name="make-notes-about-the-code"></a><a name="MakeNotes"></a>对代码进行标注

 添加注释以跟踪代码中发生的情况。 若要在注释中添加新行，请按 **Shift + Return**。

 ![向代码图上的调用堆栈添加注释](../debugger/media/debuggermap_addcomment.png)

## <a name="update-the-map-with-the-next-call-stack"></a><a name="UpdateMap"></a>使用下一个调用堆栈更新映射

 运行你的应用到下一个断点或单步执行某一函数。 此图将添加新的调用堆栈。

 ![使用下一个调用堆栈更新代码图](../debugger/media/debuggermap_addclearcallstack.png)

## <a name="add-related-code-to-the-map"></a><a name="AddRelatedCode"></a>向映射添加相关代码

 现在你有了一个地图 - 接下来做什么？ 如果使用 C# 或 Visual Basic，请添加字段、属性和其他方法等项，以跟踪代码中发生的情况。

 双击某个方法以查看其代码定义，或者使用该方法的快捷菜单。  (键盘：选择地图上的 方法，然后按 **F12**) 

 ![转到代码图上某方法的代码定义](../debugger/media/debuggermap_gotocodedefinition.png)

 添加要在图上跟踪的项。

 ![显示调用堆栈代码图上某方法中的字段](../debugger/media/debuggermap_showfields.png)

> [!NOTE]
> 默认情况下，向图添加项还会添加父组节点（如类、命名空间和程序集）。 虽然这很有用，但可以通过使用地图工具栏上的"包括父项"按钮或添加项时按 **CTRL** 来关闭此功能，使地图保持简单。

 ![调用堆栈代码图上与某方法相关的字段](../debugger/media/debuggermap_showedfields.png)

 在这里，你可以轻松查看哪些方法使用了相同的字段。 最近添加的项显示为绿色。

 继续生成图以查看更多代码。

 ![查看使用字段的方法：调用堆栈代码图](../debugger/media/debuggermap_findallreferences.png)

 ![调用堆栈代码图上使用某字段的方法](../debugger/media/debuggermap_foundallreferences.png)

## <a name="find-bugs-using-the-map"></a><a name="FindBugs"></a>使用映射查找 Bug

 通过代码可视化，可帮助你更快发现 Bug。 例如，假设你正在调查绘图程序中的 bug。 当你绘制一条线并尝试撤消该操作时，直到你绘制另一条线后才会发生变化。

 因此，可在 `clear`、`undo` 和 `Repaint` 方法中设置断点，启动调试，然后生成如下所示的图：

 ![向代码图添加另一个调用堆栈](../debugger/media/debuggermap_addpaintobjectcallstack.png)

 你注意到图中所有用户笔势均调用 `Repaint`，但 `undo` 除外。 这可能解释了 `undo` 不立即发挥作用的原因。

 在修复此 Bug 并继续运行程序后，图中增加了从 `undo` 到 `Repaint` 的新调用：

 ![向代码图上的调用堆栈添加新方法调用](../debugger/media/debuggermap_addnewcallforrepaint.png)

## <a name="q--a"></a><a name="QA"></a> 问题解答

- **并非所有调用都显示在地图上。为什么？**

   默认情况下，只有你自己的代码会显示在图中。 若要查看外部代码，请打开"调用堆栈 **"** 窗口：

   ![使用“调用堆栈”窗口显示外部代码](../debugger/media/debuggermap_callstackmenu.png)

   或关闭 **"启用仅我的代码** 调试Visual Studio选项中的"启用"：

   ![使用“选项”对话框显示外部代码](../debugger/media/debuggermap_debugoptions.png)

- **更改图是否会影响代码？**

   更改映射不会以任何方式影响代码。 你可随意在图上重命名、移动或移除任何内容。

- **此消息的含义是什么："关系图可能基于较旧版本的代码"？**

   在你上次更新图后，代码可能已发生更改。 例如，图中的某个调用可能已在代码中不存在了。 请关闭此消息，然后在再次更新图之前，尝试重新生成解决方案。

- **如何实现地图布局吗？**

   打开地图 **工具栏** 上的"布局"菜单：

  - 更改默认布局。

  - 若要自动停止重新组织地图，请调试 **时关闭"自动布局"。**

  - 若要在添加项时尽可能少地重新排列地图，请关闭增量 **布局**。

- **我能否与他人共享此图？**

   可以导出地图、将其发送给其他人（如果有 Microsoft Outlook）或将其保存到解决方案，以便将其签入源代码管理。

   ![与他人共享调用堆栈代码图](../debugger/media/debuggermap_sharewithothers.png)

- **我如何停止此图自动添加新的调用堆栈？**

   选择 ![ "按钮&#45;在代码图上自动在地图 ](../debugger/media/debuggermap_automaticupdateicon.gif) 工具栏上显示调用堆栈。 若要手动向图中添加当前的调用堆栈，请按 Ctrl + Shift + `  。

   调试时，映射将继续突出显示地图上的现有调用堆栈。

- **项图标和箭头代表什么？**

   若要获取有关项的详细信息，请移动鼠标指针并查看该项的工具提示。 还可以查看图例 **，** 了解每个图标的含义。

   ![调用堆栈代码图上各图标的含义](../debugger/media/debuggermap_showlegend.png)

  请参阅：

- [映射调用堆栈](#MapStack)

- [记下代码](#MakeNotes)

- [使用下一个调用堆栈更新映射](#UpdateMap)

- [将相关代码添加到地图](#AddRelatedCode)

- [使用地图查找 bug](#FindBugs)

## <a name="see-also"></a>请参阅

- [映射解决方案中的依赖项](../modeling/map-dependencies-across-your-solutions.md)
- [使用代码图调试应用程序](../modeling/use-code-maps-to-debug-your-applications.md)
- [使用代码图分析查找潜在问题](../modeling/find-potential-problems-using-code-map-analyzers.md)
- [浏览和重新排列代码图](../modeling/browse-and-rearrange-code-maps.md)
