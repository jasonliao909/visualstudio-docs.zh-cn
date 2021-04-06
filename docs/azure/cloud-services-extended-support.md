---
title: " (扩展支持) 使用云服务"
description: 立即了解如何使用 Azure 资源管理器与 Visual Studio 来创建和部署云服务 (扩展) 支持
author: ghogen
manager: jmartens
ms.custom: vs-azure
ms.workload: azure-vs
ms.topic: how-to
ms.date: 01/25/2021
ms.author: ghogen
monikerRange: '>=vs-2019'
ms.openlocfilehash: 289bc88d9aef40fdc260ce84395b1c4b9237c689
ms.sourcegitcommit: 2a50f4c1705baeee5c05580f04e3f468550f44e3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/05/2021
ms.locfileid: "106381591"
---
# <a name="create-and-deploy-to-cloud-services-extended-support-in-visual-studio"></a>在 Visual Studio 中创建和部署到云服务 (扩展支持) 

从 [Visual Studio 2019 版本 16.9](https://visualstudio.microsoft.com/vs/)开始，你可以使用 Azure 资源管理器使用云服务，这大大简化了 azure 资源的维护和港务局的维护和管理。 这是由称为 *云服务 (扩展支持)* 的新 Azure 服务启用的。 可以将现有的云服务发布到云服务（外延支持）。 有关此 Azure 服务的信息，请参阅[云服务（外延支持）文档](/azure/cloud-services-extended-support/overview)。

## <a name="publish-to-cloud-services-extended-support"></a>发布到云服务 (扩展支持) 

将现有的 Azure 云服务项目发布到云服务 () 扩展支持时，仍会保留发布到经典 Azure 云服务的功能。 在 Visual Studio 2019 版本16.9 及更高版本中，经典云服务项目具有特殊版本的 **publish** 命令， **发布 (扩展支持)**。 此命令显示在 **解决方案资源管理器** 的快捷菜单中。

发布到云服务 (扩展支持) 时存在一些差异。 例如，不会询问你是否发布到 **过渡** 或 **生产环境**，因为这些部署槽位不是扩展的支持发布模型的一部分。 相反，通过云服务 (扩展支持) ，你可以设置多个部署，并在 Azure 门户中交换部署。 尽管 Visual Studio 工具允许在16.9 中设置此项，但在更高版本的云服务 (扩展支持) 之前，将不会启用交换功能，并且可能会导致在预览期间部署时出现故障。

在将经典 Azure 云服务发布到云服务 (扩展支持) 之前，请检查项目使用的存储帐户，并确保它们是存储 V1 或存储 V2 帐户。 在部署时，经典存储帐户类型将失败并出现错误消息。 务必检查诊断使用的存储帐户。 若要检查诊断存储帐户，请参阅 [为 Azure 云服务和虚拟机设置诊断](vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines.md)。 如果服务使用经典存储帐户，则可以对其进行升级;请参阅 [升级到常规用途 v2 存储帐户](/azure/storage/common/storage-account-upgrade?tabs=azure-portal)。  有关存储帐户类型的常规信息，请参阅 [存储帐户概述](/azure/storage/common/storage-account-overview)。

### <a name="to-publish-a-classic-azure-cloud-service-project-to-cloud-services-extended-support"></a>若要将经典 Azure 云服务项目发布到云服务 (扩展支持) 

1. 右键单击 Azure 云服务 (经典) 项目中的项目节点，然后选择 " **发布 (扩展支持) ...**"。 **发布向导** 将在第一个屏幕上打开。

   ![从菜单中选择 "发布 (扩展支持") ](./media/cloud-services-extended-support/publish-commands-on-menu.png)

   此时将显示 **发布** 向导。

   ![登录页](./media/cloud-services-extended-support/publish-step1.png)

1. **帐户** - 选择一个帐户，或者在帐户下拉列表中选择“添加帐户”。

1. **选择订阅** - 选择要用于部署的订阅。

1. 选择“下一步”，移动到“设置”页 。

   ![通用设置](./media/cloud-services-extended-support/publish-settings.png)

1. **云服务 (扩展支持)** -使用下拉列表，选择现有的云服务 (扩展的支持) ，或选择 " **新建**"，然后创建一个。 数据中心显示在括号中，每个云服务 (扩展支持) 。 建议云服务的数据中心位置 (扩展支持) 与存储帐户的数据中心位置相同。

   如果选择创建新服务，则会看到 " **创建云服务 (扩展支持)** " 对话框。 指定要用于云服务 (扩展支持) 的位置和资源组。

   ![ (扩展支持创建云服务) ](./media/cloud-services-extended-support/extended-support-dialog.png)

1. **生成配置** - 选择“调试”或“发布”。

1. **服务配置** - 选择“云”或“本地”。

1. **存储帐户** - 选择要用于此部署的存储帐户，或者单击“新建”以创建一个存储帐户。 每个存储帐户的区域均显示在括号中。 建议存储帐户的数据中心位置与云服务的数据中心位置相同（常用设置）。

   Azure 存储帐户将存储应用程序部署的包。

1. **Key vault** -指定包含此云服务的机密的密钥保管库 (扩展支持) 。 如果启用了远程桌面，或者如果已将证书添加到配置中，则会启用此功能。

1. **为所有角色启用远程桌面** - 如果希望能够远程连接到服务，请选中此选项。 系统会要求你指定凭据。

   ![远程桌面设置](./media/cloud-services-extended-support/remote-desktop-configuration.png)

1. 选择“下一步”，移动到“诊断设置”页面 。

   ![诊断设置](./media/cloud-services-extended-support/diagnostics-settings.png)

   通过诊断，可以对 Azure 云服务 (扩展支持) 进行故障排除。 有关诊断的详细信息，请参阅 [Configuring Diagnostics for Azure Cloud Services and Virtual Machines](./vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines.md)（为 Azure 云服务和虚拟机配置诊断）。 有关 Application Insights 的信息，请参阅[什么是 Application Insights？](/azure/application-insights/app-insights-overview)。

1. 选择“下一步”，移动到“摘要”页面 。

   ![总结](./media/cloud-services-extended-support/publish-summary.png)

1. **目标配置文件** - 可以选择基于所选的设置创建发布配置文件。 例如，可以创建一个配置文件用于测试环境，并创建另一个配置文件用于生产环境。 要保存此配置文件，请选择 **“保存”** 图标。 向导将创建配置文件并将它保存在 Visual Studio 项目中。 要修改配置文件名称，请打开“目标配置文件”列表，并选择“管理…” 。

   > [!Note]
   > 发布配置文件显示在 Visual Studio 解决方案资源管理器中，配置文件设置将写入扩展名为 *.azurepubxml* 的文件中。 设置将保存为 XML 标记的属性。

1. 配置项目部署的所有设置后，请选择对话框底部的“发布”。 可以在 Visual Studio 的“Azure 活动日志”输出窗口中监视过程状态。 选择 " **在门户中打开** " 链接到 

祝贺你！ 已将云服务 (扩展支持) 项目发布到 Azure。 若要使用相同设置再次进行发布，可以重复使用发布配置文件，或重复这些步骤来创建新的配置文件。 用于部署的 Azure 资源管理器 (ARM) 模板和参数保存在 *bin/ \<configuration\> /Publish* 文件夹中。

## <a name="clean-up-azure-resources"></a>清理 Azure 资源

若要清理使用本教程创建的 Azure 资源，请参阅 " [Azure 门户](https://portal.azure.com)"，选择 " **资源组**"，查找并打开用于创建云服务 (扩展支持) 的资源组，然后选择 " **删除资源组**"。

## <a name="next-steps"></a>后续步骤

使用“发布”屏幕上的“配置”按钮设置持续集成 (CI) 。 有关详细信息，请参阅 [Azure Pipelines 文档](/azure/devops/pipelines/?view=azure-devops&preserve-view=true)。
