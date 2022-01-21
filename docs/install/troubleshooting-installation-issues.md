---
title: 安装或升级问题疑难解答
description: 有时，你难免遇到一些问题。 如果 Visual Studio 安装或升级失败，可在此页寻求帮助。
ms.date: 09/14/2021
ms.custom: vs-acquisition
ms.topic: troubleshooting
helpviewer_keywords:
- '{{PLACEHOLDER}}'
- '{{PLACEHOLDER}}'
ms.assetid: 556EDD3F-E365-43EE-B3DD-03AA4353F75B
author: anandmeg
ms.author: meghaanand
manager: jmartens
ms.workload:
- multiple
ms.prod: visual-studio-windows
ms.technology: vs-installation
ms.openlocfilehash: 1d1d5571e0f1c781e547203ce11dabbb9e1a4be8
ms.sourcegitcommit: 7746657b87b22a7684e79e508af598b02dfe24b7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/21/2022
ms.locfileid: "137609620"
---
# <a name="troubleshoot-visual-studio-installation-and-upgrade-issues"></a>Visual Studio 安装和升级问题疑难解答

> [!IMPORTANT]
> 安装时遇到问题？ 我们可以为你提供帮助。 我们提供[安装聊天](https://visualstudio.microsoft.com/vs/support/#talktous)（仅英语）支持选项。

本疑难解答指南包含可解决大多数安装问题的分步说明。

## <a name="online-installations"></a>联机安装

以下步骤适用于典型的联机安装。 对于脱机安装，请参阅[如何排查脱机安装问题](#offline-installations)。

### <a name="step-1---check-whether-the-problem-is-a-known-issue"></a>第 1 步 - 检查该问题是否为已知问题

::: moniker range="vs-2017"

Visual Studio 安装程序存在一些已知问题，Microsoft 正在努力修复中。 若要确定你遇到的问题是否有解决办法，请参阅[发行说明的“已知问题”部分](/visualstudio/releasenotes/vs2017-relnotes#-known-issues)。

::: moniker-end

::: moniker range="vs-2019"

Visual Studio 安装程序存在一些已知问题，Microsoft 正在努力修复中。 若要确定你遇到的问题是否有解决办法，请参阅[发行说明的“已知问题”部分](/visualstudio/releases/2019/release-notes#-known-issues)。

::: moniker-end

::: moniker range=">=vs-2022"

Visual Studio 安装程序存在一些已知问题，Microsoft 正在努力修复中。 在[发行说明的“已知问题”部分](/visualstudio/releases/2022/release-notes#-known-issues)检查你遇到的问题是否已解决或查找解决方法。

::: moniker-end

### <a name="step-2---try-repairing-visual-studio"></a>第 2 步 - 尝试修复 Visual Studio

修复可解决许多常见的更新问题。 有关何时以及如何修复 Visual Studio 的详细信息，请参阅[修复 Visual Studio](repair-visual-studio.md)。

### <a name="step-3---check-with-the-developer-community"></a>第 3 步 - 通过开发人员社区获取帮助

在 [Visual Studio 开发者社区](https://aka.ms/feedback/suggest?space=8)渠道中搜索你看到的错误消息。 其他社区成员可能已经找到了你所遇到的问题的解决方法。

### <a name="step-4---delete-the-visual-studio-installer-folder-to-fix-upgrade-problems"></a>第 4 步 - 删除 Visual Studio 安装程序文件夹以修复升级问题

Visual Studio 安装程序引导程序是轻型的可执行文件，用于启动 Visual Studio 安装程序的安装。 删除 Visual Studio 安装程序文件，然后重新运行引导程序即可解决一些更新失败问题。

> [!NOTE]
> 执行以下操作将重新安装 Visual Studio 安装程序文件并重置安装元数据。

::: moniker range="vs-2017"

1. 关闭 Visual Studio 安装程序。
1. 删除 Visual Studio 安装程序安装目录。 通常，该目录是 `C:\Program Files (x86)\Microsoft Visual Studio\Installer`。
1. 运行 Visual Studio 安装程序引导程序。 引导程序位于“下载”文件夹中，文件名格式为 `vs_[Visual Studio edition]__*.exe`。 如果找不到此应用程序，可以转到 [Visual Studio 下载](https://visualstudio.microsoft.com/vs/older-downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=vs+2017+download)页，然后单击你的 Visual Studio 版本所对应的“下载”，便可下载引导程序。 然后，运行此可执行文件，重置安装元数据。
1. 尝试重新安装或更新 Visual Studio。 如果安装程序仍无法安装，请转到下一步。

::: moniker-end

::: moniker range="vs-2019"

1. 关闭 Visual Studio 安装程序。
1. 删除 Visual Studio 安装程序目录。 通常，该目录是 `C:\Program Files (x86)\Microsoft Visual Studio\Installer`。
1. 运行 Visual Studio 安装程序引导程序。 引导程序可能位于“下载”文件夹中，其文件名与 `vs_[Visual Studio edition]__*.exe` 模式匹配。 如果找不到此应用程序，可以转到 [Visual Studio 下载](https://visualstudio.microsoft.com/downloads)页，然后单击你的 Visual Studio 版本所对应的“下载”，便可下载引导程序。 然后，运行此可执行文件，重置安装元数据。
1. 尝试重新安装或更新 Visual Studio。 如果安装程序仍无法安装，请转到下一步。

::: moniker-end

::: moniker range=">=vs-2022"

1. 关闭 Visual Studio 安装程序。
1. 删除 Visual Studio 安装程序文件夹。 文件夹路径通常为 `C:\Program Files (x86)\Microsoft Visual Studio\Installer`。
1. 运行 Visual Studio 安装程序引导程序。 引导程序可能位于“下载”文件夹中，其文件名与 `vs_[Visual Studio edition]__*.exe` 模式匹配。 或者，可以从 [Visual Studio 下载](https://visualstudio.microsoft.com/downloads)页下载适用于你的 Visual Studio 版本的引导程序。 然后，运行此可执行文件，重置安装元数据。
1. 尝试重新安装或更新 Visual Studio。 如果 Visual Studio 安装程序仍然失败，请继续执行[报告问题](#step-5---report-a-problem)步骤。

::: moniker-end

### <a name="step-5---report-a-problem"></a>第 5 步 - 报告问题

在某些情况下（例如，有损坏的文件时），可能需要根据不同的案例排查问题。 为了帮助我们为你解决问题，请执行以下步骤：

::: moniker range="vs-2017"

1. 收集安装日志。 有关详细信息，请参阅[如何获取 Visual Studio 安装日志](#installation-logs)。
1. 打开 Visual Studio 安装程序，然后单击“报告问题”，打开 Visual Studio 反馈工具。
![显示 Visual Studio 安装程序中“提供反馈”按钮的屏幕截图。](media/report-a-problem.png)
1. 为问题报告命名一个标题，然后输入相关详细信息。 单击“下一步”，转到“附件”部分，然后附加生成的日志文件（此文件通常位于 `%TEMP%\vslogs.zip`）。
1. 单击“下一步”检查问题报告，然后单击“提交” 。

::: moniker-end

::: moniker range="vs-2019"

1. 收集安装日志。 有关详细信息，请参阅[如何获取 Visual Studio 安装日志](#installation-logs)。
1. 打开 Visual Studio 安装程序，然后单击“报告问题”，打开 Visual Studio 反馈工具。
![显示 Visual Studio 安装程序中“提供反馈”按钮的屏幕截图。](media/vs-2019/vs-installer-report-problem.png)
1. 为问题报告命名一个标题，然后输入相关详细信息。 单击“下一步”，转到“附件”部分，然后附加生成的日志文件（此文件通常位于 `%TEMP%\vslogs.zip`）。
1. 单击“下一步”，检查问题报告，然后单击“提交”。

::: moniker-end

::: moniker range=">=vs-2022"

1. 收集安装日志。 有关详细信息，请参阅[如何获取 Visual Studio 安装日志](#installation-logs)。
1. 打开 Visual Studio 安装程序，然后选择“报告问题”打开 Visual Studio 反馈工具。
![显示 Visual Studio 安装程序中“提供反馈”按钮的屏幕截图。](media/vs-2022/vs-installer-report-problem.png)
1. 为问题报告提供标题，并提供相关的详细信息。 Visual Studio 安装程序的最新安装日志将自动添加到问题报告的“其他附件”部分。
1. 选择“提交”。

::: moniker-end

### <a name="step-6---remove-visual-studio-installation-files"></a>第 6 步 - 删除 Visual Studio 安装文件

作为最后一招，可以删除所有 Visual Studio 安装文件和产品信息：

1. 按照本文中的步骤操作：[删除 Visual Studio](uninstall-visual-studio.md#remove)页面。
1. 重新运行 Visual Studio 安装程序引导程序。 引导程序可能位于“下载”文件夹中，其文件名与 `vs_[Visual Studio edition]__*.exe` 模式匹配。 或者，可以从 [Visual Studio 下载](https://visualstudio.microsoft.com/downloads)页下载适用于你的 Visual Studio 版本的引导程序。
1. 尝试重新安装 Visual Studio。

### <a name="step-7---contact-us-optional"></a>第 7 步 - 与我们联系（可选）

如果上述步骤均未帮助你成功安装或升级 Visual Studio，请使用我们的[实时聊天](https://visualstudio.microsoft.com/vs/support/#talktous)支持选项（仅英语）与我们联系，以获取进一步的帮助。

## <a name="offline-installations"></a>脱机安装

下面列出了创建[脱机安装](create-an-offline-installation-of-visual-studio.md)和从本地布局安装时存在的一些已知问题，以及可能对你有所帮助的解决办法。

| 问题       | 解决方案 |
| ----------- | -------- |
| 用户无法访问文件 | 确保调整权限 (ACL)，使其在你共享脱机安装之前先向其他用户授予读取访问权限。 |
| 无法安装新的工作负载、组件或语言包 | 如果从部分布局进行安装，并选择事先未为该部分布局下载的工作负载、组件或语言，请确保可以访问 Internet。 |

若要解决[网络安装](create-a-network-installation-of-visual-studio.md)问题，请参阅[排查在安装或使用 Visual Studio 时出现的网络相关错误](troubleshooting-network-related-errors-in-visual-studio.md)。

## <a name="installation-logs"></a>安装日志

安装日志可帮助我们排查大部分安装问题。 使用 Visual Studio 安装程序中的[报告问题](../ide/how-to-report-a-problem-with-visual-studio.md)提交问题时，Visual Studio 安装程序的最新安装日志将自动添加到报告中。

如果你联系 Microsoft 支持部门，可能会被要求使用 [Microsoft Visual Studio 和 .NET Framework 日志收集工具](https://www.microsoft.com/download/details.aspx?id=12493)收集安装日志。 日志收集工具从 Visual Studio 安装的所有组件（包括 .NET Framework、Windows SDK 和 SQL Server）收集安装日志。 它还会收集计算机信息、Windows Installer 清单，以及 Visual Studio 安装程序、Windows Installer 和系统还原的 Windows 事件日志信息。

收集日志的具体步骤：

1. [下载工具](https://www.microsoft.com/download/details.aspx?id=12493)。
1. 打开管理命令提示符。
1. 运行该工具所保存到的文件夹中的 `Collect.exe`。
1. 该工具会在 `%TEMP%` 文件夹中生成 `vslogs.zip` 文件，该文件的路径通常为 `C:\Users\YourName\AppData\Local\Temp\vslogs.zip`。

> [!NOTE]
> 工具必须在安装失败时使用的同一用户帐户下运行。 若要从其他用户帐户运行工具，请设置 `–user:<name>` 选项，以指定安装失败时使用的用户帐户。 有关其他选项和使用情况信息，请通过管理员命令提示符运行 `Collect.exe -?`。

## <a name="problems-installing-webview2"></a>安装 WebView2 时出现问题

WebView2 是应用程序所需的Visual Studio，但组织的组策略可能会阻止安装此组件。 阻止安装 WebView2 将Visual Studio安装 WebView2。 

两个策略控制安装 WebView2 的能力[：Microsoft Edge" (WebView) "](/deployedge/microsoft-edge-update-policies#install-webview)和[Microsoft Edge"InstallDefault"。](/deployedge/microsoft-edge-update-policies#installdefault)

• 如果Microsoft Edge" (WebView) "策略，它将确定是否可以安装 WebView2。
• 如果未Microsoft Edge"安装 (WebView) "策略，Microsoft Edge"InstallDefault"策略将确定是否可以安装 WebView2。

> [!NOTE]
> 如果未配置任何策略，则组织不允许安装 WebView2。

## <a name="live-help"></a>实时帮助

如果本故障排除指南中列出的解决方法无法帮助你成功安装或升级 Visual Studio，请使用我们的[实时聊天](https://visualstudio.microsoft.com/vs/support/#talktous)支持选项（仅限英语）以获取进一步的帮助。

## <a name="see-also"></a>请参阅

* [修复 Visual Studio](repair-visual-studio.md)
* [删除 Visual Studio](uninstall-visual-studio.md#remove)
* [在防火墙或代理服务器后面安装和使用 Visual Studio 和 Azure 服务](install-and-use-visual-studio-behind-a-firewall-or-proxy-server.md)
* [用于检测和管理 Visual Studio 实例的工具](tools-for-managing-visual-studio-instances.md)
* [Visual Studio 管理员指南](visual-studio-administrator-guide.md)