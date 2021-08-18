---
title: 如何：以编程方式在 Outlook
description: 了解如何以编程方式在 Microsoft Outlook。 此示例将未读的电子邮件从收件箱移动到名为 Test 的文件夹。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Outlook folders [Office development in Visual Studio], moving items
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.technology: office-development
ms.workload:
- office
ms.openlocfilehash: c6d67712ca09fa99cd1fef00740acfda2fe34cac
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122083175"
---
# <a name="how-to-programmatically-move-items-in-outlook"></a>如何：以编程方式在 Outlook
  此示例将未读的电子邮件从收件箱移动到名为 Test  **的文件夹**。 该示例仅移动字段中包含 **"测试"** 一 `Subject` 词的消息。

 [!INCLUDE[appliesto_olkallapp](../vsto/includes/appliesto-olkallapp-md.md)]

## <a name="example"></a>示例
 :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_OL_MoveItems/thisaddin.cs" id="Snippet1":::

## <a name="compile-the-code"></a>编译代码
 此示例需要：

- 名为 Outlook **邮件文件夹**。

- 在 字段中收到一封包含 **"测试"一** `Subject` 词的电子邮件。

## <a name="see-also"></a>请参阅
- [使用文件夹](../vsto/working-with-folders.md)
- [如何：以编程方式按名称检索文件夹](../vsto/how-to-programmatically-retrieve-a-folder-by-name.md)
- [如何：以编程方式搜索特定文件夹](../vsto/how-to-programmatically-search-within-a-specific-folder.md)
- [如何：收到电子邮件时以编程方式执行的操作](../vsto/how-to-programmatically-perform-actions-when-an-e-mail-message-is-received.md)
