---
title: 创建脱机安装
description: 了解如何在 Internet 连接不可靠或带宽较低时脱机安装 Visual Studio。
ms.date: 3/3/2022
ms.topic: conceptual
f1_keywords:
- offline installation [Visual Studio]
- offline install [Visual Studio]
- layout [Visual Studio]
ms.assetid: f8625d5e-f6ea-4db0-83c0-619b77fab3cf
author: anandmeg
ms.author: meghaanand
manager: jmartens
ms.workload:
- multiple
ms.prod: visual-studio-windows
ms.technology: vs-installation
ms.openlocfilehash: e0db2d0bc3bbf86e88a8781c9c25f9f49436f698
ms.sourcegitcommit: edf8137cd90c67b6078a02c93094f7e1c3bf8930
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/08/2022
ms.locfileid: "139550632"
---
# <a name="create-an-offline-installation-package-of-visual-studio-for-local-installation"></a>创建本地安装的 Visual Studio脱机安装包

Visual Studio 经过精心设计，可在各种网络和计算机配置中良好运行。 对于涉及本地计算机的所有方案，建议使用 [Visual Studio 安装程序](https://visualstudio.microsoft.com/downloads)，这是一个小文件，用于定期检查更新，并帮助你随时了解所有最新的修补程序和功能。 本页上的信息讨论如何创建脱机安装文件包，以在本地计算机上安装。

如果你是企业 IT 管理员，想要将 Visual Studio 部署到客户端工作站网络，或者需要创建要传输或安装到另一台计算机的文件的安装包，请参阅我们的 [Visual Studio](https://aka.ms/vs/admin/guide) 管理员指南和创建基于网络的 Visual Studio [](create-a-network-installation-of-visual-studio.md) 文档。

## <a name="use-the-download-all-then-install-feature"></a>使用“全部下载，然后安装”功能
有时联机访问存在问题。 例如，Internet 连接可能不可靠，或者 Internet 连接的带宽较低。 对于此类情况，我们提供了其他方法来获取Visual Studio。 可以在安装之前使用"全部下载，然后从 Visual Studio 安装程序 安装"功能在本地计算机上下载安装包，或者可以使用命令行创建本地安装包以稍后安装。

若要下载本地安装包，请选择"全部下载"，然后在"下载"窗口的"工作负载"选项卡底部的下拉列表Visual Studio 安装程序。 此功能的目的是将下载的 Visual Studio 包预加载到你计划最终安装 Visual Studio 的同一台计算机上。 通过先在本地下载包，可以在安装客户端之前安全地断开与 internet Visual Studio。

   ![“全部下载后再安装”选项](media/vs-2019/download-all-then-install-from-installer.png)

> [!IMPORTANT]
> "**全部下载，然后安装**"功能Visual Studio本地计算机自定义的安装包。 请勿尝试将下载的安装包转移到另一台计算机，因为它并非以这种方式工作。 相反，如果要下载安装包，将其转移到另一台计算机或将其安装在另一计算机上，则需要创建一个布局，如创建 Visual Studio 的基于[网络的安装文档中所述](create-a-network-installation-of-visual-studio.md)。

还可以配置此实例的未来更新，Visual Studio **全部下载，然后安装行为**。 有关详细信息，请参阅[自定义更新设置](/visualstudio/install/update-visual-studio?#installation-and-download-behaviors-1)文档。

## <a name="use-the-command-line-to-create-a-local-layout"></a>使用命令行创建本地布局

下载需要版本的 Visual Studio引导程序，将其复制到要用作本地布局源位置的目录中。 创建布局后，可以使用它来安装Visual Studio。 引导程序是用于创建、更新和执行其他 Visual Stusio 安装操作所需的可执行文件。 必须拥有 Internet 连接才能完成此操作。

### <a name="step-1---download-the-visual-studio-bootstrapper"></a>步骤 1 - 下载 Visual Studio 引导程序

::: moniker range="vs-2017"

若要获取 Visual Studio 2017 15.9 版的最新引导程序，请下载以下文件之一。 无论何时运行这些引导程序，它们将始终安装最新版本的 Visual Studio 2017。

| 版本                                      | 引导程序            |
|----------------------------------------------|---------------------|
| Visual Studio 2017 Professional 版本 15.9 | [vs_professional.exe](https://aka.ms/vs/15/release/vs_professional.exe) |
| Visual Studio 2017 Enterprise 版本 15.9   | [vs_enterprise.exe](https://aka.ms/vs/15/release/vs_enterprise.exe)   |
| Visual Studio 2017 生成工具版本 15.9  | [vs_buildtools.exe](https://aka.ms/vs/15/release/vs_buildtools.exe)   |

::: moniker-end

::: moniker range="vs-2019"

无论何时运行下面所列的引导程序，它们都将始终安装最新且最安全的 Visual Studio 2019 版本。 或者，如果要安装特定版本的 Visual Studio [2019，请转到 Visual Studio 2019](/visualstudio/releases/2019/history#installing-an-earlier-release) 版本页，该页包含指向每个服务版本的固定版本引导程序的链接，并下载你需要的版本引导程序。 将其复制到要用作本地布局位置的目录中。

| 版本                         | 引导程序                                                                    |
|---------------------------------|-------------------------------------------------------------------------|
| Visual Studio 2019 Professional 版本 16.11 | [vs_professional.exe](https://aka.ms/vs/16/release/vs_professional.exe) |
| Visual Studio 2019 Enterprise 版本 16.11 | [vs_enterprise.exe](https://aka.ms/vs/16/release/vs_enterprise.exe) |
| Visual Studio 2019 生成工具版本 16.11 | [vs_buildtools.exe](https://aka.ms/vs/16/release/vs_buildtools.exe) |

::: moniker-end

::: moniker range="vs-2022"

无论何时运行下面所列的引导程序，它们都始终将在当前通道上安装最新且最安全的 Visual Studio 2022 版本。 或者，如果要安装特定版本或 Visual Studio 2022 的特定通道，请转到 [Visual Studio 2022](/visualstudio/releases/2022/release-history#release-dates-and-build-numbers) 发行历史记录页，该页包含每个通道上每个服务版本的 evergreen 和固定版本引导程序的链接，并下载想要的版本引导程序。 将其复制到要用作本地布局位置的目录中。

| 版本                         | 引导程序                                                            |
|---------------------------------|-------------------------------------------------------------------------|
| Visual Studio 2022 Community    | [vs_community.exe](https://aka.ms/vs/17/release/vs_community.exe)       |
| Visual Studio 2022 Professional | [vs_professional.exe](https://aka.ms/vs/17/release/vs_professional.exe) |
| Visual Studio 2022 Enterprise   | [vs_enterprise.exe](https://aka.ms/vs/17/release/vs_enterprise.exe)     |
| Visual Studio 2022 生成工具   | [vs_buildtools.exe](https://aka.ms/vs/17/release/vs_buildtools.exe)    |

::: moniker-end

::: moniker range="vs-2019"

>[!TIP]
>如果之前下载了特定的引导程序文件，并想要验证它将安装的版本，则操作说明。 在 Windows 中，打开文件资源管理器，右键单击引导程序文件，依次选择“属性”、“详细信息”选项卡，然后查看“产品版本”号    。 若要将该编号与 Visual Studio 的版本匹配，请参阅 [Visual Studio 2019 版本](/visualstudio/releases/2019/history)页面底部的表。

::: moniker-end

::: moniker range=">=vs-2022"

>[!TIP]
>如果你之前下载了一个引导程序文件，并且想要验证它将安装的版本，操作方法如下。 在 Windows 中，打开“文件资源管理器”，右键单击该引导程序文件，选择“属性”，然后选择“详细信息”选项卡。“产品版本”字段将描述该引导程序将安装的[频道和版本](/visualstudio/releases/2022/vs2022-release-rhythm)  。 版本号应始终读取为“指定内容的最新服务版本”，除非显式指定，否则频道为“当前”。 因此，产品版本为 LTSC 17.0 的引导程序将安装 17.0 LTSC 频道上提供的最新 17.0.x 服务版本。 产品版本仅显示“Visual Studio 2022”的引导程序将在当前频道上安装最新版本的 Visual Studio 2022。

::: moniker-end

### <a name="step-2---create-a-local-layout"></a>步骤 2 - 创建本地布局

必须具有 Internet 连接才能完成此步骤。

使用管理员权限打开命令提示符，导航到将引导程序下载到的目录，并使用使用命令行参数安装 [Visual Studio](use-command-line-parameters-to-install-visual-studio.md) 页中定义的引导程序参数来创建本地布局。 下文和[命令行参数示例](command-line-parameter-examples.md)页介绍了使用 Enterprise 引导程序的常见示例。 可以通过从语言`en-US`区域设置列表中将 区域设置更改为区域设置来安装英语[](#list-of-language-locales)外的语言，并且可以使用组件和工作负荷列表进一[](workload-and-component-ids.md)步自定义本地布局。

> [!TIP]
> 为了防止错误出现，请确保完全安装路径的长度小于 80 个字符。

::: moniker range="<=vs-2019"
- 对于 .NET Web 和.NET 桌面开发，请运行：

   ```shell
    vs_enterprise.exe --layout c:\localVSlayout --add Microsoft.VisualStudio.Workload.ManagedDesktop --add Microsoft.VisualStudio.Workload.NetWeb --add Component.GitHub.VisualStudio --includeOptional --lang en-US
    ```
::: moniker-end

::: moniker range=">=vs-2022"
- 对于 .NET Web 和.NET 桌面开发，请运行：

   ```shell
    vs_enterprise.exe --layout c:\localVSlayout --add Microsoft.VisualStudio.Workload.ManagedDesktop --add Microsoft.VisualStudio.Workload.NetWeb --includeOptional --lang en-US
    ```
::: moniker-end

- 对于 .NET 桌面和 Office 开发，请运行：

   ```shell
    vs_enterprise.exe --layout c:\localVSlayout --add Microsoft.VisualStudio.Workload.ManagedDesktop --add Microsoft.VisualStudio.Workload.Office --includeOptional --lang en-US
    ```

- 对于 C++ 桌面开发，请运行：

   ```shell
    vs_enterprise.exe --layout c:\localVSlayout --add Microsoft.VisualStudio.Workload.NativeDesktop --includeRecommended --lang en-US
    ```

- 若要创建包含所有功能的完整本地布局（仅限英文版）（耗时将很长，因为我们提供的功能非常多！），请运行：

   ```shell
    vs_enterprise.exe --layout c:\localVSlayout --lang en-US
    ```

::: moniker range="vs-2017"

   > [!NOTE]
   > 完整的本地布局Visual Studio至少需要 35 GB 磁盘空间。 有关详细信息，请参阅[系统需求](/visualstudio/productinfo/vs2017-system-requirements-vs/)。 

::: moniker-end

::: moniker range="vs-2019"

   > [!NOTE]
   > 完整的本地布局Visual Studio至少需要 41 GB 磁盘空间。 有关详细信息，请参阅[系统需求](/visualstudio/releases/2019/system-requirements/)。

::: moniker-end

::: moniker range="vs-2022"

   > [!NOTE]
   > 完整的本地布局Visual Studio至少需要 45 GB 磁盘空间。 有关详细信息，请参阅[系统需求](/visualstudio/releases/2022/system-requirements/)。

::: moniker-end

### <a name="step-3---install-visual-studio-from-the-local-layout"></a>步骤 3 - Visual Studio本地布局安装
从本地Visual Studio时，Visual Studio安装程序使用文件的本地版本。 但是，如果在安装过程中选择不在布局中的组件，Visual Studio安装程序会尝试从 Internet 下载它们。 若要确保仅安装之前下载的文件，请使用用于创建本地布局的相同命令行选项。[](use-command-line-parameters-to-install-visual-studio.md) 若要确保安装程序不会尝试访问 Internet，请使用 `--noweb` 开关。

例如，如果使用以下命令创建了本地安装布局：

::: moniker range="<=vs-2019"

```shell
vs_enterprise.exe --layout c:\localVSlayout --add Microsoft.VisualStudio.Workload.ManagedDesktop --add Microsoft.VisualStudio.Workload.NetWeb --add Component.GitHub.VisualStudio --includeOptional --lang en-US
```

然后使用此命令运行安装：

```shell
c:\localVSlayout\vs_enterprise.exe --noweb --add Microsoft.VisualStudio.Workload.ManagedDesktop --add Microsoft.VisualStudio.Workload.NetWeb --add Component.GitHub.VisualStudio --includeOptional
```

::: moniker-end

::: moniker range="vs-2022"

```shell
vs_enterprise.exe --layout c:\localVSlayout --add Microsoft.VisualStudio.Workload.ManagedDesktop --add Microsoft.VisualStudio.Workload.NetWeb --includeOptional --lang en-US
```

然后使用此命令运行安装：

```shell
c:\localVSlayout\vs_enterprise.exe --noweb --add Microsoft.VisualStudio.Workload.ManagedDesktop --add Microsoft.VisualStudio.Workload.NetWeb --includeOptional
```

::: moniker-end

> [!IMPORTANT]
> 如果使用的是 Visual Studio Community，则必须在安装后的 30 天内登录产品以激活它。 激活需要 Internet 连接。

> [!NOTE]
> 如果你遇到签名无效的错误，则必须[安装更新的证书](install-certificates-for-visual-studio-offline.md)。 在本地布局中打开"证书"文件夹。 双击每个证书文件，然后单击完成证书管理器向导。 如果要求输入密码，请将密码留空。


### <a name="list-of-language-locales"></a>语言区域设置列表

| **语言-区域设置** | **语言**          |
|---------------------|-----------------------|
| cs-CZ               | 捷克语                 |
| de-DE               | 德语                |
| zh-CN               | 英语               |
| es-ES               | 西班牙语               |
| fr-FR               | 法语                |
| it-IT               | 意大利语               |
| ja-JP               | 日语              |
| ko-KR               | 韩语                |
| pl-PL               | 波兰语                |
| pt-BR               | 葡萄牙语 - 巴西   |
| ru-RU               | 俄语               |
| tr-TR               | 土耳其语               |
| zh-CN               | 简体中文  |
| zh-TW               | 繁体中文 |

[!INCLUDE[install_get_support_md](includes/install_get_support_md.md)]

## <a name="see-also"></a>另请参阅

- [Visual Studio 管理员指南](https://aka.ms/vs/admin/guide)
- [安装 Visual Studio 脱机安装所需的证书](../install/install-certificates-for-visual-studio-offline.md)
- [使用命令行参数安装 Visual Studio](use-command-line-parameters-to-install-visual-studio.md)
- [Visual Studio 工作负荷和组件 ID](workload-and-component-ids.md)
