---
title: 如何：以编程方式在特定文件夹中搜索
description: 了解如何使用 Visual Studio 以编程方式在特定 Microsoft Outlook 文件夹内进行搜索。
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
ms.workload:
- office
ms.openlocfilehash: a9c7861698e678ca6d8332e3940c3ae49ff423f3
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2021
ms.locfileid: "99877871"
---
# <a name="how-to-programmatically-search-within-a-specific-folder"></a>如何：以编程方式在特定文件夹中搜索
  此代码示例使用 `Find` 和 `FindNext` 方法在 **收件箱** 中的电子邮件的 "主题" 字段中搜索文本。 此方法使用字符串筛选器来检查字母 T 是否为文本的起始字符 `Subject` 。

 [!INCLUDE[appliesto_olkallapp](../vsto/includes/appliesto-olkallapp-md.md)]

## <a name="example"></a>示例
 [!code-csharp[Trin_OL_SearchFolder#1](../vsto/codesnippet/CSharp/Trin_OL_SearchFolder/thisaddin.cs#1)]

## <a name="see-also"></a>另请参阅
- [使用文件夹](../vsto/working-with-folders.md)
- [Outlook 对象模型概述](../vsto/outlook-object-model-overview.md)
- [如何：以编程方式按名称检索文件夹](../vsto/how-to-programmatically-retrieve-a-folder-by-name.md)
