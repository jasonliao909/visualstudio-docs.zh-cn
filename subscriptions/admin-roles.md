---
title: Visual Studio 订阅的超级管理员和管理员角色
author: evanwindom
ms.author: cabuschl
manager: cabuschl
ms.assetid: 6601c395-f778-48c1-ab76-cf454b9193e4
ms.date: 03/19/2021
ms.topic: conceptual
description: 了解超级管理员和管理员角色以及如何分配管理员。
ms.openlocfilehash: 7d034dca2895fcf4660266f97b92b4d9cad82520
ms.sourcegitcommit: 8e74969ff61b609c89b3139434dff5a742c18ff4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/24/2021
ms.locfileid: "128428143"
---
# <a name="super-admins-and-admins-for-visual-studio-subscription-agreements"></a>Visual Studio 订阅协议的超级管理员和管理员

批量许可客户在新的 Visual Studio 订阅管理门户中有两种不同的角色。 这两种角色类似于 VLSC 中曾存在的“主要联系人或通知联系人”角色和“订阅管理员”角色。

**超级管理员：** 首次设置组织时，“主要联系人或通知联系人”在默认情况下会成为超级管理员。 主要联系人或通知联系人可以选择分配其他超级管理员或管理员。 超级管理员可以添加和删除其他管理员和订阅者。 如果系统中有两个以上的超级管理员，为了安全起见，超级管理员可以删除最后两个以外的所有超级管理员。

管理员：管理员只能由超级管理员分配。管理员只能在超级管理员分配给订阅者的协议中对其进行管理。

观看有关如何管理管理员的演示。 
> [!VIDEO https://www.microsoft.com/videoplayer/embed/RE4th6L]

## <a name="assigning-admins"></a>分配管理员
若要分配新的管理员，请执行以下操作：
1. 使用一个电子邮件地址登录到 https://manage.visualstudio.com ，该电子邮件地址在订阅协议上指定为超级管理员。
2. 单击标有“管理管理员”的选项卡  。
3. 单击 **添加**。
   > [!div class="mx-imgBorder"]
   > ![添加管理员](_img/admin-roles/add-admins.png "单击“管理管理员”边栏选项卡，然后单击“添加”以分配新管理员。")
4. 使用新管理员的信息完成表单。  
   > [!div class="mx-imgBorder"]
   > ![添加管理员表单](_img/admin-roles/add-form.png "输入新管理员的登录信息，并选择是否将其设置为超级管理员。然后单击“添加”。")

   > [!NOTE]
   > 如果希望此管理员能够分配其他管理员，请记得选中“超级管理员”框  。

5. 单击“添加”以分配新管理员后，他们将收到一封邀请他们登录门户的电子邮件  。  

## <a name="resources"></a>资源
- [Visual Studio 管理和订阅支持](https://aka.ms/vsadminhelp)

## <a name="see-also"></a>请参阅
- [Visual Studio 文档](/visualstudio/)
- [Azure DevOps 文档](/azure/devops/)
- [Azure 文档](/azure/)
- [Microsoft 365 文档](/microsoft-365/)

## <a name="next-steps"></a>后续步骤
- 了解如何[分配订阅](assign-license.md)
- 了解有关各种[订阅权益](https://visualstudio.microsoft.com/vs/benefits/)的详细信息
- [设置协议首选项](admin-preferences.md)