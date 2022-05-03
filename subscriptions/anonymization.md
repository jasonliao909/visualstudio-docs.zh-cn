---
title: Visual Studio 订阅者数据匿名化 | Microsoft Docs
author: evanwindom
ms.author: amast
manager: shve
ms.assetid: ce5fc8a4-484c-4df6-97c3-cb60174fb66b
ms.date: 04/26/2022
ms.topic: conceptual
description: 了解订阅访问丢失时订阅者数据的匿名方式。
ms.openlocfilehash: f348493c04eb36dd7a7dd65540f4a221a758aae1
ms.sourcegitcommit: 9e9f4cf4b34735fffa376b203ccaa74cb705ffe2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2022
ms.locfileid: "144334513"
---
# <a name="anonymization-of-visual-studio-subscriber-information"></a>Visual Studio 订阅者信息匿名化
当发生阻止订阅者使用订阅的事件时，用户的个人信息（如名称和登录帐户）会争用，使其不可用。  这种“匿名化”是为了保护订户的个人信息。  这些事件可能包括：
+ 订阅过期
+ 删除订阅者登录帐户   

[!INCLUDE [GDPR-related guidance](includes/gdpr-intro-sentence.md)]

## <a name="when-does-anonymization-occur"></a>何时发生匿名？
使订阅不可用的事件将触发匿名化。  匿名发生的速度取决于订阅类型和触发事件。 有关详细信息，请参阅下表。

| 订阅类型  | 触发匿名的事件 | 匿名发生时 |
|--------------------|--------------------------------|---------------------------|
| Visual Studio Dev Essentials | 订阅者选择退出计划或不接受使用条款 | 30 天 |
| 通过 Microsoft Store（零售）购买的 Visual Studio 订阅 | 订阅过期或未激活  | 360 天 |
| 通过 Volume License、Visual Studio Marketplace（云订阅）或 MPN 等计划获得的 Visual Studio 订阅 | 订阅过期或未分配给用户 | 180 天 |
| 所有订阅 | 用于登录订阅的 Azure Active Directory 帐户或 Microsoft 帐户 (MSA) 已关闭 | 立即 |
| 所有订阅 | 将从与 Azure Active Directory 帐户关联的租户中删除订阅者 | 立即 |

## <a name="faq"></a>FAQ
### <a name="q--does-the-anonymization-of-the-subscribers-personal-information-cause-them-to-lose-access-to-the-subscription"></a>问：订阅者个人信息匿名化是否导致他们无法访问订阅？
答：不是。  访问订阅后发生匿名化。

### <a name="q--im-an-admin-for-my-organizations-subscriptions--if-one-of-my-subscribers-information-is-anonymized-can-i-reassign-that-subscription-to-another-user"></a>问：我是组织订阅的管理员。  如果我的某个订阅者的信息匿名化，是否可以将该订阅重新分配给另一个用户？
答：可以。  如果满足以下条件，则可以重新分配订阅：
+ 订阅尚未过期。
+ 自上次将订阅分配给订阅者后至少已过去 90 天。  例如，如果在 6 月 1 日向订阅者分配了订阅，则在 8 月 30 日之前不能重新分配订阅。

### <a name="q-how-can-i-prevent-anonymization-caused-by-deleting-a-sign-in-email-address"></a>问：如何避免由删除登录电子邮件地址导致的匿名化问题？
答：可通过两种方式避免该问题：
+ 部署单个标识管理系统（MSA 或 Azure Active Directory），但不能同时部署这两者。  
+ 通过租户关联Azure Active Directory和 MSA 标识。 

## <a name="support-resources"></a>支持资源
有关 Visual Studio 订阅的销售、订阅、帐户和账单的帮助，请参阅 Visual Studio [订阅支持](https://aka.ms/vssubscriberhelp)。

## <a name="see-also"></a>另请参阅
+ [Visual Studio 文档](/visualstudio/)
+ [Azure DevOps 文档](/azure/devops/)
+ [Azure 文档](/azure/)
+ [Microsoft 365 文档](/microsoft-365/)

## <a name="next-steps"></a>后续步骤
了解如何通过[关联 MSA 和Azure Active Directory标识](/azure/active-directory/b2b/add-users-administrator)来防止匿名化。