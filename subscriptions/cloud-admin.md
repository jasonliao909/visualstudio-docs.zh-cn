---
title: 设置 Visual Studio 月度订阅的管理员 | Microsoft Docs
author: evanwindom
ms.author: amast
manager: amast
ms.assetid: 8b30e2bc-2ac3-4fcc-b296-128731471032
ms.date: 03/21/2021
ms.topic: how-to
description: 设置月度订阅的管理员
ms.openlocfilehash: d316344d633d8ea328d13860235fe221e7476754
ms.sourcegitcommit: 17202f3ac3f7f17ce3756b57dd56321f7254d1dd
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/24/2021
ms.locfileid: "133092887"
---
# <a name="set-up-admins-for-visual-studio-monthly-subscriptions"></a>设置 Visual Studio 月度订阅的管理员

Visual Studio 月度订阅由管理员进行管理。 管理员可以分配订阅、编辑分配、添加或删除订阅以及执行其他的订阅管理工作。

## <a name="the-azure-subscription-owner-is-the-first-admin"></a>Azure 订阅所有者是第一个管理员

购买 Visual Studio 月度订阅后，如果你是购买时所用的 Azure 订阅的所有者，系统会自动将你设置为这些订阅的管理员。

可通过 [Visual Studio Marketplace](https://marketplace.visualstudio.com/subscriptions) 或联系云解决方案提供商购买月度订阅。 如果通过 Visual Studio Marketplace 购买，在购买过程的最后，你将获得管理用户的机会。 选择该选项后将转到 Visual Studio 订阅管理门户 - [https://manage.visualstudio.com](https://manage.visualstudio.com)。

购买订阅后，你随时可以访问[管理门户](https://manage.visualstudio.com)。 只需登录到门户，并在左上角选择相应的 Azure 订阅即可。

如果你是购买月度订阅所用的 Azure 订阅的所有者，那么你还可分配其他管理员。

## <a name="add-admins"></a>添加管理员

若要添加管理员：

1. 通过 [portal.azure.com](https://portal.azure.com) 连接到 Azure 门户。
2. 使用购买 Visual Studio 月度订阅时所用的帐户登录。
3. 在“Azure 服务”下，选择“成本管理 + 计费”   。
   > [!div class="mx-imgBorder"]
   > ![选择“Azure 服务”下的“成本管理 + 计费”](_img/cloud-admin/azure-cost-billing.png "从 Azure 服务组中选择“成本管理”")
4. 在“我的订阅”列表中，选择用于进行购买的 Azure 订阅  。
   > [!div class="mx-imgBorder"]
   > ![选择订阅](_img/cloud-admin/subscription-list.png "选择要用于购买的 Azure 订阅。")
5. 单击左侧导航窗格中列表顶部附近的“访问控制(IAM)”  。
6. 在页面顶部单击“添加”选项卡  。
7. 单击“添加角色分配”  。
   > [!div class="mx-imgBorder"]
   > ![选择“访问控制”、“添加”和“添加角色分配”](_img/cloud-admin/access-control-add.png "从左侧列表中选择“访问控制”，然后选择“添加”。")
8. 在右侧的弹出窗格中，在窗格顶部单击“角色”下拉列表，向下滚动，然后选择“用户访问管理员”   。
9. 在用户列表中向下滚动至你想要创建管理员的用户并选择该用户。 
   > [!div class="mx-imgBorder"]
   > ![选择“角色”和“用户访问管理”](_img/cloud-admin/add-role-user-access-admin.png "依次选择“角色”、“用户访问管理员”，然后选择要使其成为管理员的用户的名称。")
10. 单击“保存”  。
11. 单击“角色分配”选项卡，验证所选用户现在是否显示为“用户访问管理员”  。

新管理员此时可登录到[管理门户](https://manage.visualstudio.com)，从页面左上角的列表中选择用于购买月度订阅的同一个 Azure 订阅，然后开始管理这些订阅。

> [!NOTE]
> 如果看到具有访问权限的用户要编辑你未以管理员身份建立的月度订阅，他们可能具有基础 Azure 订阅中的角色，使他们能够管理订阅。 这些角色包括：所有者、参与者、服务管理员或共同管理员。有关详细信息，请访问[添加账单管理员](/azure/devops/organizations/billing/add-backup-billing-managers)。

有关 Visual Studio 月度订阅的信息，请参阅“购买订阅”下的[概述](vscloud-overview.md)。 要购买 Visual Studio 月度订阅，请访问 Visual Studio Marketplace：[https://marketplace.visualstudio.com/subscriptions](https://marketplace.visualstudio.com/subscription)。

## <a name="resources"></a>资源
- [订阅支持](https://aka.ms/vsadminhelp)

## <a name="see-also"></a>另请参阅
- [Visual Studio 文档](/visualstudio/)
- [Azure DevOps 文档](/azure/devops/)
- [Azure 文档](/azure/)
- [Microsoft 365 文档](/microsoft-365/)

## <a name="next-steps"></a>后续步骤
了解有关管理 Visual Studio 订阅的详细信息。
- [分配单个订阅](assign-license.md)
- [分配多个订阅](assign-license-bulk.md)
- [编辑订阅](edit-license.md)
- [确定最大使用量](maximum-usage.md)