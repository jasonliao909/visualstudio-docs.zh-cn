---
title: 如何：以编程方式以工作簿方式打开文本文件
description: 了解如何使用 Visual Studio 以编程方式打开文本文件作为Microsoft Excel工作簿。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- workbooks, opening text files as
- text [Office development in Visual Studio], text files
- text files, opening as workbooks
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.technology: office-development
ms.workload:
- office
ms.openlocfilehash: e132cf1f729a279b13c65e9c3da3305f832dc96cdebf8c4a053264792db0e2f1
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121296861"
---
# <a name="how-to-programmatically-open-text-files-as-workbooks"></a>如何：以编程方式以工作簿方式打开文本文件
  可以将文本文件作为工作簿打开。 必须输入要打开的文本文件的名称。 可以指定多个可选参数，例如要开始分析的行号和文件中数据的列格式。

 [!INCLUDE[appliesto_xlalldocapp](../vsto/includes/appliesto-xlalldocapp-md.md)]

## <a name="example"></a>示例
 :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/Sheet1.cs" id="Snippet80":::
 :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/Sheet1.vb" id="Snippet80":::

## <a name="compile-the-code"></a>编译代码
 此示例需要以下组件：

- 一个名为 的逗号分隔文本文件 `Test.txt` ，其中包含至少三行文本。

- 要存储在 `Test.txt` 驱动器 C 上的文本文件。

## <a name="see-also"></a>请参阅
- [使用工作簿](../vsto/working-with-workbooks.md)
- [如何：以编程方式打开工作簿](../vsto/how-to-programmatically-open-workbooks.md)
- [如何：以编程方式创建新工作簿](../vsto/how-to-programmatically-create-new-workbooks.md)
- [如何：以编程方式保存工作簿](../vsto/how-to-programmatically-save-workbooks.md)
- [如何：以编程方式关闭工作簿](../vsto/how-to-programmatically-close-workbooks.md)
- [解决方案中的可选Office参数](../vsto/optional-parameters-in-office-solutions.md)
