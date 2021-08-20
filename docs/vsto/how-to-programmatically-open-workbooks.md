---
title: 如何：以编程方式打开工作簿
description: 了解如何使用 Visual Studio以编程方式打开Microsoft Excel工作簿或使用现有工作簿。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- workbooks, opening
- Excel [Office development in Visual Studio], opening workbooks
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.technology: office-development
ms.workload:
- office
ms.openlocfilehash: 529b957613ae954d35c2284870d6512c7357ac64
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122105946"
---
# <a name="how-to-programmatically-open-workbooks"></a>如何：以编程方式打开工作簿
  <xref:Microsoft.Office.Interop.Excel.Workbooks>使用 Microsoft Office Excel，可以处理所有打开的工作簿并打开工作簿。

 [!INCLUDE[appliesto_xlalldocapp](../vsto/includes/appliesto-xlalldocapp-md.md)]

## <a name="to-open-an-existing-workbook"></a>打开现有工作簿

1. 使用 <xref:Microsoft.Office.Interop.Excel.Workbooks.Open%2A> 集合的 <xref:Microsoft.Office.Interop.Excel.Workbooks> 方法，将 路径传递到工作簿。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/Sheet1.cs" id="Snippet2":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/Sheet1.vb" id="Snippet2":::

## <a name="compile-the-code"></a>编译代码
 此代码示例要求满足以下条件：

- 名为 的 `YourWorkbook.xls` 工作簿必须存在于驱动器 C 上名为 `Test` 的目录中。

## <a name="see-also"></a>请参阅
- [使用工作簿](../vsto/working-with-workbooks.md)
- [如何：以编程方式以工作簿方式打开文本文件](../vsto/how-to-programmatically-open-text-files-as-workbooks.md)
- [如何：以编程方式创建新工作簿](../vsto/how-to-programmatically-create-new-workbooks.md)
- [如何：以编程方式保存工作簿](../vsto/how-to-programmatically-save-workbooks.md)
- [如何：以编程方式关闭工作簿](../vsto/how-to-programmatically-close-workbooks.md)
- [主机项和主机控件的编程限制](../vsto/programmatic-limitations-of-host-items-and-host-controls.md)
- [解决方案中的可选Office参数](../vsto/optional-parameters-in-office-solutions.md)
- [主机项和主机控件概述](../vsto/host-items-and-host-controls-overview.md)
