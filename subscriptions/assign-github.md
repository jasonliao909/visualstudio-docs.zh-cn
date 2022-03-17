---
title: 使用 Visual Studio 设置GitHub Enterprise |Microsoft Docs
author: evanwindom
ms.author: amast
manager: shve
ms.assetid: f271d623-dcde-442a-865c-4dca5ad8a9c5
ms.date: 03/10/2022
ms.topic: conceptual
description: 管理带有 GitHub Enterprise 的 Visual Studio 订阅中的订阅
ms.openlocfilehash: 954e9f26d65d18e6f540fc3737434225eea0992a
ms.sourcegitcommit: 0bb6b0f1023cf20c39f7d0f9888ec71b82b80448
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/16/2022
ms.locfileid: "140652759"
---
# <a name="set-up-github-enterprise-licenses-with-visual-studio-subscriptions"></a>使用 GitHub Enterprise 订阅设置Visual Studio许可证
与 Microsoft Enterprise EA (协议) 客户有资格购买将标准订阅和Visual Studio结合起来的订阅GitHub Enterprise。 这是 Visual Studio 订阅者获取 GitHub Enterprise 的一种简单而实惠的方式。 

请查看此视频，了解设置组织并邀请新成员的步骤，或按照视频下面的分步说明进行操作。  

> [!VIDEO https://www.microsoft.com/videoplayer/embed/RWVcut]

现在，你已Visual Studio订阅GitHub Enterprise，让我们设置你的组织。 首先，我们将针对新客户GitHub Enterprise说明。 如果你是现有客户，请GitHub Enterprise[向组织成员](#assign-visual-studio-subscriptions-to-organization-members)分配Visual Studio订阅。

> [!IMPORTANT]
> 如果 Visual Studio 订阅管理员在没有先购买的情况下分配带有 GitHub Enterprise 的 Visual Studio 订阅，则不会通知 GitHub 你要创建 GitHub Enterprise 帐户。  在分配订阅之前，应购买至少一个带有 GitHub Enterprise 的 Visual Studio 订阅。  如果已Visual Studio订阅GitHub Enterprise订阅，则不需要在分配订阅之前等待GitHub安装过程完成。

## <a name="create-your-organization"></a>创建组织
作为新的GitHub Enterprise客户，你和团队需要获取对 GitHub Enterprise 帐户的访问权限。 一旦GitHub订单，就会创建一Enterprise分配的许可证计数的帐户。 此时，你（Enterprise管理员）将添加到帐户，你将收到电子邮件邀请。 

1. 单击此 **电子邮件中的"成为所有者...**"按钮，转到GitHub Enterprise帐户，然后单击"接受 **邀请"**。
   > [!div class="mx-imgBorder"]
   > ![接受GitHub邀请](_img/assign-github/become-an-owner.png "单击&quot;成为所有者&quot;按钮，然后选择&quot;接受邀请&quot;")

0. 若要添加用户，需要组织邀请他们加入。 若要创建组织，请选择" **新建组织"** 按钮。 

0. 输入新组织的名称。  这将是 上显示的名称 https://github.com/。  单击" **创建组织"**。

0. 接下来，你将添加应具有组织所有者权限的用户，以允许他们添加成员和管理组织级别设置。 添加完"组织所有者 **"** 后，请务必单击"完成"。 现在，新组织已准备好添加成员。

## <a name="assign-visual-studio-subscriptions-to-organization-members"></a>将Visual Studio分配给组织成员
在 Visual Studio 订阅管理门户中，Visual Studio订阅管理员可以将订阅分配给用户。 如果对订阅管理Visual Studio，应已收到订阅管理门户Visual Studio 订阅开始分配订阅的邀请。 单击该链接以登录到管理门户后，[](https://manage.visualstudio.com)可以使用"添加"下拉列表单独添加 Visual Studio 订阅者，或者使用 Microsoft Excel 或 Azure Active Directory 组批量添加订阅者。 只需按照提示添加订阅者，确保使用可接收电子邮件的电子邮件域，并选择包含订阅GitHub Enterprise。

有关分配订阅的信息，请参阅包含以下特定步骤的文章：
- [添加单用户](assign-license.md)
- [添加多个用户](assign-license-bulk.md)

> [!NOTE]
> 如果没有要移动的现有订阅者，你仍然需要邀请订阅者加入GitHub组织。  有关详细信息 [，请参阅邀请订阅者](#invite-subscribers-to-your-organization) 加入组织。

## <a name="move-existing-subscribers-to-subscriptions-with-github"></a>将现有订阅者移到具有订阅GitHub
对于从常规 Visual Studio 订阅续订到具有 GitHub Enterprise 的 Visual Studio 订阅的用户，需要将订阅者移到新级别，以便他们有资格使用 GitHub。 

1. 选择左侧 **导航** 窗格中的"概述"图标。 
   > [!div class="mx-imgBorder"]
   > ![打开概述](_img/assign-github/overview.png "选择左侧导航窗格中的概述图标。")
0. 选择 **"立即移动** "，然后按照提示完成转换。 
   > [!div class="mx-imgBorder"]
   > ![将现有订阅者移到GitHub](_img/assign-github/move-now.png "单击&quot;立即移动&quot;，将现有订阅Visual Studio订阅GitHub订阅。")
0. 选择"现在 **移动**"按钮时，一个显示面板会提供有关移动订阅和/或Enterprise和/Professional的建议：
   > [!div class="mx-imgBorder"]
   > ![浮出面板](_img/assign-github/fly-out.png)

你可以查看受到影响的订阅者，并指定是否要在移动完成后通知他们接收电子邮件通知。  此电子邮件通知订阅者，他们的权益保持不变，并鼓励他们开始在 GitHub 中建立存在感。  

单击“移动订阅者”按钮，你可以移动所有推荐的订阅者，或者从列表中选择个人。 ****    确认选择后，需要几秒钟才能完成订阅移动。 如果适用，你需要分别为 Professional 和 Enterprise 执行这些步骤。  

## <a name="invite-subscribers-to-your-organization"></a>邀请订阅者加入组织
在订阅管理员门户中为订阅Visual Studio订阅后，GitHub这些用户更新订阅，并将其反映为挂起 **成员**。 组织所有者需要邀请这些挂起的成员加入组织，以访问其GitHub Enterprise权益。 

若要将用户添加到组织，请GitHub：
1. 在左侧 **导航窗格中** 单击"组织"。
0. 选择要将订阅者添加到的组织。  
   > [!div class="mx-imgBorder"]
   > ![选择组织](_img/assign-github/organizations.png "选择要分配新成员的组织。")
0. 选择" **人员"** 选项卡。
0. 如果你是组织的所有者，则会看到"邀请成员 **"** 按钮。  选择该文件夹。 
0. 输入用于向新成员分配订阅的电子邮件地址，然后单击"邀请 **"**。
   > [!div class="mx-imgBorder"]
   > ![邀请成员](_img/assign-github/invite-member.png "输入新会员的登录电子邮件地址。")
0. 单击" **发送邀请"**。  用户现在将显示在挂起的邀请列表中。  
0. 用户收到邀请后GitHub，他们需要单击电子邮件中的按钮，该按钮会将其发送到你的组织并授予他们成员访问权限。 

> [!IMPORTANT]
> 用户邀请的有效期为 7 天，然后需要发送新的邀请。 如果企业使用企业托管用户，可能需要通知用户他们有权访问GitHub。

如果有疑问，请联系你的GitHub或Microsoft 帐户经理。 还可以访问 https://aka.ms/GHEandVSS 了解详细信息。

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
