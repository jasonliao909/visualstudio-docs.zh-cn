---
title: 将网页与 Outlook 文件夹关联
description: 了解如何将网页与 Microsoft Office Outlook 文件夹关联。 此示例在 Outlook 中检查名为 HtmlView 的文件夹。
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
ms.openlocfilehash: 5a24e2ca3942d2c122421151a3f9a96b640b2ebb
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122106180"
---
# <a name="associate-a-web-page-with-an-outlook-folder"></a>将网页与 Outlook 文件夹关联

  此示例在 Microsoft Office Outlook 中检查名为的文件夹 `HtmlView` 。 如果该文件夹不存在，则代码会创建该文件夹并向其分配网页。 如果该文件夹存在，则代码将显示文件夹内容。

 [!INCLUDE[appliesto_olkallapp](../vsto/includes/appliesto-olkallapp-md.md)]

## <a name="example"></a>示例
 :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_OL_HTMLFolder/thisaddin.cs" id="Snippet1":::

## <a name="see-also"></a>请参阅
- [使用文件夹](../vsto/working-with-folders.md)
- [如何：以编程方式按名称检索文件夹](../vsto/how-to-programmatically-retrieve-a-folder-by-name.md)
- [如何：以编程方式创建自定义文件夹项](../vsto/how-to-programmatically-create-custom-folder-items.md)
