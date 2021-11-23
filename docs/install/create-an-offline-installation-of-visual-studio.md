---
title: 创建脱机安装
description: 了解如何在 Internet 连接不可靠或带宽较低时脱机安装 Visual Studio。
ms.date: 4/16/2021
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
ms.openlocfilehash: 20d2d3324dcd96af4c2e5d679642034e1816c98b
ms.sourcegitcommit: 8b44ba7864f67afa476708d5092729345e689f93
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/20/2021
ms.locfileid: "132861583"
---
# <a name="create-an-offline-installation-of-visual-studio"></a>创建 Visual Studio 的脱机安装

Visual Studio 经过精心设计，可在各种网络和计算机配置中良好运行。 建议使用 [Visual Studio 安装程序](https://visualstudio.microsoft.com/downloads)，这是一个小文件，用于定期检查联机更新，并帮助你随时了解所有最新的修补程序和功能。 但是，有时联机访问存在问题。 例如，Internet 连接可能不可靠，或者 Internet 连接的带宽较低。 对于此类情况，我们提供了一些其他方法来获取 Visual Studio。 可使用 Visual Studio 安装程序中的“全部下载后再安装”功能，在安装之前将文件下载到本地计算机上的本地缓存中，或者可使用命令行创建文件的本地缓存，以便以后安装。

> [!NOTE]
> 如果你是企业 IT 管理员，希望将 Visual Studio 部署到客户端工作站网络，请参阅 [Visual Studio 管理员指南](https://aka.ms/vs/admin/guide)。

## <a name="use-the-download-all-then-install-feature"></a>使用“全部下载，然后安装”功能

在 Visual Studio 安装程序的“工作负载”选项卡上，可在对话框底部的下拉列表中选择“全部下载后再安装”选项 。 此功能的目的是将下载的 Visual Studio 包预加载到你计划最终安装 Visual Studio 的同一台计算机上。 通过先将包下载到本地缓存，可在安装 Visual Studio 之前安全地断开与 Internet 的连接。

   ![“全部下载后再安装”选项](media/vs-2019/download-all-then-install-from-installer.png)

> [!IMPORTANT]
> 请勿使用“全部下载后再安装”功能来创建要传输到另一台计算机的本地缓存。 这不是该功能的运作方式。 

你还可将更新配置为遵守“全部下载后再安装”行为。 有关详细信息，请参阅[自定义更新设置](/visualstudio/install/update-visual-studio?#installation-and-download-behaviors-1)文档。

## <a name="use-the-command-line-to-create-a-local-cache"></a>使用命令行创建本地缓存

可下载小型引导程序文件，然后使用命令行创建本地缓存。 创建缓存后，可使用它来安装 Visual Studio。 

### <a name="step-1---download-the-visual-studio-bootstrapper"></a>步骤 1 - 下载 Visual Studio 引导程序

必须连接 Internet 才能完成此步骤。

::: moniker range="vs-2017"

若要获取 Visual Studio 2017 15.9 版的最新引导程序，请下载以下文件之一。 无论何时运行这些引导程序，它们将始终安装最新版本的 Visual Studio 2017。

| 版本                                      | 引导程序            |
|----------------------------------------------|---------------------|
| Visual Studio 2017 Professional 版本 15.9 | [vs_professional.exe](https://aka.ms/vs/15/release/vs_professional.exe) |
| Visual Studio 2017 Enterprise 版本 15.9   | [vs_enterprise.exe](https://aka.ms/vs/15/release/vs_enterprise.exe)   |
| Visual Studio 2017 生成工具版本 15.9  | [vs_buildtools.exe](https://aka.ms/vs/15/release/vs_buildtools.exe)   |

::: moniker-end

::: moniker range="vs-2019"

若要获取始终安装最新版本 16.11 的 Visual Studio 2019 的最新引导程序，请下载以下文件之一。 或者，如果要安装特定版本的 Visual Studio 2019，请转到 [Visual Studio 2019 版本](/visualstudio/releases/2019/history#installing-an-earlier-release)页，该页包含指向每个服务版本的固定版本引导程序的链接。 

| 版本                         | 引导程序                                                                    |
|---------------------------------|-------------------------------------------------------------------------|
| Visual Studio 2019 Professional 版本 16.11 | [vs_professional.exe](https://aka.ms/vs/16/release/vs_professional.exe) |
| Visual Studio 2019 Enterprise 版本 16.11 | [vs_enterprise.exe](https://aka.ms/vs/16/release/vs_enterprise.exe) |
| Visual Studio 2019 生成工具版本 16.11 | [vs_buildtools.exe](https://aka.ms/vs/16/release/vs_buildtools.exe) |

::: moniker-end

::: moniker range="vs-2022"

若要获取始终安装最新当前频道版本的 Visual Studio 2022 的最新引导程序，请下载以下文件之一。 或者，如果要安装 Visual Studio 2022 的特定版本或特定频道，请转到 [Visual Studio 2022 版本历史记录](/visualstudio/releases/2022/release-history#release-dates-and-build-numbers)页，该页包含指向每个服务版本的固定版本引导程序的链接。 

| 版本                         | 引导程序                                                               |
|---------------------------------|-------------------------------------------------------------------------|
| Visual Studio 2022 Community    | [vs_community.exe](https://aka.ms/vs/17/release/vs_community.exe)       |
| Visual Studio 2022 Professional | [vs_professional.exe](https://aka.ms/vs/17/release/vs_professional.exe) |
| Visual Studio 2022 Enterprise   | [vs_enterprise.exe](https://aka.ms/vs/17/release/vs_enterprise.exe)     |
| Visual Studio 2022 生成工具   | [vs_buildtools.exe](https://aka.ms/vs/17/release/vs_buildtools.exe)         |

::: moniker-end

::: moniker range="vs-2019"

>[!TIP]
>如果之前从 [Visual Studio 2019 版本](/visualstudio/releases/2019/history#release-dates-and-build-numbers)页下载了特定的引导程序文件，并想要验证它将安装的版本，操作方法如下。 在 Windows 中，打开文件资源管理器，右键单击引导程序文件，依次选择“属性”、“详细信息”选项卡，然后查看“产品版本”号    。 若要将该编号与 Visual Studio 版本匹配，请参阅该页底部的表。

::: moniker-end

::: moniker range=">=vs-2022"

>[!TIP]
>如果你之前下载了一个引导程序文件，并且想要验证它将安装的版本，操作方法如下。 在 Windows 中，打开“文件资源管理器”，右键单击该引导程序文件，选择“属性”，然后选择“详细信息”选项卡。“产品版本”字段将描述该引导程序将安装的[频道和版本](/visualstudio/releases/2022/vs2022-release-rhythm)  。 版本号应始终读取为“指定内容的最新服务版本”，除非显式指定，否则频道为“当前”。 因此，产品版本为 LTSC 17.0 的引导程序将安装 17.0 LTSC 频道上提供的最新 17.0.x 服务版本。 产品版本仅显示“Visual Studio 2022”的引导程序将在当前频道上安装最新版本的 Visual Studio 2022。

::: moniker-end

### <a name="step-2---create-a-local-install-cache"></a>步骤 2 - 创建本地安装缓存

必须连接 Internet 才能完成此步骤。

打开命令提示符并使用[使用命令行参数安装 Visual Studio](use-command-line-parameters-to-install-visual-studio.md) 页中定义的引导程序参数来创建本地安装缓存。 下文和[命令行参数示例](command-line-parameter-examples.md)页介绍了使用 Enterprise 引导程序的常见示例。 可以通过从[语言区域设置列表](#list-of-language-locales)中将 `en-US` 更改为区域设置来安装非英语语言，也可以使用[组件和工作负载列表](workload-and-component-ids.md)来进一步自定义本地缓存。

> [!TIP]
> 为了防止错误出现，请确保完全安装路径的长度小于 80 个字符。

::: moniker range="<=vs-2019"
- 对于 .NET Web 和.NET 桌面开发，请运行：

   ```shell
    vs_enterprise.exe --layout c:\localVScache --add Microsoft.VisualStudio.Workload.ManagedDesktop --add Microsoft.VisualStudio.Workload.NetWeb --add Component.GitHub.VisualStudio --includeOptional --lang en-US
    ```
::: moniker-end

::: moniker range=">=vs-2022"
- 对于 .NET Web 和.NET 桌面开发，请运行：

   ```shell
    vs_enterprise.exe --layout c:\vslayout --add Microsoft.VisualStudio.Workload.ManagedDesktop --add Microsoft.VisualStudio.Workload.NetWeb --includeOptional --lang en-US
    ```
::: moniker-end

- 对于 .NET 桌面和 Office 开发，请运行：

   ```shell
    vs_enterprise.exe --layout c:\localVScache --add Microsoft.VisualStudio.Workload.ManagedDesktop --add Microsoft.VisualStudio.Workload.Office --includeOptional --lang en-US
    ```

- 对于 C++ 桌面开发，请运行：

   ```shell
    vs_enterprise.exe --layout c:\localVScache --add Microsoft.VisualStudio.Workload.NativeDesktop --includeRecommended --lang en-US
    ```

- 若要创建包含所有功能的完整本地缓存（仅限英文版）（耗时将很长，因为我们提供的功能非常多！），请运行：

   ```shell
    vs_enterprise.exe --layout c:\localVScache --lang en-US
    ```

::: moniker range="vs-2017"

   > [!NOTE]
   > 完整的 Visual Studio 本地缓存至少需要 35 GB 磁盘空间。 有关详细信息，请参阅[系统需求](/visualstudio/productinfo/vs2017-system-requirements-vs/)。 

::: moniker-end

::: moniker range="vs-2019"

   > [!NOTE]
   > 完整的 Visual Studio 本地缓存至少需要 41 GB 磁盘空间。 有关详细信息，请参阅[系统需求](/visualstudio/releases/2019/system-requirements/)。

::: moniker-end

::: moniker range="vs-2022"

   > [!NOTE]
   > 完整的 Visual Studio 本地缓存至少需要 45 GB 磁盘空间。 有关详细信息，请参阅[系统需求](/visualstudio/releases/2022/system-requirements/)。

::: moniker-end

### <a name="step-3---install-visual-studio-from-the-local-cache"></a>步骤 3 - 从本地缓存安装 Visual Studio
当你从本地安装缓存安装 Visual Studio 时，Visual Studio 安装程序会使用这些文件的本地缓存版本。 不过，如果你在安装过程中选择的组件不在缓存中，则 Visual Studio 安装程序将尝试从 Internet 下载。 若要确保仅安装先前下载的文件，请使用在创建本地缓存时所用的相同[命令行选项](use-command-line-parameters-to-install-visual-studio.md)。 若要确保安装程序不会尝试访问 Internet，请使用 `--noweb` 开关。

例如，如果使用以下命令创建了本地安装缓存：

::: moniker range="<=vs-2019"

```shell
vs_enterprise.exe --layout c:\localVScache --add Microsoft.VisualStudio.Workload.ManagedDesktop --add Microsoft.VisualStudio.Workload.NetWeb --add Component.GitHub.VisualStudio --includeOptional --lang en-US
```

然后使用此命令运行安装：

```shell
c:\localVScache\vs_enterprise.exe --noweb --add Microsoft.VisualStudio.Workload.ManagedDesktop --add Microsoft.VisualStudio.Workload.NetWeb --add Component.GitHub.VisualStudio --includeOptional
```

::: moniker-end

::: moniker range="vs-2022"

```shell
vs_enterprise.exe --layout c:\localVScache --add Microsoft.VisualStudio.Workload.ManagedDesktop --add Microsoft.VisualStudio.Workload.NetWeb --includeOptional --lang en-US
```

然后使用此命令运行安装：

```shell
c:\localVScache\vs_enterprise.exe --noweb --add Microsoft.VisualStudio.Workload.ManagedDesktop --add Microsoft.VisualStudio.Workload.NetWeb --includeOptional
```

::: moniker-end

> [!IMPORTANT]
> 如果使用的是 Visual Studio Community，则必须在安装后的 30 天内登录产品以激活它。 激活需要 Internet 连接。

> [!NOTE]
> 如果你遇到签名无效的错误，则必须[安装更新的证书](install-certificates-for-visual-studio-offline.md)。 在本地缓存中打开证书文件夹。 双击每个证书文件，然后单击完成证书管理器向导。 如果要求输入密码，请将密码留空。


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
