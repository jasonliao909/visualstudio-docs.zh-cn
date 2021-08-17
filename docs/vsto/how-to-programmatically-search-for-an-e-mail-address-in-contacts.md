---
title: 以编程方式在联系人中查找电子邮件地址
description: 了解如何使用 Visual Studio 在 Microsoft 联系人中以编程方式Outlook电子邮件地址。
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
ms.openlocfilehash: afd35041cc035bf5a03db0966cb30bafbcadfbd69fdc09f8f5a4c9219cdf8b89
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121384179"
---
# <a name="how-to-programmatically-search-for-an-email-address-in-contacts"></a>如何：以编程方式搜索联系人中的电子邮件地址
  以下示例将在联系人文件夹搜索电子邮件地址中具有域名 **example.com** 的联系人。

 [!INCLUDE[appliesto_olkallapp](../vsto/includes/appliesto-olkallapp-md.md)]

## <a name="example"></a>示例
 :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_OL_SearchEmail/thisaddin.cs" id="Snippet1":::

## <a name="compile-the-code"></a>编译代码
 此示例需要：

- 电子邮件地址中具有域名 **example.com** （例如， `somebody@example.com`且具有的名字和姓氏的联系人。

## <a name="see-also"></a>请参阅
- [使用联系人项](../vsto/working-with-contact-items.md)
- [如何：以编程方式发送电子邮件](../vsto/how-to-programmatically-send-e-mail-programmatically.md)
- [如何：以编程方式Outlook联系人](../vsto/how-to-programmatically-access-outlook-contacts.md)
- [如何：以编程方式向联系人Outlook条目](../vsto/how-to-programmatically-add-an-entry-to-outlook-contacts.md)
