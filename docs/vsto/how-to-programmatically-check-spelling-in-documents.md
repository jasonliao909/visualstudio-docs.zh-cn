---
title: 如何：以编程方式检查文档中的拼写
description: 了解若要以编程方式检查文档中的拼写，可以使用 CheckSpelling 方法。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- documents [Office development in Visual Studio], checking spelling
- spelling checker, documents
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.technology: office-development
ms.workload:
- office
ms.openlocfilehash: a2f03c61a1d35e9c66e1e660a3d2fdb56c2bac9ba6f25cd41cd795d2f172ee51
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121268074"
---
# <a name="how-to-programmatically-check-spelling-in-documents"></a>如何：以编程方式检查文档中的拼写
  若要检查文档中的拼写，请使用 <xref:Microsoft.Office.Interop.Word._Application.CheckSpelling%2A> 方法。 此方法返回一个布尔值，该值指示所提供的参数拼写是否正确。

 [!INCLUDE[appliesto_wdalldocapp](../vsto/includes/appliesto-wdalldocapp-md.md)]

## <a name="to-check-spelling-and-display-results-in-a-message-box"></a>检查拼写和在消息框中显示结果

1. 调用 <xref:Microsoft.Office.Interop.Word._Application.CheckSpelling%2A> 方法，并传递一系列文本来检查拼写错误。 若要使用此代码模板，请从项目中的 `ThisDocument` 或 `ThisAddIn` 类运行它。

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb" id="Snippet113":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs" id="Snippet113":::

## <a name="see-also"></a>另请参阅
- [如何：以编程方式定义和选择文档中的范围](../vsto/how-to-programmatically-define-and-select-ranges-in-documents.md)
- [解决方案中的可选Office参数](../vsto/optional-parameters-in-office-solutions.md)
