---
title: 以编程方式保存 Outlook 电子邮件项的附件
description: 了解如何使用 Visual Studio 以编程方式保存 Microsoft Outlook 电子邮件项的附件。
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
ms.openlocfilehash: 0099f06210dc7164df28a3e3b3f3e3e3ef7cb54865a7ead0585fdccf21d1cf0d
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121394259"
---
# <a name="how-to-programmatically-save-attachments-from-outlook-email-items"></a>如何：以编程方式保存 Outlook 电子邮件项的附件

此示例会在收件箱接收到电子邮件时将邮件中的附件保存到指定的文件夹中。

> [!IMPORTANT]
> 仅当你在 C 目录的根目录中添加一个名为 **TestFileSave** 的文件夹时，此示例才有效。

[!INCLUDE[appliesto_olkallapp](../vsto/includes/appliesto-olkallapp-md.md)]

## <a name="example"></a>示例

:::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_OL_SaveAttachments/thisaddin.cs" id="Snippet1":::

## <a name="see-also"></a>另请参阅

- [使用邮件项](../vsto/working-with-mail-items.md)
- [如何：以编程方式按名称检索文件夹](../vsto/how-to-programmatically-retrieve-a-folder-by-name.md)
- [如何：在收到电子邮件时以编程方式执行操作](../vsto/how-to-programmatically-perform-actions-when-an-e-mail-message-is-received.md)
- [如何：以编程方式在特定文件夹中搜索](../vsto/how-to-programmatically-search-within-a-specific-folder.md)
