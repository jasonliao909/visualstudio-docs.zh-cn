---
title: 教程：向匹配游戏中添加计时器
description: 在本教程中，你将使用引用变量通过 C# 或 VB Windows 窗体控制 Visual Studio 中的标签。 添加计时器以运行匹配游戏。
dev_langs:
- CSharp
- VB
author: anandmeg
ms.author: meghaanand
manager: jmartens
ms.technology: vs-ide-general
ms.topic: tutorial
ms.date: 01/07/2022
ms.custom:
- vs-acquisition
ms.openlocfilehash: 6ce2cb57087d70be2858ce625289edfdc2d87a7c
ms.sourcegitcommit: 9b1c1cceab4c59f0b91e19ae46a51969f72fcc34
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/13/2022
ms.locfileid: "136806153"
---
# <a name="tutorial-add-reference-variables-and-a-timer-control-to-your-matching-game-winforms-app"></a>教程：向匹配游戏 WinForms 应用中添加引用变量和计时器控件

在这四个教程系列中，你将构建一个匹配游戏，玩家在其中匹配隐藏的图标对。

匹配游戏程序需要跟踪玩家选择了哪些标签控件。
在玩家选择第一个标签后，该程序应显示图标。
在选择第二个标签后，该程序应短暂显示两个图标。
然后隐藏这两个图标。

程序通过引用变量跟踪第一次和第二次分别选择的标签控件。
计时器隐藏图标并控制显示图标的时间长度

> [!div class="checklist"]
> - 添加标签引用。
> - 添加计时器。

## <a name="prerequisites"></a>必备条件

本教程基于前面的教程，即[创建匹配游戏应用程序](tutorial-windows-forms-create-match-game.md)和[向匹配游戏中添加图标](tutorial-windows-forms-match-game-icons.md)。
请先参阅这些教程。

## <a name="add-label-references"></a>添加标签引用

本部分将向代码添加两个引用变量。
它们跟踪或引用标签对象。

1. 通过使用下面的代码向窗体中添加标签引用。

   :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VBCSharp/vbexpresstutorial4step5/vb/form1.vb" id="Snippet5":::
   :::code language="csharp" source="../snippets/csharp/VS_Snippets_VBCSharp/vbexpresstutorial4step5/cs/form1.cs" id="Snippet5":::

   [!INCLUDE [devlang-control-csharp-vb](./includes/devlang-control-csharp-vb.md)]

   这些语句不会导致窗体中显示标签控件，因为没有 `new` 关键字。
   当程序启动时，`firstClicked` 和 `secondClicked` 都设置为 `null`（对于 C#）或 `Nothing`（对于 Visual Basic）。

1. 修改 <xref:System.Windows.Forms.Control.Click> 事件处理程序，以使用新的 `firstClicked` 引用变量。
   移除 `label_Click()` 事件处理程序方法中的最后一个语句 (`clickedLabel.ForeColor = Color.Black;`)，并将它替换为下面的 `if` 语句。

   :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VBCSharp/vbexpresstutorial4step5/vb/form1.vb" id="Snippet6":::
   :::code language="csharp" source="../snippets/csharp/VS_Snippets_VBCSharp/vbexpresstutorial4step5/cs/form1.cs" id="Snippet6":::

1. 保存并运行程序。 选择其中一个标签控件，它的图标将显示。
   选择下一个标签控件，发现没有任何反应。

   ![屏幕截图显示具有一个图标的匹配游戏。](../ide/media/tutorial-windows-forms-match-game-icons/match-game-start.png)

   只有选择的第一个图标变为黑色。
   其他图标是不可见的。

该程序已跟踪玩家选择的第一个标签。
引用 `firstClicked` 不是 C# 中的 `null` 或 Visual Basic 中的 `Nothing`。
当 `if` 语句发现 `firstClicked` 不等于 `null` 或 `Nothing` 时，不会运行这些语句。

## <a name="add-a-timer"></a>添加计时器

匹配游戏使用 <xref:System.Windows.Forms.Timer> 控制应用。
计时器等待后，触发一个称为“Tick”的事件。
计时器可以启动操作或定期重复操作。

在程序中，计时器允许玩家选择两个图标。
如果图标不匹配，则在短暂时间后再次隐藏这两个图标。

1. 选择“工具箱”选项卡，在“组件”类别中，双击“计时器”组件或将其拖到窗体中。
   该计时器图标名为“timer1”，显示在窗体下的空间中。

   ![屏幕截图显示窗体下的计时器图标。](../ide/media/tutorial-windows-forms-match-game-labels/timer-control-icon.png)

1. 选择“Timer1”图标以选中该计时器。
   在“属性”窗口中，选择“属性”按钮以查看属性。

1. 将“间隔”属性设置为“750”，即 750 毫秒。

   “间隔”属性将通知计时器两个时钟周期之间的等待时长，或何时触发 <xref:System.Windows.Forms.Timer.Tick> 事件。
   在玩家选择第二个标签后，程序调用 <xref:System.Windows.Forms.Timer.Start> 方法启动计时器。

1. 选择计时器控件图标，然后按 Enter，或双击计时器。
   IDE 添加空的 Tick 事件处理程序。
   将代码替换为以下代码。

   :::code language="csharp" source="../snippets/csharp/VS_Snippets_VBCSharp/vbexpresstutorial4step6/cs/form1.cs" id="Snippet7":::
   :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VBCSharp/vbexpresstutorial4step6/vb/form1.vb" id="Snippet7":::

   Tick 事件处理程序将执行三项操作：

   - 通过调用 <xref:System.Windows.Forms.Timer.Stop> 方法确保计时器没有运行。
   - 它使用两个引用变量 `firstClicked` 和 `secondClicked`，使得玩家选择的两个标签的图标再次不可见。
   - 它将 `firstClicked` 和 `secondClicked` 引用变量重置为 `null`（C# 中）或 `Nothing`（Visual Basic 中）。

1. 转至代码编辑器，将以下代码添加到 `label_Click()` 事件处理程序方法的顶部和底部。
   将两个 `if` 语句添加到顶部，将三个语句添加到底部。

   :::code language="csharp" source="../snippets/csharp/VS_Snippets_VBCSharp/vbexpresstutorial4step6/cs/form1.cs" id="Snippet8":::
   :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VBCSharp/vbexpresstutorial4step6/vb/form1.vb" id="Snippet8":::

   - 该方法顶部的代码通过检查 **Enabled** 属性的值来检查计时器是否已启动。
     如果玩家选择第一个和第二个标签控件，且计时器启动，则选择第三个控件将不会执行任何操作。

   - 该方法底部的代码将 `secondClicked` 引用变量设置为跟踪第二个标签控件。
     然后将该标签的图标颜色设置为黑色以使其可见。
     然后，它在单触发模式下启动计时器，以便在等待 750 毫秒后触发单个 Tick。
     计时器的 Tick 事件处理程序会隐藏这两个图标，并重置 `firstClicked` 和 `secondClicked` 引用变量。
     窗体准备就绪供玩家选择另一对图标。

1. 保存并运行程序。
   选择一个正方形，图标将变得可见。
   选择另一个正方形。
   图标会短暂显示，然后两个图标都消失。

程序现在跟踪你选择的第一个和第二个图标。
它使用计时器在使图标消失之前暂停。

## <a name="next-steps"></a>后续步骤

请继续阅读下一篇教程，了解如何完成匹配游戏。
> [!div class="nextstepaction"]
> [为匹配游戏显示祝贺消息](tutorial-windows-forms-match-game-play.md)
