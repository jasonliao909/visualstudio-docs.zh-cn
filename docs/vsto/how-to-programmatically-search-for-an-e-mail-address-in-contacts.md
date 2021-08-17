---
title: 以编程方式在联系人中查找电子邮件地址
description: 了解如何使用 Visual Studio 以编程方式在 Microsoft Outlook 联系人中查找电子邮件地址。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- e-mail [Office development in Visual Studio], searching
- contacts [Office development in Visual Studio], searching
- searching contacts
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.technology: office-development
ms.workload:
- office
ms.openlocfilehash: ace2fef3a40695ab1165a65dd4a88ae329075b77
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122083097"
---
# <a name="how-to-programmatically-search-for-an-email-address-in-contacts"></a>如何：以编程方式在联系人中搜索电子邮件地址
  以下示例将在联系人文件夹搜索电子邮件地址中具有域名 **example.com** 的联系人。

 [!INCLUDE[appliesto_olkallapp](../vsto/includes/appliesto-olkallapp-md.md)]

## <a name="example"></a>示例
 :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_OL_SearchEmail/thisaddin.cs" id="Snippet1":::

## <a name="compile-the-code"></a>编译代码
 此示例需要：

- 电子邮件地址中具有域名 **example.com** （例如， `somebody@example.com`且具有的名字和姓氏的联系人。

## <a name="see-also"></a>请参阅
- [处理联系人项](../vsto/working-with-contact-items.md)
- [如何：以编程方式发送电子邮件](../vsto/how-to-programmatically-send-e-mail-programmatically.md)
- [如何：以编程方式访问 Outlook 联系人](../vsto/how-to-programmatically-access-outlook-contacts.md)
- [如何：以编程方式将条目添加到 Outlook 联系人](../vsto/how-to-programmatically-add-an-entry-to-outlook-contacts.md)
