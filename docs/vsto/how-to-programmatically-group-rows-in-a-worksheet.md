---
title: 如何：以编程方式对工作表中的行进行分组
description: 了解如何通过使用 NamedRange 控件或本机范围对象以编程方式Microsoft Excel一个或多个Excel行。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- worksheets, creating groups
- groups, creating in worksheets
- ranges, creating groups
- worksheets, clearing groups
- groups
- groups [Office development in Visual Studio], clearing in worksheets
- worksheets, ungrouping rows and columns
- rows [Office development in Visual Studio], ungrouping
- columns [Office development in Visual Studio], ungrouping
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.technology: office-development
ms.workload:
- office
ms.openlocfilehash: 89d71b501dc7c9c65e2cf1d0d167b34233c30383
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122147994"
---
# <a name="how-to-programmatically-group-rows-in-a-worksheet"></a>如何：以编程方式对工作表中的行进行分组
  可以将一个或多个整行分组。 若要在工作表中创建组，请使用 <xref:Microsoft.Office.Tools.Excel.NamedRange> 控件或本机Excel范围对象。

 [!INCLUDE[appliesto_xlalldocapp](../vsto/includes/appliesto-xlalldocapp-md.md)]

## <a name="use-a-namedrange-control"></a>使用 NamedRange 控件
 如果在设计时向文档级项目添加控件，可以使用 控件 <xref:Microsoft.Office.Tools.Excel.NamedRange> 以编程方式创建组。 以下示例假定同一工作表上有 <xref:Microsoft.Office.Tools.Excel.NamedRange> 三个控件 `data2001` `data2002` ：、 和 `dataAll` 。 每个命名范围都表示工作表中的整行。

### <a name="to-create-a-group-of-namedrange-controls-on-a-worksheet"></a>在工作表上创建一组 NamedRange 控件

1. 通过调用每个范围的 方法将三 <xref:Microsoft.Office.Tools.Excel.NamedRange.Group%2A> 个命名范围分组。 必须将此代码置于表类中，而不是在 `ThisWorkbook` 类中。

     [!code-csharp[Trin_VstcoreExcelAutomation#32](../vsto/codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/Sheet1.cs#32)]
     [!code-vb[Trin_VstcoreExcelAutomation#32](../vsto/codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/Sheet1.vb#32)]

    > [!NOTE]
    > 若要取消行组，请调用 <xref:Microsoft.Office.Tools.Excel.NamedRange.Ungroup%2A> 方法。

## <a name="use-native-excel-ranges"></a>使用本机Excel范围
 该代码假定工作表上Excel名为 、 和 的三 `data2001` `data2002` `dataAll` 个范围。

### <a name="to-create-a-group-of-excel-ranges-in-a-worksheet"></a>在工作表Excel组范围

1. 通过调用每个范围的 方法将三 <xref:Microsoft.Office.Interop.Excel.Range.Group%2A> 个命名范围分组。 以下示例假定同一工作表上有三个名为 、 <xref:Microsoft.Office.Interop.Excel.Range> `data2001` 和 `data2002` `dataAll` 的控件。 每个命名范围都表示工作表中的整行。

     [!code-csharp[Trin_VstcoreExcelAutomation#33](../vsto/codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/Sheet1.cs#33)]
     [!code-vb[Trin_VstcoreExcelAutomation#33](../vsto/codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/Sheet1.vb#33)]

    > [!NOTE]
    > 若要取消行组，请调用 <xref:Microsoft.Office.Interop.Excel.Range.Ungroup%2A> 方法。

## <a name="see-also"></a>请参阅
- [使用工作表](../vsto/working-with-worksheets.md)
- [NamedRange 控件](../vsto/namedrange-control.md)
- [如何：将 NamedRange 控件添加到工作表](../vsto/how-to-add-namedrange-controls-to-worksheets.md)
- [解决方案中的可选Office参数](../vsto/optional-parameters-in-office-solutions.md)
