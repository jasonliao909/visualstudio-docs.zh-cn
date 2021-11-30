---
title: 为企业部署设置默认值
description: 了解 Visual Studio 企业部署的域策略和其他配置操作。
ms.date: 11/23/2021
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
ms.openlocfilehash: 79a0e8fd07d9d30b15832c2b95accbb8ab479f62
ms.sourcegitcommit: 2281b4f1f8737f263c0d7e55e00b5ec81517327d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/25/2021
ms.locfileid: "133108856"
---
# <a name="set-defaults-for-enterprise-deployments-of-visual-studio"></a>为 Visual Studio 企业部署设置默认值

可以设置影响 Visual Studio 部署和更新行为的注册表策略。 这些策略在客户端计算机上具有全局性，并影响以下各项：

- 与其他版本或实例共享的一些包的安装位置。
- 是否要缓存及缓存位置。
- 是否应启用管理员更新以及如何应用管理员更新。
- 哪些更新通道可用，以及如何向客户端呈现这些通道。
- 通知的显示方式或者不显示通知。

可以通过在客户端计算机上使用[命令行选项](use-command-line-parameters-to-install-visual-studio.md)、直接在客户端计算机上设置注册表值，或在整个组织中使用组策略注册表值来设置这些策略。

## <a name="registry-keys"></a>注册表项

可以在多个位置上设置企业默认值，从而能够通过组策略进行控制或在注册表中直接控制。 Visual Studio 会依序检查是否已设置任何企业策略；只要按以下顺序发现了策略值，就会忽略剩余的项。

1. `HKEY_LOCAL_MACHINE\SOFTWARE\Policies\Microsoft\VisualStudio\Setup`
2. `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\VisualStudio\Setup`
3. `HKEY_LOCAL_MACHINE\SOFTWARE\WOW6432Node\Microsoft\VisualStudio\Setup`（64 位操作系统）

一些注册表值会在首次使用时自动设置（如果尚未设置的话）。 这种做法可确保后续安装使用相同的值。 这些值存储在第二个注册表项 `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\VisualStudio\Setup` 中。

可以设置以下注册表值：

## <a name="controlling-installation-and-download-behavior"></a>控制安装和下载行为
此部分中的注册表设置可控制将 Visual Studio 产品下载到客户端计算机上的方式和位置。

| **名称**                         | **类型**                    | **默认值**                                         | **说明**       |
|----------------------------------|-----------------------------|-----------------------------------------------------|----------------------------|
| `CachePath`                      | `REG_SZ` 或 `REG_EXPAND_SZ` | %ProgramData%<br>\Microsoft<br>\VisualStudio<br>\Packages       | 用于存储包清单和有效负载（可选）的目录。 有关详细信息，请参阅[禁用或移动包缓存](disable-or-move-the-package-cache.md)页面。   |
| `KeepDownloadedPayloads`         | `REG_DWORD`                 | 1                                                   | 即使在安装后，也仍会保留包有效负载。 随时都可以更改值。 禁用此策略会删除你修复或修改的实例的任何已缓存包有效负载。 有关详细信息，请参阅[禁用或移动包缓存](disable-or-move-the-package-cache.md)页面。   |
| `SharedInstallationPath`         | `REG_SZ` 或 `REG_EXPAND_SZ` | %ProgramFiles(x86)%<br>\Microsoft Visual Studio<br>\Shared  | 用于安装跨 Visual Studio 实例版本共享的一些包的目录。 虽然随时都可以更改值，但更改只会影响今后执行的安装。 不得移动旧位置上已安装的任何产品，否则它们可能无法正常运行。      |
| `BackgroundDownloadDisabled`     | `REG_DWORD`                 | 0                                                   | 阻止安装程序为所有已安装的 Visual Studio 产品自动下载更新。 随时都可以更改值。    |

> [!IMPORTANT]
> 如果在任何安装后更改 `CachePath` 注册表策略，必须将现有包缓存移到新位置，并确保其受安全保护，以便 `SYSTEM` 和 `Administrators` 拥有完全控制权限，并且 `Everyone` 拥有读取访问权限 。
> 如果无法移动现有缓存或无法确保其受安全保护，可能导致今后执行的安装出现问题。


## <a name="controlling-administrator-updates"></a>控制管理员更新
::: moniker range="vs-2017"

本部分中的注册表设置可控制是否以及如何将管理员更新应用于客户端计算机。

| **名称**                         | **类型**                    | **默认值**                                         | **说明**           |
|----------------------------------|-----------------------------|-----------------------------------------------------|---------------------------|
| `AdministratorUpdatesEnabled`    | `REG_DWORD`                 | 0                                                   | 允许将管理员更新应用到客户端计算机。 如果此值缺失或设置为 0，则将阻止管理员更新。 此值用于管理。 有关详细信息，请参阅[启用管理员更新](enabling-administrator-updates.md)。 |
| `AdministratorUpdatesOptOut`     | `REG_DWORD`                 | 0                                                   | 指示用户不想接收 Visual Studio 的管理员更新。 若缺少注册表值或设置的值为 0，这意味着 Visual Studio 用户希望接收 Visual Studio 管理员更新。 这适用于开发人员用户（如果他们拥有对客户端计算机的管理员权限）。 有关详细信息，请参阅[应用管理员更新](../install/applying-administrator-updates.md#understanding-configuration-options)。 |
| `UpdateConfigurationFile`        | `REG_SZ` 或 `REG_EXPAND_SZ` | %ProgramData%<br>\Microsoft<br>\VisualStudio<br>\updates.config | 用于配置管理更新的文件路径。 有关详细信息，请参阅[配置管理员更新的方法](../install/applying-administrator-updates.md#methods-for-configuring-an-administrator-update)。   |    

::: moniker-end

::: moniker range="vs-2019"

本部分中的注册表设置可控制是否以及如何将管理员更新应用于客户端计算机。

| **名称**                         | **类型**                    | **默认值**                                         | **说明**           |
|----------------------------------|-----------------------------|-----------------------------------------------------|---------------------------|
| `AdministratorUpdatesEnabled`    | `REG_DWORD`                 | 0                                                   | 允许将管理员更新应用到客户端计算机。 如果此值缺失或设置为 0，则将阻止管理员更新。 此值用于管理。 有关详细信息，请参阅[启用管理员更新](enabling-administrator-updates.md)。 |
| `AdministratorUpdatesOptOut`     | `REG_DWORD`                 | 0                                                   | 指示用户不想接收 Visual Studio 的管理员更新。 若缺少注册表值或设置的值为 0，这意味着 Visual Studio 用户希望接收 Visual Studio 管理员更新。 这适用于开发人员用户（如果他们拥有对客户端计算机的管理员权限）。 有关详细信息，请参阅[应用管理员更新](../install/applying-administrator-updates.md#understanding-configuration-options)。 |
| `UpdateConfigurationFile`        | `REG_SZ` 或 `REG_EXPAND_SZ` | %ProgramData%<br>\Microsoft<br>\VisualStudio<br>\updates.config | 用于配置管理更新的文件路径。 有关详细信息，请参阅[配置管理员更新的方法](../install/applying-administrator-updates.md#methods-for-configuring-an-administrator-update)。   |                        
| `BaselineStickinessVersions2019` | `REG_SZ` 或 `REG_EXPAND_SZ` | `16.7.0`                                            | 应持续为客户端使用的维护基准次版本。 有关详细信息，请参阅[应用管理员更新](../install/applying-administrator-updates.md#understanding-configuration-options)页。 |

::: moniker-end

::: moniker range=">=vs-2022"

本部分中的注册表设置可控制是否以及如何将管理员更新应用于客户端计算机。

| **名称**                         | **类型**                    | **默认值**                                         | **说明**           |
|----------------------------------|-----------------------------|-----------------------------------------------------|---------------------------|
| `AdministratorUpdatesEnabled`    | `REG_DWORD`                 | 0                                                   | 允许将管理员更新应用到客户端计算机。 如果此值缺失或设置为 0，则将阻止管理员更新。 此值用于管理。 有关详细信息，请参阅[启用管理员更新](enabling-administrator-updates.md)。 |
| `AdministratorUpdatesOptOut`     | `REG_DWORD`                 | 0                                                   | 指示用户不想接收 Visual Studio 的管理员更新。 若缺少注册表值或设置的值为 0，这意味着 Visual Studio 用户希望接收 Visual Studio 管理员更新。 这适用于开发人员用户（如果他们拥有对客户端计算机的管理员权限）。 有关详细信息，请参阅[应用管理员更新](../install/applying-administrator-updates.md#understanding-configuration-options)。 |
| `UpdateConfigurationFile`        | `REG_SZ` 或 `REG_EXPAND_SZ` | %ProgramData%<br>\Microsoft<br>\VisualStudio<br>\updates.config | 用于配置管理更新的文件路径。 有关详细信息，请参阅[配置管理员更新的方法](../install/applying-administrator-updates.md#methods-for-configuring-an-administrator-update)。   |    

::: moniker-end

::: moniker range=">=vs-2019"

## <a name="configuring-source-location-for-updates"></a>配置更新的源位置 

通过此部分中的设置，管理员可以自定义和控制可用的更新通道及其在企业组织中向客户端呈现的方式。 有关更新设置的定义及其工作原理的信息，请参阅[配置更新的源位置](update-visual-studio.md#configure-source-location-of-updates-1)文档。 
此功能要求客户端使用 Visual Studio 2022 安装程序，并且布局要使用 2021 年 11 月 10 日或之后发布的 2019 引导程序版本。 有关如何启用此功能的指南，请参阅[如何通过 Visual Studio 2019 布局在客户端计算机上获取 Visual Studio 2022 安装程序](create-a-network-installation-of-visual-studio.md#configure-the-layout-to-always-use-the-latest-installer)。

本部分中的密钥仅适用于 Computer\HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\VisualStudio\Setup\ 注册表路径

| **名称**                         | **类型**                    | **说明**                                                |
|----------------------------------|-----------------------------|-----------------------------------------------------|
| `Channels` | `Key` |  用于存储自定义布局通道信息的密钥路径。 该键的值是通道名称，显示在[更新通道下拉列表](/visualstudio/install/update-visual-studio?#configure-source-location-of-updates-1)中。 |
| `DisabledChannels` | `Key` | 用于抑制通道并阻止其在“更新通道”对话框中显示的密钥路径。 如果通道是在此处定义的，则会从对话框筛选出去。 |
| `ChannelURI` | `REG_SZ` |  channelURI 通过添加到 `Channels` 配置单元添加到更新通道值列表，或通过添加到 `DisabledChannels` 注册表配置单元从更新通道列表中进行抑制。 对于 Microsoft 托管通道，channelURI 为“https://aka.ms/vs/16/release/channel”或“https://aka.ms/vs/16/pre/channel”。  对于布局，此值需要指向布局的 ChannelManifest.json。 请参阅以下示例。 |
| `Description` | `REG_SZ` |  通道的两行自定义描述。 如果已通过布局安装，更新设置 UI 便默认为“专用通道”，你可以使用此描述对其进行更改。 |

以下示例注册表文件演示了如何在[更新设置 UI](/visualstudio/install/update-visual-studio?#configure-source-location-of-updates-1) 中为自定义更新通道添加几个布局条目，以及如何禁止显示预览通道。

```example registry file
Windows Registry Editor Version 5.00

[HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\VisualStudio\Setup\Channels]

[HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\VisualStudio\Setup\Channels\More meaningful name of my existing layout]
"channelUri"="\\\\vslayoutserver3\\vs\\2019_Enterprise\\ChannelManifest.json"
"Description"="Dev Tools based on VS 2019 16.9.Spring.2020 servicing baseline"

[HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\VisualStudio\Setup\Channels\Spring 2021 dev toolset]
"channelUri"="\\\\new2019layoutserver\\share\\new2019layout\\ChannelManifest.json"
"Description"="Dev Tools based on VS 2019 16.11.Spring.2021 servicing baseline"

[HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\VisualStudio\Setup\Channels\Next gen dev tools using VS 2022 toolset]
"channelUri"="\\\\vs2022Layoutserver\\share\\2022Enterprise\\ChannelManifest.json"
"Description"="Developer Tools based on the VS 2022 17.0.Winter.2021 LSTC servicing baseline"

[HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\VisualStudio\Setup\DisabledChannels\Preview]
"channelUri"="https://aka.ms/vs/16/pre/channel"
```

::: moniker-end

## <a name="controlling-notifications-in-the-visual-studio-ide"></a>在 Visual Studio IDE 中控制通知

::: moniker range="vs-2017"

如上所述，Visual Studio 检查其安装位置（例如，网络共享或 Internet），以确定是否有任何更新。 若有更新，Visual Studio 会在窗口右上角显示通知标志来通知用户。

   ![更新的通知标志](media/notification-flag.png)

::: moniker-end

::: moniker range=">=vs-2019"

如上所述，Visual Studio 检查其安装位置（例如，网络共享或 Internet），以确定是否有任何更新。 若有更新，Visual Studio 会在窗口右下角显示通知图标来通知用户。

   ![Visual Studio IDE 中的通知图标](media/vs-2019/notification-bar.png "Visual Studio IDE 中的通知图标")

::: moniker-end

如果不想提示最终用户进行更新，可禁用该通知。 （例如，如果通过中心软件分发机制来提供更新，可能希望禁用通知。）

::: moniker range="vs-2017"

由于 Visual Studio 2017 [将注册表项存储在专用注册表中](tools-for-managing-visual-studio-instances.md#editing-the-registry-for-a-visual-studio-instance)，因此无法照常直接编辑注册表。 不过，Visual Studio 提供可用于更改 Visual Studio 设置的实用工具 `vsregedit.exe`。 可以使用下面的命令禁用通知：

```shell
vsregedit.exe set "C:\Program Files (x86)\Microsoft Visual Studio\2017\Enterprise" HKCU ExtensionManager AutomaticallyCheckForUpdates2Override dword 0
```

可以使用下面的命令重新启用通知：

```shell
vsregedit.exe set "C:\Program Files (x86)\Microsoft Visual Studio\2017\Enterprise" HKCU ExtensionManager AutomaticallyCheckForUpdates2Override dword 1
```

若要返回到默认行为，还可以通过以下命令删除该值：

```shell
vsregedit.exe remove "C:\Program Files (x86)\Microsoft Visual Studio\2017\Enterprise" HKCU ExtensionManager AutomaticallyCheckForUpdates2Override
```

运行命令以更改 Visual Studio 设置后，启动 Visual Studio。 在关闭并重新启动 Visual Studio 之前，Visual Studio 的任何已运行的实例都不会更改行为。 另一种方法是，可以重新启动计算机，以确保设置生效。

可以使用以下命令确认该设置：

```shell
vsregedit.exe read "C:\Program Files (x86)\Microsoft Visual Studio\2017\Enterprise" HKCU ExtensionManager AutomaticallyCheckForUpdates2Override dword
```

如果值不存在（默认情况下存在此条件），前面的命令将指示它无法读取该值。 如果设置了该值，前面的命令将反映出 Visual Studio 配置中的值（它将指示 0 或 1，或者设置的任何值，只应为 0 或 1）。

::: moniker-end

::: moniker range="vs-2019"

由于 Visual Studio 2019 [将注册表项存储在专用注册表中](tools-for-managing-visual-studio-instances.md#editing-the-registry-for-a-visual-studio-instance)，因此无法照常直接编辑注册表。 不过，Visual Studio 提供可用于更改 Visual Studio 设置的实用工具 `vsregedit.exe`。 可以使用下面的命令禁用通知：

```shell
vsregedit.exe set "C:\Program Files (x86)\Microsoft Visual Studio\2019\Enterprise" HKCU ExtensionManager AutomaticallyCheckForUpdates2Override dword 0
```

可以使用下面的命令重新启用通知：

```shell
vsregedit.exe set "C:\Program Files (x86)\Microsoft Visual Studio\2019\Enterprise" HKCU ExtensionManager AutomaticallyCheckForUpdates2Override dword 1
```

若要返回到默认行为，还可以通过以下命令删除该值：

```shell
vsregedit.exe remove "C:\Program Files (x86)\Microsoft Visual Studio\2019\Enterprise" HKCU ExtensionManager AutomaticallyCheckForUpdates2Override
```

运行命令以更改 Visual Studio 设置后，启动 Visual Studio。 在关闭并重新启动 Visual Studio 之前，Visual Studio 的任何已运行的实例都不会更改行为。 另一种方法是，可以重新启动计算机，以确保设置生效。

可以使用以下命令确认该设置：

```shell
vsregedit.exe read "C:\Program Files (x86)\Microsoft Visual Studio\2019\Enterprise" HKCU ExtensionManager AutomaticallyCheckForUpdates2Override dword
```

如果值不存在（默认情况下存在此条件），前面的命令将指示它无法读取该值。 如果设置了该值，前面的命令将反映出 Visual Studio 配置中的值（它将指示 0 或 1，或者设置的任何值，只应为 0 或 1）。

::: moniker-end

::: moniker range=">=vs-2022"

由于 Visual Studio 2022 [将注册表项存储在专用注册表中](tools-for-managing-visual-studio-instances.md#editing-the-registry-for-a-visual-studio-instance)，因此无法照常直接编辑注册表。 不过，Visual Studio 提供可用于更改 Visual Studio 设置的实用工具 `vsregedit.exe`。 可以使用下面的命令禁用通知：

```shell
vsregedit.exe set "C:\Program Files\Microsoft Visual Studio\2022\Enterprise" HKCU ExtensionManager AutomaticallyCheckForUpdates2Override dword 0
```

可以使用下面的命令重新启用通知：

```shell
vsregedit.exe set "C:\Program Files\Microsoft Visual Studio\2022\Enterprise" HKCU ExtensionManager AutomaticallyCheckForUpdates2Override dword 1
```

若要返回到默认行为，还可以通过以下命令删除该值：

```shell
vsregedit.exe remove "c:\Program Files\Microsoft Visual Studio\2022\Enterprise" HKCU ExtensionManager AutomaticallyCheckForUpdates2Override
```

运行命令以更改 Visual Studio 设置后，启动 Visual Studio。 在关闭并重新启动 Visual Studio 之前，Visual Studio 的任何已运行的实例都不会更改行为。 另一种方法是，可以重新启动计算机，以确保设置生效。

可以使用以下命令确认该设置：

```shell
vsregedit.exe read "c:\Program Files\Microsoft Visual Studio\2022\Enterprise" HKCU ExtensionManager AutomaticallyCheckForUpdates2Override dword
```

如果值不存在（默认情况下存在此条件），前面的命令将指示它无法读取该值。 如果设置了该值，前面的命令将反映出 Visual Studio 配置中的值（它将指示 0 或 1，或者设置的任何值，只应为 0 或 1）。

::: moniker-end

（请确保替换目录，以匹配要编辑的已安装实例。）

> [!TIP]
> 使用 [vswhere.exe](tools-for-managing-visual-studio-instances.md#detecting-existing-visual-studio-instances) 可以在客户端工作站上查找 Visual Studio 的特定实例。

[!INCLUDE[install_get_support_md](includes/install_get_support_md.md)]

## <a name="see-also"></a>请参阅

- [安装 Visual Studio](install-visual-studio.md)
- [Visual Studio 管理员指南](visual-studio-administrator-guide.md)
- [应用管理员更新](applying-administrator-updates.md)
- [禁用或移动包缓存](disable-or-move-the-package-cache.md)
- [使用命令行参数安装 Visual Studio](use-command-line-parameters-to-install-visual-studio.md)
