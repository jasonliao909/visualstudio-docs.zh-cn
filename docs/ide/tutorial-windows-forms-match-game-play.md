---
title: 教程：在玩家获胜时显示消息
description: 在本教程中，将通过添加代码来保持匹配的对可见并在玩家获胜时显示消息，从而完成匹配游戏。
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
ms.openlocfilehash: faf624f10a9618f152427d17c4fb616d29a3af31
ms.sourcegitcommit: 9b1c1cceab4c59f0b91e19ae46a51969f72fcc34
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/13/2022
ms.locfileid: "136806151"
---
# <a name="tutorial-display-a-message-in-your-matching-game-winforms-app"></a>教程：在匹配游戏 WinForms 应用中显示消息

在这四个教程系列中，你将构建一个匹配游戏，玩家在其中匹配隐藏的图标对。

在本教程中，你将修改匹配游戏以保持匹配的对可见并在玩家获胜时显示祝贺消息。

在本教程中，你将了解如何执行以下操作：

> [!div class="checklist"]
> - 保持对可见。
> - 验证玩家是否获胜。
> - 试用其他功能。

## <a name="prerequisites"></a>必备条件

本教程基于前面的教程，即[创建匹配游戏应用程序](tutorial-windows-forms-create-match-game.md)、[向匹配游戏中添加图标](tutorial-windows-forms-match-game-icons.md)，以及[在匹配游戏中添加计时器](tutorial-windows-forms-match-game-labels.md)（请先参阅这些教程）。

## <a name="keep-pairs-visible"></a>保持对可见

当玩家匹配对时，游戏应当进行重置，这样游戏就不再跟踪使用 `firstClicked` 和 `secondClicked` 引用变量的任何标签。
不应重置匹配的两个标签的颜色。
这些标签将继续显示。

1. 将下面的 `if` 语句添加到 `label_Click()` 事件处理程序方法中。
   将它放在紧靠启动计时器的语句上方代码的结尾处。

   :::code language="csharp" source="../snippets/csharp/VS_Snippets_VBCSharp/vbexpresstutorial4step7/cs/form1.cs" id="Snippet9":::
   :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VBCSharp/vbexpresstutorial4step7/vb/form1.vb" id="Snippet9":::

   [!INCLUDE [devlang-control-csharp-vb](./includes/devlang-control-csharp-vb.md)]

   `if` 语句会检查玩家选择的第一个标签中的图标是否与第二个标签中的图标相同。
   如果图标相同，则程序运行其三个语句。
   前两个语句重置 `firstClicked` 和 `secondClicked` 引用变量。
   它们不再跟踪任何标签。
   第三个语句是 `return` 语句，它跳过方法中的其余语句，不运行它们。

1. 运行程序，然后开始选择窗体上的正方形。

   ![本教程中创建的匹配游戏的屏幕截图。](../ide/media/tutorial-windows-forms-create-match-game/match-game-final.png)

如果选择的是不匹配的对，则将触发计时器的 Tick 事件。
两个图标都会消失。

如果选择的是匹配的对，则将运行新的 `if` 语句。
return 语句会使方法跳过启动计时器的代码。
因此图标保持可见。

## <a name="verify-if-a-player-won"></a>验证玩家是否获胜

你已创建了一个有趣的游戏。
玩家获胜后，游戏应结束。
本部分添加验证玩家是否获胜的方法。

1. 在你的代码底部，`timer1_Tick()` 事件处理程序下方添加一个 `CheckForWinner()` 方法。

   :::code language="csharp" source="../snippets/csharp/VS_Snippets_VBCSharp/vbexpresstutorial4step8/cs/form1.cs" id="Snippet10":::
   :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VBCSharp/vbexpresstutorial4step8/vb/form1.vb" id="Snippet10":::

   该方法使用 C# 中的另一个 `foreach` 循环或Visual Basic 中的 `For Each` 循环以执行 <xref:System.Windows.Forms.TableLayoutPanel> 中的每个标签。
   它会检查每个标签的图标颜色，以验证它是否与背景匹配。
   如果颜色匹配，图标将保持不可见，玩家还没有匹配所有剩余的图标。

   在这种情况下，程序使用 `return` 语句跳过其余方法。
   如果循环遍历所有标签而不执行 `return` 语句，则意味着窗体上的所有图标均已匹配。
   该程序将显示一个恭喜玩家获胜的 MessageBox，然后调用 `Close()` 方法来结束游戏。

   让标签的 <xref:System.Windows.Forms.Control.Click> 事件处理程序调用新的 `CheckForWinner()` 方法。

   :::code language="csharp" source="../snippets/csharp/VS_Snippets_VBCSharp/vbexpresstutorial4step8/cs/form1.cs" id="Snippet11":::
   :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VBCSharp/vbexpresstutorial4step8/vb/form1.vb" id="Snippet11":::

   请确保程序在显示玩家选择的第二个图标后立即检查是否有赢家。 查找设置第二个选中图标颜色的行，然后在该行后直接调用 `CheckForWinner()` 方法。

1. 保存并运行程序。 玩游戏并匹配所有图标。 当你获胜时，该程序将显示一个祝贺性的消息。

   ![屏幕截图显示具有 MessageBox 的匹配游戏。](../ide/media/tutorial-windows-forms-match-game-play/match-game-congratulations.png)

   选择“确定”后，匹配游戏将关闭。

## <a name="try-other-features"></a>尝试其他功能

匹配游戏已完成。
你可以添加更多功能，使此游戏更具挑战性且更有趣。
提供以下选择。

- 将图标和颜色替换为您选择的图标和颜色。

  尝试查看标签的 [Forecolor](<xref:System.Windows.Forms.Control.ForeColor%2A>) 属性。

- 添加一个游戏计时器，记录玩家赢得游戏所用的时间。

  可以在窗体中添加一个标签来显示经过的时间。
  将其置于 TableLayoutPanel 上方。
  在窗体中添加另一个计时器来记录时间。
  使用代码在玩家开始游戏时启动计时器，并在最后两个图标匹配成功后停止计时器。

- 当玩家找到匹配的图标时会添加一种声音，当玩家发现两个不匹配的图标时会添加另一种声音，当程序再次隐藏图标时会添加第三种声音。

  若要播放声音，可以使用 <xref:System.Media> 命名空间。 有关详细信息，请参阅[在 Windows 窗体应用中播放声音 (C#)](https://www.youtube.com/watch?v=qOh4ooHg1UU&feature=youtu.be) 或[如何在 Visual Basic 中播放音频](https://www.youtube.com/watch?v=-4oPDeQrtMs&feature=youtu.be)。

- 通过将图板变大，增加游戏的难度。

  不仅需要向 TableLayoutPanel 中添加行和列，
  还需要考虑创建的图标数目。

- 如果玩家反应太慢，则隐藏第一个图标，以使游戏更具挑战性。

## <a name="next-steps"></a>后续步骤

祝贺！
你已完成该系列教程。
你已在 Visual Studio IDE 中完成以下编程和设计任务：

- 已在列表中存储对象，例如图标
- 已使用 C# 或 Visual Basic 中的循环来循环访问列表
- 已使用引用变量跟踪状态
- 已生成事件处理程序，以响应多个对象的事件
- 已添加进行倒计时并触发事件的计时器

进入本文深入了解 Windows 窗体设计器。
> [!div class="nextstepaction"]
> [教程：Windows 窗体设计器入门](../designers/walkthrough-windows-forms-designer.md)
