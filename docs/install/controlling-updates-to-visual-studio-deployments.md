---
title: 控制对部署的更新
description: 了解从网络安装时，如何更改 Visual Studio 查找更新的位置。
ms.date: 10/22/2021
ms.topic: conceptual
helpviewer_keywords:
- '{{PLACEHOLDER}}'
- '{{PLACEHOLDER}}'
ms.assetid: 35C7AB05-07D5-4B38-BCAC-AB88444E7368
author: anandmeg
ms.author: meghaanand
manager: jmartens
ms.workload:
- multiple
ms.prod: visual-studio-windows
ms.technology: vs-installation
ms.openlocfilehash: cfade1d9f357eda4a741726e65ca02f2b8f6ccc3
ms.sourcegitcommit: 0257750be796cc46e01cebd8976f637743d29417
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/23/2021
ms.locfileid: "130290611"
---
# <a name="control-updates-to-network-based-visual-studio-deployments"></a>控制对基于网络的 Visual Studio 部署的更新

企业管理员通常会创建布局，并将其托管在网络文件共享上，以供部署给最终用户。 本页介绍如何正确配置网络布局选项。

## <a name="controlling-where-visual-studio-looks-for-updates"></a>控制 Visual Studio 在何处查找更新

**方案 1：客户端最初已从布局安装，但配置为从网络布局位置或 Web 接收更新**

默认情况下，即使安装最初从网络共享进行部署，Visual Studio 也仍会继续联机查找更新。 如果 Web 上提供了更新，则用户可以安装它。 虽然首先会检查网络布局缓存中是否存在任何更新的产品位，但如果没有找到，Visual Studio 将从 Web 查找并下载更新的产品位。

**方案 2：客户端最初已安装，只应从网络布局接收更新**

如果要控制 Visual Studio 客户端查找更新的位置，例如，如果客户端计算机没有 Internet 访问权限，并且你想要确保它只能且始终从布局安装，则可以配置客户端安装程序查找更新的产品位的位置。 最好确保在正确配置了此设置后，客户端再从布局执行初始安装。

1. 创建脱机布局：

   ```shell
   vs_enterprise.exe --layout C:\vsoffline --lang en-US
   ```

2. 将脱机布局复制到托管文件共享上：

   ```shell
   xcopy /e C:\vsoffline \\server\share\VS
   ```

3. 修改布局中的 `response.json` 文件，将 `channelUri` 值更改为指向管理员控制的 channelManifest.json 的副本。

   请务必在此值中转义反斜杠，如下例所示：

   ```json
   "channelUri":"\\\\server\\share\\VS\\ChannelManifest.json"
   ```

   现在，最终用户可以从此共享运行安装程序来安装 Visual Studio。

   ```shell
   \\server\share\VS\vs_enterprise.exe
   ```

如果确定用户应更新到更高版本的 Visual Studio，企业管理员可以[更新布局位置](update-a-network-installation-of-visual-studio.md)，以纳入更新后的文件，如下所示。

1. 使用类似于以下的命令：

   ```shell
   vs_enterprise.exe --layout \\server\share\VS --lang en-US
   ```

2. 确保在更新后的布局中 `response.json` 文件仍包含自定义设置，特别是 channelUri 修改，如下所示：

   ```json
   "channelUri":"\\\\server\\share\\VS\\ChannelManifest.json"
   ```

通过此布局安装的现有 Visual Studio 将在 `\\server\share\VS\ChannelManifest.json` 中查找更新。 如果此 channelManifest.json 比用户已安装的版本更高，Visual Studio 会通知用户有更新可供安装。

从客户端启动的任何安装更新将直接通过此布局自动安装更新后的 Visual Studio 版本。

**方案 3：客户端最初已从 Web 安装，但现在只应从网络布局接收更新**

在某些情况下，客户端计算机可能已从 Web 安装 Visual Studio，但现在管理员希望从托管布局接收所有将来的更新。 唯一受支持的方法是使用所需的产品版本创建网络布局，然后在客户端计算机上，从布局位置运行引导程序（例如 `\\server\share\vs_enterprise.exe`）。 理想情况下，初始客户端安装将从正确配置了 ChannelURI 的网络布局使用引导程序执行，但也可以从网络布局位置运行更新的引导程序。 其中任一操作将在客户端计算机上嵌入与该特定布局位置的连接。 为了使此方案能够正常运行，需要注意的是，布局的 `response.json` 文件中的“ChannelURI”必须与发生原始安装时在客户端计算机上设置的 ChannelURI 相同。 此值很可能最初设置为 Internet [发布通道](https://aka.ms/vs/16/release/channel)。

## <a name="controlling-notifications-in-the-visual-studio-ide"></a>在 Visual Studio IDE 中控制通知

::: moniker range="vs-2017"

如上所述，Visual Studio 检查其安装位置（例如，网络共享或 Internet），以确定是否有任何更新。 若有更新，Visual Studio 会在窗口右上角显示通知标志来通知用户。

   ![更新的通知标志](media/notification-flag.png)

::: moniker-end

::: moniker range=">=vs-2019&quot;

如上所述，Visual Studio 检查其安装位置（例如，网络共享或 Internet），以确定是否有任何更新。 若有更新，Visual Studio 会在窗口右下角显示通知图标来通知用户。

   ![Visual Studio IDE 中的通知图标](media/vs-2019/notification-bar.png &quot;Visual Studio IDE 中的通知图标")

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

* [Visual Studio 管理员指南](visual-studio-administrator-guide.md)
* [启用管理员更新](enabling-administrator-updates.md)
* [应用管理员更新](applying-administrator-updates.md)
* [使用命令行参数安装 Visual Studio](use-command-line-parameters-to-install-visual-studio.md)
* [用于管理 Visual Studio 实例的工具](tools-for-managing-visual-studio-instances.md)
* [Visual Studio 产品生命周期和维护](/visualstudio/releases/2019/servicing/)
