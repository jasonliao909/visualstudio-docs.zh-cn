---
title: 如何分配 Visual Studio 订阅？
description: 你可以一次为最终用户分配一个订阅，也可以使用批量添加功能快速轻松地一次性上传…
ms.faqid: group1_3
ms.topic: include
ms.assetid: 59eb35fd-ec94-41ce-b24c-a8a120976bac
author: evanwindom
ms.author: amast
ms.date: 12/03/2020
ms.openlocfilehash: 8b02ecbcdbf59a588a41633b80ae8edfd09283d9
ms.sourcegitcommit: 28168514c0c9472e852de35cceb4f95837669da6
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/30/2021
ms.locfileid: "133255125"
---
## <a name="how-do-i-assign-visual-studio-subscriptions"></a>如何分配 Visual Studio 订阅？

你可以一次为最终用户分配一个订阅，也可以使用批量添加功能快速轻松地一次性上传大量订阅。

要单独分配订阅，请执行以下操作：

1. 选择 [manage.visualstudio.com](https://manage.visualstudio.com) 页面顶部的[“管理订阅者”选项卡](https://manage.visualstudio.com/subscribers)
2. 选择“添加”，然后键入要分配订阅的用户的名称和电子邮件地址。
    1. 如果你的组织使用 Azure Active Directory，则将搜索“名称”字段以查找当前控制器中的人员。 你可以从搜索结果中进行选择，也可以手动添加其他人。
3. 如果你希望订阅者在登录 [Visual Studio 订阅门户](https://my.visualstudio.com/)时可以访问软件下载项，请务必在“下载设置”部分保持启用下载项切换开关。
4. 完成“通信首选项”部分，以便我们知道用什么语言向订阅者发送分配电子邮件。
5. 如果想要添加任何与分配相关的注释，请使用“参考”选项。
6. 选择弹出面板底部的“添加”以完成订阅分配。 你的订阅者将收到一封电子邮件，并且可以立即开始使用各自的 Visual Studio 订阅（订阅者无需激活）。

要批量分配订阅，请执行以下操作：

1. 选择 [manage.visualstudio.com](https://manage.visualstudio.com) 页面顶部的[“管理订阅者”选项卡](https://manage.visualstudio.com/subscribers)。
2. 选择“批量添加”，下载 Excel 模板，然后保存本地副本。
3. 除“参考”字段外，所有字段均为必填项。
    1. 确保所有表单域均不含逗号。
    2. 删除表单域前后的空格。
    3. 确保名字和姓氏两部分之间不含额外空格（例如，用户姓名为“Maggie May”两部分，则应输成“MaggieMay”）。
4. 返回 [manage.visualstudio.com](https://manage.visualstudio.com)，选择“批量添加”，然后上传保存的 Excel 模板副本。
5. 上传成功后，你将看到确认页面，并且订阅者列表中已填充新订阅者。 你的订阅者将收到一封电子邮件，并且可以立即开始使用各自的 Visual Studio 订阅（订阅者无需激活）。

[阅读有关在 Visual Studio 订阅管理员门户中分配订阅的更多信息](https://docs.microsoft.com/visualstudio/subscriptions/assign-license#add-a-single-subscriber)，以详细了解如何快速轻松地分配订阅。  [详细了解](https://docs.microsoft.com/visualstudio/subscriptions/assign-github)如何管理带有 GitHub Enterprise 的 Visual Studio 订阅。 

## <a name="what-is-the-github-enterprise-setup-process"></a>GitHub Enterprise 的设置过程是怎样的？ 

GitHub Enterprise 的设置和管理独立于 Visual Studio 订阅。 购买带有 GitHub Enterprise 的 Visual Studio 订阅后，与在 manage.visualstudio.com 中建立协议的同时（但独立于此），GitHub Enterprise 帐户设置过程将会启动。 建立此 GitHub Enterprise 帐户可能需要一些时间。  

你的公司设置了 GitHub Enterprise 帐户后，已被分配了带有 GitHub Enterprise 的 Visual Studio 订阅的订阅者将收到来自 GitHub 的一封电子邮件，通知他们其 Visual Studio 订阅已链接。 订阅者收到此电子邮件后，他们可以联系其 GitHub 组织管理员，以收到相应组织的邀请。 

[详细了解](https://docs.microsoft.com/visualstudio/subscriptions/assign-github)如何管理带有 GitHub Enterprise 的 Visual Studio 订阅。 有关 GitHub Enterprise 设置过程的更多详细信息，请参阅[订阅者文档](https://docs.microsoft.com/visualstudio/subscriptions/access-github)。 