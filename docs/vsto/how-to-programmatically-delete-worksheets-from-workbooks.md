---
title: 如何：以编程方式从工作簿中删除工作表
description: 例如，了解如何使用工作表宿主Microsoft Excel以编程方式删除工作簿中任何工作表。
ms.custom: SEO-VS-2020
titleSuffix: ''
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- workbooks, deleting worksheets
- worksheets, deleting
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.technology: office-development
ms.workload:
- office
ms.openlocfilehash: 783ee376cda1ca5a4e293f1e3f8ef7a5805b6edc
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122148098"
---
# <a name="how-to-programmatically-delete-worksheets-from-workbooks"></a>如何：以编程方式从工作簿中删除工作表
  可以删除工作簿中的任意工作表。 若要删除工作表，请使用该工作表主机项或通过使用工作簿的表集合访问该工作表。

 [!INCLUDE[appliesto_xlalldocapp](includes/appliesto-xlalldocapp-md.md)]

## <a name="use-the-worksheet-host-item"></a>使用工作表主机项
 如果在设计时将工作表添加到了文档级自定义项，请使用 <xref:Microsoft.Office.Tools.Excel.Worksheet.Delete%2A> 方法来删除指定的工作表。 下列代码通过直接引用工作表主机项从工作簿中删除工作表。

> [!IMPORTANT]
> 此代码仅在使用下列任意项目模板创建的项目中运行：
>
> - Excel 2013 工作簿
> - Excel 2013 模板
> - Excel 2010 工作簿
> - Excel 2010 模板
>
>   如果要在任何其他类型的项目中执行此任务，则必须添加对 **Microsoft.Office。互操作。Excel** 程序集，然后必须使用该程序集中的类打开工作簿并删除工作表。 有关详细信息，请参阅如何：通过主[互操作](how-to-target-office-applications-through-primary-interop-assemblies.md)程序集Office目标应用程序，Excel [2010 主互操作程序集引用](office-primary-interop-assemblies.md)。

### <a name="to-delete-a-worksheet-by-using-a-worksheet-host-item"></a>使用工作表主机项删除工作表

1. 调用 <xref:Microsoft.Office.Tools.Excel.Worksheet.Delete%2A> 的 `Sheet1`方法。

     :::code language="csharp" source="codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/Sheet1.cs" id="Snippet17":::
     :::code language="vb" source="codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/Sheet1.vb" id="Snippet17":::

## <a name="use-the-sheets-collection-of-the-excel-workbook"></a>使用工作簿的 Sheets Excel
 在下列情况中通过 Microsoft Office Excel <xref:Microsoft.Office.Interop.Excel.Sheets> 集合访问工作表：

- 想要删除 VSTO 外接程序中的工作表。

- 想要删除的工作表是在运行时文档级自定义项中创建的。

  以下代码通过通过 Sheets 集合的索引号引用工作表，从 **工作簿中删除** 工作表。 此代码假定以编程方式创建了一个新工作表。

> [!IMPORTANT]
> 如果要在任何其他类型的项目中执行此任务，则必须添加对 **Microsoft.Office。互操作。Excel** 程序集，然后必须使用该程序集中的类打开工作簿并删除工作表。 有关详细信息，请参阅如何：通过主[互操作](how-to-target-office-applications-through-primary-interop-assemblies.md)程序集Office目标应用程序，Excel [2010 主互操作程序集引用](office-primary-interop-assemblies.md)。

### <a name="to-delete-a-worksheet-by-using-the-sheets-collection-of-the-excel-workbook"></a>使用 Excel 工作簿的表集合删除工作表

1. 调用 <xref:Microsoft.Office.Interop.Excel.Sheets> 集合的 <xref:Microsoft.Office.Interop.Excel._Worksheet.Delete%2A> 方法。

     :::code language="csharp" source="codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/Sheet1.cs" id="Snippet18":::
     :::code language="vb" source="codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/Sheet1.vb" id="Snippet18":::

## <a name="see-also"></a>请参阅
- [使用工作表](working-with-worksheets.md)
- [如何：以编程方式隐藏工作表](how-to-programmatically-hide-worksheets.md)
- [如何：以编程方式在工作簿中移动工作表](how-to-programmatically-move-worksheets-within-workbooks.md)
- [如何：以编程方式选择工作表](how-to-programmatically-select-worksheets.md)
- [如何：以编程方式将新工作表添加到工作簿](how-to-programmatically-add-new-worksheets-to-workbooks.md)
- [工作表宿主项](worksheet-host-item.md)
- [对项目中对象的全局Office访问](global-access-to-objects-in-office-projects.md)
- [主机项和主机控件的编程限制](programmatic-limitations-of-host-items-and-host-controls.md)
