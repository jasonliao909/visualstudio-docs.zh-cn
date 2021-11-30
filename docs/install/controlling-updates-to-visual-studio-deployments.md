---
title: 控制对部署的更新
description: 了解从网络安装时，如何更改 Visual Studio 查找更新的位置。
ms.date: 11/23/2021
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
ms.openlocfilehash: 620c848ee7d52ab802f8b05135f26bdade122a64
ms.sourcegitcommit: 2281b4f1f8737f263c0d7e55e00b5ec81517327d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/25/2021
ms.locfileid: "133108830"
---
# <a name="control-updates-to-network-based-visual-studio-deployments"></a>控制对基于网络的 Visual Studio 部署的更新
> [!WARNING]
> 此内容已合并到其他页面，因此将弃用。 此页已从 TOC 中删除。

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

[!INCLUDE[install_get_support_md](includes/install_get_support_md.md)]

## <a name="see-also"></a>请参阅

* [Visual Studio 管理员指南](visual-studio-administrator-guide.md)
* [启用管理员更新](enabling-administrator-updates.md)
* [应用管理员更新](applying-administrator-updates.md)
* [使用命令行参数安装 Visual Studio](use-command-line-parameters-to-install-visual-studio.md)
* [用于管理 Visual Studio 实例的工具](tools-for-managing-visual-studio-instances.md)
* [Visual Studio 产品生命周期和维护](/visualstudio/releases/2019/servicing/)
