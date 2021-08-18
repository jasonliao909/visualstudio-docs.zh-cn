---
title: Excel对象模型概述
description: 了解你可以与对象模型提供Excel交互，以开发使用 Microsoft Office Excel。
ms.custom: SEO-VS-2020
ms.date: 08/14/2019
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Worksheet object
- Range object
- object models [Office development in Visual Studio], Excel
- object models [Office development in Visual Studio], Office
- Workbook class
- objects [Office development in Visual Studio], Office object models
- Excel object model
- Office object models
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.technology: office-development
ms.workload:
- office
ms.openlocfilehash: 5c37a0251d9414871e568275bdb0b94bb55e5c401487e843186186105175d82e
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121352105"
---
# <a name="excel-object-model-overview"></a>Excel对象模型概述
  若要开发使用 Microsoft Office Excel 的解决方案，可与由 Excel 对象模型提供的对象进行交互。 本主题介绍最重要的对象：

- <xref:Microsoft.Office.Interop.Excel.Application>

- <xref:Microsoft.Office.Interop.Excel.Workbook>

- <xref:Microsoft.Office.Interop.Excel.Worksheet>

- <xref:Microsoft.Office.Interop.Excel.Range>

  [!INCLUDE[appliesto_xlalldocapp](../vsto/includes/appliesto-xlalldocapp-md.md)]

[!include[Add-ins note](includes/addinsnote.md)]

  对象模型紧跟用户界面。 <xref:Microsoft.Office.Interop.Excel.Application> 对象表示整个应用程序，并且每个 <xref:Microsoft.Office.Interop.Excel.Workbook> 对象都包含 `Worksheet` 对象的集合。 在这里，表示单元格的主要抽象是 <xref:Microsoft.Office.Interop.Excel.Range> 对象，它使你能够使用单独的单元格或单元格组。

  除了对象Excel，Office中的项目Visual Studio宿主项和宿主控件，用于扩展 Excel 对象模型中的对象。   主机项和主机控件的行为类似于它们扩展的 Excel 对象，但它们还具有其他功能（如数据绑定功能）和其他事件。 有关详细信息，请参阅使用[扩展Excel自动](../vsto/automating-excel-by-using-extended-objects.md)执行操作和主机[项和主机控件概述](../vsto/host-items-and-host-controls-overview.md)。

  本主题概要介绍 Excel 对象模型。 有关可了解有关整个对象模型Excel的资源，请参阅[使用Excel模型文档](#ExcelOMDocumentation)。

## <a name="access-objects-in-an-excel-project"></a>访问项目Excel对象
 为 VSTO 创建新的 Excel 外接程序项目时，Visual Studio会自动创建 *ThisAddIn.vb* 或 *ThisAddIn.cs* 代码文件。 可以通过使用 `Me.Application` 或 `this.Application` 访问应用程序对象。

 为 Excel 创建新的文档级项目时，可选择创建新的 Excel 工作簿或 Excel 模板项目。 Visual Studio 在新的 Excel 项目中为工作簿和模板项目自动创建以下代码文件。

|Visual Basic|C#|
|------------------|---------|
|ThisWorkbook.vb|ThisWorkbook.cs|
|Sheet1.vb|Sheet1.cs|
|Sheet2.vb|Sheet2.cs|
|Sheet3.vb|Sheet3.cs|

 可以在项目中使用 `Globals` 类来从各个类的外部访问 `ThisWorkbook`、`Sheet1`、`Sheet2` 或 `Sheet3`。 有关详细信息，请参阅[对项目 中的对象的全局Office访问](../vsto/global-access-to-objects-in-office-projects.md)。 下面的示例调用 的 方法，无论代码是放置在 n 个类 <xref:Microsoft.Office.Interop.Excel._Worksheet.PrintPreview%2A> `Sheet1` 还是 `Sheet` 类之 `ThisWorkbook` 一中。

 :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/Sheet1.cs" id="Snippet82":::
 :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/Sheet1.vb" id="Snippet82":::

 由于 Excel 文档中的数据已高度结构化，因此该对象模型是分层模型且非常简单。 Excel提供数百个对象，你可能想要与之交互，但可以通过专注于一小部分可用对象，在对象模型上获得良好的开始。 这些对象包括以下四种：

- 应用程序

- 工作簿

- 工作表

- 范围

  许多使用 Excel 完成的工作都是围绕这四种对象及其成员进行的。

### <a name="application-object"></a>应用程序对象
 Excel <xref:Microsoft.Office.Interop.Excel.Application> 对象表示 Excel 应用程序本身。 <xref:Microsoft.Office.Interop.Excel.Application> 对象公开了大量有关正在运行的应用程序、应用于该实例的选项以及在该实例内部开启的当前用户对象的信息。

> [!NOTE]
> 不应将 Excel 中 <xref:Microsoft.Office.Interop.Excel.ApplicationClass.EnableEvents%2A> 对象的 <xref:Microsoft.Office.Interop.Excel.Application> 属性设置为 **false**。 将此属性设置为 false 可防止 Excel 引发任何事件，包括主机控件的事件。

### <a name="workbook-object"></a>工作簿对象
 <xref:Microsoft.Office.Interop.Excel.Workbook> 对象表示 Excel 应用程序中的单个工作簿。

 Visual Studio 中的 Office 开发工具通过提供 <xref:Microsoft.Office.Interop.Excel.Workbook> 类型来扩展 <xref:Microsoft.Office.Tools.Excel.Workbook> 对象。 此类型使你可以访问 <xref:Microsoft.Office.Interop.Excel.Workbook> 对象的所有功能。 有关详细信息，请参阅 [工作簿主机项](../vsto/workbook-host-item.md)。

### <a name="worksheet-object"></a>Worksheet 对象
 <xref:Microsoft.Office.Interop.Excel.Worksheet> 对象是 <xref:Microsoft.Office.Interop.Excel.Worksheets> 集合的成员。 <xref:Microsoft.Office.Interop.Excel.Worksheet> 的许多属性、方法和事件与由 <xref:Microsoft.Office.Interop.Excel.Application> 或 <xref:Microsoft.Office.Interop.Excel.Workbook> 对象提供的成员相同或类似。

 Excel 提供一个 <xref:Microsoft.Office.Interop.Excel.Sheets> 集合作为 <xref:Microsoft.Office.Interop.Excel.Workbook> 对象的属性。 <xref:Microsoft.Office.Interop.Excel.Sheets> 集合的每个成员都是 <xref:Microsoft.Office.Interop.Excel.Worksheet> 或 <xref:Microsoft.Office.Interop.Excel.Chart> 对象。

 Visual Studio 中的 Office 开发工具通过提供 <xref:Microsoft.Office.Interop.Excel.Worksheet> 类型来扩展 <xref:Microsoft.Office.Tools.Excel.Worksheet> 对象。 此类型使你可以访问 <xref:Microsoft.Office.Interop.Excel.Worksheet> 对象的所有功能以及承载托管控件和处理新事件等新功能。 有关详细信息，请参阅 [工作表主机项](../vsto/worksheet-host-item.md)。

### <a name="range-object"></a>Range 对象
 <xref:Microsoft.Office.Interop.Excel.Range> 对象是你将在 Excel 应用程序中使用最多的对象。 在可以操作 Excel 内的任何区域之前，必须将其表达为 <xref:Microsoft.Office.Interop.Excel.Range> 对象，并使用该范围的方法和属性。 一个 <xref:Microsoft.Office.Interop.Excel.Range> 对象，表示一个单元格、行、列、包含一个或多个单元格块的单元格选定区域（选定区域可能是连续的，也可能不是连续的）或甚至多个工作表上的一组单元格）。

 Visual Studio 通过提供 <xref:Microsoft.Office.Tools.Excel.NamedRange> 和 <xref:Microsoft.Office.Tools.Excel.XmlMappedRange> 类型来扩展 <xref:Microsoft.Office.Interop.Excel.Range> 对象。 这些类型具有与 <xref:Microsoft.Office.Interop.Excel.Range> 对象相同的大部分功能以及数据绑定功能等新功能和新事件。 有关详细信息，请参阅 [NamedRange 控件和](../vsto/namedrange-control.md) [XmlMappedRange 控件](../vsto/xmlmappedrange-control.md)。

## <a name="use-the-excel-object-model-documentation"></a><a name="ExcelOMDocumentation"></a>使用Excel模型文档
 有关 Excel 对象模型的完整信息，可以参考 Excel 主互操作程序集 (PIA) 引用和 VBA 对象模型引用。

### <a name="primary-interop-assembly-reference"></a>主互操作程序集引用
 Excel PIA 参考文档介绍 Excel 的主互操作程序集中的类型。 本文档可从以下位置获得：Excel [2010 主互操作程序集参考](office-primary-interop-assemblies.md)。

 有关 Excel PIA 设计（例如 PIA 中类和接口之间的差异以及如何实现 PIA 中的事件）详细信息，请参阅 Office 主互操作程序集[中的类和接口](/previous-versions/office/office-12/ms247299(v=office.12))概述。

### <a name="vba-object-model-reference"></a>VBA 对象模型参考
 VBA 对象模型引用在 Excel 对象模型被公开到 Visual Basic for Applications (VBA) 代码时记录该对象模型。 有关详细信息，请参阅 Excel [2010 对象模型参考](/office/vba/api/overview/Excel/object-model)。

 VBA 对象模型引用中的所有对象和成员都对应于 Excel PIA 中的类型和成员。 例如，VBA 对象模型引用中的 Worksheet 对象对应于 EXCEL <xref:Microsoft.Office.Interop.Excel.Worksheet> PIA 中的 对象。 虽然 VBA 对象模型引用提供大多数属性、方法和事件的代码示例，但如果要在使用 Visual Studio 创建的 Excel 项目中使用本引用中的 VBA 代码，则必须将其转换为 Visual Basic 或 Visual C# 代码。

### <a name="related-topics"></a>相关主题

|Title|说明|
|-----------|-----------------|
|[Excel解决方案](../vsto/excel-solutions.md)|说明可以如何创建 Microsoft Office excel 的文档级自定义项和 VSTO 外接程序。|
|[使用范围](../vsto/working-with-ranges.md)|提供演示如何使用范围执行常见任务的示例。|
|[使用工作表](../vsto/working-with-worksheets.md)|提供演示如何使用工作表执行常见任务的示例。|
|[使用工作簿](../vsto/working-with-workbooks.md)|提供演示如何使用工作簿执行常见任务的示例。|
