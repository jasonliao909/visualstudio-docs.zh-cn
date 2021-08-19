---
title: 在文档中保留Office控件
description: 了解如何向解决方案添加代码，以在用户重新打开已关闭的文档时重新创建持久性动态控件。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Office documents [Office development in Visual Studio, Windows Forms controls
- Office documents [Office development in Visual Studio, host controls
- controls [Office development in Visual Studio], persisting in the document
- Windows Forms controls [Office development in Visual Studio], persisting in the document
- documents [Office development in Visual Studio], Windows Forms controls
- documents [Office development in Visual Studio], host controls
- host controls [Office development in Visual Studio], persisting in the document
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.technology: office-development
ms.workload:
- office
ms.openlocfilehash: 0cb0f808dae82b696ee9d766f394a91d25c50cd2
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122046238"
---
# <a name="persist-dynamic-controls-in-office-documents"></a>在文档中保留Office控件

保存并关闭文档或工作薄后，运行时添加的控件不会保留。 具体的行为与宿主控件和 Windows 窗体控件不同。 在这两种情况下，都可以为解决方案添加代码，在用户重新打开该文档时重新创建这些控件。

在运行时添加到文档中的控件称为 *动态控件*。 有关动态控件详细信息，请参阅向Office[添加控件。](../vsto/adding-controls-to-office-documents-at-run-time.md)

[!INCLUDE[appliesto_controls](../vsto/includes/appliesto-controls-md.md)]

## <a name="persist-host-controls-in-the-document"></a>在文档中保留宿主控件

保存并关闭文档后，所有动态宿主控件会从文档中删除。 只会留下基础本机 Office 对象。 例如， <xref:Microsoft.Office.Tools.Excel.ListObject?displayProperty=fullName> 宿主控件将变成 <xref:Microsoft.Office.Interop.Excel.ListObject?displayProperty=fullName>。 本机 Office 对象未连接到宿主控件事件，并且不具备宿主控件的数据绑定功能。

下表列出了文档中保留的每种宿主控件的本机 Office 对象。

|宿主控件类型|本机 Office 对象类型|
|-----------------------|-------------------------------|
|<xref:Microsoft.Office.Tools.Excel.Chart>|<xref:Microsoft.Office.Interop.Excel.Chart>|
|<xref:Microsoft.Office.Tools.Excel.ListObject>|<xref:Microsoft.Office.Interop.Excel.ListObject>|
|<xref:Microsoft.Office.Tools.Excel.NamedRange>|<xref:Microsoft.Office.Interop.Excel.Range>|
|<xref:Microsoft.Office.Tools.Word.Bookmark>|<xref:Microsoft.Office.Interop.Word.Bookmark>|
|<xref:Microsoft.Office.Tools.Word.BuildingBlockGalleryContentControl><br /><br /> <xref:Microsoft.Office.Tools.Word.ComboBoxContentControl><br /><br /> <xref:Microsoft.Office.Tools.Word.ContentControl><br /><br /> <xref:Microsoft.Office.Tools.Word.DatePickerContentControl><br /><br /> <xref:Microsoft.Office.Tools.Word.DropDownListContentControl><br /><br /> <xref:Microsoft.Office.Tools.Word.GroupContentControl><br /><br /> <xref:Microsoft.Office.Tools.Word.PictureContentControl><br /><br /> <xref:Microsoft.Office.Tools.Word.PlainTextContentControl><br /><br /> <xref:Microsoft.Office.Tools.Word.RichTextContentControl>|<xref:Microsoft.Office.Interop.Word.ContentControl>|

### <a name="re-create-dynamic-host-controls-when-documents-are-opened"></a>打开文档时重新创建动态宿主控件

用户每次打开文档时，可以重新创建动态宿主控件来代替现有的本机控件。 打开文档时，用这种方式创建宿主控件可模拟用户可能经历的体验。

若要重新创建 Word 的宿主控件，或者为 Word 重新创建或宿主 <xref:Microsoft.Office.Tools.Excel.NamedRange> <xref:Microsoft.Office.Tools.Excel.ListObject> Excel，请使用 或 `Add` \<*control class*> <xref:Microsoft.Office.Tools.Excel.ControlCollection?displayProperty=fullName> 对象的 <xref:Microsoft.Office.Tools.Word.ControlCollection?displayProperty=fullName> 方法。 使用包含本机 Office 对象参数的方法。

例如，如果想要在打开文档时从现有的本机 <xref:Microsoft.Office.Tools.Excel.ListObject?displayProperty=fullName> 中创建 <xref:Microsoft.Office.Interop.Excel.ListObject?displayProperty=fullName> 宿主控件，应使用 <xref:Microsoft.Office.Tools.Excel.ControlCollection.AddListObject%2A> 方法并传入现有的 <xref:Microsoft.Office.Interop.Excel.ListObject>。 下面的代码示例演示了如何在 Excel 的文档级项目中进行此操作。 该代码会重新创建动态 <xref:Microsoft.Office.Tools.Excel.ListObject> ，它基于 <xref:Microsoft.Office.Interop.Excel.ListObject> 类中名为 `MyListObject` 的现有 `Sheet1` 创建。

:::code language="csharp" source="../vsto/codesnippet/CSharp/trin_excelworkbookdynamiccontrols4/Sheet1.cs" id="Snippet6":::
:::code language="vb" source="../vsto/codesnippet/VisualBasic/trin_excelworkbookdynamiccontrols4/Sheet1.vb" id="Snippet6":::

### <a name="re-create-chart"></a>重新创建图表

若要重新创建主机控件，必须先删除本机 <xref:Microsoft.Office.Tools.Excel.Chart?displayProperty=fullName> ，然后使用 方法 <xref:Microsoft.Office.Interop.Excel.Chart?displayProperty=fullName> 重新创建 <xref:Microsoft.Office.Tools.Excel.Chart?displayProperty=fullName> <xref:Microsoft.Office.Tools.Excel.ControlCollection.AddChart%2A> 。 没有任何方法 `Add` \<*control class*> 可用于基于现有 <xref:Microsoft.Office.Tools.Excel.Chart?displayProperty=fullName> 创建新的 <xref:Microsoft.Office.Interop.Excel.Chart?displayProperty=fullName> 。

如果不首先删除本机 ，则重新创建 时将创建另一个重复 <xref:Microsoft.Office.Interop.Excel.Chart> 图表 <xref:Microsoft.Office.Tools.Excel.Chart?displayProperty=fullName> 。

## <a name="persist-windows-forms-controls-in-documents"></a>在Windows中持久保存窗体控件

保存并关闭文档后， [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)] 会自动从文档中删除所有动态创建的 Windows 窗体控件。 但是，对于文档级和 VSTO 外接程序项目，此行为有所不同。

在文档级自定义项中，控件及其基础 ActiveX 包装（用于在文档上承载控件）会在下次打开该文档时被删除。 没有迹象表明这里曾经存在控件。

在 VSTO 外接程序中，控件会被删除，但 ActiveX 包装仍保留在文档中。 用户下次打开文档时，还可以看到 ActiveX 包装。 在 Excel 中，ActiveX 包装会显示上次保存文档时显示的控件图像。 在 Word 中，不会显示 ActiveX 包装，除非用户单击它们，在这种情况下，会在控件边框上显示一圈虚线。 有几种方法可以删除 ActiveX 包装。 有关详细信息，请参阅[删除ActiveX中的包装器](#removingActiveX)。

### <a name="re-create-windows-forms-controls-when-documents-are-opened"></a>在打开Windows时重新创建窗体控件

当用户重新打开文档时，可以重新创建已删除的 Windows 窗体控件。 为此，必须执行下列任务：

1. 保存或关闭文档时，存储关于大小、位置和控件状态的信息。 在文档级自定义中，可以将数据保存到文档中的数据缓存。 在VSTO外接程序中，可以将数据保存到文档中的自定义 XML 部件。

2. 打开文档时，在引发的事件中重新创建控件。 在文档级项目中，可以在 n 或 事件处理程序 `Sheet`  `_Startup` `ThisDocument_Startup` 中执行此操作。 在 VSTO 外接程序项目中，可以在 <xref:Microsoft.Office.Interop.Excel.AppEvents_Event.WorkbookOpen> 或 <xref:Microsoft.Office.Interop.Word.ApplicationEvents4_Event.DocumentOpen> 事件的事件处理程序中执行此操作。

### <a name="remove-activex-wrappers-in-an-add-in"></a><a name="removingActiveX"></a>删除ActiveX外接程序中的包装器

使用 VSTO 外接程序将动态 Windows 窗体控件添加到文档时，可以阻止控件的 ActiveX 包装器在下次以下列方式打开文档时出现在文档中。

#### <a name="remove-activex-wrappers-when-the-document-is-opened"></a>打开ActiveX时删除包装器

若要删除所有 ActiveX 包装，请调用 `GetVstoObject` 方法为表示新打开文档的 <xref:Microsoft.Office.Interop.Word.Document> 或 <xref:Microsoft.Office.Interop.Excel.Workbook> 生成宿主项。 例如，若要从 Word 文档中删除所有 ActiveX 包装，可以调用 `GetVstoObject` 方法来为 <xref:Microsoft.Office.Interop.Word.Document> 对象生成宿主项，该对象会传递给 <xref:Microsoft.Office.Interop.Word.ApplicationEvents4_Event.DocumentOpen> 事件的事件处理程序。

知道只能在安装 VSTO 外接程序的计算机上打开文档时，此过程非常有用。 如果该文档可能会传递给其他未安装 VSTO 外接程序的用户，请考虑在关闭文档之前删除控件。

下面的代码示例演示如何在打开文档时调用 `GetVstoObject` 方法。

:::code language="vb" source="../vsto/codesnippet/VisualBasic/trin_wordaddindynamiccontrols/ThisAddIn.vb" id="Snippet11":::
:::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_WordAddInDynamicControls/ThisAddIn.cs" id="Snippet11":::

虽然 方法主要用于运行时生成新的主机项，但此方法也会在首次为特定文档调用文档时ActiveX清除文档的所有宿主 `GetVstoObject` 包装器。 若要详细了解如何使用 方法，请参阅扩展 Word 文档Excel运行时在 VSTO `GetVstoObject` [外接程序中扩展工作簿](../vsto/extending-word-documents-and-excel-workbooks-in-vsto-add-ins-at-run-time.md)。

如果VSTO打开文档时外接程序创建动态控件，VSTO外接程序将在创建控件的过程中调用 `GetVstoObject` 方法。 此方案中，不需要添加对 `GetVstoObject` 方法的单独调用来删除 ActiveX 包装。

#### <a name="remove-the-dynamic-controls-before-the-document-is-closed"></a>在文档关闭之前删除动态控件

在关闭文档之前，VSTO 外接程序可以从文档中显式删除每个动态控件。 对于可能传递给其他未安装 VSTO 外接程序的用户的文档而言，此过程非常有用。

以下代码示例演示了如何在文档关闭时，从 Word 文档中删除所有 Windows 窗体控件。

:::code language="vb" source="../vsto/codesnippet/VisualBasic/trin_wordaddindynamiccontrols/ThisAddIn.vb" id="Snippet10":::
:::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_WordAddInDynamicControls/ThisAddIn.cs" id="Snippet10":::

## <a name="see-also"></a>请参阅

- [运行时向Office添加控件](../vsto/adding-controls-to-office-documents-at-run-time.md)
