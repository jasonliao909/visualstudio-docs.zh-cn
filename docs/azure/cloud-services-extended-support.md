---
title: 使用云服务（外延支持）
description: 现在了解如何使用 (和扩展支持) 创建Azure 资源管理器云服务Visual Studio
author: ghogen
manager: jmartens
ms.technology: vs-azure
ms.custom: vs-azure
ms.workload: azure-vs
ms.topic: how-to
ms.date: 01/25/2021
ms.author: ghogen
monikerRange: '>=vs-2019'
ms.openlocfilehash: 547c3b6e81ad1df0f0beffec54a25ad7c0b32ed7
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126602168"
---
# <a name="create-and-deploy-to-cloud-services-extended-support-in-visual-studio"></a>在云中创建 (云服务) 云服务Visual Studio

从[Visual Studio 2019 版本 16.9](https://visualstudio.microsoft.com/vs/)开始，可以使用 Azure 资源管理器 使用云服务，这大大简化了 Azure 资源的维护和管理并实现了现代化。 这由称为云服务的新 Azure 服务启用， (*外延) 。* 可以将现有的云服务发布到云服务（外延支持）。 有关此 Azure 服务的信息，请参阅[云服务（外延支持）文档](/azure/cloud-services-extended-support/overview)。

## <a name="publish-to-cloud-services-extended-support"></a>发布到云服务 (外延) 

将现有 Azure 云服务项目发布到云服务 (外延) ，仍保留发布到经典 Azure 云服务的功能。 在 Visual Studio 2019 版本 16.9 及更高版本中，经典云服务项目具有"发布"命令的特殊版本，即"发布 (**扩展**) "。 此命令显示在 中 **快捷菜单** 解决方案资源管理器。

发布到云服务和外延支持 (存在一些) 。 例如，系统不会询问你是要发布到过渡部署还是生产部署，因为这些部署槽不是外延支持发布模型的一部分。 相反，使用云服务 (外) ，可以设置多个部署，并交换 Azure 门户。 尽管 Visual Studio 工具允许在 16.9 中设置此功能，但交换功能在云服务 (外延支持) 的更高版本之前不会启用，并且可能会导致在预览期间部署时失败。

在将经典 Azure 云服务发布到云服务 (外延) 之前，请检查项目使用的存储帐户，并确保它们存储 V1 或 存储 V2 帐户。 经典存储帐户类型将在部署时失败，并出现错误消息。 请务必检查诊断使用的存储帐户。 若要检查诊断存储帐户，请参阅为虚拟机和Azure 云服务 [设置诊断](vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines.md)。 如果服务使用经典存储帐户，可以升级它;请参阅 [升级到常规用途 v2 存储帐户](/azure/storage/common/storage-account-upgrade?tabs=azure-portal)。  有关存储帐户类型的一般信息，请参阅存储[概述](/azure/storage/common/storage-account-overview)。

### <a name="to-publish-a-classic-azure-cloud-service-project-to-cloud-services-extended-support"></a>若要将经典 Azure 云服务项目发布到云服务， (外延) 

1. 右键单击 Azure 云服务中的项目节点 (经典) ，然后选择"发布" (**扩展) ..."。** 发布 **向导将在** 第一个屏幕上打开。

   ![从菜单中 ("发布) 扩展支持"](./media/cloud-services-extended-support/publish-commands-on-menu.png)

   将显示 **"发布** "向导。

   ![登录页](./media/cloud-services-extended-support/publish-step1.png)

1. **帐户** - 选择一个帐户，或者在帐户下拉列表中选择“添加帐户”。

1. **选择订阅** - 选择要用于部署的订阅。

1. 选择“下一步”，移动到“设置”页 。

   ![通用设置](./media/cloud-services-extended-support/publish-settings.png)

1. **云服务 (扩展支持)** - 使用下拉列表，选择现有的云服务 (扩展支持) ，或选择 **"新建"** 并创建一个。 数据中心在每个云服务的括号中显示 (外延) 。 建议云服务的数据中心位置 (外延) 存储帐户的数据中心位置相同。

   如果选择创建新服务，则会看到"创建云服务" (**扩展)** 对话框。 指定要用于云服务的位置和资源组 (外延) 。

   ![创建云服务 (外延) ](./media/cloud-services-extended-support/extended-support-dialog.png)

1. **生成配置** - 选择“调试”或“发布”。

1. **服务配置** - 选择“云”或“本地”。

1. **存储帐户** - 选择要用于此部署的存储帐户，或者单击“新建”以创建一个存储帐户。 每个存储帐户的区域均显示在括号中。 建议存储帐户的数据中心位置与云服务的数据中心位置相同（常用设置）。

   Azure 存储帐户将存储应用程序部署的包。

1. **Key Vault** - 指定包含此云服务机密的密钥保管库， (外延) 。 如果启用远程桌面，或者将证书添加到配置中，则启用此功能。

1. **为所有角色启用远程桌面** - 如果希望能够远程连接到服务，请选中此选项。 系统会要求你指定凭据。

   ![远程桌面设置](./media/cloud-services-extended-support/remote-desktop-configuration.png)

1. 选择“下一步”，移动到“诊断设置”页面 。

   ![诊断设置](./media/cloud-services-extended-support/diagnostics-settings.png)

   借助诊断，你可以对 Azure 云服务进行故障排除 (扩展支持) 。 有关诊断的详细信息，请参阅 [Configuring Diagnostics for Azure Cloud Services and Virtual Machines](./vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines.md)（为 Azure 云服务和虚拟机配置诊断）。 有关 Application Insights 的信息，请参阅[什么是 Application Insights？](/azure/application-insights/app-insights-overview)。

1. 选择“下一步”，移动到“摘要”页面 。

   ![总结](./media/cloud-services-extended-support/publish-summary.png)

1. **目标配置文件** - 可以选择基于所选的设置创建发布配置文件。 例如，可以创建一个配置文件用于测试环境，并创建另一个配置文件用于生产环境。 要保存此配置文件，请选择 **“保存”** 图标。 向导将创建配置文件并将它保存在 Visual Studio 项目中。 要修改配置文件名称，请打开“目标配置文件”列表，并选择“管理…” 。

   > [!Note]
   > 发布配置文件显示在 解决方案资源管理器 Visual Studio 中，配置文件设置将写入扩展名 *为 .azurePubxml* 的文件。 设置将保存为 XML 标记的属性。

1. 配置项目部署的所有设置后，请选择对话框底部的“发布”。 可以在 Visual Studio 的“Azure 活动日志”输出窗口中监视过程状态。 选择" **在门户中打开"** 链接 

祝贺你！ 你已发布云服务， (项目) Azure。 若要使用相同设置再次进行发布，可以重复使用发布配置文件，或重复这些步骤来创建新的配置文件。 用于Azure 资源管理器 (ARM) 模板和参数保存在 *bin/ \<configuration\> /Publish* 文件夹中。

## <a name="clean-up-azure-resources"></a>清理 Azure 资源

若要按照本教程清理创建的 Azure 资源，请转到 Azure 门户，选择"资源组 ["，](https://portal.azure.com)找到并打开用于创建云服务 (外延支持) 的资源组，然后选择"删除资源组 **"。**

## <a name="next-steps"></a>后续步骤

使用“发布”屏幕上的“配置”按钮设置持续集成 (CI) 。 有关详细信息，请参阅 [Azure Pipelines 文档](/azure/devops/pipelines/?view=azure-devops&preserve-view=true)。
