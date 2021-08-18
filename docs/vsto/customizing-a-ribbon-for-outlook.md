---
title: 自定义功能区Outlook
description: 了解在应用程序中自定义功能Microsoft Office Outlook时，必须考虑自定义功能区在应用程序中的显示位置。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Inspectors [Office development in Visual Studio]
- Outlook [Office development in Visual Studio], Ribbon
- customizing the Ribbon, about customizing the Ribbon
- custom Ribbon, about customizing the Ribbon
- Ribbon [Office development in Visual Studio], Outlook
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.technology: office-development
ms.workload:
- office
ms.openlocfilehash: 3c3b200a63ed17afbf4068475ae1509f1bf0da80
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122047096"
---
# <a name="customize-a-ribbon-for-outlook"></a>自定义用于自定义Outlook
  在 Microsoft Office Outlook 中自定义功能区时，必须考虑自定义功能区在应用程序中出现的位置。 在主应用程序用户界面 (UI) 和用户执行某些任务（例如创建电子邮件消息）时打开的窗口中，Outlook 会显示功能区。 这些应用程序窗口被命名为检查器。

 [!INCLUDE[appliesto_olkallapp](../vsto/includes/appliesto-olkallapp-md.md)]

## <a name="add-a-custom-ribbon-to-the-main-application-ui"></a>将自定义功能区添加到主应用程序 UI
 主应用程序 UI 在 Outlook 中被称为资源管理器。 如果使用功能 **区 (可视化** 设计器) 项，可以通过单击"属性"窗口中功能区的功能区 **"RibbonType"** 属性，然后选择 **"Microsoft.Outlook"向资源管理器添加功能区。资源管理器**。

## <a name="assign-a-ribbon-to-an-inspector"></a>向检查器分配功能区
 通过指定与该检查器 message 类相对应的功能区类型来确定要进行自定义的检查器。

 如果使用"功能 **区 (可视化设计器)** 项，请在"属性"窗口中单击功能区的 **RibbonType** 属性，然后从值列表中选择一个或多个功能区标识。

 可以向项目添加多个功能区。 如果多个功能区共享一个功能区 ID，请重写项目的 `ThisAddin` 类中的 `CreateRibbonExtensibilityObject` 方法，以指定要在运行时显示的功能区。 有关详细信息，请参阅功能 [区概述](../vsto/ribbon-overview.md)。 有关每种功能区类型的信息，请参阅技术文章自定义[2007 Outlook功能区](/previous-versions/office/developer/office-2007/bb226712(v=office.12))。

## <a name="specify-the-ribbon-type-by-using-ribbon-xml"></a>使用功能区 XML 指定功能区类型
 如果使用 Ribbon (**XML)** 项，请检查 方法中 *ribbonID* 参数 <xref:Microsoft.Office.Core.IRibbonExtensibility.GetCustomUI%2A> 的值，并返回相应的功能区。

 <xref:Microsoft.Office.Core.IRibbonExtensibility.GetCustomUI%2A> 方法由 Visual Studio 在功能区代码文件中自动生成。 *ribbonID* 参数是标识资源管理器或特定检查器类型的字符串。 有关 *ribbonID* 参数的可能值的完整列表，请参阅技术文章自定义 [2007 Outlook功能区](/previous-versions/office/developer/office-2007/bb226712(v=office.12))。

 以下代码示例演示如何仅在 `Microsoft.Outlook.Mail.Compose` 检查器中显示自定义功能区。 这是用户创建新的电子邮件时将打开的检查器。 在 方法中指定要显示的功能 `GetResourceText()` 区，该方法是在 **功能** 区类中生成的。 有关功能区类 **的信息** ，请参阅 [功能区 XML](../vsto/ribbon-xml.md)。

 :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_RibbonOutlookBasic/Ribbon1.cs" id="Snippet1":::
 :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_RibbonOutlookBasic/Ribbon1.vb" id="Snippet1":::

## <a name="see-also"></a>请参阅
- [运行时访问功能区](../vsto/accessing-the-ribbon-at-run-time.md)
- [功能区概述](../vsto/ribbon-overview.md)
- [功能区设计器](../vsto/ribbon-designer.md)
- [Ribbon XML](../vsto/ribbon-xml.md)
