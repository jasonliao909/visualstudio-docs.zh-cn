---
title: 演练：使用内容控件创建模板
description: 了解如何创建文档级自定义项，该自定义项使用内容控件在模板模板Microsoft Word内容。
titleSuffix: ''
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- building blocks [Office development in Visual Studio]
- Word [Office development in Visual Studio], creating documents
- content controls [Office development in Visual Studio], adding to documents
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.technology: office-development
ms.workload:
- office
ms.openlocfilehash: d977aeb7eb4b16dab4de957df2a7b908fba58b18
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122075665"
---
# <a name="walkthrough-create-a-template-by-using-content-controls"></a>演练：使用内容控件创建模板
  本演练演示如何创建使用内容控件在 Microsoft Office Word 模板中创建可重用结构化内容的文档级自定义项。

 [!INCLUDE[appliesto_wdalldoc](../vsto/includes/appliesto-wdalldoc-md.md)]

 Word 使你能够创建可重用文档部件的集合，这些部件名为 *构建基块*。 本演练演示如何将两个表格作为构建基块创建。 每个表格包含几个内容控件，可以容纳不同类型的内容（如纯文本或日期）。 其中一个表格包含有关员工的信息，另一个表格包含客户反馈。

 从模板创建文档后，可通过使用几个 <xref:Microsoft.Office.Tools.Word.BuildingBlockGalleryContentControl> 对象将任一表格添加到文档，这些对象显示模板中的可用构建基块。

 本演练演示以下任务：

- 在设计时创建包含 Word 模板中内容控件的表格。

- 以编程方式填充组合框内容控件和下拉列表内容控件。

- 阻止用户编辑指定表格。

- 将表格添加到模板的构建基块集合。

- 创建一个内容控件来显示模板中的可用构建基块。

  [!INCLUDE[note_settings_general](../sharepoint/includes/note-settings-general-md.md)]

## <a name="prerequisites"></a>先决条件
 您需要满足以下条件才能完成本演练：

- [!INCLUDE[vsto_vsprereq](../vsto/includes/vsto-vsprereq-md.md)]

- Microsoft Word。

## <a name="create-a-new-word-template-project"></a>创建新的 Word 模板项目
 创建 Word 模板，以便用户可以轻松地创建他们自己的副本。

### <a name="to-create-a-new-word-template-project"></a>创建新的 Word 模板项目

1. 创建一个名称为 **MyBuildingBlockTemplate** 的 Word 模板项目。 在向导中，选择在解决方案中创建新的文档。 有关详细信息，请参阅[如何：在 Office 创建Visual Studio。](../vsto/how-to-create-office-projects-in-visual-studio.md)

     [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]在设计器中打开新的 Word 模板，并将 **MyBuildingBlockTemplate** 项目添加到 **解决方案资源管理器。**

## <a name="create-the-employee-table"></a>创建员工表
 创建一个包含四种不同类型的内容控件的表格，用户可以在其中输入有关员工的信息。

### <a name="to-create-the-employee-table"></a>创建员工表

1. 在设计器中托管的 Word 模板的功能区 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 上，单击"插入 **"** 选项卡。

2. 在" **表"** 组中，单击 **"表**"，并插入包含两列和四行的表。

3. 在第一列中键入文本，使之类似于以下列：

   ||
   |-|
   |**员工姓名**|
   |**雇佣日期**|
   |**标题**|
   |**图片**|

4. 单击第二列的第一个单元格 **， ("员工姓名"旁边的) 。**

5. 在功能区上，单击 **“开发人员”** 选项卡。

   > [!NOTE]
   > 如果看不到 **“开发人员”** 选项卡，则必须首先显示它。 有关详细信息，请参阅 [功能区 上的"如何：显示开发人员"选项卡](../vsto/how-to-show-the-developer-tab-on-the-ribbon.md)。

6. 在" **控件"** 组中，单击 **"文本"** 按钮 ![PlainTextContentControl，](../vsto/media/plaintextcontrol.gif "PlainTextContentControl") 将 <xref:Microsoft.Office.Tools.Word.PlainTextContentControl> 添加到第一个单元格。

7. 单击"雇佣日期"旁边的第二 **(第二**) 。

8. 在" **控件"** 组中，单击 **"日期选取** 器"按钮 ![DatePickerContentControl，](../vsto/media/datepicker.gif "DatePickerContentControl") 将 <xref:Microsoft.Office.Tools.Word.DatePickerContentControl> 添加到第二个单元格。

9. 单击"标题"按钮旁边的第二 (**第三**) 。

10. 在" **控件"** 组中，单击 **"组合框** "按钮 ![ComboBoxContentControl](../vsto/media/combobox.gif "ComboBoxContentControl") 将 添加到 <xref:Microsoft.Office.Tools.Word.ComboBoxContentControl> 第三个单元格。

11. 单击"图片"框旁边的第二 (**最后一) 。**

12. 在" **控件"** 组中，单击" **图片内容控件"** 按钮 ![PictureContentControl，](../vsto/media/pictcontentcontrol.gif "PictureContentControl") 将 <xref:Microsoft.Office.Tools.Word.PictureContentControl> 添加到最后一个单元格。

## <a name="create-the-customer-feedback-table"></a>创建客户反馈表
 创建一个包含三种不同类型的内容控件的表格，用户可以在其中输入客户反馈信息。

### <a name="to-create-the-customer-feedback-table"></a>创建客户反馈表

1. 在 Word 模板中，单击前面添加的员工表后的行，然后按 **Enter** 添加新段落。

2. 在功能区上，单击"插入 **"** 选项卡。

3. 在" **表"** 组中，单击 **"表**"，并插入包含两列和三行的表。

4. 在第一列中键入文本，使之类似于以下列：

   ||
   |-|
   |**客户名称**|
   |**满意度**|
   |**备注**|

5. 单击"客户名称"旁边的第二 (**第一个) 。**

6. 在功能区上，单击 **“开发人员”** 选项卡。

7. 在" **控件"** 组中，单击 **"文本"** 按钮 ![PlainTextContentControl，](../vsto/media/plaintextcontrol.gif "PlainTextContentControl") 将 <xref:Microsoft.Office.Tools.Word.PlainTextContentControl> 添加到第一个单元格。

8. 单击"满意度分级"旁边的第二 (**第二) 。**

9. 在" **控件"** 组中，单击 **下拉列表** 按钮 ![DropDownListContentControl](../vsto/media/dropdownlist.gif "DropDownListContentControl") 将 添加到第 <xref:Microsoft.Office.Tools.Word.DropDownListContentControl> 二个单元格。

10. 单击第二列的最后一个单元格 **("注释") 。**

11. 在" **控件"** 组中，单击 **"富文本"** 按钮 ![RichTextContentControl，](../vsto/media/richtextcontrol.gif "RichTextContentControl") 将 <xref:Microsoft.Office.Tools.Word.RichTextContentControl> 添加到最后一个单元格。

## <a name="populate-the-combo-box-and-drop-down-list-programmatically"></a>以编程方式填充组合框和下拉列表
 可以在设计时使用 中的"属性 **"窗口初始化** 内容控件 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 。 也可以在运行时初始化它们，这让你能够动态设置它们的初始状态。 对于本演练，请使用代码在 和 运行时填充 条目，以便查看这些 <xref:Microsoft.Office.Tools.Word.ComboBoxContentControl> <xref:Microsoft.Office.Tools.Word.DropDownListContentControl> 对象如何工作。

### <a name="to-modify-the-ui-of-the-content-controls-programmatically"></a>以编程方式修改内容控件的 UI

1. 在 **解决方案资源管理器** 中，右键单击 **ThisDocument.cs** 或 **ThisDocument.vb，** 然后单击"**查看代码"。**

2. 将以下代码添加到 `ThisDocument` 类。 此代码声明了几个对象，你稍后将在本演练中使用它们。

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/ContentControlTemplateWalkthrough/ThisDocument.vb" id="Snippet1":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/ContentControlTemplateWalkthrough/ThisDocument.cs" id="Snippet1":::

3. 将以下代码添加到 `ThisDocument` 类的 `ThisDocument_Startup` 方法。 此代码将条目添加到表格中的 <xref:Microsoft.Office.Tools.Word.ComboBoxContentControl> 和 <xref:Microsoft.Office.Tools.Word.DropDownListContentControl>，并在用户进行编辑前设置每个控件中显示的占位符文本。

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/ContentControlTemplateWalkthrough/ThisDocument.vb" id="Snippet2":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/ContentControlTemplateWalkthrough/ThisDocument.cs" id="Snippet2":::

## <a name="prevent-users-from-editing-the-employee-table"></a>阻止用户编辑员工表
 使用你之前声明的 <xref:Microsoft.Office.Tools.Word.GroupContentControl> 对象保护员工表。 保护员工表后，用户仍可编辑该表格中的内容控件。 但是，他们无法编辑第一列中的文本或以其他方式修改该表格，如添加或删除行和列。 若要详细了解如何使用 来保护文档的一部分， <xref:Microsoft.Office.Tools.Word.GroupContentControl> 请参阅 [内容控件](../vsto/content-controls.md)。

### <a name="to-prevent-users-from-editing-the-employee-table"></a>阻止用户编辑员工表

1. 将以下代码添加到 `ThisDocument` 类的 `ThisDocument_Startup` 方法中上一步添加的代码之后。 此代码可防止用户通过将表格置于你之前声明的 <xref:Microsoft.Office.Tools.Word.GroupContentControl> 对象之中来编辑员工表。

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/ContentControlTemplateWalkthrough/ThisDocument.vb" id="Snippet3":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/ContentControlTemplateWalkthrough/ThisDocument.cs" id="Snippet3":::

## <a name="add-the-tables-to-the-building-block-collection"></a>将表添加到构建基块集合
 将表格添加到模板中的文档构建基块集合，使用户可以将你创建的表格插入到文档中。 有关文档构建基块的信息，请参阅 [内容控件](../vsto/content-controls.md)。

### <a name="to-add-the-tables-to-the-building-blocks-in-the-template"></a>将表格添加到模板中的构建基块

1. 将以下代码添加到 `ThisDocument` 类的 `ThisDocument_Startup` 方法中上一步添加的代码之后。 此代码将包含表的新构建基块添加到 Microsoft。Office。Interop.Word.BuildingBlockEntries 集合，其中包含模板中所有可重用的构建基块。 新构建基块在名为"员工和客户信息"的新类别中定义，并分配有构建基块类型 `Microsoft.Office.Interop.Word.WdBuildingBlockTypes.wdTypeCustom1` 。

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/ContentControlTemplateWalkthrough/ThisDocument.vb" id="Snippet4":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/ContentControlTemplateWalkthrough/ThisDocument.cs" id="Snippet4":::

2. 将以下代码添加到 `ThisDocument` 类的 `ThisDocument_Startup` 方法中上一步添加的代码之后。 此代码将从模板删除表格。 将不再需要表格，因为已在模板中将其添加到可重用构建基块库。 代码首先将文档设置为设计模式，从而可以删除受保护的员工表。

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/ContentControlTemplateWalkthrough/ThisDocument.vb" id="Snippet5":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/ContentControlTemplateWalkthrough/ThisDocument.cs" id="Snippet5":::

## <a name="create-a-content-control-that-displays-the-building-blocks"></a>创建显示构建基块的内容控件
 创建一个内容控件，用于提供对先前创建的构建基块（即表格）的访问权限。 用户可以单击此控件以将表格添加到文档。

### <a name="to-create-a-content-control-that-displays-the-building-blocks"></a>创建显示构建基块的内容控件

1. 将以下代码添加到 `ThisDocument` 类的 `ThisDocument_Startup` 方法中上一步添加的代码之后。 此代码将初始化之前声明的 <xref:Microsoft.Office.Tools.Word.BuildingBlockGalleryContentControl> 对象。 <xref:Microsoft.Office.Tools.Word.BuildingBlockGalleryContentControl>显示在"员工和客户信息"类别中定义且具有构建基块类型 的所有构建基块 `Microsoft.Office.Interop.Word.WdBuildingBlockTypes.wdTypeCustom1` 。

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/ContentControlTemplateWalkthrough/ThisDocument.vb" id="Snippet6":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/ContentControlTemplateWalkthrough/ThisDocument.cs" id="Snippet6":::

## <a name="test-the-project"></a>测试项目
 用户可以单击文档中的构建基块库控件，以插入员工表或客户反馈表。 用户可以在两个表的内容控件中键入或选择响应。 用户可以修改客户反馈表的其他部分，但应无法修改员工表的其他部分。

### <a name="to-test-the-employee-table"></a>测试员工表

1. 按 **F5** 运行项目。

2. 单击 " **选择您的第一个构建基块** "，显示第一个构建基块库内容控件。

3. 单击控件中 " **自定义库 1** " 标题旁边的下拉箭头，然后选择 " **员工表**"。

4. 单击 " **员工姓名** " 单元格右侧的单元格，然后键入名称。

     验证你只能向此单元格添加纯文本。 <xref:Microsoft.Office.Tools.Word.PlainTextContentControl> 仅允许用户添加纯文本，不允许添加其他类型的内容（如图片或表格）。

5. 单击 " **雇佣日期** " 单元右侧的单元格，并在日期选取器中选择一个日期。

6. 单击 **标题** 单元格右侧的单元格，并在组合框中选择一个工作标题。

     也可以键入列表中不存在的职务名称。 此操作可行的原因是 <xref:Microsoft.Office.Tools.Word.ComboBoxContentControl> 允许用户从条目列表中选择或键入自己的条目。

7. 单击 **图片** 单元右侧单元格中的图标，并浏览到图像进行显示。

8. 尝试向表中添加行或列，并尝试从表中删除行和列。 验证你无法修改该表格。 <xref:Microsoft.Office.Tools.Word.GroupContentControl> 将阻止你进行任何修改。

### <a name="to-test-the-customer-feedback-table"></a>测试客户反馈表

1. 单击 " **选择第二个构建基块** "，显示第二个构建基块库内容控件。

2. 单击控件中 " **自定义库 1** " 标题旁边的下拉箭头，然后选择 " **Customer 表**"。

3. 单击 " **客户名称** " 单元右侧的单元格，然后键入名称。

4. 单击 " **满意度** " 单元格右侧的单元格，然后选择可用的选项之一。

     验证你无法键入自己的条目。 <xref:Microsoft.Office.Tools.Word.DropDownListContentControl> 仅允许用户从条目列表中进行选择。

5. 单击 " **注释** " 单元右侧的单元格，并键入一些注释。

     也可以添加文本以外的内容，如图像或嵌入式表格。 此操作可行的原因是 <xref:Microsoft.Office.Tools.Word.RichTextContentControl> 允许用户添加文本以外的内容。

6. 验证你可以向表中添加行或列，且可以从表中删除行和列。 此操作可行的原因是你没有通过将表格置于 <xref:Microsoft.Office.Tools.Word.GroupContentControl> 来保护它。

7. 关闭模板。

## <a name="next-steps"></a>后续步骤
 可从以下主题了解有关如何使用内容控件的更多信息：

- 将内容控件绑定到嵌入到文档中的 XML 片段（也称为自定义 XML 部件）。 有关详细信息，请参阅 [演练：将内容控件绑定到自定义 XML 部件](../vsto/walkthrough-binding-content-controls-to-custom-xml-parts.md)。

## <a name="see-also"></a>请参阅
- [使用扩展对象实现 Word 自动化](../vsto/automating-word-by-using-extended-objects.md)
- [内容控件](../vsto/content-controls.md)
- [如何：向 Word 文档添加内容控件](../vsto/how-to-add-content-controls-to-word-documents.md)
- [如何：使用内容控件保护文档的某些部分](../vsto/how-to-protect-parts-of-documents-by-using-content-controls.md)
- [主机项和主机控件概述](../vsto/host-items-and-host-controls-overview.md)
- [宿主项和宿主控件的编程限制](../vsto/programmatic-limitations-of-host-items-and-host-controls.md)
- [在运行时将控件添加到 Office 文档](../vsto/adding-controls-to-office-documents-at-run-time.md)
