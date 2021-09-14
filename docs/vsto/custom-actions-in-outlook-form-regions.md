---
title: 窗体Outlook中的自定义操作
description: 了解操作显示按钮（如"全部答复"和"全部答复"）如何使用户能够响应Microsoft Office Outlook项。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- form regions [Office development in Visual Studio], custom actions
- custom actions [Office development in Visual Studio]
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.technology: office-development
ms.workload:
- office
ms.openlocfilehash: 75fcc83dc06a9503b5ab1571315dc95028734446
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126664758"
---
# <a name="custom-actions-in-outlook-form-regions"></a>窗体Outlook中的自定义操作
  操作显示按钮，使用户能够响应Microsoft Office Outlook项。 例如，若要响应邮件项，用户单击"回复"、"**全部** 答复"或"**转发"** 操作按钮。 每个操作都创建新的邮件项，并使用原始项的信息填充该项的字段。

 可以创建自定义操作，以打开任何类型的Outlook项。 例如，可以添加打开新约会或任务项的自定义操作。 设置自定义操作的属性或使用自定义代码填充新项的字段。 自定义操作 **显示在"自定义** 操作"下拉列表中，该项在"自定义检查器"窗口中Outlook打开。

 [!INCLUDE[appliesto_olkallapp](../vsto/includes/appliesto-olkallapp-md.md)]

## <a name="add-custom-actions-to-a-form-region"></a>将自定义操作添加到窗体区域
 若要将自定义操作添加到窗体区域，请使用 " **自定义操作** " 对话框。 可以通过选择 解决方案资源管理器中的"窗体区域 **"，** 展开"属性"窗口中的"清单"节点，选择 **"CustomActions"** 属性，然后单击省略号按钮" (ASP.NET 移动设计器省略号 ![) "](../sharepoint/media/mwellipsis.gif "ASP.NET 移动设计器中的省略号")来打开"自定义操作"对话框。 

 可以使用 " **自定义操作** " 对话框指定 *目标窗体*。 目标窗体是用户执行自定义操作时出现的窗体。

 还可使用" **自定义操作** "对话框指定希望原始项的信息在目标窗体中的显示方式。

 下表描述了"自定义操作"对话框中 **可用的** 属性。

|Property|说明|
|--------------|-----------------|
|**AddressLike**|指定目标窗体的寻址方式。|
|**正文**|指定如何将原始项的正文追加到目标窗体。|
|**已启用**|指示是否启用自定义操作。 如果此属性设置为 **false，** 则禁用自定义操作。|
|**方法**|指定执行自定义操作时可用的响应类型。 自定义操作可以发送窗体、打开窗体或提示用户是否要发送或打开窗体。|
|**名称**|指定可用于在代码中引用此自定义操作的内部名称。|
|**ShowOnRibbon**|指示是否在原始项的功能区上显示自定义操作。|
|**SubjectPrefix**|指定在目标窗体的主题行的开始位置插入的文本。|
|**TargetForm**|指定目标窗体的消息类名称。 例如，键入 **IPM。打开** 任务窗体的任务。|
|**标题**|指定自定义操作按钮的标签。|

## <a name="customize-a-custom-action-at-run-time"></a>运行时自定义自定义操作
 还可使用代码将行为添加到自定义操作。 例如，可以添加采用电子邮件收件人姓名的代码，并将这些姓名作为参与者添加到新的约会项中。 为此，请处理 [MailItem](/office/vba/api/Outlook.MailItem.CustomAction) 对象的 [CustomAction 事件](/office/vba/api/Outlook.MailItem)。

## <a name="see-also"></a>另请参阅
- [创建Outlook窗体区域](../vsto/creating-outlook-form-regions.md)
- [演练：设计Outlook区域](../vsto/walkthrough-designing-an-outlook-form-region.md)
- [将窗体区域与Outlook类关联](../vsto/associating-a-form-region-with-an-outlook-message-class.md)
