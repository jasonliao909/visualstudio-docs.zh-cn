---
title: 通过响应文件自动执行安装
description: 了解如何创建 JSON 响应文件，以便自动安装 Visual Studio
ms.date: 11/23/2021
ms.topic: conceptual
helpviewer_keywords:
- response file
- automate
- installation
- command-line
author: anandmeg
ms.author: meghaanand
manager: jmartens
ms.workload:
- multiple
ms.prod: visual-studio-windows
ms.technology: vs-installation
ms.openlocfilehash: c3630257019227298285e32cb640dfec4f40b0a1
ms.sourcegitcommit: 7a300823cf1bd3355be03bde561cf2777bc09eae
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2021
ms.locfileid: "133978103"
---
# <a name="programmatically-configure-default-settings-using-a-response-file"></a>使用响应文件以编程方式配置默认设置

Visual Studio 响应文件是 [JSON](http://json-schema.org/) 文件，其内容反映了命令行参数和实际参数。 响应文件用于在产品的初始安装过程中初始化设置。 

## <a name="automate-installation"></a>自动安装
部署 Visual Studio 的管理员可以使用 `--in` 参数来指定响应文件，如下例所示：

```shell
vs_enterprise.exe --in customInstall.json
```
## <a name="response-file-contents"></a>响应文件内容
响应文件封装了命令行参数，并遵循以下一般规则：
 - 如果命令行参数未使用任何自变量（例如 `--quiet`、`--passive` 等），响应文件中的值应为 true/false。 
 - 如果形式参数使用实际参数（例如 `--installPath <dir>`），响应文件中的值应为字符串。 
 - 如果形式参数使用实际参数并能在命令行中多次出现（例如 `--add <id>`），响应文件中的值应为一组字符串。

命令行中指定的参数将替代响应文件中所包含的设置，但参数采用多个输入时除外（例如 `--add`）。 具有多个输入时，命令行中提供的输入将与响应文件中的设置合并。

## <a name="configure-the-response-file-used-with-network-layouts"></a>配置用于网络布局的响应文件
如果使用 `--layout` 命令创建了网络布局，则会在布局文件夹的根目录中创建初始默认 vanilla `response.json` 文件。 然后，管理员可以在布局中修改这一 `response.json` 文件，以便控制客户端在调用该布局的引导程序来在客户端上安装或更新 Visual Studio 时应使用的设置。

`response.json` 文件中的配置设置仅在客户端使用布局中的引导程序时才会得到引用和使用。 当客户端在客户端本地调用更新时，则不会使用布局中的 `response.json`。  

如果管理员创建了部分布局，则默认 `response.json` 文件将仅指定部分布局中包含的工作负载和语言。 

假设客户端执行初始安装时不使用 `--quiet` 模式，那么运行初始安装的用户可以替代 `response.json` 中指定的默认值，并可在安装实际发生前进一步选择或取消选择设置 UI 中的任何工作负载。 如果用户选择了布局中不可用的组件或工作负载，并且 `response.json` 中的 channelURI 指向 Microsoft 托管服务器，那么 Visual Studio 安装程序将尝试从 Internet 获取包。

如果 Visual Studio 安装程序从布局文件夹运行，则安装程序会自动使用相应布局文件夹中的 `response.json` 文件。 不必局限于使用 `--in` 选项。

> [!WARNING]
> 不得删除创建布局时定义的 `response.json` 中的任何属性，这一点至关重要。 可以更改这些值，但不能删除任何项。

布局中的基 `response.json` 文件应与以下示例类似，除非它具有用户想安装的产品和通道的值：

::: moniker range="vs-2017"

```Default response.json
{
  "installChannelUri": ".\\ChannelManifest.json",
  "channelUri": "https://aka.ms/vs/15/release/channel",
  "installCatalogUri": ".\\Catalog.json",
  "channelId": "VisualStudio.15.Release",
  "productId": "Microsoft.VisualStudio.Product.Enterprise"
}
```

::: moniker-end

::: moniker range="=vs-2019"

```Default response.json
{
  "installChannelUri": ".\\ChannelManifest.json",
  "channelUri": "https://aka.ms/vs/16/release/channel",
  "installCatalogUri": ".\\Catalog.json",
  "channelId": "VisualStudio.16.Release",
  "productId": "Microsoft.VisualStudio.Product.Enterprise"
}
```

::: moniker-end

::: moniker range="=vs-2022"

```Default response.json for Current channel layout
{
  "installChannelUri": ".\\ChannelManifest.json",
  "channelUri": "https://aka.ms/vs/17/release/channel",
  "installCatalogUri": ".\\Catalog.json",
  "channelId": "VisualStudio.17.Release",
  "productId": "Microsoft.VisualStudio.Product.Enterprise"
}
```

```Default response.json for LTSC 17.0 channel layout
{
  "installChannelUri": ".\\ChannelManifest.json",
  "channelUri": "https://aka.ms/vs/17/release.ltsc.17.0/channel",
  "installCatalogUri": ".\\Catalog.json",
  "channelId": "VisualStudio.17.Release.LTSC.17.0",
  "productId": "Microsoft.VisualStudio.Product.Enterprise"
}
```

::: moniker-end

创建或更新布局时，会同时创建一个 response.template.json 文件。  此文件包含所有可用的工作负载、组件和语言 ID。  此文件以模板形式提供，可包含自定义安装中的所有内容。 管理员可使用此文件作为自定义响应文件的起点。 仅需删除不需要安装的内容的 ID，并将其保存在 `response.json` 文件或自己的响应文件中。 请勿自定义 response.template.json 文件，否则一旦布局更新，所做更改就会丢失。

## <a name="example-customized-layout-response-file-content"></a>自定义布局响应文件内容示例

::: moniker range="vs-2017"

以下 `response.json` 文件示例将初始化 Visual Studio Enterprise 的客户端安装，以便包含多个常见工作负载和组件，同时包含英语和法语 UI 语言，并将更新位置配置为指向布局。 请注意，对于 Visual Studio 2017，客户端上设置更新位置 (channelURI) 后就不能再进行更改。

```Example response.json
{
  "installChannelUri": ".\\ChannelManifest.json",
  "channelUri": "\\\\server\\share\\layoutdirectory\\ChannelManifest.json",
  "installCatalogUri": ".\\Catalog.json",
  "channelId": "VisualStudio.15.Release",
  "productId": "Microsoft.VisualStudio.Product.Enterprise",

  "installPath": "C:\\VS2017",
  "quiet": false,
  "passive": false,
  "includeRecommended": true,
  "norestart": false,

  "addProductLang": [
    "en-US",
    "fr-FR"
    ],

    "add": [
        "Microsoft.VisualStudio.Workload.ManagedDesktop",
        "Microsoft.VisualStudio.Workload.Data",
        "Microsoft.VisualStudio.Workload.NativeDesktop",
        "Microsoft.VisualStudio.Workload.NetWeb",
        "Microsoft.VisualStudio.Workload.Office",
        "Microsoft.VisualStudio.Workload.Universal",
        "Component.GitHub.VisualStudio"
    ]
}
```

::: moniker-end

::: moniker range="=vs-2019"

以下 `response.json` 文件示例将初始化 Visual Studio Enterprise 的客户端安装，以便选择多个常见的工作负载和组件，同时选择英语和法语 UI 语言，并将更新位置配置为指向布局。 请注意，对于 Visual Studio 2019，更新位置 (channelURI) 只能在初始安装期间配置，并且在此之后无法更改，除非你使用最新安装程序中的功能。 有关如何对此进行配置的信息，请参阅[为 Visual Studio 企业部署设置默认值](/visualstudio/install/set-defaults-for-enterprise-deployments.md#configuring-source-location-for-updates)。

```Example response.json
{
  "installChannelUri": ".\\ChannelManifest.json",
  "channelUri": "\\\\server\\share\\layoutdirectory\\ChannelManifest.json",
  "installCatalogUri": ".\\Catalog.json",
  "channelId": "VisualStudio.16.Release",
  "productId": "Microsoft.VisualStudio.Product.Enterprise",

  "installPath": "C:\\VS2019",
  "quiet": false,
  "passive": false,
  "includeRecommended": true,
  "norestart": false,

  "addProductLang": [
    "en-US",
    "fr-FR"
    ],

    "add": [
        "Microsoft.VisualStudio.Workload.ManagedDesktop",
        "Microsoft.VisualStudio.Workload.Data",
        "Microsoft.VisualStudio.Workload.NativeDesktop",
        "Microsoft.VisualStudio.Workload.NetWeb",
        "Microsoft.VisualStudio.Workload.Office",
        "Microsoft.VisualStudio.Workload.Universal",
        "Component.GitHub.VisualStudio"
    ]
}
```

::: moniker-end

::: moniker range="=vs-2022"

以下 `response.json` 文件示例将初始化 Visual Studio Enterprise 的客户端安装，以便选择多个常见的工作负载和组件，同时选择英语和法语 UI 语言，并将更新位置配置为指向布局。 

```Example response.json
{
  "installChannelUri": ".\\ChannelManifest.json",
  "channelUri": "\\\\server\\share\\layoutdirectory\\ChannelManifest.json",
  "installCatalogUri": ".\\Catalog.json",
  "channelId": "VisualStudio.17.Release",
  "productId": "Microsoft.VisualStudio.Product.Enterprise",

  "installPath": "C:\\VS2022",
  "quiet": false,
  "passive": false,
  "includeRecommended": true,
  "norestart": false,

  "addProductLang": [
    "en-US",
    "fr-FR"
    ],

    "add": [
        "Microsoft.VisualStudio.Workload.ManagedDesktop",
        "Microsoft.VisualStudio.Workload.Data",
        "Microsoft.VisualStudio.Workload.NativeDesktop",
        "Microsoft.VisualStudio.Workload.NetWeb",
        "Microsoft.VisualStudio.Workload.Office",
        "Microsoft.VisualStudio.Workload.Universal"
    ]
}
```

::: moniker-end

## <a name="troubleshooting"></a>疑难解答
如果在将引发错误的 Visual Studio 引导程序与 `response.json` 文件配对时发生错误，请参阅[安装或使用 Visual Studio 时与网络相关错误的疑难解答](../install/troubleshooting-network-related-errors-in-visual-studio.md#error-failed-to-parse-id-from-parent-process)页，以获取详细信息。

[!INCLUDE[install_get_support_md](includes/install_get_support_md.md)]

## <a name="see-also"></a>另请参阅
* [Visual Studio 管理员指南](https://aka.ms/vs/admin/guide)
* [Visual Studio 工作负荷和组件 ID](workload-and-component-ids.md)
* [安装或使用 Visual Studio 时与网络相关错误的疑难解答](troubleshooting-network-related-errors-in-visual-studio.md)
