---
title: Microsoft 删除的 Visual Studio 订阅分配 | Microsoft Docs
author: evanwindom
ms.author: amast
manager: shve
ms.assetid: f853ed9d-3543-4f5f-a754-92381ee03523
ms.date: 09/30/2021
ms.topic: how-to
description: 了解当你看到关于 Microsoft 已删除某个订阅的通知时意味着什么。
ms.openlocfilehash: 7d8a0d44f147f3490afd85de28173839ee222629
ms.sourcegitcommit: 28168514c0c9472e852de35cceb4f95837669da6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/30/2021
ms.locfileid: "133257876"
---
# <a name="why-does-my-dashboard-shows-microsoft-removed-a-subscriber"></a>为什么我的仪表板显示 Microsoft 删除了订阅者？ 
在[管理门户](https://manage.visualstudio.com)上的仪表板的“最近的更改”部分，你可能会看到订阅已删除，原因显示为“帐户已关闭”。  出现这种情况的原因有两个。  

## <a name="subscribers-request-closure-of-their-microsoft-accounts"></a>订阅者请求关闭其 Microsoft 帐户
如果订阅者请求关闭用于登录到订阅的 Microsoft 帐户 (MSA)，则当 MSA 关闭时，订阅会被删除。  

有关详细信息（包括关闭帐户之前要考虑的重要事项），请参阅[如何关闭 Microsoft 帐户](https://support.microsoft.com/account-billing/how-to-close-your-microsoft-account-c1b2d13f-4de6-6e1b-4a31-d9d668849979)。

## <a name="subscribers-are-removed-from-azure-active-directory-tenant"></a>从 Azure Active Directory 租户中删除订阅者
如果从某个 Azure Active Directory (Azure AD) 组中删除订阅者，并且该订阅者的订阅是使用该组自动分配的，则会自动删除订阅。  

## <a name="what-happens-when-the-account-is-closed"></a>关闭帐户后会发生什么情况？
如果删除订阅，订阅者会立即失去对订阅的访问权限。  如果从 Azure AD 组中删除订阅者，则其订阅信息会在 180 天内永久删除。  如果订阅者关闭其 MSA，则会立即删除其信息。  

## <a name="resources"></a>资源
- 针对管理员的[订阅支持](https://aka.ms/vsadminhelp)

## <a name="see-also"></a>另请参阅
- [Visual Studio 文档](/visualstudio/)
- [Azure DevOps 文档](/azure/devops/)
- [Azure 文档](/azure/)
- [Microsoft 365 文档](/microsoft-365/)

## <a name="next-steps"></a>后续步骤
- 需要更改订阅而不删除它？  了解如何[编辑订阅](edit-license.md)。
- 若要查找特定订阅，请查阅[搜索订阅](search-license.md)。
- 需要创建所有订阅的列表？  请参阅[导出订阅](exporting-subscriptions.md)。
- 了解如何[删除订阅](delete-license.md)。 

