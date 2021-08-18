---
title: 如何：以编程方式显示工作表注释
description: 了解如何以编程方式在文档级别或应用程序级别的 Microsoft Excel 工作表中显示和隐藏注释。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- worksheets, comments
- comments, worksheets
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.technology: office-development
ms.workload:
- office
ms.openlocfilehash: 614fea5dc82ebd79096a81ea96d26a0a84216678
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122083235"
---
# <a name="how-to-programmatically-display-worksheet-comments"></a>如何：以编程方式显示工作表注释
  可以在 Microsoft Office Excel 工作表中以编程方式显示和隐藏注释。

 [!INCLUDE[appliesto_xlalldocapp](../vsto/includes/appliesto-xlalldocapp-md.md)]

## <a name="to-display-all-comments-on-a-worksheet-in-a-document-level-customization"></a>在文档级自定义项的工作表中显示所有注释

1. 若想显示注释，请将 <xref:Microsoft.Office.Interop.Excel.Comment.Visible%2A> 属性设置为 **true** ；否则为 **false**。 必须将此代码置于表类中，而不是在 `ThisWorkbook` 类中。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/Sheet1.cs" id="Snippet31":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/Sheet1.vb" id="Snippet31":::

## <a name="to-display-all-comments-on-a-worksheet-in-an-application-level-vsto-add-in"></a>在应用程序级 VSTO 外接程序的工作表中显示所有注释

1. 若想显示注释，请将 <xref:Microsoft.Office.Interop.Excel.Comment.Visible%2A> 属性设置为 **true** ；否则为 **false**。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/trin_vstcoreexcelautomationaddin/ThisAddIn.cs" id="Snippet21":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/trin_vstcoreexcelautomationaddin/ThisAddIn.vb" id="Snippet21":::

## <a name="see-also"></a>请参阅
- [使用工作表](../vsto/working-with-worksheets.md)
- [如何：以编程方式添加和删除工作表注释](../vsto/how-to-programmatically-add-and-delete-worksheet-comments.md)
- [主机项和主机控件概述](../vsto/host-items-and-host-controls-overview.md)
