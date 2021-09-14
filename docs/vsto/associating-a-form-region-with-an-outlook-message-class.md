---
title: 将窗体区域与Outlook类关联
description: 了解如何通过将窗体区域Microsoft Office Outlook项的消息类来指定哪些项显示窗体区域。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: conceptual
f1_keywords:
- VSTO.NewFormRegionWizard.InvalidMessageClassName
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- FormRegionMessageClassAttribute
- form regions [Office development in Visual Studio], message classes
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.technology: office-development
ms.workload:
- office
ms.openlocfilehash: f38640840b929b4044ca37d6571c82289f32b55f
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126665260"
---
# <a name="associate-a-form-region-with-an-outlook-message-class"></a>将窗体区域与Outlook类关联
  通过将窗体区域与Microsoft Office Outlook的消息类相关联，可以指定哪些项显示窗体区域。 例如，如果要将窗体区域追加到邮件项的底部，可以将窗体区域与邮件 `IPM.Note` 类关联。

 若要将窗体区域与消息类关联，请指定"新建窗体Outlook中的消息类名称，**或** 将属性应用于窗体区域工厂类。

 [!INCLUDE[appliesto_olkallapp](../vsto/includes/appliesto-olkallapp-md.md)]

## <a name="understand-outlook-message-classes"></a>了解Outlook类
 一Outlook消息类标识项Outlook类型。 下表列出了这八种标准类型的项及其消息类名称。

|Outlook项类型|消息类名称|
|-----------------------|------------------------|
|AppointmentItem|`IPM.Appointment`|
|ContactItem|`IPM.Contact`|
|DistListItem|`IPM.DistList`|
|JournalItem|`IPM.Activity`|
|MailItem|`IPM.Note`|
|PostItem|`IPM.Post` 或 `IPM.Post.RSS`|
| TaskItem|`IPM.Task`|

 还可以指定自定义消息类的名称。 自定义消息类标识在自定义窗体中定义的自定义Outlook。

> [!NOTE]
> 对于替换和全部替换窗体区域，可以指定新的自定义消息类名称。 无需使用现有自定义窗体的消息类名称。 自定义消息类的名称必须唯一。 确保名称唯一的一种方式是使用类似于以下内容的命名约定 \<*StandardMessageClassName*> \<*Company*> ：。\<*MessageClassName*>  (例如 `IPM.Note.Contoso.MyMessageClass` ：) 。

## <a name="associate-a-form-region-with-an-outlook-message-class"></a>将窗体区域与Outlook类关联
 有两种方法可以将窗体区域与消息类关联：

- 使用"**新建Outlook窗体区域"** 向导。

- 应用类特性。

### <a name="use-the-new-outlook-form-region-wizard"></a>使用"新建Outlook窗体区域"向导
 在"新建窗体 **Outlook"** 向导的最后一页上，可以选择标准消息类，并键入要与窗体区域关联的自定义消息类的名称。

 如果窗体区域旨在替换整个窗体或窗体的默认页，则标准消息类不可用。 只能为向窗体添加新页或追加到窗体底部的窗体指定标准消息类名称。 有关详细信息，请参阅[如何：将窗体区域添加到Outlook外接程序项目](../vsto/how-to-add-a-form-region-to-an-outlook-add-in-project.md)。

 若要包括一个或多个自定义消息类，请键入它们的名称，在"哪些自定义消息类 **将显示此窗体区域？"** 框中。

 键入的名称必须符合以下准则：

- 使用完全限定的消息类名称 (例如："IPM.注意.Contoso") 。

- 使用分号分隔多个消息类名称。

- 不要包括标准Outlook消息类，例如"IPM.注意"或"IPM.联系人"。 仅包括自定义消息类，例如"IPM"。注意.Contoso"。

- 请勿指定基消息类本身， (例如："IPM") 。

- 每条消息类名称不超过 256 个字符。

  单击 **"Outlook"** 时，"新建窗体区域"向导将验证输入 **的格式**。

> [!NOTE]
> "**新建Outlook** 窗体区域"向导不会验证你提供的消息类名称是否正确或有效。

 完成向导后，"新建Outlook **窗体** 区域向导将属性应用于包含指定消息类名称的窗体区域类。 还可以手动应用这些属性。

### <a name="apply-class-attributes"></a>应用类特性
 完成"新建窗体区域"Outlook后，可以将窗体区域与Outlook **类** 关联。 为此，将属性应用于窗体区域工厂类。

 以下示例显示了已应用于名为 的窗体区域 <xref:Microsoft.Office.Tools.Outlook.FormRegionMessageClassAttribute> 工厂类的两个属性 `myFormRegion` 。 第一个属性将窗体区域与邮件窗体的标准邮件类关联。 第二个属性将窗体区域与名为 的自定义消息类关联 `IPM.Task.Contoso` 。

 :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_Outlook_FR_Attributes/FormRegion1.vb" id="Snippet1":::
 :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_Outlook_FR_Attributes/FormRegion1.cs" id="Snippet1":::

 属性必须符合以下准则：

- 对于自定义消息类，请使用完全限定的消息类名称 (例如："IPM。注意.Contoso") 。

- 请勿指定基消息类本身， (例如："IPM") 。

- 每条消息类名称不超过 256 个字符。

- 如果窗体区域替换整个窗体或窗体的默认页，则不要包含标准消息类的名称。 只能为向窗体添加新页或追加到窗体底部的窗体指定标准消息类名称。 有关详细信息，请参阅[如何：将窗体区域添加到Outlook外接程序项目](../vsto/how-to-add-a-form-region-to-an-outlook-add-in-project.md)。

  Visual Studio生成项目时验证消息类名称的格式。

> [!NOTE]
> Visual Studio不会验证你提供的消息类名称是否正确或有效。

## <a name="see-also"></a>另请参阅
- [运行时访问窗体区域](../vsto/accessing-a-form-region-at-run-time.md)
- [创建Outlook窗体区域](../vsto/creating-outlook-form-regions.md)
- [演练：设计Outlook区域](../vsto/walkthrough-designing-an-outlook-form-region.md)
- [创建表单Outlook指南](../vsto/guidelines-for-creating-outlook-form-regions.md)
- [窗体名称和消息类概述](/office/vba/outlook/Concepts/Forms/form-name-and-message-class-overview)
- [表单Outlook项如何协同工作](/office/vba/outlook/Concepts/Forms/how-outlook-forms-and-items-work-together)
