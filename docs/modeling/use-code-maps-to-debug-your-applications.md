---
title: 使用代码图调试你的应用程序
description: 了解如何使用代码图来帮助避免在大型代码库、不熟悉的代码或旧代码中丢失。
ms.custom: SEO-VS-2020
ms.date: 09/28/2018
ms.topic: conceptual
helpviewer_keywords:
- Visual Studio Ultimate, visualizing code
- Visual Studio Ultimate, navigating code visually
- Visual Studio Ultimate, understanding code
- Visual Studio Ultimate, mapping code relationships
- Visual Studio Ultimate, code maps
- mapping code relationships
- code maps
- mapping relationships in code
author: mgoertz-msft
ms.author: mgoertz
manager: jmartens
ms.technology: vs-ide-modeling
ms.workload:
- multiple
ms.openlocfilehash: 8888191a2b482aba2ff1fed2233e7156a0bf52564f1cac3339d8293d10fb36e2
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121399018"
---
# <a name="use-code-maps-to-debug-your-applications"></a>使用代码图调试你的应用程序

[Visual Studio 中的代码图](../modeling/map-dependencies-across-your-solutions.md)可以帮助你避免在大型代码库、不熟悉的代码或旧代码中丢失。 例如，当您进行调试时，可能需要跨多个文件和项目查看代码。 使用代码图在这些代码段中导航，了解代码段之间的关系。 这样，你不必在脑海中跟踪此代码，或绘制单独的关系图。 所以，在你的工作中断时，代码图有助于让你回想起你正在处理的代码。

![代码图 &#45; 在代码中映射关系](../modeling/media/codemapstoryboardpaint.png)

**绿色箭头显示你的光标在编辑器中的显示位置**

有关使用代码图时可以使用的命令和操作的详细信息，请参阅 [浏览和重新排列代码图](../modeling/browse-and-rearrange-code-maps.md)。

详细了解如何[通过调试器工具在 Visual Studio 中进行调试](../debugger/debugger-feature-tour.md)。

> [!NOTE]
> 若要创建和编辑代码图，需要 Visual Studio Enterprise 版本。 在 Visual Studio Community 和 Professional 版本中，你可以打开在 Enterprise edition 中生成的关系图，但不能对其进行编辑。

## <a name="understand-the-problem"></a>了解问题
 假定你正在处理的绘图程序中有 Bug。 若要重现 bug，请在 Visual Studio 中打开解决方案，然后按 **F5** 开始调试。

 绘制线条并选择 " **撤消最后一个笔画**" 时，直到绘制下一行。

 ![代码图 &#45; 重现 bug](../modeling/media/codemapstoryboardpaint0.png)

 因此你开始通过搜索 `Undo` 方法来进行调查。 你将会在 `PaintCanvas` 类中找到它。

 ![&#45; 查找代码的代码图](../modeling/media/codemapstoryboardpaint1.png)

## <a name="start-mapping-the-code"></a>开始映射代码
 现在开始映射 `undo` 方法及其关系。 从代码编辑器中，将 `undo` 方法及其引用的字段添加到新的代码图。 创建新的代码图时，可能需要一些时间来为代码编制索引。 这有助于加快后续操作的运行速度。

 ![代码图 &#45; 显示方法和相关字段](../modeling/media/codemapstoryboardpaint3.png)

> [!TIP]
> 突出显示的绿色部分显示了上次添加到代码图中的项。 绿色箭头显示你的光标在代码中的位置。 各项之间的箭头表示不同的关系。 你可以通过将鼠标悬停在项上并查看相应的工具提示来详细了解有关代码图上各项的详细信息。

 ![代码图 &#45; 显示工具提示](../modeling/media/codemapstoryboardpaint4.png)

## <a name="navigate-and-examine-code-from-the-map"></a>浏览并检查映射中的代码
 若要查看每个字段的代码定义，请双击地图上的字段，或选择该字段并按 **F12**。 绿色箭头在代码图上的各项之间移动。 代码编辑器中的光标也会自动移动。

 !["代码图" 窗口的屏幕截图，其中选择了 "历史记录" 字段和 "代码编辑器" 窗口，其中突出显示了历史记录的所有实例。](../modeling/media/codemapstoryboardpaint5.png)

 !["代码图" 窗口的屏幕截图，其中选择了 "paintObjects" 字段和 "代码编辑器" 窗口，其中 paintObjects 的所有实例都会突出显示。](../modeling/media/codemapstoryboardpaint5a.png)

> [!TIP]
> 你还可以通过在代码编辑器中移动光标来移动代码图上的绿色箭头。

## <a name="understand-relationships-between-pieces-of-code"></a>了解代码部分之间的关系
 现在你需要知道与 `history` 和 `paintObjects` 字段交互的其他代码。 你可以将引用这些字段的所有方法添加到代码图。 你可以通过代码图或代码编辑器执行此操作。

 ![&#45; 查找所有引用的代码图](../modeling/media/codemapstoryboardpaint6.png)

 ![从代码编辑器打开代码图](../modeling/media/codemapstoryboardpaint6a.png)

> [!NOTE]
> 如果你从多个应用（如 Windows Phone 或 Windows 应用商店）之间共享的项目添加项，那么这些项将始终与当前活动的应用程序项目一起显示在代码图上。 因此，如果将上下文更改为另一个应用项目，那么代码图上的上下文也会更改为共享项目中的任何新添加项。 你对代码图上的项执行的操作仅适用于共享相同上下文的项。

 更改布局以重新排列关系流并使代码图更容易阅读。 你还可以通过在代码图上拖动各个项来移动它们。

 ![代码图窗口的屏幕截图，其中打开了布局菜单并选中了 "左侧到 Rgiht" 命令。](../modeling/media/codemapstoryboardpaint7a.png)

> [!TIP]
> 默认情况下，" **增量布局** " 处于打开状态。 当你添加新的项时，这会尽可能少地重新排列代码图。 若要在每次添加新项时重新排列整个映射，请关闭 " **增量布局**"。

 ![在从左到右的字段之间有 relationshiop 箭头的代码图窗口的屏幕截图。](../modeling/media/codemapstoryboardpaint7.png)

 让我们检查这些方法。 在地图上，双击 " **PaintCanvas** " 方法，或选择此方法并按 " **F12**"。 你将了解到，此方法将以空列表的形式创建 `history` 和 `paintObjects`。

 ![代码图窗口的屏幕截图，其中选择了 PaintCanvas 方法，并显示了显示 PainCanvas 方法名称的代码段图像。](../modeling/media/codemapstoryboardpaint8.png)

 现在请重复相同的步骤以检查 `clear` 方法定义。 你将了解到，`clear` 会通过 `paintObjects` 和 `history` 执行某些任务， 然后它将调用 `Repaint` 方法。

 ![代码图窗口的屏幕截图，其中选择了 Clear 方法，并显示了显示 Clear 方法代码的代码段图像。](../modeling/media/codemapstoryboardpaint9.png)

 现在请检查 `addPaintObject` 方法定义。 它也使用 `history` 和 `paintObjects` 执行某些任务， 它还调用 `Repaint`。

 !["代码图" 窗口的屏幕截图，其中选择了 addPaintObject 方法和一个显示 addPaintObject 方法代码的代码段图像。](../modeling/media/codemapstoryboardpaint10.png)

## <a name="find-the-problem-by-examining-the-map"></a>通过检查映射找到问题
 似乎修改 `history` 和 `paintObjects` 的所有方法都会调用 `Repaint`。 但是，`undo` 方法不会调用 `Repaint`，即使 `undo` 修改相同的字段。 因此，你认为可以通过从 `Repaint` 调用 `undo` 来解决此问题。

 ![&#45; 查找缺少的方法调用的代码图](../modeling/media/codemapstoryboardpaint11.png)

 如果你没有可显示此缺失调用的代码图，要找到此问题或许更加困难，尤其是在具有更复杂的代码时。

## <a name="share-your-discovery-and-next-steps"></a>共享发现和后续步骤
 在你或其他人修复此 Bug 之前，你可在代码图上针对此问题和解决方法进行注释。

 ![用于跟踪的代码映射 &#45; 注释和标记项](../modeling/media/codemapstoryboardpaint12.png)

 例如，你可以在代码图上添加注释并使用颜色标记项。

 ![代码图 &#45; 注释和标记的项](../modeling/media/codemapstoryboardpaint12a.png)

 如果已安装 Microsoft Outlook，则可以将代码图以电子邮件的形式发送给其他人。 还可以将代码图导出为图像或其他格式。

 ![代码图 &#45; 共享、导出、发送邮件](../modeling/media/codemapstoryboardpaint13.png)

## <a name="fix-the-problem-and-show-what-you-did"></a>解决该问题并显示你所做的工作
 若要修复此 Bug，你需要将 `Repaint` 的调用添加到 `undo`。

 ![代码图 &#45; 添加缺失的方法调用](../modeling/media/codemapstoryboardpaint14.png)

 若要确认你的修复，请重新启动你的调试会话并尝试重现 Bug。 现在，选择 " **撤消上一个笔划"** 会按预期工作，并确认已进行正确的修复。

 ![代码图 &#45; 确认代码修复](../modeling/media/codemapstoryboardpaint15.png)

 你可以更新代码图以显示所做的修复。

 ![缺少方法调用的代码图 &#45; 更新映射](../modeling/media/codemapstoryboardpaint16.png)

 你的地图现在显示 **撤消** 和重 **绘** 之间的链接。

 ![用方法调用更新映射 &#45; 代码图](../modeling/media/codemapstoryboardpaint17.png)

> [!NOTE]
> 更新代码图时，你可能会看到说明用于创建代码图的代码索引已更新的消息。 这意味着有人更改了代码，造成你的代码图与当前代码不匹配。 这不会阻止你更新代码图，但你可能必须重新创建代码图以确认它与代码匹配。

 现在，你已经完成了调查。 你通过映射代码成功找到并解决了问题。 你也拥有可帮助你浏览代码的代码图，请记住你所学的内容并演示你用于解决此问题的步骤。

## <a name="see-also"></a>请参阅

- [调试时映射调用堆栈上的方法](../debugger/map-methods-on-the-call-stack-while-debugging-in-visual-studio.md)
- [代码可视化](../modeling/visualize-code.md)
