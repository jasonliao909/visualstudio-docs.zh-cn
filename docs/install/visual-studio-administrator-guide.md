---
title: Visual Studio 管理员指南
titleSuffix: ''
description: 详细了解如何在企业环境中部署 Visual Studio。
ms.date: 11/23/2021
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
ms.openlocfilehash: f9c378b732d8a74f8435533958f29a785d23192d
ms.sourcegitcommit: 2281b4f1f8737f263c0d7e55e00b5ec81517327d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/25/2021
ms.locfileid: "133108661"
---
# <a name="visual-studio-administrator-guide"></a>Visual Studio 管理员指南

在企业环境中，系统管理员通常会从网络共享或通过使用系统管理软件向最终用户部署安装。 我们精心设计了 Visual Studio 安装程序引擎，使系统管理员可以创建网络安装位置、预配置安装默认值、在安装过程中部署产品密钥以及管理成功推出的产品更新，从而支持企业部署。

本管理员指南通过各种情境，提供有关在网络环境中进行企业部署的指导。

## <a name="before-you-begin"></a>在开始之前

在组织内部署 Visual Studio 之前，需作出几项决策，完成几项任务：

::: moniker range="=vs-2022"

* 确保每台目标计算机满足[最低安装要求](/visualstudio/releases/2022/system-requirements)。

::: moniker-end

::: moniker range="=vs-2019"

* 确保每台目标计算机满足[最低安装要求](/visualstudio/releases/2019/system-requirements)。

::: moniker-end

::: moniker range="vs-2017"

* 确保每台目标计算机满足[最低安装要求](/visualstudio/productinfo/vs2017-system-requirements-vs)。

::: moniker-end

::: moniker range="=vs-2019"

* 确定安全性和兼容性需求。

  如果公司需要继续使用某一功能集，但仍想获取常规维护安全更新，则应计划使用维护基线。 有关详细信息，请参阅 [Visual Studio 产品生命周期和维护](/visualstudio/releases/2019/servicing-vs2019#support-options-for-enterprise-and-professional-customers)页面以及[在维修基线上更新 Visual Studio](update-servicing-baseline.md)页面的“Enterprise 和 Professional 客户的支持选项”部分。
  
::: moniker-end

::: moniker range=">=vs-2022"

* 确定安全性和兼容性需求。

  如果公司需要继续使用某一功能集，但仍想获取常规维护安全更新，则应计划使用维护基线。 有关详细信息，请参阅 [Visual Studio 产品生命周期和维护](/visualstudio/releases/2019/servicing-vs2022#support-options-for-enterprise-and-professional-customers)页面以及[在维修基线上更新 Visual Studio](update-servicing-baseline.md)页面的“Enterprise 和 Professional 客户的支持选项”部分。
  
::: moniker-end  

* 确定更新模型。

  希望单个[客户端计算机在哪里获得产品更新](/visualstudio/install/update-a-network-installation-of-visual-studio)？ 具体而言，确定是希望客户端从[公司范围的网络布局](/visualstudio/install/create-a-network-installation-of-visual-studio)还是从 Internet 获取更新。
  
  还需要确定是单个用户可以自行更新客户端，还是需要管理员以编程方式更新客户端。 启动更新的任何人都必须拥有计算机的管理权限。 最好在客户端计算机上进行原始安装前做决定。 

  可以使用最新的产品更新来[更新 Visual Studio 的网络布局](/visualstudio/install/create-a-network-installation-of-visual-studio#update-or-modify-your-layout)，以便将它用作 Visual Studio 最新更新的安装点，同时还可用于维护已部署到客户端工作站的安装。 

  利用企业部署工具的组织可以充分利用 Visual Studio 更新在 Microsoft 更新目录和 Windows Server Update Services 上可用这一事实。 有关详细信息，请参阅[启用管理员更新](/visualstudio/install/enabling-administrator-updates)和[应用管理员更新](/visualstudio/install/applying-administrator-updates)。

  对于未连接到 Internet 的计算机，可[以编程方式更新客户端并阻止 Internet 访问](/visualstudio/install/update-a-network-installation-of-visual-studio#programatically-update-a-client-that-doesnt-have-internet-access)，也可以[使用最小布局更新 Visual Studio](update-minimal-layout.md)。 

* 确定公司所需的[工作负载和组件](workload-and-component-ids.md)。

* 确定是否使用[响应文件](automated-installation-with-response-file.md)，从而可以设置安装默认值。

* 确定是否要启用组策略，以及是否要在个人计算机上将 Visual Studio 配置为禁用客户反馈。

## <a name="step-1---download-visual-studio-product-files"></a>第 1 步 - 下载 Visual Studio 产品文件

* [选择要安装的工作负载和组件](workload-and-component-ids.md)。

* [创建 Visual Studio 产品文件的网络布局](create-a-network-installation-of-visual-studio.md)。

## <a name="step-2---build-an-installation-script"></a>第 2 步 - 生成安装脚本

* 生成一个安装脚本，该脚本使用[命令行参数](use-command-line-parameters-to-install-visual-studio.md)[从网络布局将 Visual Studio 安装到客户端计算机](/visualstudio/install/create-a-network-installation-of-visual-studio#install-visual-studio-onto-a-client-machine-from-a-network-installation。

* （可选）[应用批量许可证产品密钥](automatically-apply-product-keys-when-deploying-visual-studio.md)作为安装脚本的一部分，这样用户便无需单独激活软件。

* （可选）[设置影响 Visual Studio 部署和行为的注册表策略](set-defaults-for-enterprise-deployments.md)，例如与其他版本或实例共享的某些包的安装位置、包的缓存位置及是否缓存、是否应启用管理员更新或应如何应用、有哪些更新通道可用及其如何呈现给客户端，以及通知的方式或不出现通知。

* （可选）设置组策略。 还可在个人计算机上[将 Visual Studio 配置为禁用客户反馈](../ide/visual-studio-experience-improvement-program.md)。

## <a name="step-3---deploy-updates"></a>第 3 步 - 部署更新

使用所选部署技术，在目标开发者工作站上执行脚本。  

* [使用所需的 Visual Studio 版本更新网络布局](/visualstudio/install/create-a-network-installation-of-visual-studio.md#update-or-modify-your-layout)

* 使用 Visual Studio [的最新更新刷新客户端计算机](/visualstudio/install/update-a-network-installation-of-visual-studio)。

* 可以使用类似 System Center Configuration Manager 的工具从 Windows Server Update Services 或 Windows 更新目录部署 Visual Studio。 有关详细信息，请参阅[应用管理员更新](applying-administrator-updates.md)。 

## <a name="step-4---optional-use-visual-studio-tools-to-verify-installation"></a>第 4 步 -（可选）使用 Visual Studio 工具验证安装

我们提供了几种工具来帮助你在客户端计算机上[检测和管理安装的 Visual Studio 实例](tools-for-managing-visual-studio-instances.md)。

::: moniker range="vs-2019"

## <a name="advanced-configuration"></a>高级配置

默认情况下，Visual Studio 安装允许从错误列表 F1 和代码链接在必应搜索中包含自定义类型。 可以通过按策略更改以下注册表项的值，将 Visual Studio 配置为禁止搜索机制包括任何自定义用户类型：

**“PutCustomTypeInBingSearch” DWORD 0**

注册表位于专用注册表配置单元的 `Software\Microsoft\VisualStudio\16.0_{InstanceId}\Roslyn\Internal\Diagnostics\` 目录中。 有关如何打开注册表配置单元的说明，请参阅[编辑 Visual Studio 实例的注册表](tools-for-managing-visual-studio-instances.md?view=vs-2019&preserve-view=true#editing-the-registry-for-a-visual-studio-instance)。

::: moniker-end

::: moniker range="vs-2017"

## <a name="advanced-configuration"></a>高级配置

默认情况下，Visual Studio 安装允许从错误列表 F1 和代码链接在必应搜索中包含自定义类型。 可以通过按策略更改以下注册表项的值，将 Visual Studio 配置为禁止搜索机制包括任何自定义用户类型：

**“PutCustomTypeInBingSearch” DWORD 0**

注册表位于专用注册表配置单元的 `Software\Microsoft\VisualStudio\15.0_{InstanceId}\Roslyn\Internal\Diagnostics\` 目录中。 有关如何打开注册表配置单元的说明，请参阅[编辑 Visual Studio 实例的注册表](tools-for-managing-visual-studio-instances.md?view=vs-2017&preserve-view=true#editing-the-registry-for-a-visual-studio-instance)。

::: moniker-end

[!INCLUDE[install_get_support_md](includes/install_get_support_md.md)]

## <a name="see-also"></a>请参阅

* [启用管理员更新](enabling-administrator-updates.md)
* [应用管理员更新](applying-administrator-updates.md)
* [命令行参数示例](command-line-parameter-examples.md)
* [安装 Visual Studio 脱机安装所需的证书](install-certificates-for-visual-studio-offline.md)
* [导入或导出安装配置](import-export-installation-configurations.md)
* [Visual Studio 安装存档](https://devblogs.microsoft.com/setup/tag/vs2017/)
* [Visual Studio 产品生命周期和维护](/visualstudio/releases/2019/servicing/)
* [同步自动加载设置](../extensibility/synchronously-autoloaded-extensions.md)
