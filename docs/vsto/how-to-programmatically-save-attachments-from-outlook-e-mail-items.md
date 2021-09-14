---
title: 以编程方式Outlook电子邮件项中的附件
description: 了解如何使用电子邮件Visual Studio以编程方式保存 Microsoft 电子邮件Outlook附件。
ms.custom: SEO-VS-2020
titleSuffix: ''
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- CSharp
helpviewer_keywords:
- Outlook [Office development in Visual Studio], attachments
- e-mail [Office development in Visual Studio], attachments
- saving e-mail attachments
- mail items [Office development in Visual Studio], attachments
- attachments [Office development in Visual Studio]
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.technology: office-development
ms.workload:
- office
ms.openlocfilehash: e635d1ddba2d7032820fee6e5979b402b2d38360
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126664717"
---
# <a name="how-to-programmatically-save-attachments-from-outlook-email-items"></a>如何：以编程方式从电子邮件Outlook附件

此示例会在收件箱接收到电子邮件时将邮件中的附件保存到指定的文件夹中。

> [!IMPORTANT]
> 只有在 C 目录的根目录中添加名为 **TestFileSave** 的文件夹时，此示例才有效。

[!INCLUDE[appliesto_olkallapp](../vsto/includes/appliesto-olkallapp-md.md)]

## <a name="example"></a>示例

:::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_OL_SaveAttachments/thisaddin.cs" id="Snippet1":::

## <a name="see-also"></a>另请参阅

- [使用邮件项](../vsto/working-with-mail-items.md)
- [如何：以编程方式按名称检索文件夹](../vsto/how-to-programmatically-retrieve-a-folder-by-name.md)
- [如何：收到电子邮件时以编程方式执行的操作](../vsto/how-to-programmatically-perform-actions-when-an-e-mail-message-is-received.md)
- [如何：以编程方式搜索特定文件夹](../vsto/how-to-programmatically-search-within-a-specific-folder.md)
