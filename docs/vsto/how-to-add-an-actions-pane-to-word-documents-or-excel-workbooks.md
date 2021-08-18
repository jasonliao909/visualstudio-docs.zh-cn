---
title: 将"操作"窗格添加到 Word 文档或Excel工作簿
description: 了解若要将操作窗格添加到 Microsoft Office Word 文档或 Microsoft Excel工作簿，应首先创建一个Windows窗体用户控件。
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
ms.technology: office-development
ms.workload:
- office
ms.openlocfilehash: e86893fd1ae5ba42ee0f2ed5f8d4bbc6fdad50f8
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122083552"
---
# <a name="how-to-add-an-actions-pane-to-word-documents-or-excel-workbooks"></a>如何：向 Word 文档或 Excel 工作簿添加操作窗格
  若要将操作窗格添加到 Microsoft Office Word 文档或 Microsoft Excel工作簿，请首先创建一Windows窗体用户控件。 然后，将用户控件添加到项目中 Word (或) <xref:Microsoft.Office.Tools.ActionsPane.Controls%2A> `ThisDocument.ActionsPane` 字段 (Excel) `ThisWorkbook.ActionsPane` 属性。

 [!INCLUDE[appliesto_alldoc](../vsto/includes/appliesto-alldoc-md.md)]

> [!NOTE]
> 以下说明中的某些 Visual Studio 用户界面元素在计算机上出现的名称或位置可能会不同。 这些元素取决于你所使用的 Visual Studio 版本和你所使用的设置。 有关详细信息，请参阅[个性化设置 Visual Studio IDE](../ide/personalizing-the-visual-studio-ide.md)。

## <a name="creating-the-user-control"></a>创建用户控件
 以下过程演示如何在 Word 或 Excel 项目中创建用户控件。 它还向用户控件添加一个按钮，该按钮在单击时向文档或工作簿写入文本。

#### <a name="to-create-the-user-control"></a>创建用户控件

1. 在 Excel 中打开 Word 或 Visual Studio。

2. 在 **“项目”** 菜单上，单击 **“添加新项”**。

3. 在"**添加新项"对话框中**，选择"**操作"窗格控件**，将其命名 **为 HelloControl，** 然后单击"添加 **"。**

    > [!NOTE]
    > 或者，可以将用户 **控件项** 添加到项目。 操作窗格 **控件和用户** 控件项生成的 **类** 在功能上是等效的。

4. 从 **"Windows"** 的"窗体"选项卡 **中，** 将 **"按钮"** 控件拖到控件上。

    > [!NOTE]
    > 如果控件在设计器中不可见，请在 中双击 **HelloControl 解决方案资源管理器。** 

5. 将代码添加到 <xref:System.Windows.Forms.Control.Click> 按钮的事件处理程序。 以下示例显示 Word 文档Microsoft Office代码。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreActionsPaneWordCS/HelloControl.cs" id="Snippet12":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreActionsPaneWordVB/HelloControl.vb" id="Snippet12":::

6. 在 C# 中，必须为按钮单击添加事件处理程序。 调用 后，可以将此 `HelloControl` 代码放在构造函数中 `InitializeComponent` 。

     若要了解如何创建事件处理程序，请参阅[如何：](../vsto/how-to-create-event-handlers-in-office-projects.md)在项目Office处理程序。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreActionsPaneWordCS/HelloControl.cs" id="Snippet13":::

## <a name="add-the-user-control-to-the-actions-pane"></a>将用户控件添加到操作窗格
 若要显示操作窗格，将用户控件添加到 Word (或 <xref:Microsoft.Office.Tools.ActionsPane.Controls%2A> `ThisDocument.ActionsPane`) `ThisWorkbook.ActionsPane` 字段 (Excel) 。

### <a name="to-add-the-user-control-to-the-actions-pane"></a>将用户控件添加到操作窗格

1. 将以下代码作为类级声明添加到 `ThisDocument` `ThisWorkbook` 或 类， (不要将此代码添加到方法) 。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreActionsPaneWordCS/ThisDocument.cs" id="Snippet14":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreActionsPaneWordVB/ThisDocument.vb" id="Snippet14":::

2. 将以下代码添加到 `ThisDocument_Startup` 类的事件 `ThisDocument` 处理程序或 `ThisWorkbook_Startup` 类的事件 `ThisWorkbook` 处理程序。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreActionsPaneWordCS/ThisDocument.cs" id="Snippet15":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreActionsPaneWordVB/ThisDocument.vb" id="Snippet15":::

## <a name="see-also"></a>请参阅
- [操作窗格概述](../vsto/actions-pane-overview.md)
- [演练：从操作窗格中将文本插入文档](../vsto/walkthrough-inserting-text-into-a-document-from-an-actions-pane.md)
- [如何：管理操作窗格上的控件布局](../vsto/how-to-manage-control-layout-on-actions-panes.md)
- [演练：从操作窗格中将文本插入文档](../vsto/walkthrough-inserting-text-into-a-document-from-an-actions-pane.md)
