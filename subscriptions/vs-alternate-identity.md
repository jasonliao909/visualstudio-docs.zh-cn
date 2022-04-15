---
title: Visual Studio 订阅者标识
author: evanwindom
ms.author: amast
manager: shve
ms.assetid: 86f2856c-8adf-4085-9962-f4136679e5ed
ms.date: 04/14/2022
ms.topic: conceptual
description: 了解如何为Visual Studio订阅添加备用标识以用于Azure DevOps和 Azure
ms.openlocfilehash: 1e11f5ac1e48ec13cd95b7cd59908084916bc79b
ms.sourcegitcommit: 3bb62c9d6e4e1b71d70848fef01b33e4d2050577
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/15/2022
ms.locfileid: "142637780"
---
# <a name="identities-for-visual-studio-subscribers"></a>Visual Studio 订阅者标识
激活 Visual Studio 订阅时，我们会将用户激活期间使用的标识（或登录名）与 Visual Studio 订阅关联起来。 这样，我们便能在 [Visual Studio 订阅者门户](https://my.visualstudio.com?wt.mc_id=o~msft~docs)、Azure DevOps 和 Azure 中识别你。

在 Azure DevOps 中，我们会在你每次登录时检查你的 Visual Studio 订阅状态，并在你所属的每个组织中自动授予相应功能。
由于这些功能是作为订阅者权益随附，因此可以在你使用与 Visual Studio 订阅关联的标识时，将你添加为任何 Azure DevOps 组织的成员。

在 Azure 中，用户激活其[每月 Azure 开发测试个人额度](https://azure.microsoft.com/pricing/member-offers/credit-for-visual-studio-subscribers/)（一项订阅者权益）时，我们会检查其 Visual Studio 订阅状态。

在 [Visual Studio 订阅者门户](https://my.visualstudio.com?wt.mc_id=o~msft~docs)中，除激活过程中使用的标识外，还可添加“备用标识”  。 如果使用 Microsoft 帐户激活订阅，则可添加备用标识。 这样，你还能添加工作或学校帐户（登录 Visual Studio、Microsoft 365 或公司/学校网络时使用的帐户），以使用个人帐户和工作或学校帐户访问 Azure DevOps。

## <a name="add-an-alternate-account-to-your-subscription"></a>向订阅添加备用帐户
向 Visual Studio 订阅添加备用帐户后，可享受某些订阅权益（如 Azure DevOps 和 Azure），或者可使用与订阅分配到的标识不同的标识登录到 Visual Studio IDE。 在过去，仅当 Visual Studio (VS) 订阅已分配到 Microsoft 帐户 (MSA) 时此功能才可用。 我们已经将此功能扩展到 Azure Active Directory (Azure AD) 中的工作或学校帐户。

> [!NOTE]
> 备用 ID 只允许你使用第二个 ID 激活 Azure 额度和 Azure DevOps，并登录到 Visual Studio IDE。  不能使用它在 <https://my.visualstudio.com> 登录到订阅门户。  你仍需要使用订阅分配到的 ID 登录到该门户。 

对于所有订阅，都可添加“工作或学校帐户”，从而使用此帐户享受需要登录的权益（VS IDE、Azure DevOps 和 Azure）。

### <a name="add-the-alternate-account"></a>添加备用帐户
1. 使用 Microsoft 帐户 (https://my.visualstudio.com) 登录到 Visual Studio 订阅者门户。
2. 选择 **“订阅”** 选项卡。
3. 选择“添加备用帐户”  。
4. 添加工作或学校帐户。
    > [!div class="mx-imgBorder"]
    > ![添加工作或学校帐户](_img/vs-alternate-identity/enter-alternate-account-my-visual-studio-com-portal.png "在订阅中添加工作或学校帐户作为备用帐户。")

5. 使用工作或学校帐户登录 Azure DevOps (https://{youraccount}.visualstudio.com)。

此时，备用帐户已添加到 Visual Studio 订阅中，可使用两个标识享受需要使用备用帐户登录的订阅权益（IDE、Azure DevOps 和 Azure）。

## <a name="faq"></a>FAQ
### <a name="q--why-doesnt-azure-devops-recognize-me-as-a-visual-studio-subscriber"></a>问：为什么 Azure DevOps 未将我识别为 Visual Studio 订阅者？
答：如果你使用主要标识或备用标识登录，Azure DevOps 应该会自动识别你的订阅。 如果没有，可尝试以下操作：
- 检查是否拥有包含 [Azure DevOps 权益](vs-azure-devops.md#eligibility)的有效 Visual Studio 订阅。
- 确认使用的登录名/标识是 Visual Studio 订阅的主要或备用标识。  例如，许多人还会有一个与其他登录 ID 相关联的 Visual Studio Dev Essentials 成员身份。  尝试登录到具有该 ID 的其他订阅将失败，除非这些订阅与该电子邮件地址相关联。
- 登录 Azure DevOps 前，至少先访问一次 [Visual Studio 订阅者门户](https://my.visualstudio.com?wt.mc_id=o~msft~docs)。

如果 Azure DevOps 仍无法识别你的订阅，请联系 [Azure DevOps 支持](https://azure.microsoft.com/support/devops/)。

## <a name="resources"></a>资源
[Visual Studio 订阅支持](https://aka.ms/vssubscriberhelp)

## <a name="see-also"></a>另请参阅
- [Visual Studio 文档](/visualstudio/)
- [Azure DevOps 文档](/azure/devops/)
- [Azure 文档](/azure/)
- [Microsoft 365 文档](/microsoft-365/)

## <a name="next-steps"></a>后续步骤 
有关如何使用 Azure、Azure DevOps 或 Visual Studio IDE 的详细信息，请查看以下资源：
- [Azure 开发测试套餐/额度](/azure/devtest/offer/)
- [Azure DevOps](vs-azure-devops.md)
- [Visual Studio](vs-ide-benefit.md)