---
title: 使用 CheckBox 控件更改文档格式设置
description: 了解如何在文档Windows自定义项中使用窗体控件Microsoft Word更改文本格式。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Word documents, changing formatting using controls
- documents [Office development in Visual Studio], formatting
- check boxes, Word documents
- documents [Office development in Visual Studio], check box controls
- controls [Office development in Visual Studio], adding to documents
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.technology: office-development
ms.workload:
- office
ms.openlocfilehash: e9f280b2e8db25788e89bdb66d9ec5455c7a1efe
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122032051"
---
# <a name="walkthrough-change-document-formatting-using-checkbox-controls"></a>演练：使用 CheckBox 控件更改文档格式
  本演练演示如何在文档Windows自定义项中将窗体控件用于 Microsoft Office Word 以更改文本格式。

 [!INCLUDE[appliesto_wdalldoc](../vsto/includes/appliesto-wdalldoc-md.md)]

 本演练演示以下任务：

- 在设计时向文档级项目中的文档添加文本和控件。

- 选择选项时设置文本格式。

  若要将结果作为已完成的示例查看，请参阅本文中的 Word 控件示例Office[示例和演练](../vsto/office-development-samples-and-walkthroughs.md)。

  [!INCLUDE[note_settings_general](../sharepoint/includes/note-settings-general-md.md)]

## <a name="prerequisites"></a>先决条件
 您需要满足以下条件才能完成本演练：

- [!INCLUDE[vsto_vsprereq](../vsto/includes/vsto-vsprereq-md.md)]

- [!INCLUDE[Word_15_short](../vsto/includes/word-15-short-md.md)] 或 [!INCLUDE[Word_14_short](../vsto/includes/word-14-short-md.md)]。

## <a name="create-the-project"></a>创建项目
 第一步是创建 Word 文档项目。

### <a name="create-a-new-project"></a>创建新项目

1. 创建一个名称为 My **Word Formatting 的 Word 文档项目**。 在向导中，选择 **"创建新文档"。**

     有关详细信息，请参阅[如何：在 Office 创建Visual Studio。](../vsto/how-to-create-office-projects-in-visual-studio.md)

     Visual Studio设计器中打开新的 Word 文档，并将 **"我的 Word 格式设置"** 项目添加到 **解决方案资源管理器。**

## <a name="add-text-and-controls-to-the-word-document"></a>向 Word 文档添加文本和控件
 对于本演练，请在 Word 文档中添加三个复选框和控件中的 <xref:Microsoft.Office.Tools.Word.Bookmark> 一些文本。 复选框会向用户显示用于设置文本格式的选项。

### <a name="add-three-check-boxes"></a>添加三个复选框

1. 验证该文档已在 Visual Studio 设计器中打开。

2. 从" **工具箱"的** "公共控件 **"** 选项卡中，将第 <xref:Microsoft.Office.Tools.Word.Controls.CheckBox> 一个控件拖动到文档。

3. 在 **“属性”** 窗口中，更改下列属性。

    |属性|值|
    |--------------|-----------|
    |**名称**|**applyBoldFont**|
    |**文本**|**加粗**|

4. 按 **Enter** 将插入点移到第一个复选框下方。

5. 将第二个复选框添加到此复选框下面的 `ApplyBoldFont` 文档，并更改以下属性。

    |属性|值|
    |--------------|-----------|
    |**名称**|**applyItalicFont**|
    |**文本**|**斜体**|

6. 按 **Enter** 将插入点移到第二个复选框下方。

7. 将第三个复选框添加到此复选框下面的 `ApplyItalicFont` 文档，并更改以下属性。

    |属性|值|
    |--------------|-----------|
    |**名称**|**applyUnderlineFont**|
    |**文本**|**强调**|

### <a name="add-text-and-a-bookmark-control"></a>添加文本和书签控件

1. 将插入点移到复选框控件下方并键入以下文本：

    **单击复选框可更改此文本的格式。**

2. 从" **工具箱"的** "Word 控件 **"选项卡** 中， <xref:Microsoft.Office.Tools.Word.Bookmark> 将控件拖动到文档。

    将显示 **"添加书签控件** "对话框。

3. 选择添加到文档的文本，然后单击"确定 **"。**

    名为 <xref:Microsoft.Office.Tools.Word.Bookmark> **Bookmark1** 的控件将添加到文档中的选定文本中。

4. 在"**属性**"窗口中，将"名称" (**属性的值**) "fontText"。 

   接下来，编写代码，在选中或清除复选框时设置文本格式。

## <a name="format-the-text-when-a-check-box-is-checked-or-cleared"></a>选中或清除复选框时设置文本格式
 当用户选择格式设置选项时，更改文档中文本的格式。

### <a name="change-formatting-when-a-check-box-is-selected"></a>选中复选框时更改格式设置

1. 右键 `ThisDocument` 单击解决方案资源管理器，然后单击快捷菜单 **上的**"查看代码"。

2. 仅对于 C#，将以下常量添加到 **ThisDocument** 类。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreProgrammingControlsWordCS/ThisDocument.cs" id="Snippet2":::

3. 将以下代码添加到 <xref:System.Windows.Forms.Control.Click> 复选框的事件 `applyBoldFont` 处理程序。

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/my chart options/ThisDocument.vb" id="Snippet3":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreProgrammingControlsWordCS/ThisDocument.cs" id="Snippet3":::

4. 将以下代码添加到 <xref:System.Windows.Forms.Control.Click> 复选框的事件 `applyItalicFont` 处理程序。

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/my chart options/ThisDocument.vb" id="Snippet4":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreProgrammingControlsWordCS/ThisDocument.cs" id="Snippet4":::

5. 将以下代码添加到 <xref:System.Windows.Forms.Control.Click> 复选框的事件 `applyUnderlineFont` 处理程序。

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/my chart options/ThisDocument.vb" id="Snippet5":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreProgrammingControlsWordCS/ThisDocument.cs" id="Snippet5":::

6. 在 C# 中，必须为事件添加文本框的事件 <xref:Microsoft.Office.Tools.Word.Document.Startup> 处理程序。 若要了解如何创建事件处理程序，请参阅如何：在项目中创建[Office处理程序](../vsto/how-to-create-event-handlers-in-office-projects.md)。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreProgrammingControlsWordCS/ThisDocument.cs" id="Snippet6":::

## <a name="test-the-application"></a>测试应用程序
 现在，可以在选中或清除复选框时测试文档，以验证文本的格式是否正确。

### <a name="test-your-document"></a>测试文档

1. 按 **F5** 运行项目。

2. 选中或清除复选框。

3. 确认文本格式正确。

## <a name="next-steps"></a>后续步骤
 本演练演示了在 Word 文档上使用复选框和以编程方式更改文本格式的基础知识。 以下是接下来可能要执行的一些任务：

- 使用按钮填充文本框。 有关详细信息，请参阅演练：使用按钮 在文档中 [的文本框中显示文本](../vsto/walkthrough-displaying-text-in-a-text-box-in-a-document-using-a-button.md)。

- 使用单选按钮以选择图表样式。 有关详细信息，请参阅演练：使用单选按钮 [更新文档中的图表](../vsto/walkthrough-updating-a-chart-in-a-document-using-radio-buttons.md)。

## <a name="see-also"></a>请参阅
- [使用 Word 的演练](../vsto/walkthroughs-using-word.md)
- [Office开发示例和演练](../vsto/office-development-samples-and-walkthroughs.md)
- [NamedRange 控件](../vsto/namedrange-control.md)
- [文档Windows窗体控件Office限制](../vsto/limitations-of-windows-forms-controls-on-office-documents.md)
