---
title: 如何：将 ListObject 列映射到数据
description: 了解如何在调用 SetDataBinding 方法时，映射要在 ListObject 中显示的列。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- data [Office development in Visual Studio], mapping to ListObject column
- ListObject control, mapping data
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.technology: office-development
ms.workload:
- office
ms.openlocfilehash: e611ebd51428b91311dade00b42095ba0501d276b2dfe91f7a407593894348fc
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121394649"
---
# <a name="how-to-map-listobject-columns-to-data"></a>如何：将 ListObject 列映射到数据
  将 <xref:Microsoft.Office.Tools.Excel.ListObject> 控件绑定到 <xref:System.Data.DataTable>时，可能不希望显示列表中的所有列，或可能具有未绑定到数据的特定列。 调用 <xref:Microsoft.Office.Tools.Excel.ListObject> 方法时，可以映射希望出现在 <xref:Microsoft.Office.Tools.Excel.ListObject.SetDataBinding%2A> 中的列。

 [!INCLUDE[appliesto_xlalldocapp](../vsto/includes/appliesto-xlalldocapp-md.md)]

## <a name="map-columns"></a>映射列

### <a name="to-map-a-data-table-to-columns-in-a-list"></a>将数据表映射到列表中的列

1. 在类级创建 <xref:System.Data.DataTable> 。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreHostControlsExcelCS/Sheet3.cs" id="Snippet16":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreHostControlsExcelVB/Sheet3.vb" id="Snippet16":::

2. 在文档级项目中的类 (的事件处理程序中添加示例列和数据 `Startup` `Sheet1`) 或 `ThisAddIn` VSTO 外接程序项目中的类 () 。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreHostControlsExcelCS/Sheet3.cs" id="Snippet17":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreHostControlsExcelVB/Sheet3.vb" id="Snippet17":::

3. 调用 <xref:Microsoft.Office.Tools.Excel.ListObject.SetDataBinding%2A> 方法并以列名应显示的顺序传入列表。 List 对象将绑定到新创建的 <xref:System.Data.DataTable> ，但列表对象中列的顺序将与它们在中出现的顺序不同 <xref:System.Data.DataTable> 。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreHostControlsExcelCS/Sheet3.cs" id="Snippet18":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreHostControlsExcelVB/Sheet3.vb" id="Snippet18":::

## <a name="specify-unmapped-columns"></a>指定未映射的列
 将列映射到 <xref:System.Data.DataTable>时，还可以通过传入空字符串来指定特定列不应绑定到数据。 未绑定到数据的新列随后会添加到 <xref:Microsoft.Office.Tools.Excel.ListObject> 控件。

### <a name="to-specify-an-unmapped-column-when-mapping-listobject-columns"></a>在映射 ListObject 列时指定未映射的列

1. 调用 <xref:Microsoft.Office.Tools.Excel.ListObject.SetDataBinding%2A> 方法并以列名应显示的顺序传入列表。 使用空字符串可指示添加未映射的列的位置；在此例中，是介于标题.栏与最后一个名称列之间。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreHostControlsExcelCS/Sheet3.cs" id="Snippet19":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreHostControlsExcelVB/Sheet3.vb" id="Snippet19":::

## <a name="compile-the-code"></a>编译代码
 此代码示例假定在此代码出现的工作表中有一个名为 <xref:Microsoft.Office.Tools.Excel.ListObject> 的现有 `list1` 。

## <a name="see-also"></a>请参阅
- [在运行时扩展 Word 文档和 Excel VSTO 外接程序中的工作簿](../vsto/extending-word-documents-and-excel-workbooks-in-vsto-add-ins-at-run-time.md)
- [Office 文档上的控件](../vsto/controls-on-office-documents.md)
- [在运行时将控件添加到 Office 文档](../vsto/adding-controls-to-office-documents-at-run-time.md)
- [如何：用数据填充 ListObject 控件](../vsto/how-to-fill-listobject-controls-with-data.md)
- [使用扩展对象自动 Excel](../vsto/automating-excel-by-using-extended-objects.md)
- [ListObject 控件](../vsto/listobject-control.md)
