---
title: 向 Word 文档或 Excel 工作簿添加操作窗格
description: 了解要将操作窗格添加到 Microsoft Office Word 文档或 Microsoft Excel 工作簿，您应该首先创建一个 Windows 窗体用户控件。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- smart documents [Office development in Visual Studio], creating in Word
- smart documents [Office development in Visual Studio], adding controls
- actions panes [Office development in Visual Studio], creating in Word
- actions panes [Office development in Visual Studio], adding controls
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 9cf079727581b9cec4b6cb77a0a0c3f0b503b3a0
ms.sourcegitcommit: 4b40aac584991cc2eb2186c3e4f4a7fcd522f607
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/21/2021
ms.locfileid: "107825519"
---
# <a name="how-to-add-an-actions-pane-to-word-documents-or-excel-workbooks"></a>如何：向 Word 文档或 Excel 工作簿添加操作窗格
  若要将操作窗格添加到 Microsoft Office Word 文档或 Microsoft Excel 工作簿，请先创建一个 Windows 窗体用户控件。 然后，将该用户控件添加到 <xref:Microsoft.Office.Tools.ActionsPane.Controls%2A> `ThisDocument.ActionsPane` 项目中 (Word) 或 `ThisWorkbook.ActionsPane` (Excel) 字段的属性。

 [!INCLUDE[appliesto_alldoc](../vsto/includes/appliesto-alldoc-md.md)]

> [!NOTE]
> 以下说明中的某些 Visual Studio 用户界面元素在计算机上出现的名称或位置可能会不同。 这些元素取决于你所使用的 Visual Studio 版本和你所使用的设置。 有关详细信息，请参阅[个性化设置 Visual Studio IDE](../ide/personalizing-the-visual-studio-ide.md)。

## <a name="creating-the-user-control"></a>创建用户控件
 下面的过程演示如何在 Word 或 Excel 项目中创建用户控件。 它还向用户控件添加一个按钮，该按钮在单击文档或工作簿时向其写入文本。

#### <a name="to-create-the-user-control"></a>创建用户控件

1. 在 Visual Studio 中打开 Word 或 Excel 文档级项目。

2. 在 **“项目”** 菜单上，单击 **“添加新项”**。

3. 在 " **添加新项** " 对话框中，选择 " **操作窗格控件**"，将其命名为 **HelloControl**，然后单击 " **添加**"。

    > [!NOTE]
    > 也可以将 **用户控件** 项添加到项目。 **操作窗格控件** 和 **用户控件** 项生成的类在功能上是等效的。

4. 从 "工具箱" 的 " **Windows 窗体** " 选项卡中 **，** 将 " **按钮** " 控件拖动到控件上。

    > [!NOTE]
    > 如果控件在设计器中不可见，请在 **解决方案资源管理器** 中双击 " **HelloControl** "。

5. 将代码添加到 <xref:System.Windows.Forms.Control.Click> 按钮的事件处理程序中。 下面的示例演示 Microsoft Office Word 文档的代码。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreActionsPaneWordCS/HelloControl.cs" id="Snippet12":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreActionsPaneWordVB/HelloControl.vb" id="Snippet12":::

6. 在 c # 中，必须为按钮单击添加一个事件处理程序。 可以在调用后将此代码放在 `HelloControl` 构造函数中 `InitializeComponent` 。

     有关如何创建事件处理程序的信息，请参阅 [如何：在 Office 项目中创建事件处理程序](../vsto/how-to-create-event-handlers-in-office-projects.md)。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreActionsPaneWordCS/HelloControl.cs" id="Snippet13":::

## <a name="add-the-user-control-to-the-actions-pane"></a>将用户控件添加到操作窗格
 若要显示操作窗格，请将用户控件添加到 <xref:Microsoft.Office.Tools.ActionsPane.Controls%2A> `ThisDocument.ActionsPane` (Word) 或 `ThisWorkbook.ActionsPane` (Excel) 字段的属性。

### <a name="to-add-the-user-control-to-the-actions-pane"></a>将用户控件添加到 "操作" 窗格

1. 将以下代码 `ThisDocument` `ThisWorkbook` 作为类级别声明添加到或类中 (不要将此代码添加到方法) 。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreActionsPaneWordCS/ThisDocument.cs" id="Snippet14":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreActionsPaneWordVB/ThisDocument.vb" id="Snippet14":::

2. 将下面的代码添加到类的 `ThisDocument_Startup` 事件处理程序 `ThisDocument` 或 `ThisWorkbook_Startup` 类的事件处理 `ThisWorkbook` 程序中。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreActionsPaneWordCS/ThisDocument.cs" id="Snippet15":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreActionsPaneWordVB/ThisDocument.vb" id="Snippet15":::

## <a name="see-also"></a>另请参阅
- [操作窗格概述](../vsto/actions-pane-overview.md)
- [演练：将文本从操作窗格插入到文档中](../vsto/walkthrough-inserting-text-into-a-document-from-an-actions-pane.md)
- [如何：管理操作窗格上的控件布局](../vsto/how-to-manage-control-layout-on-actions-panes.md)
- [演练：将文本从操作窗格插入到文档中](../vsto/walkthrough-inserting-text-into-a-document-from-an-actions-pane.md)
