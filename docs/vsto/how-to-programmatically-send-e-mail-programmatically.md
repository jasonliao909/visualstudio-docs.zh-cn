---
title: 如何：以编程方式发送电子邮件
description: 使用 Visual Studio 以编程方式从 Microsoft Outlook。 此示例向域名为 example.com 的联系人发送电子邮件。
ms.custom: SEO-VS-2020
ms.date: 08/14/2019
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- mail items [Office development in Visual Studio], sending e-mail
- Outlook [Office development in Visual Studio], creating e-mail
- Outlook [Office development in Visual Studio], sending e-mail
- e-mail [Office development in Visual Studio], sending
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.technology: office-development
ms.workload:
- office
ms.openlocfilehash: c1a8f2fb5843ccb39808250ef847e8e5b4355960
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122115234"
---
# <a name="how-to-programmatically-send-email"></a>如何：以编程方式发送电子邮件
  此示例向电子邮件地址中具有域名的联系人 example.com **发送电子邮件。**

 [!INCLUDE[appliesto_olkallapp](../vsto/includes/appliesto-olkallapp-md.md)]

[!include[Add-ins note](includes/addinsnote.md)]

## <a name="example"></a>示例
 :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_OL_ProgramEMail/thisaddin.cs" id="Snippet1":::

## <a name="compile-the-code"></a>编译代码
 此示例需要：

- 具有域名的联系人 **example.com** 电子邮件地址中。

## <a name="robust-programming"></a>可靠编程
 不要删除在 中搜索域名的 **example.com。** 如果删除筛选器，解决方案会向所有联系人发送电子邮件。

## <a name="see-also"></a>请参阅
- [使用邮件项](../vsto/working-with-mail-items.md)
- [如何：以编程方式创建电子邮件项](../vsto/how-to-programmatically-create-an-e-mail-item.md)
- [如何：以编程方式Outlook联系人](../vsto/how-to-programmatically-access-outlook-contacts.md)
- [如何：收到电子邮件时以编程方式执行的操作](../vsto/how-to-programmatically-perform-actions-when-an-e-mail-message-is-received.md)
