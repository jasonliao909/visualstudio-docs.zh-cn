---
title: 如何：以编程方式移动 Outlook 中的项
description: 了解如何以编程方式移动 Microsoft Outlook 中的项。 此示例将收件箱中的未读电子邮件移动到名为 Test 的文件夹中。
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
ms.openlocfilehash: 38804ef26d96dc7db8c69742632187c097c89553f7bb314333953f052f93e558
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121394402"
---
# <a name="how-to-programmatically-move-items-in-outlook"></a>如何：以编程方式移动 Outlook 中的项
  此示例将 **收件箱** 中的未读电子邮件移动到名为 **Test** 的文件夹中。 此示例仅移动字段中包含单词 **Test** 的消息 `Subject` 。

 [!INCLUDE[appliesto_olkallapp](../vsto/includes/appliesto-olkallapp-md.md)]

## <a name="example"></a>示例
 :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_OL_MoveItems/thisaddin.cs" id="Snippet1":::

## <a name="compile-the-code"></a>编译代码
 此示例需要：

- 名为 **Test** Outlook 邮件文件夹。

- 一封电子邮件，它在字段中使用字词 **Test** `Subject` 。

## <a name="see-also"></a>另请参阅
- [使用文件夹](../vsto/working-with-folders.md)
- [如何：以编程方式按名称检索文件夹](../vsto/how-to-programmatically-retrieve-a-folder-by-name.md)
- [如何：以编程方式在特定文件夹中搜索](../vsto/how-to-programmatically-search-within-a-specific-folder.md)
- [如何：在收到电子邮件时以编程方式执行操作](../vsto/how-to-programmatically-perform-actions-when-an-e-mail-message-is-received.md)
