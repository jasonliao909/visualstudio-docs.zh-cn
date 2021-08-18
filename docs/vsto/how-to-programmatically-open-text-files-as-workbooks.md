---
title: 如何：以编程方式将文本文件作为工作簿打开
description: 了解如何使用 Visual Studio 以编程方式将文本文件作为 Microsoft Excel 工作簿打开。
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
ms.openlocfilehash: 68ee509eca06d6785f47fc776ad42c9f010b5219
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122106037"
---
# <a name="how-to-programmatically-open-text-files-as-workbooks"></a>如何：以编程方式将文本文件作为工作簿打开
  您可以将文本文件作为工作簿打开。 必须传入要打开的文本文件的名称。 您可以指定多个可选参数，如开始分析的行号以及文件中数据的列格式。

 [!INCLUDE[appliesto_xlalldocapp](../vsto/includes/appliesto-xlalldocapp-md.md)]

## <a name="example"></a>示例
 :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/Sheet1.cs" id="Snippet80":::
 :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/Sheet1.vb" id="Snippet80":::

## <a name="compile-the-code"></a>编译代码
 此示例需要以下组件：

- 一个名为的逗号分隔 `Test.txt` 的文本文件，其中至少包含三行文本。

- `Test.txt`要存储在驱动器 C 上的文本文件。

## <a name="see-also"></a>请参阅
- [使用工作簿](../vsto/working-with-workbooks.md)
- [如何：以编程方式打开工作簿](../vsto/how-to-programmatically-open-workbooks.md)
- [如何：以编程方式创建新的工作簿](../vsto/how-to-programmatically-create-new-workbooks.md)
- [如何：以编程方式保存工作簿](../vsto/how-to-programmatically-save-workbooks.md)
- [如何：以编程方式关闭工作簿](../vsto/how-to-programmatically-close-workbooks.md)
- [Office 解决方案中的可选参数](../vsto/optional-parameters-in-office-solutions.md)
