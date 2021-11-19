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
ms.openlocfilehash: 5cad03cae4baed3aff150b9af613de432f6df87c
ms.sourcegitcommit: a98fa8a8362525f67824ce52b7e71757f10f1362
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/18/2021
ms.locfileid: "132736676"
---
# <a name="create-an-offline-installation-of-visual-studio"></a>创建 Visual Studio 的脱机安装

我们设计的 Visual Studio 在各种网络和计算机配置中都能正常工作。 建议你使用[Visual Studio 安装程序](https://visualstudio.microsoft.com/downloads)，这是一个小文件，用于定期检查联机更新，并可帮助你随时了解最新的修补程序和功能。 但是，有时联机访问会出现问题。 例如，你可能具有不可靠的 internet 连接或 internet 连接的带宽较低。 对于这种情况，我们提供了一些其他方法用于获取 Visual Studio。 你可以使用 "**全部下载"，然后** 从 Visual Studio 安装程序安装功能，在安装之前将文件下载到本地计算机上的本地缓存中，也可以使用命令行创建文件的本地缓存，以便以后安装。

> [!NOTE]
> 如果你是企业 IT 管理员，想要对客户端工作站的网络执行 Visual Studio 部署，请参阅我们的[Visual Studio 管理员指南](https://aka.ms/vs/admin/guide)。

## <a name="use-the-download-all-then-install-feature"></a>使用“全部下载，然后安装”功能

在 Visual Studio 安装程序的 "**工作负荷**" 选项卡上，可以选择对话框底部下拉列表中的 "**全部下载"、"安装**" 选项。 此功能的目的是减少将 Visual Studio 包下载到计划最终安装 Visual Studio 的计算机上。 首先将包下载到本地缓存中，然后在安装 Visual Studio 之前，可以安全地从 internet 断开连接。

   ![“全部下载后再安装”选项](media/vs-2019/download-all-then-install-from-installer.png)

> [!IMPORTANT]
> 不要使用 " **全部下载"、"安装** " 功能创建想要传输到另一台计算机的本地缓存。 这不是该功能的运作方式。 

你还可以将更新配置为遵循 " **全部下载"、"安装"** 行为。 有关详细信息，请参阅 [自定义更新设置](/visualstudio/install/update-visual-studio?#installation-and-download-behaviors-1) 文档。

## <a name="use-the-command-line-to-create-a-local-cache"></a>使用命令行创建本地缓存

可下载小型引导程序文件，然后使用命令行创建本地缓存。 创建缓存后，可以使用它来安装 Visual Studio。 

### <a name="step-1---download-the-visual-studio-bootstrapper"></a>步骤 1 - 下载 Visual Studio 引导程序

必须连接 Internet 才能完成此步骤。

::: moniker range="vs-2017"

若要获取 Visual Studio 2017 版本15.9 的最新引导程序，请下载下面其中一个文件。 无论何时运行，这些引导程序都将始终安装最新版本的 Visual Studio 2017。

| 版本                                      | 引导程序            |
|----------------------------------------------|---------------------|
| Visual Studio 2017 Professional 版本 15.9 | [vs_professional.exe](https://aka.ms/vs/15/release/vs_professional.exe) |
| Visual Studio 2017 Enterprise 版本 15.9   | [vs_enterprise.exe](https://aka.ms/vs/15/release/vs_enterprise.exe)   |
| Visual Studio 2017 生成工具版本 15.9  | [vs_buildtools.exe](https://aka.ms/vs/15/release/vs_buildtools.exe)   |

::: moniker-end

::: moniker range="vs-2019"

若要获取将始终安装最新版本16.11 的 Visual Studio 2019 的最新引导程序，请下载下面其中一个文件。 或者，如果你想要安装 Visual Studio 2019 的特定版本，请参阅[Visual Studio 2019 版本](/visualstudio/releases/2019/history#installing-an-earlier-release)"页，其中包含指向每个维护版本的已修复版本引导程序的链接。 

| 版本                         | 引导程序                                                                    |
|---------------------------------|-------------------------------------------------------------------------|
| Visual Studio 2019 Professional 版本16.11 | [vs_professional.exe](https://aka.ms/vs/16/release/vs_professional.exe) |
| Visual Studio 2019 Enterprise 版本16.11 | [vs_enterprise.exe](https://aka.ms/vs/16/release/vs_enterprise.exe) |
| Visual Studio 2019 生成工具版本16.11 | [vs_buildtools.exe](https://aka.ms/vs/16/release/vs_buildtools.exe) |

::: moniker-end

::: moniker range="vs-2022"

若要获取将始终安装最新版本的最新版本的 Visual Studio 2022 的最新引导程序，请下载下面其中一个文件。 或者，如果要安装 Visual Studio 2022 的特定版本或特定通道，请参阅[Visual Studio 2022 发行历史记录](/visualstudio/releases/2022/release-history#release-dates-and-build-numbers)页，其中包含指向每个维护版本的已修复版本引导程序的链接。 

| 版本                         | 引导程序                                                               |
|---------------------------------|-------------------------------------------------------------------------|
| Visual Studio 2022 Community    | [vs_community.exe](https://aka.ms/vs/17/release/vs_community.exe)       |
| Visual Studio 2022 Professional | [vs_professional.exe](https://aka.ms/vs/17/release/vs_professional.exe) |
| Visual Studio 2022 Enterprise   | [vs_enterprise.exe](https://aka.ms/vs/17/release/vs_enterprise.exe)     |
| Visual Studio 2022 生成工具   | [vs_buildtools.exe](https://aka.ms/vs/17/release/vs_buildtools.exe)         |

::: moniker-end

::: moniker range="vs-2019"

>[!TIP]
>如果以前从[Visual Studio 2019 版本](/visualstudio/releases/2019/history#release-dates-and-build-numbers)页面下载了特定的引导程序文件，并且想要验证它将安装何种版本，以下是操作方法。 在 Windows 中，打开文件资源管理器，右键单击引导程序文件，依次选择“属性”、“详细信息”选项卡，然后查看“产品版本”号    。 若要将该数字与 Visual Studio 的版本相匹配，请参阅该页面底部的表格。

::: moniker-end

::: moniker range=">=vs-2022"

>[!TIP]
>如果你以前下载了一个引导程序文件，并且想要验证它将安装何种版本，以下是操作方法。 在 Windows 中，打开文件资源管理器，右键单击引导程序文件，选择 "**属性**"，然后选择 "**详细信息**" 选项卡。"**产品版本**" 字段将描述引导程序将安装的 [通道和版本](/visualstudio/releases/2022/vs2022-release-rhythm)。 版本号应始终作为 "所指定内容的最新服务版本" 读取，除非显式指定，否则通道是最新的。 因此，产品版本为 LTSC 17.0 的引导程序将安装 17.0 LTSC 通道上提供的最新17.0 服务版本。 使用产品版本的引导程序，该产品版本只是说 Visual Studio 2022 将在当前频道上安装最新版本的 Visual Studio 2022。

::: moniker-end

### <a name="step-2---create-a-local-install-cache"></a>步骤 2 - 创建本地安装缓存

必须连接 Internet 才能完成此步骤。

打开命令提示符并使用[使用命令行参数安装 Visual Studio](use-command-line-parameters-to-install-visual-studio.md) 页中定义的引导程序参数来创建本地安装缓存。 下文和[命令行参数示例](command-line-parameter-examples.md)页介绍了使用 Enterprise 引导程序的常见示例。 您可以通过 `en-US` 从 [语言区域设置列表](#list-of-language-locales)中更改为区域设置来安装英语以外的语言，还可以使用 [组件和工作负荷列表](workload-and-component-ids.md) 来进一步自定义本地缓存。

> [!TIP]
> 为了防止错误出现，请确保完全安装路径的长度小于 80 个字符。

- 对于 .NET Web 和.NET 桌面开发，请运行：
::: moniker range="<=vs-2019"
   ```shell
    vs_enterprise.exe --layout c:\localVScache --add Microsoft.VisualStudio.Workload.ManagedDesktop --add Microsoft.VisualStudio.Workload.NetWeb --add Component.GitHub.VisualStudio --includeOptional --lang en-US
    ```
::: moniker-end

::: moniker range=">=vs-2022"
   ```shell
    vs_enterprise.exe --layout c:\vslayout --add Microsoft.VisualStudio.Workload.ManagedDesktop --add Microsoft.VisualStudio.Workload.NetWeb --includeOptional --lang en-US
    ```
::: moniker-end

::: moniker-end

::: moniker range="vs-2022"

- For .NET web and .NET desktop development, run:

   ```shell
    vs_enterprise.exe --layout c:\localVScache --add Microsoft.VisualStudio.Workload.ManagedDesktop --add Microsoft.VisualStudio.Workload.NetWeb --includeOptional --lang en-US
    ```

::: moniker-end

- For .NET desktop and Office development, run:

   ```shell
    vs_enterprise.exe --layout c:\localVScache --add Microsoft.VisualStudio.Workload.ManagedDesktop --add Microsoft.VisualStudio.Workload.Office --includeOptional --lang en-US
    ```

- For C++ desktop development, run:

   ```shell
    vs_enterprise.exe --layout c:\localVScache --add Microsoft.VisualStudio.Workload.NativeDesktop --includeRecommended --lang en-US
    ```

- To create a complete local cache, English only, with all features (this will take a long time&mdash;we have _lots_ of features!), run:

   ```shell
    vs_enterprise.exe --layout c:\localVScache --lang en-US
    ```

::: moniker range="vs-2017"

   > [!NOTE]
   > A complete local cache of Visual Studio requires a minimum of 35 GB of disk space. For more information, see [System requirements](/visualstudio/productinfo/vs2017-system-requirements-vs/). 

::: moniker-end

::: moniker range="vs-2019"

   > [!NOTE]
   > A complete local cache of Visual Studio requires a minimum of 41 GB of disk space. For more information, see [System requirements](/visualstudio/releases/2019/system-requirements/).

::: moniker-end

::: moniker range="vs-2022"

   > [!NOTE]
   > A complete local cache of Visual Studio requires a minimum of 45 GB of disk space. For more information, see [System requirements](/visualstudio/releases/2022/system-requirements/).

::: moniker-end

### Step 3 - Install Visual Studio from the local cache
When you install Visual Studio from a local install cache, the Visual Studio installer uses the local cached versions of the files. But, if you select components during installation that aren't in the cache, then the Visual Studio installer will attempt to download them from the internet. To make sure that you install only the files that you've previously downloaded, use the same [command-line options](use-command-line-parameters-to-install-visual-studio.md) that you used to create the local cache. To make sure your installer doesn't try to access the internet, use the `--noweb` switch.

For example, if you created a local installation cache with the following command:

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
> 如果你遇到签名无效的错误，则必须[安装更新的证书](install-certificates-for-visual-studio-offline.md)。 打开本地缓存中的 "证书" 文件夹。 双击每个证书文件，然后单击完成证书管理器向导。 如果要求输入密码，请将密码留空。


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
