---
title: 为企业部署设置默认值
description: 了解 Visual Studio 企业部署的域策略和其他配置操作。
ms.date: 04/13/2021
ms.topic: conceptual
f1_keywords:
- gpo
- policy
helpviewer_keywords:
- '{{PLACEHOLDER}}'
- '{{PLACEHOLDER}}'
ms.assetid: 9B7B4608-7A3F-4FF4-BDCE-42D9F7CE6DBA
author: anandmeg
ms.author: meghaanand
manager: jmartens
ms.workload:
- multiple
ms.prod: visual-studio-windows
ms.technology: vs-installation
ms.openlocfilehash: 8d36951502fb9c3e6a012532b5c872e017847219
ms.sourcegitcommit: 215680b355cf613bfa125cf6b864c8bb5f2c71a5
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/15/2021
ms.locfileid: "132453173"
---
# <a name="set-defaults-for-enterprise-deployments-of-visual-studio"></a>为 Visual Studio 企业部署设置默认值

可以设置影响 Visual Studio 部署的注册表策略。 这些策略对于计算机是全局性的，并影响：

- 与其他版本或实例共享的一些包的安装位置
- 包是否要缓存及缓存位置
- 应如何应用管理员更新

可以使用[命令行选项](use-command-line-parameters-to-install-visual-studio.md)设置部分策略，并能在计算机上设置注册表值，也可以在整个组织中使用组策略进行分发。

## <a name="registry-keys"></a>注册表项

可以在多个位置上设置企业默认值，从而能够通过组策略进行控制或在注册表中直接控制。 Visual Studio 会依序检查是否已设置任何企业策略；只要按以下顺序发现了策略值，就会忽略剩余的项。

1. `HKEY_LOCAL_MACHINE\SOFTWARE\Policies\Microsoft\VisualStudio\Setup`
2. `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\VisualStudio\Setup`
3. `HKEY_LOCAL_MACHINE\SOFTWARE\WOW6432Node\Microsoft\VisualStudio\Setup`（64 位操作系统）

一些注册表值会在首次使用时自动设置（如果尚未设置的话）。 这种做法可确保后续安装使用相同的值。 这些值存储在第二个注册表项 `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\VisualStudio\Setup` 中。

可以设置以下注册表值：

::: moniker range="vs-2017"

| **名称**                      | **类型**                    | **默认值**                                         | **说明**                                                                                                                                                                                                                                                                                                                                                                                                                                                              |
|-------------------------------|-----------------------------|-----------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `CachePath`                   | `REG_SZ` 或 `REG_EXPAND_SZ` | %ProgramData%\Microsoft\VisualStudio\Packages       | 用于存储包清单和有效负载（可选）的目录。 有关详细信息，请参阅[禁用或移动包缓存](disable-or-move-the-package-cache.md)页面。                                                                                                                                                                                                                                                                                        |
| `KeepDownloadedPayloads`      | `REG_DWORD`                 | 1                                                   | 即使在安装后，也仍会保留包有效负载。 随时都可以更改值。 禁用此策略会删除你修复或修改的实例的任何已缓存包有效负载。 有关详细信息，请参阅[禁用或移动包缓存](disable-or-move-the-package-cache.md)页面。                                                                                                                                                                             |
| `SharedInstallationPath`      | `REG_SZ` 或 `REG_EXPAND_SZ` | %ProgramFiles(x86)%\Microsoft Visual Studio\Shared  | 用于安装跨 Visual Studio 实例版本共享的一些包的目录。 虽然随时都可以更改值，但更改只会影响今后执行的安装。 不得移动旧位置上已安装的任何产品，否则它们可能无法正常运行。                                                                                                                                                                                  |
| `BackgroundDownloadDisabled`  | `REG_DWORD`                 | 0                                                   | 阻止安装程序为所有已安装的 Visual Studio 产品自动下载更新。 随时都可以更改值。                                                                                                                                                                                                                                                                                                                                             |
| `AdministratorUpdatesEnabled` | `REG_DWORD`                 | 0                                                   | 允许将管理员更新应用到客户端计算机。 如果此值缺失或设置为 0，则将阻止管理员更新。 此值用于管理。 有关详细信息，请参阅[启用管理员更新](enabling-administrator-updates.md)。                                                                                                                                                                                      |
| `AdministratorUpdatesOptOut`  | `REG_DWORD`                 | 0                                                   | 指示用户不想接收 Visual Studio 的管理员更新。 若缺少注册表值或设置的值为 0，这意味着 Visual Studio 用户希望接收 Visual Studio 管理员更新。 这适用于开发人员用户（如果他们拥有对客户端计算机的管理员权限）。 有关详细信息，请参阅[应用管理员更新](../install/applying-administrator-updates.md#understanding-configuration-options)。 |
| `UpdateConfigurationFile`     | `REG_SZ` 或 `REG_EXPAND_SZ` | %ProgramData%\Microsoft\VisualStudio\updates.config | 用于配置管理更新的文件路径。 有关详细信息，请参阅[配置管理员更新的方法](../install/applying-administrator-updates.md#methods-for-configuring-an-administrator-update)。                                                                                                                                                                                                                                             |

::: moniker-end

::: moniker range="vs-2019"

| **名称**                         | **类型**                    | **默认值**                                         | **说明**                                                                                                                                                                                                                                                                                                                                                                                                                                                              |
|----------------------------------|-----------------------------|-----------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `CachePath`                      | `REG_SZ` 或 `REG_EXPAND_SZ` | %ProgramData%\Microsoft\VisualStudio\Packages       | 用于存储包清单和有效负载（可选）的目录。 有关详细信息，请参阅[禁用或移动包缓存](disable-or-move-the-package-cache.md)页面。                                                                                                                                                                                                                                                                                        |
| `KeepDownloadedPayloads`         | `REG_DWORD`                 | 1                                                   | 即使在安装后，也仍会保留包有效负载。 随时都可以更改值。 禁用此策略会删除你修复或修改的实例的任何已缓存包有效负载。 有关详细信息，请参阅[禁用或移动包缓存](disable-or-move-the-package-cache.md)页面。                                                                                                                                                                             |
| `SharedInstallationPath`         | `REG_SZ` 或 `REG_EXPAND_SZ` | %ProgramFiles(x86)%\Microsoft Visual Studio\Shared  | 用于安装跨 Visual Studio 实例版本共享的一些包的目录。 虽然随时都可以更改值，但更改只会影响今后执行的安装。 不得移动旧位置上已安装的任何产品，否则它们可能无法正常运行。                                                                                                                                                                                  |
| `BackgroundDownloadDisabled`     | `REG_DWORD`                 | 0                                                   | 阻止安装程序为所有已安装的 Visual Studio 产品自动下载更新。 随时都可以更改值。                                                                                                                                                                                                                                                                                                                                             |
| `AdministratorUpdatesEnabled`    | `REG_DWORD`                 | 0                                                   | 允许将管理员更新应用到客户端计算机。 如果此值缺失或设置为 0，则将阻止管理员更新。 此值用于管理。 有关详细信息，请参阅[启用管理员更新](enabling-administrator-updates.md)。                                                                                                                                                                                      |
| `AdministratorUpdatesOptOut`     | `REG_DWORD`                 | 0                                                   | 指示用户不想接收 Visual Studio 的管理员更新。 若缺少注册表值或设置的值为 0，这意味着 Visual Studio 用户希望接收 Visual Studio 管理员更新。 这适用于开发人员用户（如果他们拥有对客户端计算机的管理员权限）。 有关详细信息，请参阅[应用管理员更新](../install/applying-administrator-updates.md#understanding-configuration-options)。 |
| `UpdateConfigurationFile`        | `REG_SZ` 或 `REG_EXPAND_SZ` | %ProgramData%\Microsoft\VisualStudio\updates.config | 用于配置管理更新的文件路径。 有关详细信息，请参阅[配置管理员更新的方法](../install/applying-administrator-updates.md#methods-for-configuring-an-administrator-update)。                                                                                                                                                                                                                                             |
| `BaselineStickinessVersions2019` | `REG_SZ` 或 `REG_EXPAND_SZ` | `16.7.0`                                            | 应持续为客户端使用的维护基准次版本。 有关详细信息，请参阅[应用管理员更新](../install/applying-administrator-updates.md#understanding-configuration-options)页。                                                                                                                                                                                                                                                    |

::: moniker-end

::: moniker range=">=vs-2022"

| **名称**                         | **类型**                    | **默认值**                                         | **说明**                                                                                                                                                                                                                                                                                                                                                                                                                                                              |
|----------------------------------|-----------------------------|-----------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `CachePath`                      | `REG_SZ` 或 `REG_EXPAND_SZ` | %ProgramData%\Microsoft\VisualStudio\Packages       | 用于存储包清单和有效负载（可选）的目录。 有关详细信息，请参阅[禁用或移动包缓存](disable-or-move-the-package-cache.md)页面。                                                                                                                                                                                                                                                                                        |
| `KeepDownloadedPayloads`         | `REG_DWORD`                 | 1                                                   | 即使在安装后，也仍会保留包有效负载。 随时都可以更改值。 禁用此策略会删除你修复或修改的实例的任何已缓存包有效负载。 有关详细信息，请参阅[禁用或移动包缓存](disable-or-move-the-package-cache.md)页面。                                                                                                                                                                             |
| `SharedInstallationPath`         | `REG_SZ` 或 `REG_EXPAND_SZ` | %ProgramFiles%\Microsoft Visual Studio\Shared       | 用于安装跨 Visual Studio 实例版本共享的一些包的目录。 虽然随时都可以更改值，但更改只会影响今后执行的安装。 不得移动旧位置上已安装的任何产品，否则它们可能无法正常运行。                                                                                                                                                                                  |
| `BackgroundDownloadDisabled`     | `REG_DWORD`                 | 0                                                   | 阻止安装程序为所有已安装的 Visual Studio 产品自动下载更新。 随时都可以更改值。                                                                                                                                                                                                                                                                                                                                             |
| `AdministratorUpdatesEnabled`    | `REG_DWORD`                 | 0                                                   | 允许将管理员更新应用到客户端计算机。 如果此值缺失或设置为 0，则将阻止管理员更新。 此值用于管理。 有关详细信息，请参阅[启用管理员更新](enabling-administrator-updates.md)。                                                                                                                                                                                      |
| `AdministratorUpdatesOptOut`     | `REG_DWORD`                 | 0                                                   | 指示用户不想接收 Visual Studio 的管理员更新。 若缺少注册表值或设置的值为 0，这意味着 Visual Studio 用户希望接收 Visual Studio 管理员更新。 这适用于开发人员用户（如果他们拥有对客户端计算机的管理员权限）。 有关详细信息，请参阅[应用管理员更新](../install/applying-administrator-updates.md#understanding-configuration-options)。 |
| `UpdateConfigurationFile`        | `REG_SZ` 或 `REG_EXPAND_SZ` | %ProgramData%\Microsoft\VisualStudio\updates.config | 用于配置管理更新的文件路径。 有关详细信息，请参阅[配置管理员更新的方法](../install/applying-administrator-updates.md#methods-for-configuring-an-administrator-update)。                                                                                                                                                                                                                                             |
| `BaselineStickinessVersions2019` | `REG_SZ` 或 `REG_EXPAND_SZ` | `16.7.0`                                            | 应持续为客户端使用的维护基准次版本。 有关详细信息，请参阅[应用管理员更新](../install/applying-administrator-updates.md#understanding-configuration-options)页。                                                                                                                                                                                                                                                    |

::: moniker-end

> [!IMPORTANT]
> 如果在任何安装后更改 `CachePath` 注册表策略，必须将现有包缓存移到新位置，并确保其受安全保护，以便 `SYSTEM` 和 `Administrators` 拥有完全控制权限，并且 `Everyone` 拥有读取访问权限。
> 如果无法移动现有缓存或无法确保其受安全保护，可能导致今后执行的安装出现问题。

[!INCLUDE[install_get_support_md](includes/install_get_support_md.md)]

## <a name="see-also"></a>另请参阅

- [安装 Visual Studio](install-visual-studio.md)
- [Visual Studio 管理员指南](visual-studio-administrator-guide.md)
- [应用管理员更新](applying-administrator-updates.md)
- [禁用或移动包缓存](disable-or-move-the-package-cache.md)
- [使用命令行参数安装 Visual Studio](use-command-line-parameters-to-install-visual-studio.md)
