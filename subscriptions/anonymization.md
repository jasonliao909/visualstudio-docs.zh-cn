---
title: Visual Studio 订阅者数据匿名化 | Microsoft Docs
author: evanwindom
ms.author: amast
manager: shve
ms.assetid: ce5fc8a4-484c-4df6-97c3-cb60174fb66b
ms.date: 03/11/2021
ms.topic: conceptual
description: 了解订阅访问丢失时订阅者数据的匿名方式。
ms.openlocfilehash: 6e7f775213b158765448dc306d676ffc2a86e4ea
ms.sourcegitcommit: 28168514c0c9472e852de35cceb4f95837669da6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/30/2021
ms.locfileid: "133254392"
---
# <a name="anonymization-of-visual-studio-subscriber-information"></a>Visual Studio 订阅者信息匿名化
当发生阻止订阅者使用订阅的事件时，例如订阅到期或删除订阅者的登录帐户，用户的个人信息（如姓名和登录帐户）基本上被扰乱以使其无法使用。  这样做是为了保护订阅者的个人信息。

[!INCLUDE [GDPR-related guidance](includes/gdpr-intro-sentence.md)]

## <a name="when-does-anonymization-occur"></a>何时发生匿名？
致使订阅者无法订阅的事件将触发匿名。  匿名发生的速度取决于订阅类型和触发事件。 有关详细信息，请参阅下表。

| 订阅类型                                                                                                                       | 触发匿名的事件                                                                                                     | 匿名发生时 |
|-----------------------------------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------|---------------------------|
| Visual Studio Dev Essentials                                                                                                            | 订阅者选择退出该计划或不接受使用条款                                    | 30 天               |
| 通过 Microsoft Store（零售）购买的 Visual Studio 订阅                                                                      | 订阅过期或没有激活                                                                   | 360 天                  |
| 通过 Volume License、Visual Studio Marketplace（云订阅）或 MPN 等计划获得的 Visual Studio 订阅 | 订阅过期或未分配给用户                                                          | 180 天                  |
| 所有订阅                                                                                                                       | 用于登录订阅的 Azure Active Directory 帐户或 Microsoft 帐户 (MSA) 已关闭 | 立即               |
| 所有订阅                                                                                                                       | 将从与 Azure Active Directory 帐户关联的租户中删除订阅者                                | 立即               |

## <a name="faq"></a>FAQ
### <a name="q--does-the-anonymization-of-the-subscribers-personal-information-cause-them-to-lose-access-to-the-subscription"></a>问：订阅者个人信息匿名化是否导致他们无法访问订阅？
答：不是。  匿名化是针对导致订阅权限丢失但不导致缺乏访问权限的事件而进行的。

### <a name="q--im-an-admin-for-my-organizations-subscriptions--if-one-of-my-subscribers-information-is-anonymized-can-that-subscription-be-reassigned-to-another-user"></a>问：我是组织订阅的管理员。  如果某个订阅者的信息是匿名的，那么该订阅是否可以重新分配给其他用户？
答：可以。  如果满足以下条件， 重新分配订阅：
- 订阅未过期
- 自上次将订阅分配给订阅者后至少已过去 90 天。  例如，如果在 6 月 1 日向订阅者分配了订阅，则在 8 月 30 日之前不能重新分配订阅。

### <a name="q-how-can-i-prevent-anonymization-caused-by-deleting-a-sign-in-email-address"></a>问：如何避免由删除登录电子邮件地址导致的匿名化问题？
答：可通过两种方式避免该问题：
- 部署单一标识管理系统（MSA 或AAD），但不能同时部署这两者。  
- 通过租户关联 AAD 和 MSA 标识。 

## <a name="support-resources"></a>支持资源
- 有关 Visual Studio 订阅的销售、订阅、帐户和账单的帮助，请参阅 Visual Studio [订阅支持](https://aka.ms/vssubscriberhelp)。

## <a name="see-also"></a>另请参阅
- [Visual Studio 文档](/visualstudio/)
- [Azure DevOps 文档](/azure/devops/)
- [Azure 文档](/azure/)
- [Microsoft 365 文档](/microsoft-365/)

## <a name="next-steps"></a>后续步骤
通过[链接 MSA 和 AAD 标识](/azure/active-directory/b2b/add-users-administrator)了解如何防止匿名。