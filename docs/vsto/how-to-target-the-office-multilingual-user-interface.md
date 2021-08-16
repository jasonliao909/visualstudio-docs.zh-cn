---
title: 如何：面向 Office 多语言用户界面
description: 了解如何使用 Visual Studio 以编程方式面向 Microsoft Office 多语言用户界面。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- globalization [Office development in Visual Studio], user interface targeting
- MUI [Office development in Visual Studio]
- Office applications [Office development in Visual Studio], localization
- Multilingual User Interface [Office development in Visual Studio]
- localization [Office development in Visual Studio], user interface targeting
- Office applications [Office development in Visual Studio], globalization
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.technology: office-development
ms.workload:
- office
ms.openlocfilehash: ac56fece4197aee23b4e7ac03f14df4b9da634f8ce82609fa71eae5a4f40be6b
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121394181"
---
# <a name="how-to-target-the-office-multilingual-user-interface"></a>如何：面向 Office 多语言用户界面
  多语言用户界面 (MUI) 是一项 Microsoft Office 功能，使最终用户能够更改 (UI) 的用户界面语言。 例如，使用英语 UI 的最终用户可将 UI 的语言更改为西班牙语。

 [!INCLUDE[appliesto_all](../vsto/includes/appliesto-all-md.md)]

 如果你的应用程序将由使用多种 Office 语言的人员使用，则可以添加代码，以自动更改用户计算机上 Office 使用的语言， (如果用户已安装正确的资源) 。

## <a name="to-check-the-current-office-ui-setting"></a>检查当前 Office UI 设置

1. 使用 <xref:System.Threading.Thread.CurrentUICulture%2A> 当前线程的属性。 设置您的 UI 字符串的语言以与当前在用户计算机上运行的 Office 版本所使用的语言相匹配。

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreCreatingExcelVB/Sheet1.vb" id="Snippet10":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreCreatingExcelCS/Sheet1.cs" id="Snippet10":::

## <a name="see-also"></a>请参阅
- [如何：通过主互操作程序集面向 Office 应用程序](../vsto/how-to-target-office-applications-through-primary-interop-assemblies.md)
- [Office 解决方案中的后期绑定](../vsto/late-binding-in-office-solutions.md)
