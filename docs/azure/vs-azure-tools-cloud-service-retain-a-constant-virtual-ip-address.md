---
title: 为 Azure 云服务保留固定的虚拟 IP
description: 了解如何确保 Azure 云服务的虚拟 IP 地址 (VIP) 不更改。
ms.custom: SEO-VS-2020
author: ghogen
manager: jmartens
ms.technology: vs-azure
ms.workload: azure-vs
ms.topic: how-to
ms.date: 03/21/2017
ms.author: ghogen
ms.openlocfilehash: b29f7b4380233a510fb34c3e72cf2aac9b948ba1
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126602160"
---
# <a name="retain-a-constant-virtual-ip-address-for-an-azure-cloud-service"></a>为 Azure 云服务保留固定的虚拟 IP 地址
更新托管于 Azure 中的云服务时，可能需要确保该服务的虚拟 IP 地址 (VIP) 不发生更改。 许多域管理服务使用域名系统 (DNS) 注册域名。 仅当 VIP 保持不变时，DNS 才适用。 可使用 Azure Tools 中的 **发布向导** 来确保云服务的 VIP 在更新时不更改。 有关如何将 DNS 域管理用于云服务的详细信息，请参阅[为 Azure 云服务配置自定义域名](/azure/cloud-services/cloud-services-custom-domain-name-portal)。

## <a name="publish-a-cloud-service-without-changing-its-vip"></a>发布云服务，而不更改其 VIP
在特定环境（如生产环境）中第一次将云服务部署到 Azure 时，其 VIP 就已分配。 VIP 仅会在显式删除部署或部署更新过程将其隐式删除时发生更改。 若要保留 VIP，则切勿删除部署，且务必确保 Visual Studio 不会自动删除部署。

可以在 **发布向导** 中指定部署设置，该向导支持多个部署选项。 可以指定全新部署或更新部署，后者可以是增量更新或同时更新。 这两种更新部署都将保留 VIP。 有关这些不同类型的部署的定义，请参阅 [Publish Azure application wizard](vs-azure-tools-publish-azure-application-wizard.md)（发布 Azure 应用程序向导）。 此外，还可以控制出错时是否删除云服务以前的部署。 如果未正确设置该选项，VIP 可能会发生意外改变。

## <a name="update-a-cloud-service-without-changing-its-vip"></a>更新云服务，而不更改其 VIP
1. 在 Visual Studio 中创建或打开 Azure 云服务项目。

2. 在“解决方案资源管理器”中，右键单击项目。 在快捷菜单上，选择“发布”。

    ![发布菜单](./media/vs-azure-tools-cloud-service-retain-a-constant-virtual-ip-address/solution-explorer-publish-menu.png)

3. 在“发布 Azure 应用程序”对话框中，选择要部署的 Azure 订阅。 必要时进行登录，并选择“下一步”。

    ![发布 Azure 应用程序“登录”页](./media/vs-azure-tools-cloud-service-retain-a-constant-virtual-ip-address/azure-publish-signin.png)

4. 在“常用设置”选项卡中，验证要部署到的云服务的名称、“环境”、“生成配置”和“服务配置”是否全部正确。

    ![发布 Azure 应用程序“常用设置”选项卡](./media/vs-azure-tools-cloud-service-retain-a-constant-virtual-ip-address/azure-publish-common-settings.png)

5. 在“高级设置”选项卡上，确认“部署标签”和“存储帐户”正确无误。 确认“失败时删除部署”复选框处于未选中状态，并确认“部署更新”复选框处于选中状态。 通过清除“失败时删除部署”复选框，确保部署期间出错时不会丢失 VIP。 通过选中“部署更新”复选框，确保重新发布应用程序时不会删除部署且不会丢失 VIP。

    ![发布 Azure 应用程序“高级设置”选项卡](./media/vs-azure-tools-cloud-service-retain-a-constant-virtual-ip-address/azure-publish-advanced-settings.png)

6. 若要进一步指定要更新角色的方式，请选择“部署更新”旁边的“设置”。 选择“增量更新”或“同时更新”，并选择“确定”。 选择“增量更新”会逐个更新应用程序的每个实例，以使应用程序始终可用。 选择“同时更新”会同时更新应用程序的所有实例。 同时更新速度更快，但在更新过程中服务可能不可用。 完成后，选择“下一步”。

    ![发布 Azure 应用程序“部署设置”页](./media/vs-azure-tools-cloud-service-retain-a-constant-virtual-ip-address/azure-publish-deployment-update-settings.png)

7. 在“发布 Azure 应用程序”对话框中，选择“下一步”，直到显示“摘要”页。 验证设置，并选择“发布”。

    ![发布 Azure 应用程序“摘要”页](./media/vs-azure-tools-cloud-service-retain-a-constant-virtual-ip-address/azure-publish-summary.png)

## <a name="next-steps"></a>后续步骤
- [使用 Visual Studio“发布 Azure 应用程序”向导 | Microsoft Docs](vs-azure-tools-publish-azure-application-wizard.md)
