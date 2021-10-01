---
title: 在订阅管理门户中删除 Visual Studio 订阅分配 | Microsoft Docs
author: evanwindom
ms.author: cabuschl
manager: cabuschl
ms.assetid: e49242bc-e9f2-49e8-8caa-f574d508aba6
ms.date: 03/21/2021
ms.topic: how-to
description: 了解管理员可如何在 Visual Studio 订阅管理门户中删除订阅分配
ms.openlocfilehash: 6963d3b6f3cc478eaa80672499a28bf42d094264
ms.sourcegitcommit: 8e74969ff61b609c89b3139434dff5a742c18ff4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/24/2021
ms.locfileid: "128428067"
---
# <a name="delete-assignments-in-visual-studio-subscriptions"></a>删除 Visual Studio 订阅中的分配
当订阅者不再需要 Visual Studio 订阅时，比如当他们离开公司、完成项目或转换为新的作业角色时，你可以删除他们的订阅，并将订阅分配给其他人。 请注意，重新分配订阅时，并非所有订阅者权益都将重置。  新用户将能够认领任何无人认领的密钥并查看以前认领过的密钥，但认领限制 **不** 会重置。  组织若具有企业协议 (EA)，将重置供原始用户使用的任何权益（如 Pluralsight 培训）。 
> [!Important]
> 上次分配订阅后至少经过 90 天，才可将订阅分配给不同的用户。  例如，如果在 6 月 1 日向某订阅者分配了订阅，则在 8 月 30 日之前不能将订阅分配给新订阅者。 

观看此视频或继续阅读，了解如何删除分配。  

> [!VIDEO https://www.microsoft.com/videoplayer/embed/RE4yG2q]

## <a name="delete-a-subscription-assignment"></a>删除订阅分配
1. 单击要删除的订阅者名称。 若要选择多个要删除的订阅者，可以单击订阅者名称左侧的圆圈来选择每个订阅者。  或者，你可以按住 CTRL 键，然后单击要删除的每个订阅者。 若要删除某一范围的订阅服务器，请单击第一个订阅服务器，按 Shift 键，然后单击最后一个。  按 CTRL + A，选择并删除所有订阅者。 在此示例中，将删除三个订阅者，即 Amber、Kai 和 Madison。 
2. 若要删除所选订阅者，请单击“删除”。
3. 出现要求确认删除的消息时，单击“确定”。
   > [!div class="mx-imgBorder"]
   > ![删除订阅者](_img/delete-license/delete-subscribers.png "选择要删除的用户，然后单击“删除”。可以使用 CTRL 和 Shift 键来选择多个订阅者。")

   > [!NOTE]
   > 使用模板进行批量删除的功能不可用。 
   >
   > 如果通过 Azure Active Directory 安全组添加了订阅分配，则最长可能需要 24 小时才能在管理门户中删除更新。  有关使用 Azure Active Directory 组管理订阅的详细信息，请参阅[我们的文章](assign-license-bulk.md#use-azure-active-directory-groups-to-assign-subscriptions)。 

## <a name="resources"></a>资源
- [订阅支持](https://aka.ms/vsadminhelp)

## <a name="see-also"></a>另请参阅
- [Visual Studio 文档](/visualstudio/)
- [Azure DevOps 文档](/azure/devops/)
- [Azure 文档](/azure/)
- [Microsoft 365 文档](/microsoft-365/)

## <a name="next-steps"></a>后续步骤
- 需要更改订阅而不删除它？  了解如何[编辑订阅](edit-license.md)
- 有关查找特定订阅的帮助，请查阅[搜索订阅](search-license.md)。
- 需要创建所有订阅的列表？  请参阅[导出订阅](exporting-subscriptions.md)。