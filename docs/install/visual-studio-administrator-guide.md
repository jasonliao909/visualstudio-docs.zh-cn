---
title: Visual Studio 管理员指南
titleSuffix: ''
description: 详细了解如何在企业环境中部署 Visual Studio。
ms.date: 3/3/2022
ms.topic: overview
helpviewer_keywords:
- network installation, Visual Studio
- administrator guide, Visual Studio
- installing Visual Studio, administrator guide
ms.assetid: 4af353f5-6cfd-4ebe-bcfb-f42306e451a0
author: anandmeg
ms.author: meghaanand
manager: jmartens
ms.workload:
- multiple
ms.prod: visual-studio-windows
ms.technology: vs-installation
ms.openlocfilehash: ee2d852f1c4e45abe4af9d66a15431ab985b01f5
ms.sourcegitcommit: edf8137cd90c67b6078a02c93094f7e1c3bf8930
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/08/2022
ms.locfileid: "139552377"
---
# <a name="visual-studio-administrator-guide"></a>Visual Studio 管理员指南

在企业环境中，系统管理员通常会在最终用户计算机上部署和更新软件。 Visual Studio 产品通过向系统管理员提供管理和控制 Visual Studio 软件部署和更新的时间和方式的能力，使其在这些类型的环境中很好地集成。 Visual Studio 可以从 internet、网络共享或产品缓存中获取，也可以通过编程方式或通过使用系统管理软件来手动部署和更新。 Visual Studio 提供了创建和维护获取位置、预配置安装默认值、在安装过程中部署产品密钥以及在成功推出后管理产品更新的能力。 本管理员指南提供了有关企业部署的基于方案的指南的快速链接。

## <a name="research-and-plan-before-you-begin"></a>开始之前的研究和规划

你需要制定计划以了解如何在组织中部署 Visual Studio。 下表列出了一些需要考虑的关键因素，最好是在客户端计算机上进行初始安装之前进行规划和决策。 

::: moniker range="=vs-2022"

- 确保每台目标计算机满足[最低安装要求](/visualstudio/releases/2022/system-requirements)。 请注意，Visual Studio 不支持应用程序虚拟化解决方案，如 Microsoft app-v 或 .msix for Windows 或第三方应用虚拟化技术。

::: moniker-end

::: moniker range="=vs-2019"

- 确保每台目标计算机满足[最低安装要求](/visualstudio/releases/2019/system-requirements)。 请注意，Visual Studio 不支持应用程序虚拟化解决方案，如 Microsoft app-v 或 .msix for Windows 或第三方应用虚拟化技术。

::: moniker-end

::: moniker range="vs-2017"

- 确保每台目标计算机满足[最低安装要求](/visualstudio/productinfo/vs2017-system-requirements-vs)。 请注意，Visual Studio 不支持应用程序虚拟化解决方案，如 Microsoft app-v 或 .msix for Windows 或第三方应用虚拟化技术。

::: moniker-end

- 阐明您的安全性和兼容性需求。 是否需要确保你的组织始终运行最新和最安全的软件？   

::: moniker range="=vs-2019"

如果公司需要继续使用某一功能集，但仍想获取常规维护安全更新，则应计划使用维护基线。 有关安全基线的详细信息，请参阅 [Visual Studio 产品生命周期和服务](/visualstudio/releases/2019/servicing-vs2019#support-options-for-enterprise-and-professional-customers)页的 **支持选项 Enterprise 和 Professional 客户** 部分。  
  
::: moniker-end

::: moniker range=">=vs-2022"

如果公司需要继续使用某一功能集，但仍想获取常规维护安全更新，则应计划使用维护基线。 有关详细信息，请参阅 [Visual Studio 产品生命周期和维护](/visualstudio/releases/2022/servicing-vs2022#enterprise-professional-and-build-tools-editions-support)页面的“Enterprise 和 Professional 客户的支持选项”部分。  
  
::: moniker-end  

- 确定更新模型。

   - 你的客户端计算机从何处获取产品更新？ 换句话说，他们是否应从 IT 托管的 [公司范围的网络布局](update-a-network-installation-of-visual-studio.md)获取更新，或者是否应该从 internet 获取更新？ 这通常取决于客户端是否有权访问 internet。
   - 允许 Who 更新客户端计算机？ 请记住，启动更新的任何人都必须在计算机上具有管理权限。 是否允许用户更新其计算机，或管理员是否需要集中或以编程方式调用它？ 
   - 何时应进行更新？ 是否应将其留给用户决定何时进行更新，或者你是否希望在更新发生时强制实施中心 IT 控制？  

- 决定是否要在客户端计算机上配置组策略设置。  

- 确定公司所需的[工作负载和组件](workload-and-component-ids.md)。  

- 按照 [Windows 安全基线](/windows/security/threat-protection/windows-security-baselines)的说明操作。 Microsoft 专注于为客户提供安全的操作系统（如 Windows 10 和 Windows Server）以及安全的应用（如 Microsoft Edge）。 除了产品的安全保障，Microsoft 还通过提供各种配置功能使你良好地控制环境。

## <a name="install-visual-studio"></a>安装 Visual Studio

以下资源将帮助你在常见的企业方案中进行 Visual Studio 的初始安装。

- **[查看安装 Visual Studio 文档](install-visual-studio.md)** 以大致了解最终用户可用的安装选项。 选择要在客户端计算机上安装的[工作负载和组件](workload-and-component-ids.md)。  

- **[获取正确的 Visual Studio 引导程序以安装该产品](/visualstudio/install/create-a-network-installation-of-visual-studio#download-the-visual-studio-bootstrapper-to-create-the-network-layout)。** 您可以选择不同的引导程序。 有些引导程序安装产品的特别版本，而其他引导程序则初始化服务基准通道。 

- **[使用命令行参数安装 Visual Studio](use-command-line-parameters-to-install-visual-studio.md)** 。 使用多种参数以编程方式控制或自定义 Visual Studio 安装。 你可以构建自动执行安装过程的安装脚本。 有关详细信息，请参阅[命令行参数示例](command-line-parameter-examples.md)。

- **[创建 Visual Studio 布局 (网络安装)](create-a-network-installation-of-visual-studio.md)**。 布局是网络上某个文件夹中 Visual Studio 文件的缓存，可用于初始安装和所有产品更新。 如果客户端计算机的 internet 连接受到限制，则可以使用布局。 您可以使用 [响应文件](automated-installation-with-response-file.md)，这允许您在 [安装到客户端计算机](create-a-network-installation-of-visual-studio.md#install-visual-studio-onto-a-client-machine-from-a-network-installation)时设置默认值。 你还可以配置希望[布局在客户端更新设置对话框中的显示](/visualstudio/install/set-defaults-for-enterprise-deployments?#configuring-source-location-for-updates)方式。 创建布局后，应 [定期维护](create-a-network-installation-of-visual-studio.md#update-or-modify-your-layout)。 

- [安装脱机安装所需的证书](/visualstudio/install/install-certificates-for-visual-studio-offline)。 如果客户端计算机已与 Internet 完全断开连接，则安装所需的证书。

- **[部署 Visual Studio 时，自动应用产品或订阅密钥](automatically-apply-product-keys-when-deploying-visual-studio.md)**。 您可以以编程方式将订阅或产品密钥应用于用于自动部署 Visual Studio 的脚本的一部分，这样用户就不需要单独激活软件。 可以在安装 Visual Studio 期间或安装完成后设置此项。 

- **[在防火墙或代理服务器后面安装和使用 Visual Studio 和 Azure 服务](install-and-use-visual-studio-behind-a-firewall-or-proxy-server.md)** 。 如果你的组织使用防火墙或代理服务器等安全措施，则包含有可能需要将其添加到“允许列表”的域 URL，以及可能需要打开的端口和协议，以便在安装和使用 Visual Studio 以及 Azure 服务时获得最佳体验。 


## <a name="update-visual-studio"></a>更新 Visual Studio

以下资源将帮助你保持 Visual Studio 更新、当前和安全。

- **[查看更新 Visual Studio 文档](update-visual-studio.md)** 以大致了解最终用户可用的更新选项，以及如何通知最终用户有更新可用。  

- 如果要严格控制更新的时间和位置，**[请确保已正确配置了服务基线](/visualstudio/install/update-servicing-baseline)**。

- [使用 Microsoft Endpoint Configuration Manager (SCCM) 启用管理员更新](enabling-administrator-updates.md)。  Visual Studio 更新包含在 [Microsoft 更新目录](https://www.catalog.update.microsoft.com/Home.aspx)和 [Windows Server Update Services (WSUS)](/windows-server/administration/windows-server-update-services/get-started/windows-server-update-services-wsus) 中。 [在客户端计算机上启用](enabling-administrator-updates.md#encoding-administrator-intent-on-the-client-machines)管理员更新后，Enterprise 管理员可使用标准部署工具（例如 Microsoft Endpoint Configuration Manager (SCCM) ）[分发并应用这些更新以 Visual Studio 客户端计算机](../install/applying-administrator-updates.md)。 请注意，如果客户端连接到 internet 或布局，则管理员更新工作。  

- **[保持布局 (网络安装) 定期更新](create-a-network-installation-of-visual-studio.md#update-or-modify-your-layout)** ，使其保持最新，并使用最新的产品更新来保证其安全性。 布局旨在用作 Visual Studio 的新客户端安装的安装点，以及已部署到客户端工作站的安装的更新产品位源。 Visual Studio 在每月的第二个星期二发布修补程序，我们强烈建议你按每月节奏更新你的布局。

- **[使用命令行参数更新 Visual Studio](use-command-line-parameters-to-install-visual-studio.md)**。 使用多种参数以编程方式更新 Visual Studio。 有关详细信息，请参阅[命令行参数示例](command-line-parameter-examples.md)。

- **[更新基于网络布局的客户端计算机](update-a-network-installation-of-visual-studio.md)**。 更新布局后，可以从更新的网络布局中更新 Visual Studio 的客户端安装。 此方案还适用于通过 SCCM 和 WSUS 分布式更新时的工作。 
 
- **对于未连接到 internet 的计算机**，可以 [通过编程方式更新客户端并阻止 internet 访问](update-a-network-installation-of-visual-studio.md#programatically-update-a-client-that-doesnt-have-internet-access)，也可以 [使用最小脱机布局更新 Visual Studio](update-minimal-layout.md)。 


## <a name="configure-visual-studio"></a>配置 Visual Studio

- **[设置影响 Visual Studio 部署和行为的注册表策略](set-defaults-for-enterprise-deployments.md)**，如安装与其他版本或实例共享的某些包的位置、是否缓存包、是否应启用管理员更新、是否应启用管理员更新、更新通道的显示方式以及通知显示或不显示的方式。

* **[将 Visual Studio 配置为](../ide/visual-studio-experience-improvement-program.md)** 在单个计算机上禁用客户反馈。

- **[创建自定义引导程序包](../deployment/creating-bootstrapper-packages.md)**。 了解有关如何创建自定义引导程序包以通过创建产品和程序包清单进一步控制安装配置的高级方法。 

* **[导入或导出](import-export-installation-configurations.md)** 到其他计算机或布局的安装配置。


## <a name="manage-modify-or-repair-visual-studio"></a>管理、修改或修复 Visual Studio

- **[检测、验证和管理](tools-for-managing-visual-studio-instances.md)** 客户端计算机上安装的 Visual Studio 实例。

- **[获取故障排除提示](troubleshooting-installation-issues.md)** 。 在安装或更新 Visual Studio 时获得帮助，并了解在遇到问题时如何报告问题。 这些提示包含可解决大多数联机或脱机安装问题的分步说明。 

- **[修复 Visual Studio](repair-visual-studio.md) 以解决更新问题**。 Visual Studio 安装有时会损毁或损坏。 修复对于修复所有安装操作（包括更新）中的安装时问题非常有用。 


[!INCLUDE[install_get_support_md](includes/install_get_support_md.md)]

## <a name="see-also"></a>另请参阅

* [启用管理员更新](enabling-administrator-updates.md)
* [应用管理员更新](applying-administrator-updates.md)
* [命令行参数示例](command-line-parameter-examples.md)
* [安装 Visual Studio 脱机安装所需的证书](install-certificates-for-visual-studio-offline.md)
* [Visual Studio 产品生命周期和维护](/visualstudio/releases/2019/servicing/)
* [同步自动加载设置](../extensibility/synchronously-autoloaded-extensions.md)
