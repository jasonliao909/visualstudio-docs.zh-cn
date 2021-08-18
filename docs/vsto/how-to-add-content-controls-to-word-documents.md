---
title: 如何：向 Word 文档添加内容控件
description: 了解在文档级 Word 项目中，可以在设计时或运行时将内容控件添加到项目中的文档。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- restricted permissions [Office development in Visual Studio]
- DropDownListContentControl, adding to documents
- BuildingBlockGalleryContentControl, adding to documents
- partial document protection [Office development in Visual Studio]
- RichTextContentControl, adding to documents
- Word [Office development in Visual Studio], partial document protection
- content controls [Office development in Visual Studio], protecting
- PictureContentControl, adding to documents
- GroupContentControl, adding to documents
- document protection [Office development in Visual Studio]
- PlainTextContentControl, adding to documents
- content controls [Office development in Visual Studio], adding
- ComboBoxContentControl, adding to documents
- DatePickerContentControl, adding to documents
- Word [Office development in Visual Studio], restricted permissions
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.technology: office-development
ms.workload:
- office
ms.openlocfilehash: a9df9bebf1ff731b20f4a5673b3450e5ccc0c10a
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122100200"
---
# <a name="how-to-add-content-controls-to-word-documents"></a>如何：向 Word 文档添加内容控件
  在文档级 Word 项目中，你可以在设计时或在运行时向项目中的文档添加内容控件。 在 Word VSTO 外接程序项目中，可以在运行时向任何打开的文档添加内容控件。

 [!INCLUDE[appliesto_wdalldocapp](../vsto/includes/appliesto-wdalldocapp-md.md)]

 本主题介绍了以下任务：

- [在设计时添加内容控件](#designtime)

- [在文档级项目中运行时添加内容控件](#runtimedoclevel)

- [在外接程序项目中VSTO内容控件](#runtimeaddin)

  有关内容控件的信息，请参阅 [内容控件](../vsto/content-controls.md)。

## <a name="add-content-controls-at-design-time"></a><a name="designtime"></a> 在设计时添加内容控件
 在设计时向文档级项目中的文档添加内容控件有以下几种方式：

- 从“ **工具箱”** 的 **“Word 控件”** 选项卡添加内容控件。

- 用和在 Word 中添加本机内容控件相同的方式向文档添加内容控件。

- 从 **“数据源”** 窗口将内容控件拖动到你的文档中。 当你想要在创建控件后将控件绑定到数据时会非常有用。 有关详细信息，请参阅 [如何：使用对象的数据](../vsto/how-to-populate-documents-with-data-from-objects.md) 填充文档和 [如何：使用数据库中的数据填充文档](../vsto/how-to-populate-documents-with-data-from-a-database.md)。

  [!INCLUDE[note_settings_general](../sharepoint/includes/note-settings-general-md.md)]

### <a name="to-add-a-content-control-to-a-document-by-using-the-toolbox"></a>若要使用工具箱向文档添加内容控件

1. 在托管在 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 设计器的文档中，将光标置于想要添加内容控件的地方，或选择想要内容控件替换的文本。

2. 打开 **“工具箱”** 并单击 **“Word 控件”** 选项卡。

3. 通过以下方式之一添加控件：

    - 双击 **“工具箱”** 中的某个内容控件。

         或

    - 单击"工具箱"中 **的内容控件** ，然后按 **Enter** 键。

         或

    - 将某个内容控件从 **“工具箱”** 拖动到文档中。 内容控件将添加到文档中当前所选内容的位置，而不是鼠标指针的位置。

> [!NOTE]
> 你不能使用 <xref:Microsoft.Office.Tools.Word.GroupContentControl> “工具箱” **添加**。 在 Word 中或在运行时，只可添加 <xref:Microsoft.Office.Tools.Word.GroupContentControl> 。

> [!NOTE]
> Visual Studio 在工具箱中不提供复选框内容控件。 若要向文档添加复选框内容控件，则必须以编程方式创建一个 <xref:Microsoft.Office.Tools.Word.ContentControl> 对象。 有关详细信息，请参阅内容 [控件](../vsto/content-controls.md)。

#### <a name="to-add-a-content-control-to-a-document-in-word"></a>若要在 Word 中向文档添加内容控件

1. 在托管在 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 设计器的文档中，将光标置于想要添加内容控件的地方，或选择想要内容控件替换的文本。

2. 在功能区上，单击 **“开发人员”** 选项卡。

    > [!NOTE]
    > 如果看不到 **“开发人员”** 选项卡，则必须首先显示它。 有关详细信息，请参阅 [功能区 上的"如何：显示开发人员"选项卡](../vsto/how-to-show-the-developer-tab-on-the-ribbon.md)。

3. 在 **“控件”** 组中，单击你想要添加的内容控件的图标。

## <a name="add-content-controls-at-run-time-in-a-document-level-project"></a><a name="runtimedoclevel"></a> 在文档级项目中运行时添加内容控件
 可以通过使用项目中 <xref:Microsoft.Office.Tools.Word.Document.Controls%2A> 类的 `ThisDocument` 属性的方法在运行时以编程方式向文档添加内容控件。 每种方法有三个重载可用于按以下方式添加内容控件：

- 在当前所选内容中添加控件。

- 在指定范围内添加控件。

- 添加基于文档中的本机内容控件的控件。

  文档关闭时，动态创建的内容控件将不保留在文档中。 但是，本机内容控件会保留在文档中。 在下次打开该文档时，你可以重新创建基于本机内容控件的内容控件。 有关详细信息，请参阅[向Office添加控件。](../vsto/adding-controls-to-office-documents-at-run-time.md)

> [!NOTE]
> 若要在 Word 2010 项目中向文档添加复选框内容控件，则必须创建一个 <xref:Microsoft.Office.Tools.Word.ContentControl> 对象。 有关详细信息，请参阅内容 [控件](../vsto/content-controls.md)。

### <a name="to-add-a-content-control-at-the-current-selection"></a>在当前所选内容中添加内容控件

1. 使用名称为 (，其中 control 类是要添加的内容控件的类名，例如 <xref:Microsoft.Office.Tools.Word.ControlCollection> `Add` \<*control class*> ) ，并且具有一个参数作为新控件 <xref:Microsoft.Office.Tools.Word.ControlCollection.AddRichTextContentControl%2A> 的名称。

     下面的代码示例使用 <xref:Microsoft.Office.Tools.Word.ControlCollection.AddRichTextContentControl%2A> 方法将一个新 <xref:Microsoft.Office.Tools.Word.RichTextContentControl> 添加到文档的开头。 若要运行此代码，将此代码添加到项目的 `ThisDocument` 类中，然后从 `AddRichTextControlAtSelection` 事件处理程序调用 `ThisDocument_Startup` 方法。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/trin_wordcontentcontrolreference/RichText.cs" id="Snippet700":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/trin_contentcontrolreference/RichText.vb" id="Snippet700":::

### <a name="to-add-a-content-control-at-a-specified-range"></a>在指定范围内添加内容控件

1. 使用名称为 (，其中 control 类是要添加的内容控件类的名称，例如 <xref:Microsoft.Office.Tools.Word.ControlCollection> `Add` \<*control class*>  <xref:Microsoft.Office.Tools.Word.ControlCollection.AddRichTextContentControl%2A>) ，并且具有 <xref:Microsoft.Office.Interop.Word.Range> 参数。

     下面的代码示例使用 <xref:Microsoft.Office.Tools.Word.ControlCollection.AddRichTextContentControl%2A> 方法将一个新 <xref:Microsoft.Office.Tools.Word.RichTextContentControl> 添加到文档的开头。 若要运行此代码，将此代码添加到项目的 `ThisDocument` 类中，然后从 `AddRichTextControlAtRange` 事件处理程序调用 `ThisDocument_Startup` 方法。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/trin_wordcontentcontrolreference/RichText.cs" id="Snippet701":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/trin_contentcontrolreference/RichText.vb" id="Snippet701":::

### <a name="to-add-a-content-control-that-is-based-on-a-native-content-control"></a>要添加基于本机内容控件的内容控件

1. 使用名称为 (，其中 control 类是要添加的内容控件类的名称，例如 <xref:Microsoft.Office.Tools.Word.ControlCollection> `Add` \<*control class*>  <xref:Microsoft.Office.Tools.Word.ControlCollection.AddRichTextContentControl%2A>) ，并且具有 `Microsoft.Office.Interop.Word.ContentControl` 参数。

     下面的代码示例使用 <xref:Microsoft.Office.Tools.Word.ControlCollection.AddRichTextContentControl%2A> 方法为文档中的每个本机多格式文本控件创建一个新的 <xref:Microsoft.Office.Tools.Word.RichTextContentControl> 。 若要运行此代码，将此代码添加到项目的 `ThisDocument` 类中，然后从 `CreateRichTextControlsFromNativeControls` 事件处理程序调用 `ThisDocument_Startup` 方法。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/trin_wordcontentcontrolreference/RichText.cs" id="Snippet702":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/trin_contentcontrolreference/RichText.vb" id="Snippet702":::

## <a name="add-content-controls-at-run-time-in-a-vsto-add-in-project"></a><a name="runtimeaddin"></a>在外接程序项目中VSTO控件
 你可以通过使用 VSTO 外接程序在运行时以编程方式向任何打开的文档添加内容控件。 若要执行此操作，生成基于打开的文档的 <xref:Microsoft.Office.Tools.Word.Document> 主机项，然后使用此主机项的 <xref:Microsoft.Office.Tools.Word.Document.Controls%2A> 属性的方法。 每种方法有三个重载可用于按以下方式添加内容控件：

- 在当前所选内容中添加控件。

- 在指定范围内添加控件。

- 添加基于文档中的本机内容控件的控件。

  文档关闭时，动态创建的内容控件将不保留在文档中。 但是，本机内容控件会保留在文档中。 在下次打开该文档时，你可以重新创建基于本机内容控件的内容控件。 有关详细信息，请参阅在文档[文档中Office控件](../vsto/persisting-dynamic-controls-in-office-documents.md)。

  有关在外接程序项目中VSTO宿主项的信息，请参阅在 VSTO 外接程序中运行时扩展 Word 文档[和 Excel 工作簿](../vsto/extending-word-documents-and-excel-workbooks-in-vsto-add-ins-at-run-time.md)。

> [!NOTE]
> 若要向文档添加复选框内容控件，则必须创建一个 <xref:Microsoft.Office.Tools.Word.ContentControl> 对象。 有关详细信息，请参阅内容 [控件](../vsto/content-controls.md)。

### <a name="to-add-a-content-control-at-the-current-selection"></a>在当前所选内容中添加内容控件

1. 使用名称为 (，其中 control 类是要添加的内容控件的类名，例如 <xref:Microsoft.Office.Tools.Word.ControlCollection> `Add` \<*control class*> ) ，并且具有一个参数作为新控件 <xref:Microsoft.Office.Tools.Word.ControlCollection.AddRichTextContentControl%2A> 的名称。

     下面的代码示例使用 <xref:Microsoft.Office.Tools.Word.ControlCollection.AddRichTextContentControl%2A> 方法将一个新 <xref:Microsoft.Office.Tools.Word.RichTextContentControl> 添加到活动文档的开头。 若要运行此代码，将此代码添加到项目的 `ThisAddIn` 类中，然后从 `AddRichTextControlAtSelection` 事件处理程序调用 `ThisAddIn_Startup` 方法。

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/trin_wordaddindynamiccontrols/ThisAddIn.vb" id="Snippet1":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_WordAddInDynamicControls/ThisAddIn.cs" id="Snippet1":::

### <a name="to-add-a-content-control-at-a-specified-range"></a>在指定范围内添加内容控件

1. 使用名称为 (，其中 control 类是要添加的内容控件类的名称，例如 <xref:Microsoft.Office.Tools.Word.ControlCollection> `Add` \<*control class*>  <xref:Microsoft.Office.Tools.Word.ControlCollection.AddRichTextContentControl%2A>) ，并且具有 <xref:Microsoft.Office.Interop.Word.Range> 参数。

     下面的代码示例使用 <xref:Microsoft.Office.Tools.Word.ControlCollection.AddRichTextContentControl%2A> 方法将一个新 <xref:Microsoft.Office.Tools.Word.RichTextContentControl> 添加到活动文档的开头。 若要运行此代码，将此代码添加到项目的 `ThisAddIn` 类中，然后从 `AddRichTextControlAtRange` 事件处理程序调用 `ThisAddIn_Startup` 方法。

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/trin_wordaddindynamiccontrols/ThisAddIn.vb" id="Snippet2":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_WordAddInDynamicControls/ThisAddIn.cs" id="Snippet2":::

#### <a name="to-add-a-content-control-that-is-based-on-a-native-content-control"></a>要添加基于本机内容控件的内容控件

1. 使用名称为 (，其中 control 类是要添加的内容控件类的名称，例如 <xref:Microsoft.Office.Tools.Word.ControlCollection> `Add` \<*control class*>  <xref:Microsoft.Office.Tools.Word.ControlCollection.AddRichTextContentControl%2A>) ，并且具有 `Microsoft.Office.Interop.Word.ContentControl` 参数。

     下面的代码示例使用 <xref:Microsoft.Office.Tools.Word.ControlCollection.AddRichTextContentControl%2A> 方法以在文档打开之后为文档中的每个本机多格式文本控件创建一个新的 <xref:Microsoft.Office.Tools.Word.RichTextContentControl> 。 若要运行此代码，将代码添加到项目中的 `ThisAddIn` 类。

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/trin_wordaddindynamiccontrols/ThisAddIn.vb" id="Snippet3":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_WordAddInDynamicControls/ThisAddIn.cs" id="Snippet3":::

     对于 C#，则还必须将 `Application_DocumentOpen` 事件处理程序附加到 <xref:Microsoft.Office.Interop.Word.ApplicationEvents4_Event.DocumentOpen> 事件。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_WordAddInDynamicControls/ThisAddIn.cs" id="Snippet6":::

## <a name="see-also"></a>请参阅
- [使用扩展对象自动执行 Word](../vsto/automating-word-by-using-extended-objects.md)
- [主机项和主机控件概述](../vsto/host-items-and-host-controls-overview.md)
- [运行时向Office文档添加控件](../vsto/adding-controls-to-office-documents-at-run-time.md)
- [主机项和主机控件的编程限制](../vsto/programmatic-limitations-of-host-items-and-host-controls.md)
- [程序VSTO外接程序](../vsto/programming-vsto-add-ins.md)
- [计划文档级自定义项](../vsto/programming-document-level-customizations.md)
