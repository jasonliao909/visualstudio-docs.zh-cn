---
title: 如何：向工作表添加 ListObject 控件
description: 了解如何在设计时和运行时在文档级项目中将 ListObject 控件添加到 Microsoft Office Excel 工作表。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- ListObject control, adding to worksheets
- controls [Office development in Visual Studio], adding to worksheets
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.technology: office-development
ms.workload:
- office
ms.openlocfilehash: 0d10d82a404ec5248e06c3d4f71d622c793f62ad
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122083513"
---
# <a name="how-to-add-listobject-controls-to-worksheets"></a>如何：向工作表添加 ListObject 控件
  在文档级项目中，你可以在设计时和运行时将 <xref:Microsoft.Office.Tools.Excel.ListObject> 控件添加到 Microsoft Office Excel 工作表。

 [!INCLUDE[appliesto_xlalldocapp](../vsto/includes/appliesto-xlalldocapp-md.md)]

 你也可以在 VSTO 外接程序项目中，在运行时添加 <xref:Microsoft.Office.Tools.Excel.ListObject> 控件。

 本主题介绍了以下任务：

- [在设计时添加 ListObject 控件](#designtime)

- [在运行时在文档级项目中添加 ListObject 控件](#runtimedoclevel)

- [在运行时在 VSTO 外接程序项目中添加 ListObject 控件](#runtimeaddin)

  有关控件的详细信息 <xref:Microsoft.Office.Tools.Excel.ListObject> ，请参阅 [ListObject 控件](../vsto/listobject-control.md)。

## <a name="add-listobject-controls-at-design-time"></a><a name="designtime"></a> 在设计时添加 ListObject 控件
 有多种方法可 <xref:Microsoft.Office.Tools.Excel.ListObject> 在设计时在文档级项目中将控件添加到工作表：在 Excel 中，从 Visual Studio **"工具箱**"，以及从 "**数据源**" 窗口。

 [!INCLUDE[note_settings_general](../sharepoint/includes/note-settings-general-md.md)]

### <a name="to-use-the-ribbon-in-excel"></a>在 Excel 中使用功能区

1. 在“插入”  选项卡上，单击“表”  组中的“表” 。

2. 选择要包含在列表中的一个或多个单元格，然后单击“确定” 。

#### <a name="to-use-the-toolbox"></a>使用工具箱

1. 从“工具箱”  的“Excel 控件” 选项卡上，拖动 <xref:Microsoft.Office.Tools.Excel.ListObject> 到工作表。

     “添加 ListObject 控件”  对话框随即出现。

2. 选择要包含在列表中的一个或多个单元格，然后单击“确定” 。

     如果不希望保留默认名称，可以在“属性”  窗口中更改名称。

#### <a name="to-use-the-data-sources-window"></a>使用“数据源”窗口

1. 打开“数据源”  窗口并为项目创建数据源。 有关详细信息，请参阅 [添加新连接](../data-tools/add-new-connections.md)。

2. 将表从“数据源”  窗口拖到工作表中。

     数据绑定 <xref:Microsoft.Office.Tools.Excel.ListObject> 控件将添加到工作表中。 有关详细信息，请参阅[数据绑定和 Windows 窗体](/dotnet/framework/winforms/data-binding-and-windows-forms)。

## <a name="add-listobject-controls-at-run-time-in-a-document-level-project"></a><a name="runtimedoclevel"></a> 在运行时在文档级项目中添加 ListObject 控件
 可以在运行时动态添加 <xref:Microsoft.Office.Tools.Excel.ListObject> 控件。 这使得你可以创建宿主控件以响应事件。 工作表关闭时，动态创建的列表对象不作为宿主控件保留在工作表中。 有关详细信息，请参阅[在运行时将控件添加到 Office 文档](../vsto/adding-controls-to-office-documents-at-run-time.md)。

#### <a name="to-add-a-listobject-control-to-a-worksheet-programmatically"></a>以编程方式将 ListObject 控件添加到工作表中

1. 在 <xref:Microsoft.Office.Tools.Excel.Worksheet.Startup> 的 `Sheet1`事件处理程序中，插入下列代码以将 <xref:Microsoft.Office.Tools.Excel.ListObject> 控件添加到 **A1** 至 **A4** 单元格。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreHostControlsExcelCS/Sheet1.cs" id="Snippet2":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreHostControlsExcelVB/Sheet1.vb" id="Snippet2":::

## <a name="add-listobject-controls-at-run-time-in-a-vsto-add-in-project"></a><a name="runtimeaddin"></a>在运行时在 VSTO 外接程序项目中添加 ListObject 控件
 可以按编程方式将 <xref:Microsoft.Office.Tools.Excel.ListObject> 控件添加到 VSTO 外接程序项目中任何打开的工作表中。 工作表保存并关闭时，动态创建的列表对象不作为宿主控件保留在工作表中。 有关详细信息，请参阅在[运行时 VSTO 外接程序中扩展 Word 文档和 Excel 工作簿](../vsto/extending-word-documents-and-excel-workbooks-in-vsto-add-ins-at-run-time.md)。

#### <a name="to-add-a-listobject-control-to-a-worksheet-programmatically"></a>以编程方式将 ListObject 控件添加到工作表中

1. 下面的代码将生成基于打开工作表的工作表宿主项，然后将 <xref:Microsoft.Office.Tools.Excel.ListObject> 控件添加到 **A1** 至 **A4** 单元格。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_Excel_Dynamic_Controls/ThisAddIn.cs" id="Snippet8":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_Excel_Dynamic_Controls/ThisAddIn.vb" id="Snippet8":::

## <a name="see-also"></a>请参阅
- [在运行时扩展 Word 文档和 Excel VSTO 外接程序中的工作簿](../vsto/extending-word-documents-and-excel-workbooks-in-vsto-add-ins-at-run-time.md)
- [Office 文档上的控件](../vsto/controls-on-office-documents.md)
- [ListObject 控件](../vsto/listobject-control.md)
- [使用扩展对象自动 Excel](../vsto/automating-excel-by-using-extended-objects.md)
- [主机项和主机控件概述](../vsto/host-items-and-host-controls-overview.md)
- [如何：调整 ListObject 控件的大小](../vsto/how-to-resize-listobject-controls.md)
- [在 Office 解决方案中将数据绑定到控件](../vsto/binding-data-to-controls-in-office-solutions.md)
- [宿主项和宿主控件的编程限制](../vsto/programmatic-limitations-of-host-items-and-host-controls.md)
