---
title: 如何使用 Azure Active Directory 组自动完成 Visual Studio 订阅
author: esteban-herrera
ms.author: esherrer
manager: shve
ms.date: 07/22/2021
ms.topic: how-to
description: 了解管理员如何使用 Azure Active Directory 组来分配订阅
ms.openlocfilehash: de485170185049270d4819a418ea7d027b1a9d4b
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "127833017"
---
# <a name="how-to-automate-your-visual-studio-subscriptions-using-azure-active-directory-groups"></a>如何使用 Azure Active Directory 组自动完成 Visual Studio 订阅

本指南将演示如何利用 Azure Active Directory (Azure AD) 组来创建一个简单且方便的流程，以便自动完成并管理 Visual Studio 订阅。
将订阅级别分配到 Azure Active Directory 组后，用户就能够根据其所需的订阅级别请求加入 Azure Active Directory 组。 一旦用户获批加入该组，系统就会自动为用户分配相应的订阅。 如果从组或 Azure Active Directory 中删除用户，则会自动删除其订阅。

## <a name="requirements"></a>要求
- 你的组织必须使用 Azure Active Directory 租户进行标识管理。
- 你必须拥有[管理门户](https://manage.visualstudio.com)的管理员权限和访问权限。
- 在 [Azure Active Directory 管理中心](https://aad.portal.azure.com/)，你必须拥有目录的“全局管理员”或“特权角色管理员”角色。

## <a name="how-to"></a>操作说明
1.  为你计划使用的每个订阅级别创建一个 Azure Active Directory 组 
    > [!NOTE]
    > 创建 Azure Active Directory 组时的一些提示：
    > - 将至少一个成员添加到组中。
    > - 成员必须全部位于顶层（不要嵌套其他组）。
    > - 将订阅级别合并到 Azure Active Directory 组名中，以便清楚地表明组的用途。 
    > - 所有组成员都会收到以相同语言编写的“欢迎使用 Visual Studio 订阅”电子邮件。 请为每个区域使用不同的组，以确保订阅者以其首选语言接收此电子邮件。
    > - 所有成员都必须有与其 Azure Active Directory 帐户关联的电子邮件地址。

2.  （可选）为用户设置请求加入组的方式，有多个选项可供选择：
    1.  创建一个利用 [Azure Active Directory Graph API](https://docs.microsoft.com/graph/api/resources/groups-overview?view=graph-rest-1.0) 来管理组成员身份的内部门户。
    2.  通过访问面板使用[自助门户](https://docs.microsoft.com/azure/active-directory/enterprise-users/groups-self-service-management) 
3.  转到[管理门户](https://manage.visualstudio.com)。
4.  选择“添加”和“Azure Active Directory 组”
    > [!div class="mx-imgBorder"]
    > ![“添加 Azure Active Directory 组”按钮的屏幕截图。](media/add-azure-ad-group.png "单击“添加”按钮，然后单击“Azure Active Directory 组”")

5.  在“添加组”滑出式控制板中，找到要为其分配订阅的 Azure Active Directory 组。 在单击“添加”按钮之前，请确保订阅级别正确并完成其余字段。
    a.  如果已为 Azure Active Directory 组的成员分配了一个订阅，则这些成员将更新为在将来由该组进行管理。\*
    > [!div class="mx-imgBorder"]
    > ![Azure Active Directory 组详细信息窗格的屏幕截图。](media/azure-ad-group-details.png "选择组，并选择要分配给该组的订阅级别")

6.  如有必要，请针对每个订阅级别重复此过程，例如，为 Visual Studio Professional 用户创建一个 Azure Active Directory 组，并为 Visual Studio Enterprise 用户创建一个。
7.  大功告成！ 在 Azure Active Directory 组中添加或删除用户时，系统会自动为用户分配或取消分配订阅，并通过电子邮件进行通知。

\* 如果你已管理 Visual Studio 订阅一段时间，你很可能想要将一些分配更新为使用 Azure Active Directory 组。 我们已让该流程变得很简单！ 如果添加一个 Azure Active Directory 组，其中包含已具有订阅的个人用户，则在第一次同步完成后，系统会自动将这些个人用户分组到新添加的 Azure Active Directory 组中。 订阅者会保留其订阅 ID，不会发现任何更改。 如果将来从 Azure Active Directory 组中删除用户，则会自动删除其订阅。 

> [!NOTE]
>如果单个订阅对应于另一订阅级别，则会为用户提供新级别的其他订阅。 示例：如果用户有一个单独的 Visual Studio Professional 订阅，并且用户是某个组的成员，该组已分配有 Visual Studio Enterprise 订阅，则用户现在将同时拥有这两个订阅。 
