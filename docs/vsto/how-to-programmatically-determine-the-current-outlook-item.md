---
title: 如何：以编程方式确定当前 Outlook 项
description: 了解如何以编程方式确定当前的 Microsoft Outlook 项。 此示例使用 SelectionChange 事件。
ms.custom: SEO-VS-2020
titleSuffix: ''
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- mail items [Office development in Visual Studio], current
- e-mail [Office development in Visual Studio], current item
- SelectionChange event
- Outlook [Office development in Visual Studio], current item
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.technology: office-development
ms.workload:
- office
ms.openlocfilehash: 9d2f6ba1230ce306f742468d96c47dfdcf17b8d5
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122083226"
---
# <a name="how-to-programmatically-determine-the-current-outlook-item"></a>如何：以编程方式确定当前 Outlook 项
  此示例使用 `Explorer.SelectionChange` 事件显示当前文件夹的名称和有关选定项的某些信息。 然后，该代码显示选定的项。

 [!INCLUDE[appliesto_olkallapp](../vsto/includes/appliesto-olkallapp-md.md)]

## <a name="example"></a>示例
 :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_OL_CurrentItem/thisaddin.vb" id="Snippet1":::
 :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_OL_CurrentItem/thisaddin.cs" id="Snippet1":::

## <a name="compile-the-code"></a>编译代码
 此示例需要：

- Microsoft Office Outlook 中的约会、联系人和电子邮件项。

## <a name="see-also"></a>请参阅
- [Outlook 对象模型概述](../vsto/outlook-object-model-overview.md)
- [如何：以编程方式按名称检索文件夹](../vsto/how-to-programmatically-retrieve-a-folder-by-name.md)
- [如何：以编程方式搜索特定联系人](../vsto/how-to-programmatically-search-for-a-specific-contact.md)
