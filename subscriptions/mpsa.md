---
title: MPSA 中的 Visual Studio 订阅 | Microsoft Docs
author: evanwindom
ms.author: amast
manager: shve
ms.assetid: b331c837-3524-42b7-820e-b4fdd5e12793
ms.date: 03/21/2021
ms.topic: conceptual
description: 了解如何管理 Microsoft 产品和服务协议 (MPSA) 中的 Visual Studio 订阅
ms.openlocfilehash: c196ca15b02357b12066c8c5d4ea7a2dbbae958b
ms.sourcegitcommit: 28168514c0c9472e852de35cceb4f95837669da6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/30/2021
ms.locfileid: "133257578"
---
# <a name="visual-studio-subscriptions-in-a-microsoft-products-and-services-agreement-mpsa"></a>Microsoft 产品和服务协议 (MPSA) 中的 Visual Studio 订阅
如果你是通过 MPSA 计划购买 Visual Studio 订阅的，那么在成为 Visual Studio 订阅管理员并向用户分配订阅之前，需要注意一些事项。 如果你已被设置为管理员，则可直接转到 Visual Studio 订阅[管理门户](https://manage.visualstudio.com/)。

MPSA 客户通过名为[业务中心](https://businessaccount.microsoft.com/Customer)的门户管理通过 MPSA 购买的资产，该门户支持与批量许可服务中心 (VLSC) 类似的功能。 其中包括查看许可证摘要、订单、下载内容、密钥、用户等。但 MPSA 中 Visual Studio 订阅的行为与云服务非常相似。 业务中心还使用工作帐户（而不是 Microsoft 帐户 (MSA)）登录。 如果组织在使用 Office 365 或 Azure Active Directory 等云服务，且这两项服务中的任意一项使用了你的电子邮件，则该电子邮件已经是工作帐户。 在这种情况下，可以使用现有密码注册到业务中心。 如果组织未使用云服务，且你的电子邮件不是工作帐户，你可以使用该电子邮件注册到业务中心。

此外，你在成为 Visual Studio 订阅管理员之后，应在 Visual Studio 订阅[管理门户](https://manage.visualstudio.com/)中分配订阅。在 MPSA 中，必须将 Visual Studio 订阅设置为其各自的管理门户，即 Visual Studio 订阅管理门户。 为此，需要将购买帐户关联到租户（即 contoso.onmicrosoft.com）。

请注意，存在两种类型的租户（托管租户和非托管租户）。 托管租户是指已以组织管理员的身份对其进行管理的租户。

非托管租户是未分配任何管理员的租户，不适用于 Office 365 等联机服务。 使用非工作帐户的电子邮件注册到业务中心时也会创建非托管租户。 如果注册到业务中心时系统要求创建密码，则表明该电子邮件不是工作帐户，并将创建一个非托管帐户。

完成租户关联之前，还需满足下面几个要求/步骤才能成为 Visual Studio 订阅管理员。

## <a name="pre-tenant-association-managed-tenant"></a>预租户关联（托管租户）
- 必须是业务中心的已注册用户。
- 必须（至少）是所在租户中的用户管理员或全局管理员。 （如果公司已在使用云服务，这条也同样适用）。 需要有角色是 Visual Studio 订阅管理员。
- 必须是所在租户中的全局管理员才能将购买帐户关联到租户。
- 必须是业务中心的帐户管理员或帐户管理者。
- [Azure](https://portal.azure.com/) 用户配置文件中（或任何其他用户）的“国家或地区”字段需根据所在区域（美国、加拿大等）正确填写。 

> [!NOTE]
> 你中意的 Visual Studio 订阅管理员人选不必是业务中心的用户，他们只需要满足标准 2 和 5 即可。

满足上述标准后，你可按以下步骤继续将购买帐户关联到租户。
1. 登录[业务中心](https://businessaccount.microsoft.com/Customer)。
2. 单击“帐户”选项卡并选择“关联域”   。
3. 选择“购买帐户”（如有多个购买帐户）  。
4. 选择“租户”（例如 contoso.onmicrosoft.com）。
5. 单击“关联域”  。

通常情况下，关联后，系统会在几分钟内将满足标准的所有用户都设置为 Visual Studio 订阅管理员。 但是有时可能需要长达 24 小时。 预配租户后，你便能访问 Visual Studio 订阅管理门户。 如果花费的时间超过 24 小时，请联系[企业中心支持](https://businessaccount.microsoft.com/Customer/ContactUs)。

> [!NOTE]
> 如果在关联后有新用户满足步骤 2 和步骤 5 中标准，必须联系 MPSA 支持。 MPSA 支持部门将帮助你设置新的 Visual Studio 订阅管理员。

## <a name="tenant-association-unmanaged"></a>租户关联（非托管）
如上文所述，如果用于注册到业务中心的电子邮件不是工作帐户（未在 Azure Active Directory“Azure AD”中注册），则帐户关联略有不同。 需执行所谓的“域接管”。 在此过程中，你将成为全局管理员并将租户从非托管变为托管。

有关此过程的更详细说明，请参阅[快速入门指南](https://www.microsoft.com/Licensing/existing-customer/business-center-training-and-resources.aspx)。 下载名为“设置和使用联机服务”的指南，该指南将指导你完成域接管。 完成此操作后，购买帐户也会关联到租户。

> [!NOTE]
> 完成域接管过程时，必须遵守“预租户关联（托管）”部分中 5 个步骤的标准。 满足这些标准后，只需联系 MPSA 支持部门预配其他 Visual Studio 订阅管理员即可。

## <a name="support-resources"></a>支持资源
- 如需有关管理 Visual Studio 订阅的帮助，请联系 [Visual studio 订阅支持](https://aka.ms/vsadminhelp)。

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
- [删除订阅](delete-license.md)
- [确定最大使用量](maximum-usage.md)