---
title: 调试时映射调用堆栈上的方法
description: 了解如何创建代码图，以便在调试时对调用堆栈进行可视化跟踪。 另外，了解在图中进行标注以跟踪代码执行的操作。
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
ms.technology: vs-ide-modeling
ms.workload:
- multiple
ms.openlocfilehash: c2c9a458c1955e999196574ed4fd9a174241f66a
ms.sourcegitcommit: fc874be3fe4637a23997b4ef2d99a2ee9a499581
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/22/2021
ms.locfileid: "135517282"
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

- 可调试的代码，例如 Visual C#、Visual Basic、C++、JavaScript 或 X++

  请参阅：

- [生成调用堆栈图](#MapStack)

- [对代码进行标注](#MakeNotes)

- [使用下一个调用堆栈更新图](#UpdateMap)

- [向图中添加相关代码](#AddRelatedCode)

- [使用图查找 bug](#FindBugs)

- [问答](#QA)

  若要详细了解使用代码图时能使用的命令和操作，请参阅[浏览和重新排列代码图](../modeling/browse-and-rearrange-code-maps.md)。

## <a name="map-the-call-stack"></a><a name="MapStack"></a>映射调用堆栈

1. 开始调试。 （键盘：F5）

2. 在应用进入中断模式或你单步执行某一函数之后，请选择“代码图”。 （键盘：Ctrl + Shift + `  ）

     ![选择代码图以开始映射调用堆栈](../debugger/media/debuggermap_choosecodemap.png)

     当前的调用堆栈在新代码图上显示为橙色：

     ![查看代码图上的调用堆栈](../debugger/media/debuggermap_seeundocallstack.png)

     在你继续调试时，该代码图将自动更新。 请参阅[使用下一个调用堆栈更新图](#UpdateMap)。

## <a name="make-notes-about-the-code"></a><a name="MakeNotes"></a>对代码进行标注

 添加注释以跟踪代码中的情况。 若要在注释中添加新行，请按 Shift + Return。

 ![向代码图上的调用堆栈添加注释](../debugger/media/debuggermap_addcomment.png)

## <a name="update-the-map-with-the-next-call-stack"></a><a name="UpdateMap"></a>使用下一个调用堆栈更新映射

 运行你的应用到下一个断点或单步执行某一函数。 此图将添加新的调用堆栈。

 ![使用下一个调用堆栈更新代码图](../debugger/media/debuggermap_addclearcallstack.png)

## <a name="add-related-code-to-the-map"></a><a name="AddRelatedCode"></a>向映射添加相关代码

 现在你已生成一个图，下一步做什么？ 如果你使用的是 C# 或 Visual Basic，请添加字段、属性和其他方法等项，以便跟踪代码中发生的情况。

 双击某个方法以查看其代码定义，或者使用该方法的快捷菜单。 （键盘：在图上选择该方法，然后按 F12）

 ![转到代码图上某方法的代码定义](../debugger/media/debuggermap_gotocodedefinition.png)

 添加要在图上跟踪的项。

 ![显示调用堆栈代码图上某方法中的字段](../debugger/media/debuggermap_showfields.png)

> [!NOTE]
> 默认情况下，向图添加项还会添加父组节点（如类、命名空间和程序集）。 尽管这很有用，不过可以通过使用图工具栏上的“包括父级”按钮关闭此功能，或通过在添加项时按 CTRL，来仅仅保留图 。

 ![调用堆栈代码图上与某方法相关的字段](../debugger/media/debuggermap_showedfields.png)

 在这里，你可以轻松查看哪些方法使用了相同的字段。 最近添加的项显示为绿色。

 继续生成图以查看更多代码。

 ![查看使用字段的方法：调用堆栈代码图](../debugger/media/debuggermap_findallreferences.png)

 ![调用堆栈代码图上使用某字段的方法](../debugger/media/debuggermap_foundallreferences.png)

## <a name="find-bugs-using-the-map"></a><a name="FindBugs"></a>使用映射查找 Bug

 通过代码可视化，可帮助你更快发现 Bug。 例如，假设你正在一个绘图程序中调查 bug。 当你绘制一条线并尝试撤消该操作时，直到你绘制另一条线后才会发生变化。

 因此，可在 `clear`、`undo` 和 `Repaint` 方法中设置断点，启动调试，然后生成如下所示的图：

 ![向代码图添加另一个调用堆栈](../debugger/media/debuggermap_addpaintobjectcallstack.png)

 你注意到图中所有用户笔势均调用 `Repaint`，但 `undo` 除外。 这可能解释了 `undo` 不立即发挥作用的原因。

 在修复此 Bug 并继续运行程序后，图中增加了从 `undo` 到 `Repaint` 的新调用：

 ![向代码图上的调用堆栈添加新方法调用](../debugger/media/debuggermap_addnewcallforrepaint.png)

## <a name="q--a"></a><a name="QA"></a> 问题解答

- **并非所有调用都会显示在图中。这是为什么？**

   默认情况下，只有你自己的代码会显示在图中。 若要查看外部代码，请在”调用堆栈“窗口中打开它：

   ![使用“调用堆栈”窗口显示外部代码](../debugger/media/debuggermap_callstackmenu.png)

   或在 Visual Studio 调试选项中关闭“启用仅我的代码”：

   ![使用“选项”对话框显示外部代码](../debugger/media/debuggermap_debugoptions.png)

- **更改图是否会影响代码？**

   更改图不会对代码造成任何影响。 你可随意在图上重命名、移动或移除任何内容。

- **“关系图可能基于旧版本的代码”这一消息的含义是什么？**

   在你上次更新图后，代码可能已发生更改。 例如，图中的某个调用可能已在代码中不存在了。 请关闭此消息，然后在再次更新图之前，尝试重新生成解决方案。

- **我如何控制图的布局？**

   打开图工具栏上的“布局”菜单：

  - 更改默认布局。

  - 若要停止自动重新排列图，请关闭“调试时自动布局”。

  - 若要在添加新项时尽可能少地重新排列图，请关闭“增量布局”。

- **我能否与他人共享此图？**

   你可以导出图，将其发送给他人（如果你有 Microsoft Outlook）或保存到你的解决方案中，以便你将其签入源代码管理。

   ![与他人共享调用堆栈代码图](../debugger/media/debuggermap_sharewithothers.png)

- **我如何停止此图自动添加新的调用堆栈？**

   选择菜单栏上的![按钮 &#45; 自动在代码图上显示调用堆栈](../debugger/media/debuggermap_automaticupdateicon.gif)。 若要手动向图中添加当前的调用堆栈，请按 Ctrl + Shift + `  。

   在你进行调试时，图中将继续突出显示现有调用堆栈。

- **项图标和箭头代表什么？**

   若要获取有关某个项的详细信息，请将鼠标指针移动到它上方，然后查看该项的工具提示。 你还可以查看“图例”来了解每个图标的含义。

   ![调用堆栈代码图上各图标的含义](../debugger/media/debuggermap_showlegend.png)

  请参阅：

- [生成调用堆栈图](#MapStack)

- [对代码进行标注](#MakeNotes)

- [使用下一个调用堆栈更新图](#UpdateMap)

- [向图中添加相关代码](#AddRelatedCode)

- [使用图查找 bug](#FindBugs)

## <a name="see-also"></a>请参阅

- [映射解决方案中的依赖项](../modeling/map-dependencies-across-your-solutions.md)
- [使用代码图调试应用程序](../modeling/use-code-maps-to-debug-your-applications.md)
- [使用代码图分析查找潜在问题](../modeling/find-potential-problems-using-code-map-analyzers.md)
- [浏览和重新排列代码图](../modeling/browse-and-rearrange-code-maps.md)
