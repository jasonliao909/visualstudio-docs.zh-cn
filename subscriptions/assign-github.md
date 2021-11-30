---
title: 分配带有 GitHub Enterprise 的 Visual Studio 订阅 | Microsoft Docs
author: evanwindom
ms.author: amast
manager: shve
ms.assetid: f271d623-dcde-442a-865c-4dca5ad8a9c5
ms.date: 03/03/2021
ms.topic: conceptual
description: 管理带有 GitHub Enterprise 的 Visual Studio 订阅中的订阅
ms.openlocfilehash: 912ff9c3cbfbbed24d3fed3c8a2767fda0608c83
ms.sourcegitcommit: 28168514c0c9472e852de35cceb4f95837669da6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/30/2021
ms.locfileid: "133257695"
---
# <a name="manage-visual-studio-subscriptions-with-github-enterprise"></a>管理带有 GitHub Enterprise 的 Visual Studio 订阅
与 Microsoft 签订了企业协议 (EA) 的客户有资格购买新的订阅套餐，该套餐将 Visual Studio 标准订阅和 GitHub Enterprise 结合在了一起。 这是 Visual Studio 订阅者获取 GitHub Enterprise 的一种简单而实惠的方式。 

当你的组织购买带有 GitHub Enterprise 的 Visual Studio 订阅时，这些订阅将按两部分进行预配和管理。

## <a name="manage-visual-studio-subscriptions"></a>管理 Visual Studio 订阅
当你的组织购买带有 GitHub Enterprise 的 Visual Studio 订阅时，订阅中的 Visual Studio 部分将立即预配，且可在 Visual Studio [订阅管理](https://manage.visualstudio.com)门户中分配和管理这些订阅。 分配带有 GitHub Enterprise 的 Visual Studio 订阅后，订阅者将收到一封电子邮件，告知他们可以在 <https://my.visualstudio.com/subscriptions> 访问 Visual Studio 订阅。

要详细了解如何管理 Visual Studio 订阅，请查看以下主题：
- [使用管理门户](using-admin-portal.md)
- [分配订阅](assign-license.md)
- [编辑订阅](edit-license.md)
- [删除订阅](delete-license.md)
- [过度分配](handle-overclaimed-license.md)

> [!Important]
> 如果 Visual Studio 订阅管理员在没有先购买的情况下分配带有 GitHub Enterprise 的 Visual Studio 订阅，则不会通知 GitHub 你要创建 GitHub Enterprise 帐户。  在分配订阅之前，应购买至少一个带有 GitHub Enterprise 的 Visual Studio 订阅。

## <a name="moving-to-visual-studio-with-github-enterprise"></a>移动到带有 GitHub Enterprise 的 Visual Studio
</br>

> [!VIDEO https://www.microsoft.com/videoplayer/embed/RWEAsv]

如果你的组织在分配了标准 Visual Studio Enterprise 和 Visual Studio Professional 订阅后，购买了带有 GitHub Enterprise 捆绑包的 Visual Studio 订阅，则管理门户将包含一项功能，可帮助你将现有订阅者移动到相应的带有 GitHub Enterprise 的 Visual Studio Enterprise 和/或带有 GitHub Enterprise 订阅的 Visual Studio Professional。  例如，带有 Visual Studio Professional 订阅的订阅者将移至带有 GitHub Enterprise 订阅的 Visual Studio Professional。 在左侧栏的“概述”面板中，你将看到以下图块：

   > [!div class="mx-imgBorder"]
   > ![“立即移动”按钮](_img/assign-github/move-now.png "单击“立即移动”将订阅升级到带有 GitHub Enterprise 订阅的 Visual Studio")

> [!IMPORTANT]
> 如上所述，现有的订阅者数据、历史记录和订阅 ID 将得以保留，并且他们激活的任何权益都不会因本次移动而中断。  


单击“立即移动”按钮时，浮出面板将为你提供有关移动 Enterprise 和/或 Professional 订阅的建议：

   > [!div class="mx-imgBorder"]
   > ![浮出面板](_img/assign-github/fly-out.png)

在此图块中，你可以查看受影响的订阅者，并指定是否希望在移动完成后通知他们接收电子邮件通知。  此电子邮件通知订阅者，他们的权益保持不变，并鼓励他们开始在 GitHub 中建立存在感。  

单击“移动订阅者”按钮，你可以移动所有推荐的订阅者，或者从列表中选择个人。 ****    确认选择后，需要几秒钟才能完成订阅移动。 如果适用，你需要分别为 Professional 和 Enterprise 执行这些步骤。  

## <a name="what-is-the-visual-studio-with-github-enterprise-setup-process"></a>带有 GitHub Enterprise 的 Visual Studio 的设置过程是怎样的？
GitHub Enterprise 的设置和管理独立于 Visual Studio 订阅。 购买带有 GitHub Enterprise 的 Visual Studio 订阅后，与在 [manage.visualstudio.com](https://manage.visualstudio.com) 中建立协议的同时（但独立于此），GitHub Enterprise 帐户设置过程将会启动。 建立此 GitHub Enterprise 帐户可能需要一些时间。 

你的公司设置了 GitHub Enterprise 帐户后，已被分配了带有 GitHub Enterprise 的 Visual Studio 订阅的订阅者将收到来自 GitHub 的一封电子邮件，通知他们其 Visual Studio 订阅已链接。 订阅者收到此电子邮件后，他们可以联系其 GitHub 组织管理员，以收到相应组织的邀请。

有关 GitHub Enterprise 设置的详细信息，请参阅[订阅者文档](access-github.md)。   

## <a name="manage-github-enterprise-subscriptions"></a>管理 GitHub Enterprise 订阅
购买 GitHub Enterprise 订阅时，GitHub 会与客户合作，帮助他们创建和配置将访问 GitHub 和确定管理员的组织。  这些管理员之后会收到一则通知，其中指出已将其设置为管理员。  

这个过程更复杂，因此在购买订阅后，可能需要数天时间才能完全设置好组织和管理员。

GitHub 可作为基于云的 GitHub.com 提供，也可提供为本地 GitHub Enterprise Server。  这两种版本的管理过程有所不同。  GitHub 提供了各种帮助主题和管理员指南来帮助你管理 GitHub Enterprise 订阅。  我们提供了下述精选主题的链接。  

## <a name="support-resources"></a>支持资源
- 访问 [GitHub 文档](https://docs.github.com/en/enterprise-cloud@latest/billing/managing-licenses-for-visual-studio-subscriptions-with-github-enterprise/about-visual-studio-subscriptions-with-github-enterprise)，了解有关 GitHub 分配的详细信息
- 有关各种 GitHub 主题的问题解答，请查看 [GitHub 帮助](https://help.github.com/en)。
- 在 [GitHub 社区论坛](https://github.community/)获取其他 GitHub 用户的帮助。
- 如需有关管理 Visual Studio 订阅的帮助，请联系 [Visual studio 订阅支持](https://aka.ms/vsadminhelp)。
- 对有关 Visual Studio IDE、Azure DevOps Services 或其他 Visual Studio 产品或服务有疑问？  请访问 [Visual Studio 支持](https://visualstudio.microsoft.com/support/)。
- 获取 GitHub Enterprise 的[技术支持](https://support.microsoft.com/supportforbusiness/productselection?sapId=b77fe80f-5417-80bd-4b2a-275cf0018c24)。   

## <a name="see-also"></a>请参阅
- [Visual Studio 文档](/visualstudio/)
- [Azure DevOps 文档](/azure/devops/)
- [Azure 文档](/azure/)
- [Microsoft 365 文档](/microsoft-365/)

## <a name="next-steps"></a>后续步骤
了解有关管理 Visual Studio 订阅的详细信息。
- [分配单个订阅](assign-license.md)
- [分配多个订阅](assign-license-bulk.md)
- [编辑订阅](edit-license.md)
- [删除订阅](delete-license.md)
- [确定最大使用量](maximum-usage.md)

要详细了解如何管理带 GitHub Enterprise 的 Visual Studio 订阅，请查看 Visual Studio [订阅管理门户](https://visualstudio.microsoft.com/subscriptions-administration/)。
