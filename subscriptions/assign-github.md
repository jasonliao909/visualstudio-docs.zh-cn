---
title: 使用 GitHub Enterprise | 设置Visual Studio订阅Microsoft Docs
author: evanwindom
ms.author: amast
manager: shve
ms.assetid: f271d623-dcde-442a-865c-4dca5ad8a9c5
ms.date: 04/25/2022
ms.topic: conceptual
description: 管理带有 GitHub Enterprise 的 Visual Studio 订阅中的订阅
ms.openlocfilehash: b0f0d3b288ac13fb6875e53b563c7d69026b485b
ms.sourcegitcommit: 9e9f4cf4b34735fffa376b203ccaa74cb705ffe2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2022
ms.locfileid: "144334279"
---
# <a name="set-up-github-enterprise-licenses-with-visual-studio-subscriptions"></a>使用 Visual Studio 订阅设置GitHub Enterprise许可证
与 Microsoft 签订Enterprise协议 (EA) 的客户有资格购买将Visual Studio标准订阅和GitHub Enterprise相结合的订阅产品/服务。 这是 Visual Studio 订阅者获取 GitHub Enterprise 的一种简单而实惠的方式。 

请查看此视频，了解设置组织并邀请新成员的步骤，或按照视频下方的分步说明进行操作。  

> [!VIDEO https://www.microsoft.com/videoplayer/embed/RWVcut]

现在，你已使用 GitHub Enterprise 购买了Visual Studio订阅，接下来让我们设置你的组织。 我们将从新GitHub Enterprise客户的说明开始。 如果你是现有GitHub Enterprise客户，请跳到[向组织成员分配Visual Studio订阅](#assign-visual-studio-subscriptions-to-organization-members)。

> [!IMPORTANT]
> 如果 Visual Studio 订阅管理员在没有先购买的情况下分配带有 GitHub Enterprise 的 Visual Studio 订阅，则不会通知 GitHub 你要创建 GitHub Enterprise 帐户。  在分配订阅之前，应购买至少一个带有 GitHub Enterprise 的 Visual Studio 订阅。  如果已购买Visual Studio GitHub Enterprise订阅，则无需在分配订阅之前等待GitHub设置过程完成。

## <a name="create-your-organization"></a>创建组织
作为新的GitHub Enterprise客户，你和你的团队需要访问你的GitHub Enterprise帐户。 一旦GitHub处理订单，就会使用分配的许可证计数创建一个Enterprise帐户。 此时，你（Enterprise管理员）将添加到帐户，你将收到电子邮件邀请。 

1. 单击此电子邮件中的 **“成为所有者...”** 按钮转到GitHub Enterprise帐户，然后单击“**接受邀请**”。
   > [!div class="mx-imgBorder"]
   > ![接受GitHub邀请](_img/assign-github/become-an-owner.png "单击“成为所有者”按钮，然后选择“接受邀请”")

0. 若要添加用户，需要有一个组织邀请他们加入。 若要创建组织，请选择“ **新建组织** ”按钮。 

0. 输入新组织的名称。  这是显示在该名称上 https://github.com/的名称。  单击“ **创建组织**”。

0. 接下来，将添加应具有组织所有者权限的用户，允许他们添加成员并管理组织级别设置。 请务必在添加组织所有者后单击“ **完成** ”。 现在，新组织已准备好添加成员。

## <a name="assign-visual-studio-subscriptions-to-organization-members"></a>向组织成员分配Visual Studio订阅
在Visual Studio订阅管理门户中，Visual Studio订阅管理员可以向用户分配订阅。 如果你不熟悉Visual Studio订阅管理，则应收到Visual Studio 订阅管理门户的邀请以开始分配订阅。 单击链接以登录到 [管理门户](https://manage.visualstudio.com)后，可以使用 **“添加**”下拉列表单独添加Visual Studio订阅者，或使用Microsoft Excel批量添加或Azure Active Directory组。 只需按照提示添加订阅者，确保使用可以接收电子邮件的电子邮件域并选择包含GitHub Enterprise的订阅级别。

有关分配订阅的详细信息，请参阅我们的文章，具体步骤如下：
- [添加单用户](assign-license.md)
- [添加多个用户](assign-license-bulk.md)

> [!NOTE]
> 如果没有要移动的现有订阅者，仍需邀请订阅者加入GitHub组织。  有关详细信息，请参阅 [邀请订阅者到组织](#invite-subscribers-to-your-organization) 。

## <a name="move-existing-subscribers-to-subscriptions-with-github"></a>使用 GitHub 将现有订阅者移动到订阅
对于从常规Visual Studio订阅续订到具有GitHub Enterprise Visual Studio订阅的用户，需要将订阅者移动到新级别，以便他们有资格使用GitHub。 

1. 选择左侧导航窗格中的 **“概述** ”图标。 
   > [!div class="mx-imgBorder"]
   > ![打开概述](_img/assign-github/overview.png "选择左侧导航窗格中的概述图标。")
0. 选择“ **立即移动** ”，然后按照提示完成转换。 
   > [!div class="mx-imgBorder"]
   > ![将现有订阅者移动到GitHub](_img/assign-github/move-now.png "单击“立即移动”，将现有订阅者迁移到具有GitHub订阅的Visual Studio。")
0. 选择“**立即移动**”按钮时，弹出面板会显示有关移动Enterprise和/或Professional订阅的建议：
   > [!div class="mx-imgBorder"]
   > ![浮出面板](_img/assign-github/fly-out.png)

可以查看受影响的订阅者，并指定是否在移动完成后通知他们接收电子邮件通知。  此电子邮件通知订阅者，他们的权益保持不变，并鼓励他们开始在 GitHub 中建立存在感。  

单击“移动订阅者”按钮，你可以移动所有推荐的订阅者，或者从列表中选择个人。 ****    确认选择后，需要几秒钟才能完成订阅移动。 如果适用，你需要分别为 Professional 和 Enterprise 执行这些步骤。  

## <a name="invite-subscribers-to-your-organization"></a>邀请订阅者加入组织
在Visual Studio订阅管理门户中为订阅分配订阅后，GitHub将更新这些用户，并将这些用户反映为 **挂起成员**。 组织所有者需要邀请这些挂起的成员访问其GitHub Enterprise权益。 

若要将用户添加到组织，请在GitHub：
1. 单击左侧导航窗格中 **的组织** 。
0. 选择要向其添加订阅者的组织。  
   > [!div class="mx-imgBorder"]
   > ![选择组织](_img/assign-github/organizations.png "选择要分配新成员的组织。")
0. 选择“ **人员** ”选项卡。
0. 如果你是组织的所有者，你将看到“ **邀请成员** ”按钮。  选择该文件夹。 
0. 输入用于向新成员分配订阅的电子邮件地址，然后单击“ **邀请**”。
   > [!div class="mx-imgBorder"]
   > ![邀请成员](_img/assign-github/invite-member.png "输入新成员的登录电子邮件地址。")
0. 单击“ **发送邀请**”。  用户现在将显示在挂起的邀请列表中。  
0. 用户收到GitHub邀请后，他们需要单击电子邮件中的按钮，该按钮会将他们带到你的组织，并向其授予成员访问权限。 

> [!IMPORTANT]
> 需要发送新邀请之前，用户邀请有效期为 7 天。 如果你的企业使用企业管理的用户使用企业管理的用户，则可能需要通知用户他们有权访问GitHub。

如有疑问，请联系GitHub或 Microsoft 客户经理。 还可以访问 https://aka.ms/GHEandVSS 以获取详细信息。

## <a name="support-resources"></a>支持资源
+ 访问 [GitHub 文档](https://docs.github.com/en/enterprise-cloud@latest/billing/managing-licenses-for-visual-studio-subscriptions-with-github-enterprise/about-visual-studio-subscriptions-with-github-enterprise)，了解有关 GitHub 分配的详细信息
+ 有关各种 GitHub 主题的问题解答，请查看 [GitHub 帮助](https://help.github.com/en)。
+ 在 [GitHub 社区论坛](https://github.community/)获取其他 GitHub 用户的帮助。
+ 如需有关管理 Visual Studio 订阅的帮助，请联系 [Visual studio 订阅支持](https://aka.ms/vsadminhelp)。
+ 对有关 Visual Studio IDE、Azure DevOps Services 或其他 Visual Studio 产品或服务有疑问？  请访问 [Visual Studio 支持](https://visualstudio.microsoft.com/support/)。
+ 获取 GitHub Enterprise 的[技术支持](https://support.microsoft.com/supportforbusiness/productselection?sapId=b77fe80f-5417-80bd-4b2a-275cf0018c24)。   

## <a name="see-also"></a>请参阅
+ [Visual Studio 文档](/visualstudio/)
+ [Azure DevOps 文档](/azure/devops/)
+ [Azure 文档](/azure/)
+ [Microsoft 365 文档](/microsoft-365/)

## <a name="next-steps"></a>后续步骤
了解有关管理 Visual Studio 订阅的详细信息。
+ [分配单个订阅](assign-license.md)
+ [分配多个订阅](assign-license-bulk.md)
+ [编辑订阅](edit-license.md)
+ [删除订阅](delete-license.md)
+ [确定最大使用量](maximum-usage.md)

要详细了解如何管理带 GitHub Enterprise 的 Visual Studio 订阅，请查看 Visual Studio [订阅管理门户](https://visualstudio.microsoft.com/subscriptions-administration/)。
