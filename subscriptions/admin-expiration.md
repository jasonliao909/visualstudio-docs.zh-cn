---
title: 管理员门户对过期 Visual Studio 订阅协议的更改 | Microsoft Docs
author: evanwindom
ms.author: cabuschl
manager: cabuschl
ms.assetid: f38092ba-051c-4e58-97f5-4255dbe873ba
ms.date: 10/08/2021
ms.topic: conceptual
description: 了解协议过期后会对管理员产生什么影响
ms.openlocfilehash: fc7513e09323d82af531ec58684909c09cd6b636
ms.sourcegitcommit: 5f1e0171626e13bb2c5a6825e28dde48061208a4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/09/2021
ms.locfileid: "129704742"
---
# <a name="admin-portal-changes-for-expired-agreements"></a>管理员门户对过期协议的更改
如果用于购买 Visual Studio 订阅的协议过期，则该协议和在该协议中分配的订阅将在有限的时间内保持可用。  对于所有协议而言，该时间段可能并不相同，在通过电子邮件和管理门户接收的通信中将提供有关该时长的更多具体信息。  根据公司的计划，你可能需要采取一些措施来帮助订阅者或防止丢失重要信息。

## <a name="expiration-timeline"></a>过期时间线 
协议过期时间线包含三个阶段：
- [过期之前](#prior-to-expiration)
- [已过期](#expired)
- [已禁用](#disabled)

### <a name="prior-to-expiration"></a>过期之前
在协议到期前约 120 天，我们将开始向管理员和超级管理员发送通知，其中包含有关过期的信息以及你可能需要执行的步骤，具体取决于你的公司是否计划续订协议。 

### <a name="expired"></a>已过期
当你的协议到期时，管理员和订阅者将在有限的时间仍有权访问。  这样做是为了让你的公司能够完成任何正在进行的购买过程，让管理员和订阅者有机会在你的公司未续订协议或选择购买新协议的情况下，采取适当的措施来保留重要数据。  管理员将继续在该时间段内接收通知，以及指向特定信息的链接，以帮助保留信息（如订阅者列表）供将来使用。  订阅者还会开始接收通知，其中提供有关保留信息（如他们可能已在现有 Azure 订阅中创建的任何资产）的指导。  

在此阶段中，管理员和订阅者将继续访问其各自的门户。  管理员仍将能够执行所有订阅管理任务。  订阅者将继续拥有其订阅权益的无限制访问权限。  

> [!IMPORTANT]
> 尽管管理员和订阅者将继续拥有各自资源的访问权限，但重要的是要快速执行操作，以便在此时段过期及失去对信息的访问权限之前保留重要数据。

### <a name="disabled"></a>已禁用
协议过期时：
- 管理员和超级管理员将失去对[管理员门户](https://manage.visualstudio.com)中的过期协议访问权限。  他们将无法对协议内的订阅进行任何更改。  （他们对管理门户中任何其他当前协议的访问权限将不受影响，  还将继续提供[获取帮助](https://manage.visualstudio.com/gethelp)页。）
- 订阅者将失去对[订阅者门户](https://my.visualstudio.com)中的过期订阅访问权限。  如果他们将任何其他订阅作为其他协议的一部分分配给他们，则这些订阅将不会受到影响。 禁用 Visual Studio 订阅的 30 天后，系统还会删除依赖于 Visual Studio 订阅的任何 Azure 订阅，因此，如果订阅者希望保留 Azure 订阅，请务必将 Azure 资产移到另一个有效的订阅。  在这种情况下，Azure 具有自己的通知过程，可帮助指导订阅者。  

## <a name="preserving-your-information"></a>保留你的信息
作为管理员，如果你的协议到期或购买新的协议，你可能想要保留一些信息。 
- 最大用量。  了解你在协议生命期内分配的订阅数量可帮助你的组织根据你的需求购买适当数量的订阅。  你可以在管理门户中[查看使用情况和导出报表](maximum-usage.md)。  
- 订阅者列表。  导出当前协议中的[订阅者列表](exporting-subscriptions.md)可以帮助你快速将这些订阅移动到新的协议。  

## <a name="assisting-subscribers"></a>协助订阅者
当他们开始接收订阅过期通知时，订阅者可能会与你联系，咨询一些问题。  当然，这些问题的答案将取决于贵公司的计划。  如果你的公司计划续订协议或购买新的协议，你可以帮助订阅者了解你的公司处于哪个过程。  如果你的公司不打算续订，你可以在保存其重要信息的过程中协助指导他们。  你可能会发现，在协议过期时各个订阅者会受到何种影响。 有关详细信息，请查看我们的《[订阅过期时](subscription-expiration.md)》一文。 

## <a name="moving-to-a-new-agreement"></a>移动到新协议
如果你的公司购买了新协议，你可以[将订阅者移动到新协议](migrate-subscriptions.md)，而不是在新协议中重新创建这些订阅者。  

## <a name="next-steps"></a>后续步骤
- 了解[各个订阅者](subscription-expiration.md)会因过期协议受到何种影响。
- 了解如何[导出订阅者列表](exporting-subscriptions.md)。
- 了解如何[将订阅移动到新协议](migrate-subscriptions.md)
- 了解如何[使用 Azure Active Directory 组添加订阅者](assign-license-bulk.md#use-azure-active-directory-groups-to-assign-subscriptions)。
