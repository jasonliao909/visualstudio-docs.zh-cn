---
description: 通常使用 Visual Studio 安装程序项目扩展将应用程序打包为 MSI。
title: Visual Studio 安装程序 Projects 和 .NET 6.0
titleSuffix: ''
ms.date: 02/18/2022
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
ms.openlocfilehash: c7523727b4dabef9ef6b67ff9731509febcd9521
ms.sourcegitcommit: edf8137cd90c67b6078a02c93094f7e1c3bf8930
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/08/2022
ms.locfileid: "139551100"
---
# <a name="visual-studio-installer-projects-extension-and-net-60"></a>Visual Studio 安装程序项目扩展和 .NET 6.0

通常使用 Visual Studio 安装程序项目扩展将应用程序打包为 MSI。

本文适用于面向 .NET Core 3.1、.NET 5 和 .NET 6 的应用。

可在此处下载扩展：

::: moniker range=">= vs-2022"
[Visual Studio 安装程序项目](https://marketplace.visualstudio.com/items?itemName=VisualStudioClient.MicrosoftVisualStudio2022InstallerProjects)
::: moniker-end
::: moniker range="vs-2019"
[Visual Studio 安装程序项目](https://marketplace.visualstudio.com/items?itemName=VisualStudioClient.MicrosoftVisualStudio2017InstallerProjects)
::: moniker-end

## <a name="update-for-net-core"></a>.NET Core 更新

.NET Core 有两种不同的发布模型。

- 依赖框架的部署

- 独立应用程序包括运行时。

若要详细了解这些部署策略，请参阅 [.NET Core 应用程序发布概述](/dotnet/core/deploying/)。

## <a name="create-a-setup-project"></a>创建安装项目

1. 从Visual Studio，选择"**扩展"** > "管理扩展"，然后搜索"Visual Studio 安装程序项目"。 或者，直接从市场下载扩展。

2. 在"开始"窗口中， **选择"创建新** 项目"，然后在搜索框中键入"setup"。 选择一个安装程序项目，然后按照说明进行操作。

   有关详细信息，请参阅 [安装和部署项目](/previous-versions/visualstudio/visual-studio-2010/wx3b589t(v=vs.100))。

### <a name="workflow-changes-for-net-core-31-and-later-versions"></a>.NET Core 3.1 及更高版本的工作流更改

1. 选择 **"发布项** "而不是" **主输出** "，获取 .NET Core 3.1、.NET 5.0 或 .NET 6.0 项目的正确输出。  若要打开此对话框，请从项目的上下文菜单中选择“添加” > “项目输出...”。

    ![“添加项目输出组”对话框中的“发布项”输出组](../deployment/media/installer-projects-net-core-publish-items-output.png "选取发布项")

2. 若要创建独立安装程序，请对设置项目中的“发布项”节点设置“PublishProfilePath”属性，使用设置了正确属性的发布配置文件的相对路径。

    ![在“发布项”项目输出项上设置发布配置文件](../deployment/media/installer-projects-net-core-publish-profile.png "设置发布配置文件")

>[!NOTE]
>ASP.NET Core 应用程序不支持此工作流，仅 Windows 桌面应用程序支持。

### <a name="prerequisites"></a>先决条件

如果希望安装程序能够为依赖框架的 .NET Core 3.1、.NET 5.0 或 .NET 6.0 应用安装所需的运行时，可以使用先决条件来这样做。[](../deployment/application-deployment-prerequisites.md)  在安装程序项目的属性对话框中，打开“必备组件...”对话框，你将看到以下条目：

![“必备组件”对话框中的 .NET Core 项](../deployment/media/installer-projects-net-core-prerequisites.png ".NET Core 系统必备组件")

应为控制台应用程序选择“.NET Core Runtime...”选项，并为 WPF/WinForms 应用程序选择“.NET Desktop Runtime...”。

>[!NOTE]
>这些项从 Visual Studio 2019 Update 7 版本开始提供。

## <a name="see-also"></a>另请参阅

- [“系统必备”对话框](../ide/reference/prerequisites-dialog-box.md)
- [应用程序部署必备](../deployment/application-deployment-prerequisites.md)
