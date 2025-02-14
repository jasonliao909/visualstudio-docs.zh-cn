---
title: MPSA 中的 Visual Studio 订阅 | Microsoft Docs
author: evanwindom
ms.author: amast
manager: shve
ms.assetid: b331c837-3524-42b7-820e-b4fdd5e12793
ms.date: 05/18/2022
ms.topic: conceptual
description: 了解如何管理 Microsoft 产品和服务协议 (MPSA) 中的 Visual Studio 订阅
ms.openlocfilehash: b9fa5fd4e75d0d5f3aa0495fc6384feba2b954eb
ms.sourcegitcommit: 2c4ca71e7711d9c4a468b1bcff026565c765952c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/19/2022
ms.locfileid: "145172607"
---
# <a name="visual-studio-subscriptions-in-a-microsoft-products-and-services-agreement-mpsa"></a>Microsoft 产品和服务协议 (MPSA) 中的 Visual Studio 订阅

如果你已通过 MPSA 计划购买了Visual Studio 订阅，可以先了解一些事项，然后才能成为Visual Studio订阅管理员并向用户分配订阅。 如果已设置为管理员，可以直接转到Visual Studio订阅[管理门户](https://manage.visualstudio.com/)。

MPSA 客户通过名为[业务中心](https://businessaccount.microsoft.com/Customer)的门户管理通过 MPSA 购买的资产，该门户支持与批量许可服务中心 (VLSC) 类似的功能。 其中包括查看许可证摘要、订单、下载内容、密钥、用户等。但 MPSA 中 Visual Studio 订阅的行为与云服务非常相似。 业务中心还使用工作帐户（而不是 Microsoft 帐户 (MSA)）登录。 如果访问Azure Active Directory或Office 365等服务，则电子邮件已是工作帐户。 在这种情况下，可以使用现有密码注册到业务中心。 如果组织未使用云服务，且你的电子邮件不是工作帐户，你可以使用该电子邮件注册到业务中心。

Visual Studio订阅[管理门户](https://manage.visualstudio.com/)是在成为Visual Studio订阅管理员后分配订阅的位置。在 MPSA 中，必须将Visual Studio订阅预配到各自的管理门户，即Visual Studio 订阅管理门户。 为此，需要将购买帐户关联到租户 (示例：contoso.onmicrosoft.com) 。

有两种类型的租户 - 托管租户和非托管租户。 托管租户是指已以组织管理员的身份对其进行管理的租户。

非托管租户是未分配任何管理员的租户，不适用于 Office 365 等联机服务。 使用非工作帐户的电子邮件注册到业务中心时也会创建非托管租户。 如果在 Business Center 上注册时创建了密码，则电子邮件不是工作帐户，并且创建了非托管租户。

完成租户关联之前，还需满足下面几个要求/步骤才能成为 Visual Studio 订阅管理员。

## <a name="pre-tenant-association-managed-tenant"></a>预租户关联（托管租户）

+ 必须是业务中心的已注册用户。
+ 你必须是用户管理员 (，至少) 或属于租户的全局管理员。 （如果公司已在使用云服务，这条也同样适用）。 需要有角色是 Visual Studio 订阅管理员。
+ 你必须是租户中的全局管理员，才能将购买帐户关联到租户。
+ 必须是业务中心的帐户管理员或帐户管理者。
+ 用户配置文件中的“国家或地区”字段 (和 [Azure](https://portal.azure.com/) 中的任何其他用户) 都需要根据区域 (（如 US、CA 等 ) ）进行适当填充。 

> [!NOTE]
> 你中意的 Visual Studio 订阅管理员人选不必是业务中心的用户，他们只需要满足标准 2 和 5 即可。

满足上述条件后，可以继续按照以下步骤将购买帐户关联到租户。
1. 登录[业务中心](https://businessaccount.microsoft.com/Customer)。
2. 选择“帐户”选项卡，然后选择“关联域” 。
3. 选择“购买帐户”（如有多个购买帐户）  。
4. 选择“租户”（例如 contoso.onmicrosoft.com）。
5. 选择“关联域”。

通常情况下，关联后，系统会在几分钟内将满足标准的所有用户都设置为 Visual Studio 订阅管理员。 但是有时可能需要长达 24 小时。 预配租户后，你将能够访问Visual Studio 订阅管理门户。 如果花费的时间超过 24 小时，请联系[企业中心支持](https://businessaccount.microsoft.com/Customer/ContactUs)。

> [!NOTE]
> 如果在关联后有新用户满足步骤 2 和步骤 5 中标准，必须联系 MPSA 支持。 MPSA 支持部门将帮助你设置新的 Visual Studio 订阅管理员。

## <a name="tenant-association-unmanaged"></a>租户关联（非托管）

如果注册到 Business Center 的电子邮件不是在 Azure Active Directory (Azure AD) 中注册的工作帐户，则租户关联将略有不同。 需要执行所谓的“域接管”的内容。 此过程将使你成为全局管理员，并将租户从非托管更改为托管租户。

有关此过程的更详细说明，请参阅[快速入门指南](https://www.microsoft.com/Licensing/existing-customer/business-center-training-and-resources.aspx)。 下载名为“设置和使用联机服务”的指南，该指南将指导你完成域接管。 完成此操作后，购买帐户也会关联到租户。

> [!NOTE]
> 完成域接管过程时，必须遵守“预租户关联（托管）”部分中 5 个步骤的标准。 满足这些标准后，只需联系 MPSA 支持部门预配其他 Visual Studio 订阅管理员即可。

## <a name="support-resources"></a>支持资源

如需有关管理 Visual Studio 订阅的帮助，请联系 [Visual studio 订阅支持](https://aka.ms/vsadminhelp)。

## <a name="see-also"></a>另请参阅

+ [Visual Studio 文档](/visualstudio/)
+ [Azure DevOps 文档](/azure/devops/)
+ [Azure 文档](/azure/)
+ [Microsoft 365 文档](/microsoft-365/)

## <a name="next-steps"></a>后续步骤

了解有关管理 Visual Studio 订阅的详细信息。
+ [分配单个订阅](assign-license.md)
+ [分配多个订阅](assign-license-bulk.md)
+ [编辑订阅](edit-license.md)
+ [删除订阅](delete-license.md)
+ [确定最大使用量](maximum-usage.md)