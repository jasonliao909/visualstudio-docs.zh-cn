---
description: 通常使用项目扩展将应用程序打包Visual Studio 安装程序 MSI。
title: Visual Studio 安装程序项目和 .NET Core 3.1
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
ms.openlocfilehash: 95e3b044c3f4f3ce72e15704874c2d8e03e3a2e3868ead006d1fab0635be9072
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121418403"
---
# <a name="visual-studio-installer-projects-extension-and-net-core-31"></a>Visual Studio 安装程序项目扩展和 NET Core 3.1

通常使用项目扩展将应用程序打包Visual Studio 安装程序 MSI。

可在此处下载扩展：Visual Studio 安装程序[项目](https://marketplace.visualstudio.com/items?itemName=VisualStudioClient.MicrosoftVisualStudio2017InstallerProjects)

## <a name="update-for-net-core"></a>.NET Core 的更新
.NET Core 有两种不同的发布模型。

- 依赖于框架的部署

- 独立应用程序包括运行时。

若要详细了解这些部署策略，请参阅 [.NET Core 应用程序发布概述](/dotnet/core/deploying/)。

### <a name="workflow-changes-for-net-core-31"></a>.NET Core 3.1 的工作流更改

1. 选择 **"发布项** "而不是" **主输出** "，获取 .NET Core 3.1 项目的正确输出。  若要打开此对话框，请从Project菜单中选择"添加输出  >  ..."。

    !["添加输出组Project"中的"发布项"输出组](../deployment/media/installer-projects-net-core-publish-items-output.png "选取发布项")

2. 若要创建自包含安装程序，请对安装项目中的"发布项"节点设置 **PublishProfilePath** 属性，使用具有正确属性集的发布配置文件的相对路径。

    ![在"发布项"项目输出项上设置发布配置文件](../deployment/media/installer-projects-net-core-publish-profile.png "设置发布配置文件")

### <a name="prerequisites-for-net-core-31"></a>.NET Core 3.1 的先决条件

如果希望安装程序能够安装依赖于框架的 .NET Core 3.1 应用所需的运行时，可以使用 [先决条件 来这样做](../deployment/application-deployment-prerequisites.md)。  在安装程序项目的属性对话框中，打开"先决条件 **..."** 对话框，你将看到以下条目：

!["先决条件"对话框中的 .NET Core 项](../deployment/media/installer-projects-net-core-prerequisites.png ".NET Core 系统必备组件")

应为 **控制台应用程序选择".NET Core** 运行时..."选项，应为 WPF/WinForms 应用程序选择 **".NET 桌面** 运行时..."。

>[!NOTE]
>这些项从 2019 Visual Studio 7 版本开始提供。

## <a name="see-also"></a>另请参阅

- [“系统必备”对话框](../ide/reference/prerequisites-dialog-box.md)
- [应用程序部署必备](../deployment/application-deployment-prerequisites.md)
