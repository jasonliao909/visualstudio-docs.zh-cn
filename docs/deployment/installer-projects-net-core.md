---
description: 通常使用 Visual Studio 安装程序项目扩展将应用程序打包为 MSI。
title: Visual Studio 安装程序项目和 .NET Core 3.1 和 .NET 5.0
titleSuffix: ''
ms.date: 08/18/2020
ms.topic: conceptual
helpviewer_keywords:
- installer projects
- installer projects, .NETCore
author: MSLukeWest
ms.author: lukewest
manager: MSLukeWest
monikerRange: '>= vs-2019'
ms.workload:
- multiple
ms.openlocfilehash: d1c756ce38a397b3dc7fe94a0d2627f1a55da9c2
ms.sourcegitcommit: 8e74969ff61b609c89b3139434dff5a742c18ff4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/24/2021
ms.locfileid: "128426395"
---
# <a name="visual-studio-installer-projects-extension-and-net-core-31--net-50"></a>Visual Studio 安装程序项目扩展和 .NET Core 3.1 / .NET 5.0

通常使用 Visual Studio 安装程序项目扩展将应用程序打包为 MSI。

可在此处下载扩展：[Visual Studio 安装程序项目](https://marketplace.visualstudio.com/items?itemName=VisualStudioClient.MicrosoftVisualStudio2017InstallerProjects)

## <a name="update-for-net-core"></a>.NET Core 更新
.NET Core 有两种不同的发布模型。

- 依赖框架的部署

- 独立应用程序包括运行时。

若要详细了解这些部署策略，请参阅 [.NET Core 应用程序发布概述](/dotnet/core/deploying/)。

### <a name="workflow-changes-for-net-core-31-and-net-50"></a>.NET Core 3.1 和 .NET 5.0 的工作流更改

1. 选择“发布项”而不是“主输出”，获取 .NET Core 3.1 和 .NET 5.0 项目的正确输出。  若要打开此对话框，请从项目的上下文菜单中选择“添加” > “项目输出...”。

    ![“添加项目输出组”对话框中的“发布项”输出组](../deployment/media/installer-projects-net-core-publish-items-output.png "选取发布项")

2. 若要创建独立安装程序，请对设置项目中的“发布项”节点设置“PublishProfilePath”属性，使用设置了正确属性的发布配置文件的相对路径。

    ![在“发布项”项目输出项上设置发布配置文件](../deployment/media/installer-projects-net-core-publish-profile.png "设置发布配置文件")

>[!NOTE]
>ASP.NET Core 应用程序不支持此工作流，仅 Windows 桌面应用程序支持。

### <a name="prerequisites-for-net-core-31-and-net-50"></a>.NET Core 3.1 和 .NET 5.0 的必备组件

如果希望安装程序能够为依赖框架的 .NET Core 3.1 或 .NET 5.0 应用安装所需的运行时，可以使用[必备组件](../deployment/application-deployment-prerequisites.md)执行此操作。  在安装程序项目的属性对话框中，打开“必备组件...”对话框，你将看到以下条目：

![“必备组件”对话框中的 .NET Core 项](../deployment/media/installer-projects-net-core-prerequisites.png ".NET Core 系统必备组件")

应为控制台应用程序选择“.NET Core Runtime...”选项，并为 WPF/WinForms 应用程序选择“.NET Desktop Runtime...”。

>[!NOTE]
>这些项从 Visual Studio 2019 Update 7 版本开始提供。

## <a name="see-also"></a>另请参阅

- [“系统必备”对话框](../ide/reference/prerequisites-dialog-box.md)
- [应用程序部署必备](../deployment/application-deployment-prerequisites.md)
