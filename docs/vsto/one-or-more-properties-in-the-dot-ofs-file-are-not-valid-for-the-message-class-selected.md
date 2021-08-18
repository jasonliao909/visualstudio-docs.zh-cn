---
title: 邮件类的 .ofs 文件中的属性无效 "
description: 了解如何更正 .ofs 文件中的一个或多个属性对于所选邮件类无效时发生的错误。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: conceptual
f1_keywords:
- VSTO.NewFormRegionWizard.OFSPropertyError
dev_langs:
- VB
- CSharp
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.technology: office-development
ms.workload:
- office
ms.openlocfilehash: 603a0a8aaa25ac8ec203780f9b509613c33f6c3e
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122147813"
---
# <a name="invalid-properties-in-the-ofs-file-for-the-message-class"></a>Message 类的 .ofs 文件中的属性无效

  当您导入在 Outlook 中设计的窗体区域时，.ofs 文件中的一个或多个属性对于所选邮件类无效，但窗体区域中的一个或多个字段与在 "**新建窗体区域**" 向导的最后一页上选择的邮件类不兼容。

例如，你可能在“新建窗体区域”  向导最后一页上选择了“任务(IPM.Task)”  。 如果窗体区域包含 " **业务地址** " 字段，则会收到此错误，因为任务没有企业地址。 因此，" **业务地址** " 字段与 `IPM.Task` 邮件类不兼容。

 你可以选择 " **Task (IPM"。** " **新建窗体区域** " 向导最后一页上的任务) 。 如果窗体区域包含 " **业务地址** " 字段，则会收到此错误，因为任务没有企业地址。 因此，" **业务地址** " 字段与 `IPM.Task` 邮件类不兼容。

## <a name="to-correct-this-error"></a>更正此错误

- 在“新建窗体区域”  向导最后一页上，选择与窗体区域上的字段兼容的邮件类。

- 在 Outlook 的窗体设计器中，删除与消息类不兼容的字段。 删除你计划在 " **新建窗体区域** " 向导的最后一页上选择的字段。

## <a name="see-also"></a>请参阅
- [演练：导入在 Outlook 中设计的窗体区域](../vsto/walkthrough-importing-a-form-region-that-is-designed-in-outlook.md)
