---
title: 教程：向匹配游戏中添加图标
description: 在本教程中，你将为匹配游戏 Windows 窗体上的每个标签分配一个随机图标，并实现一个事件处理程序以在 Visual Studio 中使用 C# 或 VB 显示图标。
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
ms.openlocfilehash: ebe688c089b561c1cbf15a29b61d244d5237680e
ms.sourcegitcommit: 169b7b66d13b7e3c86097b42206dd33389cd9166
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/09/2022
ms.locfileid: "138149267"
---
# <a name="tutorial-add-icons-to-your-matching-game-winforms-app"></a>教程：向匹配游戏 WinForms 应用中添加图标

在这四个教程系列中，你将构建一个匹配游戏，玩家在其中匹配隐藏的图标对。

在匹配游戏中，玩家选择一个方块来查看图标，然后选择另一个方块。
如果图标互相匹配，则它们保持可见。
如果不匹配，游戏将隐藏这两个图标。
在本教程中，你将随机向标签分配图标。
将其设置为隐藏，然后在选中时显示。

在第二个教程中，你将了解如何：

> [!div class="checklist"]
> - 添加 Random 对象和图标列表。
> - 向每个标签分配一个随机图标。
> - 添加事件处理程序，用于显示标签的图标。

## <a name="prerequisites"></a>必备条件

此教程基于上一教程[创建匹配游戏应用程序](tutorial-windows-forms-create-match-game.md)。
如果尚未学习此教程，请先完成此教程。

## <a name="add-a-random-object-and-a-list-of-icons"></a>添加 Random 对象和图标列表

在本部分中，你要为游戏创建一组匹配的符号。
每个符号将添加到窗体上 TableLayoutPanel 中的两个随机单元格。

使用 `new` 语句创建两个对象。
第一个是 <xref:System.Random> 对象，随机选择 TableLayoutPanel 中的单元格。
第二个是 <xref:System.Collections.Generic.List%601> 对象。
它存储随机选择的符号。

1. 打开 Visual Studio。 匹配游戏项目显示在“打开最近使用的文件”下。

1. 如果使用的是 C#，请选择“Form1.cs”，如果使用的是 Visual Basic，则选择“Form1.vb”。 然后选择“查看” > “代码”。 
   也可以选择 F7 键或双击“Form1” 。
   Visual Studio IDE 显示 Form1 的代码模块。

1. 在现有代码中，添加以下代码。

   :::code language="csharp" source="../../snippets/csharp/VS_Snippets_VBCSharp/vbexpresstutorial4step2_3_4/cs/form1.cs" id="Snippet1":::
   :::code language="vb" source="../../snippets/visualbasic/VS_Snippets_VBCSharp/vbexpresstutorial4step2_3_4/vb/form1.vb" id="Snippet1":::

   [!INCLUDE [devlang-control-csharp-vb](../includes/devlang-control-csharp-vb.md)]

   如果你使用 C#，请确保将代码放在左大括号后面，紧靠类声明 (`public partial class Form1 : Form`) 之后。 如果你使用 Visual Basic，请将代码放在紧靠类声明 (`Public Class Form1`) 之后。

可以使用列表对象跟踪不同类型的项目。
列表可以包含数字、true/false 值、文本或其他对象。
在匹配游戏中，列表对象具有 16 个字符串，每个字符串对应 TableLayoutPanel 面板中的每个单元格。
每个字符串都是对应于标签中的图标的单个字母。
这些字符在 Webdings 字体中显示为公共汽车、自行车和其他符号。

> [!NOTE]
> 列表可以根据需要收缩或增长，这在此程序中非常重要。

若要详细了解列表，请参阅 <xref:System.Collections.Generic.List%601>。 若要查看 C# 中的示例，请参阅[基本列表示例](/dotnet/csharp/tour-of-csharp/tutorials/arrays-and-collections#a-basic-list-example)。 若要查看 Visual Basic 中的示例，请参阅[使用简单集合](/dotnet/visual-basic/programming-guide/concepts/collections#using-a-simple-collection)。

## <a name="assign-a-random-icon-to-each-label"></a>向每个标签分配一个随机图标

每次运行该程序时，它都会使用 `AssignIconsToSquares()` 方法将图标随机分配给 Label 控件。
此代码使用关键字 `foreach`（C# 中）或 `For Each`（Visual Basic 中）。

1. 添加 `AssignIconsToSquares()` 方法。

   :::code language="csharp" source="../../snippets/csharp/VS_Snippets_VBCSharp/vbexpresstutorial4step2_3_4/cs/form1.cs" id="Snippet2":::
   :::code language="vb" source="../../snippets/visualbasic/VS_Snippets_VBCSharp/vbexpresstutorial4step2_3_4/vb/form1.vb" id="Snippet2":::

   可以在上一节中添加的代码之下输入此代码。

   > [!NOTE]
   > 其中有一行被故意注释掉了。
   > 稍后在此过程中将其添加。

   `AssignIconsToSquares()` 方法循环访问 TableLayoutPanel 中的每个标签控件。
   它对每个控件运行相同的语句。
   语句从列表中提取随机图标。

   - 第一行将 control  变量转换为名为“iconLabel”  的标签。 
   - 第二行是 `if` 语句，用于检查以确保转换起作用。
     如果转换起作用，则 `if` 语句中的语句将运行。
   - `if` 语句中的第一行将创建一个名为“randomNumber”的变量，该变量包含一个与图标列表中的项对应的随机数。
     它使用 <xref:System.Random> 对象的 <xref:System.Random.Next> 方法。
     `Next` 方法将返回此随机数。
     此行也使用“图标”  列表的 <xref:System.Collections.Generic.List%601.Count> 属性来确定随机数的选择范围。
   - 下一行会将图标列表项之一分配给标签的 <xref:System.Windows.Forms.Label.Text> 属性。
   - 下一行将隐藏这些图标。
     该行已在此处注释掉，因此你可以在继续操作之前验证代码的其余部分。
   - `if` 语句中最后一行将从列表中删除已添加到窗体中的图标。

1. 将调用添加到 Form1 构造函数的 `AssignIconsToSquares()` 方法。
   此方法用图标填充游戏板。
   构造函数在创建对象时进行调用。

   :::code language="csharp" source="../../snippets/csharp/VS_Snippets_VBCSharp/vbexpresstutorial4step2_3_4/cs/form1.cs" id="Snippet13":::

   对于 Visual Basic，将 `AssignIconsToSquares()` 方法调用添加到 `Form1_Load` 方法。

   ```vb
   Private Sub Form1_Load(sender As Object, e As EventArgs) Handles MyBase.Load
       AssignIconsToSquares()
   End Sub
   ```

   有关详细信息，请参阅[构造函数（C# 编程指南）](/dotnet/csharp/programming-guide/classes-and-structs/constructors)或[使用构造函数和析构函数](/previous-versions/visualstudio/visual-studio-2008/2z08e49e\(v\=vs.90\))。

1. 保存并运行程序。 它应该显示一个窗体，其中每个标签都分配了随机图标。

   > [!TIP]
   > 如果窗体上的 Webdings 图标不能正确显示，请将窗体上标签的 UseCompatibleTextRendering 属性设置为 True。 

1. 关闭程序，然后重新运行。 向每个标签分配不同的图标。

   ![屏幕截图显示其中显示了随机图标的匹配游戏。](../media/tutorial-windows-forms-match-game-icons/display-random-icons.png)

   你没有隐藏这些图标，所以现在可以看到。 若要向玩家隐藏图标，可以将每个标签的“ForeColor”  属性设置为与“BackColor”  属性相同的颜色。

1. 停止程序。 删除循环内注释的代码行的注释标记。

   :::code language="csharp" source="../../snippets/csharp/VS_Snippets_VBCSharp/vbexpresstutorial4step2_3_4/cs/form1.cs" id="Snippet15":::
   :::code language="vb" source="../../snippets/visualbasic/VS_Snippets_VBCSharp/vbexpresstutorial4step2_3_4/vb/form1.vb" id="Snippet15":::

如果再次运行该程序，图标似乎已消失。
只显示蓝色背景。
图标是随机分配的，仍然存在。

## <a name="add-event-handlers-to-labels"></a>向标签添加事件处理程序

在此匹配游戏中，玩家先显示一个隐藏图标，然后再显示第二个图标。
如果图标互相匹配，则它们保持可见。
否则，两个图标都会再次隐藏。

若要使游戏以这种方式工作，请添加一个 <xref:System.Windows.Forms.Control.Click> 事件处理程序，它将更改所选标签的颜色以与背景匹配。

1. 在“Windows 窗体设计器”中打开窗体。 选择“Form1.cs”或“Form1.vb”，然后选择“查看” > “设计器”。   

1. 选择第一个标签控件以选中它。 然后，按住 Ctrl 键的同时选择其他每个标签。
   确保选中每个标签。

1. 在“属性”窗口中，选择“事件”按钮，这是一个闪电形符号。 
   对于“Click”事件，请在框中选择“label1_Click” 。

     ![屏幕截图显示其中显示了 Click 事件的“属性”窗口。](../media/tutorial-windows-forms-match-game-icons/click-event.png)

1. 选择 **Enter** 键。 IDE 将名为 label1 _Click() 的 `Click` 事件处理程序添加到代码中。
   由于你选择了所有标签，因此处理程序会与每个标签挂钩。

1. 填写其余代码。

   :::code language="csharp" source="../../snippets/csharp/VS_Snippets_VBCSharp/vbexpresstutorial4step2_3_4/cs/form1.cs" id="Snippet4":::
   :::code language="vb" source="../../snippets/visualbasic/VS_Snippets_VBCSharp/vbexpresstutorial4step2_3_4/vb/form1.vb" id="Snippet4":::

   > [!NOTE]
   > 如果你复制和粘贴 `label1_Click()` 代码块，而不是手动输入代码，请确保替换现有的 `label1_Click()` 代码。
   > 否则，你将得到重复的代码块。

1. 选择“调试” > “开始调试”以运行程序。  您应该看到一个背景为蓝色的空窗体。 选择窗体中的任意单元格。 其中一个图标应可见。 继续在窗体中选择不同位置。 当选择图标时，它们应显示。

   ![屏幕截图显示具有一个可见图标的匹配游戏。](../media/tutorial-windows-forms-match-game-icons/match-game-start.png)

## <a name="next-steps"></a>后续步骤

请继续学习下一教程，了解如何使用计时器更改标签。
> [!div class="nextstepaction"]
> [在匹配游戏中使用计时器](tutorial-windows-forms-match-game-labels.md)
