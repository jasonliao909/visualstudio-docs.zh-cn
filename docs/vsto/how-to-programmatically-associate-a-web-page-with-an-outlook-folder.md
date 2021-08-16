---
title: 将网页与 Outlook 文件夹关联
description: 了解如何将网页与文件夹Microsoft Office Outlook关联。 此示例检查文件夹中的名为 HtmlView 的文件夹Outlook。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- folders [Office development in Visual Studio], Web pages and
- Outlook [Office development in Visual Studio], Web pages attached to folders
- Web pages [Office development in Visual Studio], Outlook folders
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.technology: office-development
ms.workload:
- office
ms.openlocfilehash: 6fce0a1a6fbe4537e87d88120550bd7a1f7788c07ab84a02f70cb9514c3fac7e
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121394578"
---
# <a name="associate-a-web-page-with-an-outlook-folder"></a>将网页与 Outlook 文件夹关联

  此示例检查中名为 的文件夹 `HtmlView` Microsoft Office Outlook。 如果该文件夹不存在，代码将创建文件夹，并为其分配网页。 如果该文件夹存在，代码将显示文件夹内容。

 [!INCLUDE[appliesto_olkallapp](../vsto/includes/appliesto-olkallapp-md.md)]

## <a name="example"></a>示例
 :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_OL_HTMLFolder/thisaddin.cs" id="Snippet1":::

## <a name="see-also"></a>另请参阅
- [使用文件夹](../vsto/working-with-folders.md)
- [如何：以编程方式按名称检索文件夹](../vsto/how-to-programmatically-retrieve-a-folder-by-name.md)
- [如何：以编程方式创建自定义文件夹项](../vsto/how-to-programmatically-create-custom-folder-items.md)
