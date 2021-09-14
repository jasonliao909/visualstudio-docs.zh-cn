---
title: 将新行添加到 ListObject 控件时验证数据
description: 了解如何在将新Visual Studio ListObject 控件时，使用列来验证数据。
ms.custom: SEO-VS-2020
titleSuffix: ''
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- controls [Office development in Visual Studio], validating data
- ListObject control, new row
- ListObject control, validating data
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.technology: office-development
ms.workload:
- office
ms.openlocfilehash: 0b9b70630708ebc558a798371a6d39ff30aed6f9
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126665244"
---
# <a name="how-to-validate-data-when-a-new-row-is-added-to-a-listobject-control"></a>如何：在将新行添加到 ListObject 控件时验证数据
  用户可以向绑定到数据的 <xref:Microsoft.Office.Tools.Excel.ListObject> 控件添加新行。 可以在将更改提交到数据源之前验证用户数据。

 [!INCLUDE[appliesto_xlalldocapp](../vsto/includes/appliesto-xlalldocapp-md.md)]

## <a name="data-validation"></a>数据验证
 每当向绑定到数据的 <xref:Microsoft.Office.Tools.Excel.ListObject> 添加行时，便会引发 <xref:Microsoft.Office.Tools.Excel.ListObject.BeforeAddDataBoundRow> 事件。 可以处理此事件以执行数据验证。 例如，如果应用程序要求只有 18 到 65 岁员工才能添加到数据源，请验证输入的年龄是否在此范围内，然后再添加行。

> [!NOTE]
> 除了在客户端上，还应始终在服务器上检查用户输入。 有关详细信息，请参阅保护 [客户端应用程序](/dotnet/framework/data/adonet/secure-client-applications)。

### <a name="to-validate-data-when-a-new-row-is-added-to-data-bound-listobject"></a>在向数据绑定 ListObject 添加新行时验证数据

1. 在类级别为 ID 和 <xref:System.Data.DataTable> 创建变量。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreHostControlsExcelCS/Sheet1.cs" id="Snippet8":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreHostControlsExcelVB/Sheet1.vb" id="Snippet8":::

2. 在 VSTO 外接程序项目文档中的文档级项目) 或类 (中，在 (类的事件处理程序中创建新的和添加示例列 <xref:System.Data.DataTable> `Startup` `Sheet1` `ThisAddIn`) 和数据。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreHostControlsExcelCS/Sheet1.cs" id="Snippet9":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreHostControlsExcelVB/Sheet1.vb" id="Snippet9":::

3. 向 `list1_BeforeAddDataBoundRow` 事件处理程序添加代码以检查输入的年龄是否处于可接受的范围内。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreHostControlsExcelCS/Sheet1.cs" id="Snippet10":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreHostControlsExcelVB/Sheet1.vb" id="Snippet10":::

## <a name="compile-the-code"></a>编译代码
 此代码示例假定在此代码出现的工作表中有一个名为 <xref:Microsoft.Office.Tools.Excel.ListObject> 的现有 `list1` 。

## <a name="see-also"></a>另请参阅
- [在外接程序Excel扩展 Word 文档VSTO工作簿](../vsto/extending-word-documents-and-excel-workbooks-in-vsto-add-ins-at-run-time.md)
- [文档上的Office控件](../vsto/controls-on-office-documents.md)
- [运行时向Office添加控件](../vsto/adding-controls-to-office-documents-at-run-time.md)
- [ListObject 控件](../vsto/listobject-control.md)
- [使用Excel对象自动执行自动执行](../vsto/automating-excel-by-using-extended-objects.md)
- [如何：将 ListObject 列映射到数据](../vsto/how-to-map-listobject-columns-to-data.md)
