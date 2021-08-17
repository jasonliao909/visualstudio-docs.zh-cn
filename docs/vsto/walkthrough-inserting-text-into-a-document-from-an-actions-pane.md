---
title: 演练：从操作窗格中将文本插入文档
description: 在文档创建操作Microsoft Word窗格。 了解操作窗格包含两个控件，用于收集输入，然后将文本发送到文档。
ms.custom: SEO-VS-2020
titleSuffix: ''
ms.date: 02/02/2017
ms.topic: conceptual
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
ms.openlocfilehash: 071f447e8f32d53feef912b6c804af27fe69aa1e
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122025430"
---
# <a name="walkthrough-insert-text-into-a-document-from-an-actions-pane"></a>演练：从操作窗格中将文本插入文档
  本演练演示如何在 Word 文档中创建Microsoft Office窗格。 操作窗格包含两个控件，用于收集输入，然后将文本发送到文档。

 [!INCLUDE[appliesto_wdalldoc](../vsto/includes/appliesto-wdalldoc-md.md)]

 本演练演示以下任务：

- 在操作窗格控件Windows窗体控件设计接口。

- 应用程序打开时显示操作窗格。

> [!NOTE]
> 以下说明中的某些 Visual Studio 用户界面元素在计算机上出现的名称或位置可能会不同。 这些元素取决于你所使用的 Visual Studio 版本和你所使用的设置。 有关详细信息，请参阅[个性化设置 Visual Studio IDE](../ide/personalizing-the-visual-studio-ide.md)。

## <a name="prerequisites"></a>先决条件
 您需要满足以下条件才能完成本演练：

- [!INCLUDE[vsto_vsprereq](../vsto/includes/vsto-vsprereq-md.md)]

- [!INCLUDE[Word_15_short](../vsto/includes/word-15-short-md.md)] 或 [!INCLUDE[Word_14_short](../vsto/includes/word-14-short-md.md)]。

## <a name="create-the-project"></a>创建项目
 第一步是创建 Word 文档项目。

### <a name="to-create-a-new-project"></a>创建新项目的步骤

1. 创建一个名称为"我的基本操作窗格"的 Word **文档项目**。 在向导中，选择 **"创建新文档"。** 有关详细信息，请参阅[如何：在 Office 创建Visual Studio。](../vsto/how-to-create-office-projects-in-visual-studio.md)

     Visual Studio设计器中打开新的 Word 文档，并将"我的基本操作 **窗格**"项目添加到 **解决方案资源管理器。**

## <a name="add-text-and-bookmarks-to-the-document"></a>向文档添加文本和书签
 操作窗格将文本发送到文档中的书签。 若要设计文档，请键入一些文本以创建基本窗体。

### <a name="to-add-text-to-your-document"></a>向文档添加文本

1. 在 Word 文档中键入以下文本：

    **2008 年 3 月 21 日**

    **名称**

    **Address**

    **这是 Word 中基本操作窗格的示例。**

   可以通过从控件的"工具箱"拖动控件Visual Studio Word 中的"书签"对话框，将控件 <xref:Microsoft.Office.Tools.Word.Bookmark> 添加到文档。  

### <a name="to-add-a-bookmark-control-to-your-document"></a>向文档添加书签控件

1. 从" **工具箱"的** "Word 控件 **"选项卡** 中， <xref:Microsoft.Office.Tools.Word.Bookmark> 将控件拖到文档中。

     将显示 **"添加书签控件** "对话框。

2. 选择"名称 **"一** 词，而不选择段落标记，然后单击"确定 **"。**

    > [!NOTE]
    > 段落标记应位于书签之外。 如果段落标记在文档中不可见，请单击"工具"菜单，指向Microsoft Office **Word 工具"，然后单击"** 选项 **"。** 单击"**视图**"选项卡，然后选中"选项"对话框的"**格式设置** 标记"部分中的"**段落标记"** 复选框。

3. 在"**属性"** 窗口中，将 **Bookmark1** **的 Name** 属性更改为 **showName**。

4. 选择"地址 **"一词**，而不选择段落标记。

5. 在功能 **区的"** 插入"选项卡上的"链接 **"** 组中，单击"书签 **"。**

6. 在"**书签"** 对话框中，在"书签名称"框中键入 **showAddress，****然后单击"** 添加 **"。**

## <a name="add-controls-to-the-actions-pane"></a>将控件添加到操作窗格
 若要设计操作窗格界面，请向项目添加操作窗格控件，然后将Windows窗体控件添加到操作窗格控件。

### <a name="to-add-an-actions-pane-control"></a>添加操作窗格控件

1. 在 中选择 **"我的基本操作"** 窗格 **解决方案资源管理器。**

2. 在 **“项目”** 菜单上，单击 **“添加新项”**。

3. 在"**添加新项"对话框中**，单击"**操作"窗格控件**，将控件命名 **InsertTextControl，** 然后单击"添加 **"。**

#### <a name="to-add-windows-form-controls-to-the-actions-pane-control"></a>将Windows窗体控件添加到操作窗格控件

1. 如果操作窗格控件在设计器中不可见，请双击 **InsertTextControl**。

2. 从" **工具箱"的** "公共控件 **"选项卡** 中，将 **"标签"** 控件拖到操作窗格控件。

3. 将"**标签"** 控件的"Text"属性更改为"**名称"。**

4. 将 **文本框控件** 添加到操作窗格控件，并更改以下属性。

    |属性|值|
    |--------------|-----------|
    |**名称**|**getName**|
    |**大小**|**130, 20**|

5. 将第二 **个"标签**"控件添加到操作窗格控件，将 **"文本"** 属性更改为"**地址"。**

6. 将第二 **个 Textbox** 控件添加到操作窗格控件，并更改以下属性。

    |属性|值|
    |--------------|-----------|
    |**名称**|**getAddress**|
    |**接受返回**|**True**|
    |**多行**|**True**|
    |**大小**|**130, 40**|

7. 将 **Button** 控件添加到操作窗格控件，并更改以下属性。

    |属性|值|
    |--------------|-----------|
    |**名称**|**addText**|
    |**文本**|插入|

## <a name="add-code-to-insert-text-into-the-document"></a>添加代码以将文本插入文档
 在操作窗格中，编写将文本框中的文本插入文档中相应 <xref:Microsoft.Office.Tools.Word.Bookmark> 控件的代码。 可以使用 类 `Globals` 从操作窗格上的控件访问文档上的控件。 有关详细信息，请参阅[对项目 中的对象的全局Office访问](../vsto/global-access-to-objects-in-office-projects.md)。

### <a name="to-insert-text-from-the-actions-pane-in-a-bookmark-in-the-document"></a>在文档中的书签中插入操作窗格中的文本

1. 将以下代码添加到 <xref:System.Windows.Forms.Control.Click> **addText** 按钮的事件处理程序。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreActionsPaneWordCS/InsertTextControl.cs" id="Snippet8":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreActionsPaneWordVB/InsertTextControl.vb" id="Snippet8":::

2. 在 C# 中，必须为按钮单击添加事件处理程序。 调用 后，可以将此 `InsertTextControl` 代码放在构造函数中 `InitializeComponent` 。 有关创建事件处理程序的信息，请参阅如何：在项目中创建[Office处理程序](../vsto/how-to-create-event-handlers-in-office-projects.md)。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreActionsPaneWordCS/InsertTextControl.cs" id="Snippet9":::

## <a name="add-code-to-show-the-actions-pane"></a>添加代码以显示操作窗格
 若要显示操作窗格，将创建的控件添加到控件集合。

### <a name="to-show-the-actions-pane"></a>显示操作窗格

1. 在 类中创建操作窗格控件的新 `ThisDocument` 实例。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreActionsPaneWordCS/ThisDocument.cs" id="Snippet10":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreActionsPaneWordVB/ThisDocument.vb" id="Snippet10":::

2. 将以下代码添加到 <xref:Microsoft.Office.Tools.Word.Document.Startup> 的事件处理程序 `ThisDocument` 。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreActionsPaneWordCS/ThisDocument.cs" id="Snippet11":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreActionsPaneWordVB/ThisDocument.vb" id="Snippet11":::

## <a name="test-the-application"></a>测试应用程序
 测试文档，验证打开文档时操作窗格是否打开，以及单击按钮时，文本框中键入的文本是否插入到书签中。

### <a name="to-test-your-document"></a>测试文档

1. 按 **F5** 运行项目。

2. 确认操作窗格可见。

3. 在操作窗格的文本框中键入名称和地址，然后单击"插入 **"。**

## <a name="next-steps"></a>后续步骤
 以下是接下来可能要执行的一些任务：

- 在 Excel 中创建操作窗格。 有关详细信息，请参阅[如何：将操作窗格添加到 Excel 工作簿](/previous-versions/visualstudio/visual-studio-2010/e3zbk0hz(v=vs.100))。

- 将数据绑定到操作窗格上的控件。 有关详细信息，请参阅 [演练：将数据绑定到 Word 操作窗格上的控件](../vsto/walkthrough-binding-data-to-controls-on-a-word-actions-pane.md)。

## <a name="see-also"></a>请参阅
- [操作窗格概述](../vsto/actions-pane-overview.md)
- [如何：向 Word 文档或 Excel 工作簿添加操作窗格](../vsto/how-to-add-an-actions-pane-to-word-documents-or-excel-workbooks.md)
- [如何：将操作窗格添加到 Excel 工作簿](/previous-versions/visualstudio/visual-studio-2010/e3zbk0hz(v=vs.100))
- [如何：管理操作窗格上的控件布局](../vsto/how-to-manage-control-layout-on-actions-panes.md)
- [Bookmark 控件](../vsto/bookmark-control.md)
