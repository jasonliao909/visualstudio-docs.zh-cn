---
title: Visual Studio 订阅中的 Microsoft Azure 权益 | Microsoft Docs
author: evanwindom
ms.author: cabuschl
manager: cabuschl
ms.assetid: 872c5746-5357-4764-949b-aa525a0adf1a
ms.date: 10/14/2021
ms.topic: how-to
description: 了解如何激活 Visual Studio 订阅中包含的 Azure 开发测试个人额度权益。
ms.openlocfilehash: b76d87792fc96021206552e14c78634b546f55f0
ms.sourcegitcommit: a8e6a8c6ca36dc76cdc44d1db934eae43470b5fa
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/15/2021
ms.locfileid: "130030279"
---
# <a name="use-microsoft-azure-in-visual-studio-subscriptions"></a>在 Visual Studio 订阅中使用 Microsoft Azure
Visual Studio 订阅者无需额外付费即可使用 Microsoft Azure。  通过[每月 Azure 开发测试个人额度](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/)，可将 Azure 用作开发/测试的个人沙盒。  你可以预配虚拟机、云服务和其他 Azure 资源。  信用额度因订阅级别而异。

## <a name="activation-steps"></a>激活步骤
1. 登录到 [https://my.visualstudio.com/benefits](https://my.visualstudio.com/benefits?wt.mc_id=o~msft~docs)。

2. 在“权益”页上的“工具”部分中找到“Azure”磁贴，然后选择“权益”磁贴底部的“激活”链接。
   > [!div class="mx-imgBorder"]
   > ![Azure 磁贴](_img/vs-azure/vs-azure-tile.png "单击 Azure 磁贴上的“激活”按钮即可开始使用。")

3. 如果没有现有的 Azure 订阅，系统将要求你填写所需信息以创建 Azure 订阅。  第一步是提供个人信息，然后选择“下一步”。
   > [!div class="mx-imgBorder"]
   > ![Azure 注册](_img/vs-azure/vs-azure-about-you.png "将你的个人联系信息添加到 Azure 订阅。")

4. 接下来，需要使用简单的验证码验证身份。 提供电话号码，并选择是通过短信还是电话接收代码。  输入收到的代码，选择“验证代码”。   
   > [!div class="mx-imgBorder"]
   > ![Azure 准备工作](_img/vs-azure/vs-azure-identity.png "请求验证码，然后输入该验证码以继续。")

5. 最后一步，选中复选框以接受条款，然后选择“注册”。  就这么简单！
   > [!div class="mx-imgBorder"]
   > ![Azure 注册](_img/vs-azure/vs-azure-agreement.png "单击“注册”按钮，完成 Azure 订阅的创建。")

0. Azure 仪表板快速入门中心将加载。  
   > [!div class="mx-imgBorder"]
   > ![Azure 仪表板](_img/vs-azure/vs-azure-quick-start.png "创建 Azure 订阅后，将重定向到 Azure 门户。") 

0. 可将 [Azure 门户](https://portal.azure.com)收藏为书签，方便日后访问。

## <a name="maintain-a-subscription-to-use-monthly-credits"></a>维护订阅以使用每月额度
如果你的 Visual Studio 订阅到期或被删除，所有订阅权益（包括每月 Azure 开发/测试单独额度）将不再可用。 若要在有每月额度的情况下继续使用 Azure，你需要续订订阅、购买新订阅，以及/或者将 Azure 资源转移到另一个包含 Azure 开发/测试个人额度的 Azure 订阅。  

> [!IMPORTANT]
> 在当前 Azure 订阅被禁用之前，必须将资源转移到另一个 Azure 订阅，否则你将无法访问数据。  

可以通过多种方式继续使用 Azure 的每月额度。  要保存 Azure 资源，无论你在下面选择什么操作，都需要[将资源转移到另一个 Azure 订阅](/azure/azure-resource-manager/management/move-resource-group-and-subscription)。 

- 如果直接购买 Visual Studio 订阅，请通过 Microsoft Store 购买新订阅或续订订阅。  
    - [Visual Studio Enterprise](https://www.microsoft.com/p/visual-studio-enterprise-subscription/dg7gmgf0dst4?activetab=pivot%3aoverviewtab)
    - [Visual Studio Professional](https://www.microsoft.com/p/visual-studio-professional-subscription/dg7gmgf0dst3?activetab=pivot%3aoverviewtab)
    - [Visual Studio Test Professional](https://www.microsoft.com/p/visual-studio-test-professional-subscription/dg7gmgf0dst6?activetab=pivot%3aoverviewtab)
- 如果组织中的某个人代表组织购买订阅，请[联系组织的 Visual Studio 订阅管理员](./contact-my-admin.md)，并申请包含所需每月额度的订阅。  
- 如果你有另一个活动的 Visual Studio 订阅（在同一订阅级别），则可以使用它设置新的 Azure 额度订阅。  

请通过以下资格表来确定各订阅类型包含多少额度。  


## <a name="convert-your-azure-subscription-to-pay-as-you-go"></a>将 Azure 订阅转换为即用即付类型
如果不再需要 Visual Studio 订阅或额度，但要继续使用 Azure 资源，请[将资源移到另一个 Azure 订阅](/azure/azure-resource-manager/management/move-resource-group-and-subscription)，或通过[删除支出限制](/azure/cost-management-billing/manage/spending-limit#remove-the-spending-limit-in-azure-portal)将 Azure 订阅转换为即用即付定价。 

如果你未执行上述任何操作，你的 Azure 订阅会在电子邮件通知中的指定时间被禁用。  如果禁用了订阅，则可以按照[这些步骤](https://docs.microsoft.com/azure/cost-management-billing/manage/switch-azure-offer)将其重新启用为即用即付订阅。

## <a name="have-a-question"></a>遇到问题？
如果你有关于转移资源、删除支出限制或其他 Azure 主题的问题，可以在 Azure 门户中[提交 Azure 支持请求](https://portal.azure.com/#blade/Microsoft_Azure_Support/HelpAndSupportBlade/overview)。 

## <a name="eligibility"></a>资格
|                 订阅级别/计划                 |           好处           |                         是否续订？                          |
|--------------------------------------------------------------|-----------------------------|-------------------------------------------------------------|
|              Visual Studio Enterprise Standard               |     150 美元月信用额度     |                             是                             |
|              包含 GitHub Enterprise 的 Visual Studio Enterprise 订阅               |     150 美元月信用额度     |                             是                             |
|               Visual Studio Enterprise 月度               |        不可用        |                                                             |
|             Visual Studio Professional Standard              |     50 美元月信用额度      |                             是
|              包含 GitHub Enterprise 的 Visual Studio Professional 订阅              |     50 美元月信用额度     |                             是                             |
|              Visual Studio Professional 月度              |        不可用        |                                                             |
|                    Visual Studio Test Pro                    |     50 美元月信用额度      |                             是                             |
|                        MSDN 平台                        |     100 美元月信用额度     |                             是                             |
|               Visual Studio Enterprise - NFR<sup>1</sup>                 |     150 美元月信用额度     |                             是                             |
|                Visual Studio Enterprise - FTE                |     150 美元月信用额度     |                             是                             |
|     Visual Studio Enterprise - Microsoft 合作伙伴网络     |     150 美元月信用额度     |                             是                             |
|    Visual Studio Professional - Microsoft 合作伙伴网络    |        不可用        |                                                             |
|        Visual Studio Enterprise – Imagine（标准）         |        不可用        |                                                             |
|         Visual Studio Enterprise – Imagine（高级）         |        不可用        |                                                             |
|             Visual Studio Enterprise – BizSpark              |     150 美元月信用额度     |                             是                             |
|      Visual Studio Enterprise – MCT 软件和服务      |     100 美元月信用额度     |                             是                             |
| Visual Studio Enterprise – MCT 软件和服务开发人员 |     150 美元月信用额度     |                             是                             |

<sup>1</sup>  *包括：不得转售 (NFR)、最有价值专家 (MVP)、区域总监 (RD)、Visual Studio 行业合作伙伴 (VSIP) 不包括：  NFR Basic*

> [!NOTE]
> Microsoft 不再在云订阅中提供 Visual Studio Professional 年度订阅和 Visual Studio Enterprise 年度订阅。 现有客户体验以及续订、增加、减少或取消订阅的能力不会发生变化。 建议新客户访问 [https://visualstudio.microsoft.com/vs/pricing/](https://visualstudio.microsoft.com/vs/pricing/)，查看各 Visual Studio 购买选项。

无法确定正在使用哪些订阅？  连接到 [https://my.visualstudio.com/subscriptions](https://my.visualstudio.com/subscriptions?wt.mc_id=o~msft~docs)，查看分配给电子邮件地址的所有订阅。 如果没有看到所有订阅，则可能是有一个或多个订阅分配给了不同的电子邮件地址。  你需要使用其他电子邮件地址登录来查看那些订阅。

## <a name="frequently-asked-questions"></a>常见问题
### <a name="q-how-do-i-submit-a-technical-support-incident-from-within-the-azure-portal"></a>问：如何从 Azure 门户提交技术支持事件？
答：从 Azure 门户提交支持事件是一个三步过程。
1. 激活技术支持权益，并获取合同 ID 访问 ID。
2. 将支持合同链接到 Azure 订阅。
3. 提交支持事件。

有关完整详细信息，请访问[技术支持](vs-tech-support.md)文档。

### <a name="q-who-owns-the-intellectual-property-i-create-using-my-azure-devtest-individual-credit"></a>问：谁拥有我使用我的 Azure DevTest 个人点数创建的知识产权？
答：员工根据该公司提供的资源创建的知识产权是提供该资源的公司的知识产权。 因此，如果你通过你的雇主接收 Visual Studio 订阅，则其知识产权政策适用。 

### <a name="q-how-can-i-find-out-what-my-azure-credit-balance-is"></a>问：如何查明我的 Azure 额度余额是多少？
答：若要监视余额并了解有关 Azure 额度的其他有用信息，请参阅[跟踪 Microsoft 客户协议 Azure 额度余额](https://docs.microsoft.com/azure/cost-management-billing/manage/mca-check-azure-credits-balance?tabs=portal)。

## <a name="support-resources"></a>支持资源
- 需要与 Azure 有关的帮助？  请参阅下列资源：
  - 技术支持：[https://azure.microsoft.com/support/options/](https://azure.microsoft.com/support/options/)
  - [Azure 提示与技巧](https://microsoft.github.io/AzureTipsAndTricks/ "Azure 提示与技巧") 
- 有关 Visual Studio 订阅的销售、订阅、帐户和账单的帮助，请与 Visual Studio [订阅支持](https://aka.ms/vssubscriberhelp)联系。
- 对有关 Visual Studio IDE、Azure DevOps Services 或其他 Visual Studio 产品或服务有疑问？  请访问 [Visual Studio 支持](https://visualstudio.microsoft.com/support/)。

## <a name="see-also"></a>请参阅
- [Visual Studio 文档](/visualstudio/)
- [Azure DevOps 文档](/azure/devops/)
- [Azure 文档](/azure/)
- [Microsoft 365 文档](/microsoft-365/)

## <a name="next-steps"></a>后续步骤
有关 Microsoft 工具和服务的详细信息，请查看针对以下内容的相关文档：
- [Azure](/azure/)
- [Azure DevOps](/azure/devops/)
- [Visual Studio IDE](/visualstudio/)