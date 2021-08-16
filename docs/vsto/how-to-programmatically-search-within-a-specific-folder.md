---
title: 如何：以编程方式搜索特定文件夹
description: 了解如何使用 Visual Studio 以编程方式搜索特定 Microsoft Outlook 文件夹中。
ms.custom: SEO-VS-2020
titleSuffix: ''
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Outlook folders [Office development in Visual Studio], searching
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.technology: office-development
ms.workload:
- office
ms.openlocfilehash: dd14e88b64eff4c4273282bcc743b3acbb2ca6fa51ffff90b93db1bd8ffd0416
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121394246"
---
# <a name="how-to-programmatically-search-within-a-specific-folder"></a>如何：以编程方式搜索特定文件夹
  此代码示例使用 和 方法在收件箱 中电子邮件的主题字段中 `Find` `FindNext` 搜索 **文本**。 此方法使用字符串筛选器检查字母 T 是否用作文本的 `Subject` 起始字母。

 [!INCLUDE[appliesto_olkallapp](../vsto/includes/appliesto-olkallapp-md.md)]

## <a name="example"></a>示例
 :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_OL_SearchFolder/thisaddin.cs" id="Snippet1":::

## <a name="see-also"></a>请参阅
- [使用文件夹](../vsto/working-with-folders.md)
- [Outlook对象模型概述](../vsto/outlook-object-model-overview.md)
- [如何：以编程方式按名称检索文件夹](../vsto/how-to-programmatically-retrieve-a-folder-by-name.md)
