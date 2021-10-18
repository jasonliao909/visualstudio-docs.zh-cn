---
title: 如何解决批量上传问题？
description: 超级管理员或管理员认为他们向新协议分配了用户，但他们将用户添加到了错误的协议。
ms.topic: include
ms.assetid: 273f5f7a-739e-4de0-b7f7-d0bdd616e059
author: CaityBuschlen
ms.author: cabuschl
ms.date: 06/01/2021
user.type: admin
tags: bulk, upload
subscription.type: vl, cloud, retail, partner
sap.id: b84fffb5-3363-eb7d-224e-1c63faf4067b
ms.openlocfilehash: 451629c284ae4e6630e461dc67e74c28b0c2ddfb
ms.sourcegitcommit: 485f0f6f578568ee31b2ac093e32a6d01dc9c1c5
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/14/2021
ms.locfileid: "130019392"
---
## <a name="how-do-i-fix-a-bulk-upload-to-use-the-correct-agreement"></a>我如何解决批量上传问题，以使用正确的协议？

如果错误地批量上传到错误的协议，请按照以下步骤解决问题。

首先，请确保将订阅者上传到正确的协议，然后从另一个协议中删除订阅者。 你可以通过管理门户批量删除或修复单个用户的问题。

## <a name="individual-users"></a>个人用户

1. 在[管理门户的“订阅者”](https://manage.visualstudio.com/subscribers)页面上，单击列名和排序，查找需要删除的订阅者。 你还可使用筛选器选项，更轻松地查找用户。
2. 找到要删除的订阅者后，选中用户旁边的复选框。 你可以一次性选择任意数量的用户。 你还可以选择要删除列表中的第一位用户，然后选择“Shift”，接着是列表中的最后一位用户。 这些步骤会选择列表中的所有用户。 你还可以选择列表顶部的选中图标以选择所有用户。 
3. 选择网格顶部的“删除”，然后确认删除。

## <a name="azure-active-directory-azure-ad-group"></a>Azure Active Directory (Azure AD) 组

如果用户是通过 Azure AD 组添加的，则你需要直接从 Azure AD 组中删除用户。 从组中删除用户后，系统最多可能需要 24 小时才能在管理员门户中显示删除操作。 

## <a name="impact-of-moving-subscriptions"></a>移动订阅的影响

当订阅者移动到新协议时，他们会收到新的订阅 ID。 此更改会中断连接与每月 Azure 额度权益关联的 Azure 订阅。 链接断开时，旧的 Azure 订阅会最终停用。 要避免中断，使用新的 Visual Studio 订阅中的权益创建新的 Azure 订阅，并[将旧的 Azure 订阅中的任何现有 Azure 资产传输](https://docs.microsoft.com/azure/azure-resource-manager/management/move-resource-group-and-subscription)到新订阅。