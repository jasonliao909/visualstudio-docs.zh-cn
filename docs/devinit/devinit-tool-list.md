---
title: 可用工具
description: 可用于自定义开发环境的所有 devinit 工具的列表。
ms.date: 02/08/2021
ms.topic: reference
author: andysterland
ms.author: andster
manager: jmartens
ms.workload:
- multiple
monikerRange: '>= vs-2019'
ms.prod: visual-studio-windows
ms.technology: devinit
ms.openlocfilehash: 482e838edf47d63235f60f013bd18eff586f83e8
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "127833050"
---
# <a name="available-tools"></a>可用工具

> [!IMPORTANT]
> 从 2021 年 4 月 12 日开始，将不再支持从 Visual Studio 2019 连接到 GitHub Codespaces，此个人预览版已结束。 我们的工作重点是改进云支持型内部循环和针对多种 Visual Studio 工作负载优化的 VDI 解决方案的体验。 在此期间，`devinit` 和关联工具将不再可用。 建议参与 Visual Studio 的开发人员社区论坛，了解未来要推出的预览版和路线图信息。

下表包含 devinit 的所有当前可用工具的列表。

| 工具                                                                                             | 说明                                                                                                 |
|--------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------|
| [**azurecli-login**](tool-azurecli-login.md)                                                     | 用于执行 Azure CLI 命令 `az login --device-code` 的工具。                                             |
| [**choco-install**](tool-choco-install.md)                                                       | 用于安装 chocolatey 包的工具。                                                                        |
| [**choco-upgrade**](tool-choco-upgrade.md)                                                       | 用于升级 chocolatey 包的工具。                                                                        |
| [**dotnet-restore**](tool-dotnet-restore.md)                                                     | 用于还原 .NET 项目的依赖项和工具的工具。                                               |
| [**dotnet-toolinstall**](tool-dotnet-toolinstall.md)                                             | 用于安装 .NET Core 工具的工具（例如， dotnet-ef）                                                |
| [**enable-iis**](tool-enable-iis.md)                                                             | 用于启用 IIS 功能并安装最新 ASP.NET 托管捆绑包的工具。                                  |
| [**msi-install**](tool-msi-install.md)                                                           | 用于安装 MSI 文件的工具（给定路径或 URL）。                                                              |
| [**npm-install**](tool-npm-install.md)                                                           | 用于安装 NPM 包的工具。                                                                               |
| [**nuget-restore**](tool-nuget-restore.md)                                                       | 用于还原 NuGet 包的工具。                                                                         |
| [**require-azureartifactscredentialprovider**](tool-require-azureartifactscredentialprovider.md) | 安装 Azure Artifacts 凭据提供程序。                                                           |
| [**require-azurecli**](tool-require-azurecli.md)                                                 | 用于安装 Azure CLI 的工具。                                                                              |
| [**require-dotnetcoresdk**](tool-require-dotnetcoresdk.md)                                       | 用于安装 .NET Core SDK 和共享运行时的工具。                                                       |
| [**require-dotnetframeworksdk**](tool-require-dotnetframeworksdk.md)                             | 用于安装 .NET Framework SDK 的工具。                                                                     |
| [**require-mssql**](tool-require-mssql.md)                                                       | 用于安装 MS SQL Server 2019 的工具。                                                                         |
| [**require-nodejs**](tool-require-nodejs.md)                                                     | 用于安装 Nodejs 和 NPM 的工具。                                                                             |
| [**require-nuget**](tool-require-nuget.md)                                                       | 用于安装 NuGet 的工具。                                                                                      |
| [**require-npm**](tool-require-npm.md)                                                           | 用于安装 NPM 的工具。                                                                                        |
| [**require-psmodule**](tool-require-psmodule.md)                                                 | 用于从库中安装 PowerShell 模块的工具。                                                        |
| [**require-vcpkg**](tool-require-vcpkg.md)                                                       | 用于安装 vcpkg 的工具。                                                                                      |
| [**require-vscomponent**](tool-require-vscomponent.md)                                           | 用于基于 `.vsconfig` 文件修改 VS 安装的工具。                                                |
| [**require-winget**](tool-require-winget.md)                                                     | 用于安装 winget 的工具。                                                                                     |
| [**windowsfeature-enable**](tool-windowsfeature-enable.md)                                       | 工具集启用 Windows 功能。                                                                           |
| [**windowsfeature-disable**](tool-windowsfeature-disable.md)                                     | 工具集禁用 Windows 功能。                                                                          |
| [**windowsfeature-list**](tool-windowsfeature-list.md)                                           | 用于列出所有 Windows 功能的启用/禁用状态的工具。                                              |
| [**set-env**](tool-set-env.md)                                                                   | 用于查看和设置环境变量的工具。                                                                 |
| [**vcpkg-install**](tool-vcpkg-install.md)                                                       | 用于通过 vcpkg 安装包的工具。                                                                         |
| [**winget-install**](tool-winget-install.md)                                                     | 用于通过 winget 安装包的工具。                                                                        |
| [**wsl-install**](tool-wsl-install.md)                                                           | 用于针对适用于 Linux 的 Windows 子系统安装和配置 Linux 发行版的工具。                             |
