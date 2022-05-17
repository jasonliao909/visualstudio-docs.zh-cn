---
title: 组织名称更改对 Visual Studio 订阅的影响 | Microsoft Docs
author: evanwindom
ms.author: amast
manager: shve
ms.assetid: bda8772c-cc0b-4949-8419-1084331cc54b
ms.date: 04/25/2022
ms.topic: how-to
description: 了解在电子邮件域发生更改时如何操作以确保可不间断地访问管理门户和订阅。
ms.openlocfilehash: 2914046881643a340c2605fdcb3d3ec7ab40fb5c
ms.sourcegitcommit: b7c53d0e5c8ed5cc4c4928072d267622377085fe
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/14/2022
ms.locfileid: "145031339"
---
# <a name="what-happens-when-your-organizations-name-or-email-domain-changes"></a>当组织的名称或电子邮件域发生更改时会发生什么情况

在如今快速变化的商业环境中，组织可能会经历重大变化。  合并、收购、分拆和品牌重塑都可能导致组织及其租户和域的名称发生更改。  更改电子邮件地址可能会影响订阅者和管理员对 Visual Studio 订阅的访问。  例如，如果你是一名管理员，你的电子邮件地址发生更改，那么你将无法使用新地址登录到管理门户。  按照本文中的步骤操作，以确保你可以继续访问订阅。

## <a name="what-to-do-if-your-organizations-email-addresses-change"></a>如果组织的电子邮件地址发生更改，该如何操作

> [!IMPORTANT]
> 你需要在协议中成为超级管理员才能进行其中一些更改。  如果你不是，可以请求超级管理员为你执行这些操作。 请务必在电子邮件地址发生更改之前更新你的管理员信息。

完成以下步骤，将管理员和订阅者移动到新的电子邮件地址：

### <a name="update-your-admins"></a>更新管理员

1. 登录到管理门户。
0. 选择“管理管理员”。
0. 如果你有多个协议，请选择要更改的协议。 
0. 使用你的新电子邮件地址添加你自己，并确保选中“超级管理员”复选框。  详细了解如何[分配管理员](https://docs.microsoft.com/visualstudio/subscriptions/admin-roles#assigning-admins)。
0. 使用其他管理员的新电子邮件地址添加其他管理员。 
> [!IMPORTANT]
> 请勿删除你当前的管理员电子邮件地址，直到你的新电子邮件地址处于活动状态并且不再需要当前电子邮件地址。  这将确保管理员可以不间断地访问管理门户。

### <a name="update-your-subscribers"></a>更新订阅者

在订阅者的电子邮件地址更改后执行以下步骤。  
1. 登录到管理门户。
0. 选择“管理订阅者”。
0. 对于订阅者列表中单独列出的订阅，请使用[批量添加](assign-license-bulk.md)功能以轻松更新所有订阅者。  
0. 对于分配给 Azure Active Directory (AD) 组成员的订阅，无需在管理门户中执行任何操作。  在 Azure AD 组中更新他们的电子邮件地址时，其订阅将在管理门户中自动更新。 

## <a name="resources"></a>资源

针对管理员的[订阅支持](https://aka.ms/vsadminhelp)

## <a name="next-steps"></a>后续步骤

+ 需要更改订阅而不删除它？  了解如何[编辑订阅](edit-license.md)。
+ 若要查找特定订阅，请查阅[搜索订阅](search-license.md)。
+ 需要创建所有订阅的列表？  请参阅[导出订阅](exporting-subscriptions.md)。
+ 了解如何[删除订阅](delete-license.md)。 
+ [将现有订阅迁移到新协议](migrate-subscriptions.md)。