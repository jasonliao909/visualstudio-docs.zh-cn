---
title: 使用按钮在文档中的文本框中显示文本
description: 了解如何使用文档级自定义项中的按钮和文本框Microsoft Word。
ms.custom: SEO-VS-2020, devdivchpfy22
ms.date: 01/31/2022
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- text boxes, displaying text in documents
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.technology: office-development
ms.workload:
- office
ms.openlocfilehash: 39b8d9d88e0a86510fa067e99a0ab92165266cf0
ms.sourcegitcommit: 169b7b66d13b7e3c86097b42206dd33389cd9166
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/09/2022
ms.locfileid: "138148578"
---
# <a name="walkthrough-display-text-in-a-text-box-in-a-document-using-a-button"></a>演练：使用按钮在文档中的文本框中显示文本
  本演练演示如何在 Microsoft Office Word 的文档级自定义项中使用按钮和文本框。

 [!INCLUDE[appliesto_wdalldoc](../vsto/includes/appliesto-wdalldoc-md.md)]

 本演练阐释了以下任务：

- 设计时，将控件添加到文档级项目中的 Word 文档。

- 单击按钮时将填充文本框。

  [!INCLUDE[note_settings_general](../sharepoint/includes/note-settings-general-md.md)]

## <a name="prerequisites"></a>先决条件
 您需要满足以下条件才能完成本演练：

- [!INCLUDE[vsto_vsprereq](../vsto/includes/vsto-vsprereq-md.md)]

- Microsoft Word

## <a name="create-the-project"></a>创建项目
 第一步是创建 Word 文档项目。

### <a name="to-create-a-new-project"></a>创建新项目的步骤

1. 创建一个名称为 My **Word Button 的 Word 文档项目**。 在向导中，选择 **"创建新文档"**。

     有关详细信息，请参阅[如何：在 Office 创建Visual Studio](../vsto/how-to-create-office-projects-in-visual-studio.md)。

     Visual Studio设计器中打开新的 Word 文档，并将"**我的 Word 按钮**"**项目添加到** 解决方案资源管理器。

## <a name="add-controls-to-the-word-document"></a>向 Word 文档添加控件
 用户界面控件包含一个按钮和一个 Word 文档上的文本框。

### <a name="to-add-a-button-and-a-text-box"></a>添加一个按钮和一个文本框

1. 验证该文档已在 Visual Studio 设计器中打开。

2. 从"**工具箱"的****"公共控件**"选项卡中，将<xref:Microsoft.Office.Tools.Word.Controls.TextBox>控件拖动到文档。

   > [!NOTE]
   > 在 Word 中，默认情况下控件将按照文本进行删除。 可以通过更改 Word 中"选项"对话框的"编辑"选项卡上的默认值来修改控件 **和** 形状对象的插入方式。

3. 在“视图”菜单上选择“属性”窗口。  

4. 在"属性 **"窗口下** 拉框中查找 **TextBox1**，将文本框的 Name 属性更改为 **displayText**。

5. 将 **Button** 控件拖动到文档并更改以下属性。

   |属性|值|
   |--------------|-----------|
   |**名称**|**insertText**|
   |**文本**|**插入文本**|

   现在，你可以编写将在单击该按钮时运行的代码。

## <a name="populate-the-text-box-when-the-button-is-clicked"></a>单击按钮时填充文本框
 每次用户选择按钮时，Hello World **！** 将 添加到文本框中。

### <a name="to-write-to-the-text-box-when-the-button-is-clicked"></a>在单击按钮时写入文本框

1. 在 **解决方案资源管理器**，右键单击" **ThisDocument**"， **然后选择快捷菜单** 上的"查看代码"。

2. 将下列代码添加到按钮的 <xref:System.Windows.Forms.Control.Click> 事件处理程序。

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/my chart options/ThisDocument.vb" id="Snippet7":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreProgrammingControlsWordCS/ThisDocument.cs" id="Snippet7":::

3. 在 C# 中，必须向 <xref:Microsoft.Office.Tools.Word.Document.Startup> 事件添加按钮的事件处理程序。 有关创建事件处理程序的信息，请参阅[如何：](../vsto/how-to-create-event-handlers-in-office-projects.md)在项目中创建Office处理程序。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreProgrammingControlsWordCS/ThisDocument.cs" id="Snippet8":::

## <a name="test-the-application"></a>测试应用程序
 现在可以测试文档，确保消息Hello World **！** 选择按钮时，文本框中会显示 。

### <a name="to-test-your-document"></a>测试文档

1. 按 **F5** 运行项目。

2. 选择该按钮。

3. 确认Hello World **！** 显示在文本框中。

## <a name="next-steps"></a>后续步骤
 本演练演示在 Word 文档中使用按钮和文本框的基础知识。 以下是接下来可能要执行的一些任务：

- 使用组合框来更改格式设置。 有关详细信息，请参阅 [演练：使用 CheckBox 控件更改文档格式](../vsto/walkthrough-changing-document-formatting-using-checkbox-controls.md)。

- 使用单选按钮以选择图表样式。 有关详细信息，请参阅演练：使用单选按钮 [更新文档中的图表](../vsto/walkthrough-updating-a-chart-in-a-document-using-radio-buttons.md)。

## <a name="see-also"></a>另请参阅
- [Windows文档上的 Office 窗体控件概述](../vsto/windows-forms-controls-on-office-documents-overview.md)
- [使用 Word 的演练](../vsto/walkthroughs-using-word.md)
- [Office开发示例和演练](../vsto/office-development-samples-and-walkthroughs.md)
- [如何：将Windows窗体控件添加到Office文档](../vsto/how-to-add-windows-forms-controls-to-office-documents.md)
- [主机项和主机控件概述](../vsto/host-items-and-host-controls-overview.md)
