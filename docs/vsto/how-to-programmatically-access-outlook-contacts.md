---
title: 如何：以编程方式访问 Outlook 联系人
description: 了解如何以编程方式访问 Outlook 联系人。 此示例查找姓氏中包含指定搜索字符串的所有联系人。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- contacts [Office development in Visual Studio], searching
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.technology: office-development
ms.workload:
- office
ms.openlocfilehash: c6fd5d8adf5709738bda1e470c0657e71752bc15
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122046745"
---
# <a name="how-to-programmatically-access-outlook-contacts"></a>如何：以编程方式访问 Outlook 联系人
  此示例查找姓氏中包含指定搜索字符串的所有联系人。

 [!INCLUDE[appliesto_olkallapp](../vsto/includes/appliesto-olkallapp-md.md)]

## <a name="example"></a>示例
 :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_OL_AccessContacts.trin_ol_accesscontacts/thisaddin.cs" id="Snippet1":::
 :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_OL_AccessContacts/thisaddin.vb" id="Snippet1":::


## <a name="compile-the-code"></a>编译代码
 此示例需要：

- 姓氏中包含字符串 "**Na"** 的联系人 (例如，Tzipi Butnaru) 在 **Contacts** 文件夹中。

## <a name="see-also"></a>请参阅
- [处理联系人项](../vsto/working-with-contact-items.md)
- [如何：以编程方式将条目添加到 Outlook 联系人](../vsto/how-to-programmatically-add-an-entry-to-outlook-contacts.md)
- [如何：以编程方式搜索特定联系人](../vsto/how-to-programmatically-search-for-a-specific-contact.md)
- [如何：以编程方式在联系人中搜索电子邮件地址](../vsto/how-to-programmatically-search-for-an-e-mail-address-in-contacts.md)
- [如何：以编程方式删除 Outlook 联系人](../vsto/how-to-programmatically-delete-outlook-contacts.md)
