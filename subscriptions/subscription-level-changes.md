---
title: 更改 Visual Studio 订阅级别的影响 | Visual Studio Marketplace
author: evanwindom
ms.author: cabuschl
manager: cabuschl
ms.assetid: bb2fa359-8170-4db0-a0c5-d49fc692b0aa
ms.date: 10/13/2021
ms.topic: conceptual
description: 了解升级或下载 Visual Studio 订阅级别的影响。
ms.openlocfilehash: 6d49b868c28210fcf69b73a8b392f1e7f4dba8ae
ms.sourcegitcommit: 72f8ce4992cc62c4833e6dcb0f79febb328c44be
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/14/2021
ms.locfileid: "130010998"
---
# <a name="what-happens-when-you-change-visual-studio-subscription-levels"></a>更改 Visual Studio 订阅级别后会出现什么情况？
在 Visual Studio 订阅中，软件、工具、服务以及可供你使用的其他权益取决于你的订阅级别。  通常，你的订阅级别越高，它提供的权益就越可靠。  

在某些情况下，你可以从一个订阅级别开始，然后增加（升级）或降低（降级）到其他级别。  这些情况的示例包括：
- 你决定需要功能更齐全的 Visual Studio IDE 版本，或者可以访问更广泛的软件下载，因此选择升级。 
- 公司的订阅管理员可以根据你当前的角色或项目或公司购买计划中的更改来选择更改你的订阅级别。 例如，你的公司可以选择更改购买的订阅的组合以实现成本节约。  

根据你是升级还是降级，以及你拥有的订阅级别，你可能需要采取措施来访问新订阅中的权益。

## <a name="how-do-my-benefits-change"></a>我的权益如何变化？
你将看到的针对特定权益的更改取决于权益本身。  我们将查看一些示例，并讨论各项的升级和降级的影响。

### <a name="visual-studio-ide"></a>Visual Studio IDE
有关订阅中包含哪个版本的 Visual Studio 的信息，请查看我们的 [Visual Studio 订阅权益页](https://visualstudio.microsoft.com/vs/benefits/)。 请访问[比较 Visual Studio 2019 版本](https://visualstudio.microsoft.com/vs/compare/)页，了解订阅中包含的版本之间的差异。
 
升级：你将可以访问你的新订阅中提供的 IDE 级别。  若要使用它，你将需要卸载较低版本，并安装新的更高版本。  

降级：对于更高的订阅级别中提供的版本，你仍具有永久的使用权限。  不过，你将无法登录以访问该版本的 IDE，因此你将需要使用产品密钥来激活它，然后才能失去对更高级别订阅的访问权限。  可以通过访问订阅者门户中的[产品密钥页](https://my.visualstudio.com/productkeys)来获取产品密钥。  如果你已索取 Visual Studio 的产品密钥，则还可以导出你已索取的密钥列表。 详细了解如何[查找和索取产品密钥](find-keys.md)。

### <a name="individual-azure-credits"></a>个人 Azure 额度
个人 Azure 额度的配额因订阅级别而异。  你可能会收到介于 $0 和 $150 之间的每月额度，具体取决于你的订阅级别。  

如果你的 Visual Studio 订阅发生更改，则可能会遇到三种情况。  除了潜在的升级或降级，公司的订阅管理员还可以为你分配一个你目前拥有的同一级别的订阅，但具有不同的订阅 ID。  在所有这三种情况下，对 Azure 订阅的影响都是相同的，只有个人额度的数量可能会改变。 

更改你的 Visual Studio 订阅会断开与你的 Azure 订阅的链接，该链接可接收额度，并在你激活新订阅中的权益时创建新的 Azure 订阅。  出现这种情况时，旧的 Azure 订阅将被迫最终停用。  若要避免此问题，请选择下列解决方法之一：
- 将订阅转换为即用即付。  有关详细信息，请访问我们的 [Azure 开发测试即用即付订阅](vs-azure-payg.md)一文。  你需要将付款方式（例如信用卡）附加到此订阅。 
- 使用新的 Visual Studio 订阅中的权益创建新的 Azure 订阅，并将旧的 Azure 订阅中的任何现有 Azure 资产传输到新订阅。 
  > [!IMPORTANT]
  > 重要的是，将 Azure 资产移至新的 Azure 订阅，或将现有的 Azure 订阅更改为即用即付，以避免丢失现有的 Azure 资产。 
 
### <a name="software-downloads"></a>软件下载
可供你使用的软件下载取决于你的订阅级别。  有关详细信息，请参阅我们的[可用软件下载列表](software-download-list.md)一文。 

  > [!TIP] 
  > 你在[下载页](https://my.visualstudio.com/downloads)上看到的软件标题列表取决于你为登录电子邮件地址分配的最高订阅级别。  你将看到适用于你拥有的 **最高** 订阅级别的所有标题。  例如，如果你拥有 Visual Studio Enterprise 订阅和 Visual Studio Dev Essentials 成员身份，你将看到 Enterprise 订阅中包含的所有标题，即使你已登录到 Dev Essentials 成员身份也是如此。  

### <a name="other-benefits"></a>其他优点 
更改订阅级别对其他权益的影响可能会很大。  

#### <a name="benefits-with-a-fixed-length"></a>具有固定时长的权益
我们的合作伙伴提供的很多权益都是具有固定时长的产品/服务。  如果你在订阅级别中进行任何更改之前激活了这些权益，则其中许多权益将不受影响，并且在正常期限结束之前，将一直可用。  例如，如果你已在 Enterprise 订阅中激活了六个月订阅作为培训权益，并且你的 Visual Studio 订阅已降级到 Visual Studio Professional，则在培训订阅上仍将有剩余时间。  

#### <a name="benefits-that-require-authentication"></a>要求身份验证的权益
如果你使用的是每次登录 Visual Studio 时都会进行身份验证的权益，则对你的订阅级别进行降级后，这些权益将不可用。  

#### <a name="benefits-that-are-not-available-in-lower-subscription-levels"></a>在较低的订阅级别中不可用的权益
如果你使用的是当前订阅中提供的权益，而不是降级的订阅中提供的权益，则可能会失去对这些权益的访问权限。  

## <a name="support-resources"></a>支持资源
- 有关 Visual Studio 订阅的销售、订阅、帐户和账单的帮助，请联系 [Visual Studio 订阅支持](https://my.visualstudio.com/gethelp)。
- 对有关 Visual Studio IDE、Azure DevOps 或其他 Visual Studio 产品或服务有疑问？  请访问 [Visual Studio 支持](https://visualstudio.microsoft.com/support/)。

## <a name="see-also"></a>另请参阅
- [Visual Studio 文档](/visualstudio/)
- [Azure DevOps 文档](/azure/devops/)
- [Azure 文档](/azure/)
- [Microsoft 365 文档](/microsoft-365/)

## <a name="next-steps"></a>后续步骤
- 了解 [Azure DevOps](https://azure.microsoft.com/services/devops/) 功能
- 了解 [Visual Studio IDE 功能（按版本）](https://visualstudio.microsoft.com/vs/compare/)