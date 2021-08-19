---
title: 演练：为书签创建快捷菜单
description: 了解如何在文档级自定义项中为书签控件创建快捷菜单，Microsoft Word。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- context menus, Word
- Bookmark control, events
- shortcut menus, Word
- menus, creating in Office applications
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.technology: office-development
ms.workload:
- office
ms.openlocfilehash: b852dce9799ebe7aee87bbecbe2beee7a6cd4616
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122115013"
---
# <a name="walkthrough-create-shortcut-menus-for-bookmarks"></a>演练：为书签创建快捷菜单
  本演练演示如何在 Word 的文档级自定义项中为控件 <xref:Microsoft.Office.Tools.Word.Bookmark> 创建快捷菜单。 当用户右键单击书签中的文本时，将显示一个快捷菜单，并为用户提供用于设置文本格式的选项。

 [!INCLUDE[appliesto_wdalldoc](../vsto/includes/appliesto-wdalldoc-md.md)]

 本演练演示以下任务：

- [创建项目](#BKMK_CreateProject)。

- [向文档 添加文本和书签](#BKMK_addtextandbookmarks)。

- [将命令添加到快捷菜单](#BKMK_AddCmndsShortMenu)。

- [设置书签 中的文本格式](#BKMK_formattextbkmk)。

  [!INCLUDE[note_settings_general](../sharepoint/includes/note-settings-general-md.md)]

## <a name="prerequisites"></a>先决条件
 您需要满足以下条件才能完成本演练：

- [!INCLUDE[vsto_vsprereq](../vsto/includes/vsto-vsprereq-md.md)]

- [!INCLUDE[Word_15_short](../vsto/includes/word-15-short-md.md)] 或 [!INCLUDE[Word_14_short](../vsto/includes/word-14-short-md.md)]

## <a name="create-the-project"></a><a name="BKMK_CreateProject"></a> 创建项目
 第一步是在 Visual Studio 创建 Word 文档项目。

### <a name="to-create-a-new-project"></a>创建新项目的步骤

- 创建一个名称为"我的书签快捷菜单"的 Word **文档项目**。 在向导中，选择 **"创建新文档"。** 有关详细信息，请参阅[如何：在 Office 创建Visual Studio。](../vsto/how-to-create-office-projects-in-visual-studio.md)

     Visual Studio设计器中打开新的 Word 文档，并将"我的书签快捷 **菜单**"项目添加到 **解决方案资源管理器。**

## <a name="add-text-and-bookmarks-to-the-document"></a><a name="BKMK_addtextandbookmarks"></a> 向文档添加文本和书签
 向文档添加一些文本，然后添加两个重叠书签。

### <a name="to-add-text-to-your-document"></a>向文档添加文本

- 在显示在项目设计器中的文档中，键入以下文本。

     **这是右键单击书签中的文本时创建快捷菜单的示例。**

### <a name="to-add-a-bookmark-control-to-your-document"></a>向文档添加书签控件

1. 在" **工具箱"** 中，从 **"Word 控件"** 选项卡中， <xref:Microsoft.Office.Tools.Word.Bookmark> 将控件拖动到文档。

    将显示 **"添加书签控件** "对话框。

2. 选择"右键单击文本时创建快捷菜单"一词，然后单击"确定 **"。**

    `bookmark1` 将 添加到文档。

3. 向 <xref:Microsoft.Office.Tools.Word.Bookmark> 单词"右键单击书签中的文本"添加另一个控件。

    `bookmark2` 将 添加到文档。

   > [!NOTE]
   > 单词"右键单击文本"同时在 和 `bookmark1` 中 `bookmark2` 。

   在设计时向文档添加书签时， <xref:Microsoft.Office.Tools.Word.Bookmark> 将创建控件。 可以针对书签的几个事件进行编程。 可以在书签中编写代码，以便当用户右键单击书签中的文本时 <xref:Microsoft.Office.Tools.Word.Bookmark.BeforeRightClick> ，会显示快捷菜单。

## <a name="add-commands-to-a-shortcut-menu"></a><a name="BKMK_AddCmndsShortMenu"></a> 将命令添加到快捷菜单
 将按钮添加到右键单击文档时出现的快捷菜单。

### <a name="to-add-commands-to-a-shortcut-menu"></a>将命令添加到快捷菜单

1. 向项目 **添加功能** 区 XML 项。 有关详细信息，请参阅 [如何：开始自定义功能区](../vsto/how-to-get-started-customizing-the-ribbon.md)。

2. 在 **解决方案资源管理器** 中，选择 **"ThisDocument.cs"** 或 **"ThisDocument.vb"。**

3. 在菜单栏上，选择“视图” > “代码”。

     **ThisDocument** 类文件将在代码编辑器中打开。

4. 将以下代码添加到 **ThisDocument** 类。 此代码重写 CreateRibbonExtensibilityObject 方法，将功能区 XML 类返回到Office应用程序。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/trin_word_document_menus.cs/thisdocument.cs" id="Snippet1":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/trin_word_document_menus.vb/thisdocument.vb" id="Snippet1":::

5. 在“解决方案资源管理器” 中，选择功能区 XML 文件。 默认情况下，功能区 XML 文件命名为 Ribbon1.xml。

6. 在菜单栏上，选择“视图” > “代码”。

     功能区 XML 文件随即在代码编辑器中打开。

7. 在代码编辑器中，将功能区 XML 文件的内容替换为以下代码。

    ```xml
    <?xml version="1.0" encoding="UTF-8"?>
    <customUI xmlns="http://schemas.microsoft.com/office/2009/07/customui" onLoad="Ribbon_Load">
      <contextMenus>
        <contextMenu idMso="ContextMenuText">
          <button id="BoldButton" label="Bold" onAction="ButtonClick"
               getVisible="GetVisible" />
          <button id="ItalicButton" label="Italic" onAction="ButtonClick"
              getVisible="GetVisible"/>
        </contextMenu>
      </contextMenus>
    </customUI>
    ```

     此代码将两个按钮添加到右键单击文档时出现的快捷菜单。

8. 在 **解决方案资源管理器** 中，右键单击 `ThisDocument` ，然后单击"**查看代码"。**

9. 在类级别声明以下变量和书签变量。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/trin_word_document_menus.cs/thisdocument.cs" id="Snippet2":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/trin_word_document_menus.vb/thisdocument.vb" id="Snippet2":::

10. 在 **解决方案资源管理器** 中，选择功能区代码文件。 默认情况下，功能区代码文件名为 **Ribbon1.cs** 或 **Ribbon1.vb**。

11. 在菜单栏上，选择“视图” > “代码”。

     功能区代码文件将在代码编辑器中打开。

12. 在功能区代码文件中，添加以下方法。 这是已添加到文档的快捷菜单的两个按钮的回调方法。 此方法确定这些按钮是否显示在快捷菜单中。 只有在右键单击书签中的文本时，才显示粗体和向右转的按钮。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/trin_word_document_menus.cs/ribbon1.cs" id="Snippet5":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/trin_word_document_menus.vb/ribbon1.vb" id="Snippet5":::

## <a name="format-the-text-in-the-bookmark"></a><a name="BKMK_formattextbkmk"></a> 设置书签中文本的格式

### <a name="to-format-the-text-in-the-bookmark"></a>设置书签中文本的格式

1. 在功能区代码文件中，添加 `ButtonClick` 事件处理程序以将格式设置应用于书签。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/trin_word_document_menus.cs/ribbon1.cs" id="Snippet6":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/trin_word_document_menus.vb/ribbon1.vb" id="Snippet6":::

2. **解决方案资源管理器，** 请选择 **ThisDocument.cs** 或 **ThisDocument.vb**。

3. 在菜单栏上，选择“视图” > “代码”。

     **ThisDocument** 类文件将在代码编辑器中打开。

4. 将以下代码添加到 **ThisDocument** 类。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/trin_word_document_menus.cs/thisdocument.cs" id="Snippet3":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/trin_word_document_menus.vb/thisdocument.vb" id="Snippet3":::

    > [!NOTE]
    > 必须编写代码来处理书签重叠的情况。 如果不这样做，默认情况下，将为所选内容的所有书签调用代码。

5. 在 C# 中，必须为事件添加书签控件的事件 <xref:Microsoft.Office.Tools.Word.Document.Startup> 处理程序。 有关创建事件处理程序的信息，请参阅如何：在项目中创建[Office处理程序](../vsto/how-to-create-event-handlers-in-office-projects.md)。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/trin_word_document_menus.cs/thisdocument.cs" id="Snippet4":::

## <a name="test-the-application"></a>测试应用程序
 测试文档，验证在右键单击书签中的文本并且文本格式正确时，快捷菜单中是否显示粗体和向右的菜单项。

### <a name="to-test-your-document"></a>测试文档

1. 按 **F5** 运行项目。

2. 右键单击第一个书签，然后单击"粗体 **"。**

3. 验证 中所有文本的格式 `bookmark1` 是否都是粗体。

4. 右键单击书签重叠的文本，然后单击 **"Italic"。**

5. 验证 中所有文本都是"ital"，并且只有中重叠的文本部分 `bookmark2` `bookmark1` `bookmark2` 为"italic"。

## <a name="next-steps"></a>后续步骤
 以下是接下来可能要执行的一些任务：

- 编写代码以响应中主机控件Excel。 有关详细信息，请参阅 [演练：针对 NamedRange 控件的事件进行编程](../vsto/walkthrough-programming-against-events-of-a-namedrange-control.md)。

- 使用复选框更改书签中的格式设置。 有关详细信息，请参阅 [演练：使用 CheckBox 控件更改文档格式](../vsto/walkthrough-changing-document-formatting-using-checkbox-controls.md)。

## <a name="see-also"></a>请参阅
- [使用 Word 的演练](../vsto/walkthroughs-using-word.md)
- [OfficeUI 自定义](../vsto/office-ui-customization.md)
- [使用扩展对象自动执行 Word](../vsto/automating-word-by-using-extended-objects.md)
- [书签控件](../vsto/bookmark-control.md)
- [解决方案中的可选Office参数](../vsto/optional-parameters-in-office-solutions.md)
