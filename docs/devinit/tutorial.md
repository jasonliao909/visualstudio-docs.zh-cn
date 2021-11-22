---
title: 教程
description: devinit 教程。
ms.date: 11/18/2020
ms.topic: reference
author: andysterland
ms.author: andster
manager: jmartens
ms.workload:
- multiple
monikerRange: '>= vs-2019'
ms.prod: visual-studio-windows
ms.technology: devinit
ms.openlocfilehash: 5fc53a534b592b4f6a4799100ce16b1d45049457
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "127833097"
---
# <a name="tutorial"></a>教程

> [!IMPORTANT]
> 从 2021 年 4 月 12 日开始，将不再支持从 Visual Studio 2019 连接到 GitHub Codespaces，此个人预览版已结束。 我们的工作重点是改进云支持型内部循环和针对多种 Visual Studio 工作负载优化的 VDI 解决方案的体验。 建议参与 Visual Studio 的开发人员社区论坛，了解未来要推出的预览版和路线图信息。

在本教程中，我们将探讨使用 devinit 和 Codespaces 设置 [eShopOnWeb 存储库](https://github.com/andysterland/eShopOnWeb)。 本教程假设 devinit 已可用，如[入门页面](getting-started-with-devinit.md)所述。

## <a name="step-1-determining-setup-steps"></a>步骤 1：确定安装步骤

如[入门页面](getting-started-with-devinit.md)中所述，第一步始终是确定项目具有的依赖项和安装步骤。 这因特定项目而异，但需要考虑一些问题：

- 项目依赖于哪些运行时或 SDK？
- 项目是否需要任何包（例如 Chocolatey）？
- 安装过程是否需要执行任何操作（例如，运行脚本）？
- 项目是否针对随 Visual Studio 安装的任何内容具有隐式依赖关系？
  - 如果是，最好也将这些内容包含在 devinit 安装中。 这样，可以避免对 Visual Studio 安装的耦合。

确定此信息的最佳方法之一是浏览当前为存储库保留的手动设置步骤。 对于 eShopOnWeb，需要处理一些操作：

- 安装最新版本的 .NET Core SDK
- 安装最新版本的 .NET Entity Framework Core Tools CLI
- 安装 SQL Server 2019 Express
- 使用 .NET Entity Framework CLI 将本地数据库更新为最新迁移

接下来，我们将探讨如何在 devinit 的上下文中完成所有这些内容。

## <a name="step-2-the-devinitjson"></a>步骤 2：.devinit.json

首先，将要构造 [.devinit.json 文件](devinit-json.md)，并将其放在存储库的根中。 该文件将包含稍后将作为 `devinit init` 命令的一部分执行的一系列步骤。 若要确定应包含在 `.devinit.json` 文件中的内容，可以执行安装步骤列表，并与 [devinit tools](devinit-tool-list.md) 列表进行对比。 现在，让我们使用上述安装步骤来进行操作。

| 步骤                                                              | devinit 能否为我们处理此问题？                                                                        |
| :---------------------------------------------------------------- | :----------------------------------------------------------------------------------------------------  |
| 安装最新的 .NET Core SDK                                      | 是！ 我们可以使用 [`require-dotnetcoresdk` 工具](tool-require-dotnetcoresdk.md)                  |
| 安装 .NET Entity Framework Core Tools CLI                      | 是！ 我们可以使用 [`dotnet-toolinstall` 工具](tool-dotnet-toolinstall.md)                        |
| 安装 SQL Server 2019 Express                                   | 是！ 我们可以使用 [`choco-install` 工具](tool-choco-install.md)                                  |
| 使用 .NET Entity Framework 更新本地数据库                 | 否，但仍通过将 devinit 与脚本相结合来实现此操作！                               |

至此，我们已经了解清楚，让我们从基本的 `.devinit.json` 开始。 将包含对 [`.devinit.json` 架构](https://json.schemastore.org/devinit.schema-2.0)的引用以及空的 `run` 部分：

```json
{
  "$schema": "https://json.schemastore.org/devinit.schema-2.0",
  "run": []
}
```

现在，让我们添加一些工具！

首先，我们将添加 [`require-dotnetcoresdk`](tool-require-dotnetcoresdk.md)。 从该工具的文档中，可以看出默认行为是安装最新的 SDK 版本。 这正是我们想要的，因此让我们将其添加到 `.devinit.json` 中：

```json
{
  "$schema": "https://json.schemastore.org/devinit.schema-2.0",
  "run": [
    {
      "comments": "Install the latest version of the .NET Core SDK.",
      "tool": "require-dotnetcoresdk"
    }
  ]
}
```

其次，将添加 [`dotnet-toolinstall`](tool-dotnet-toolinstall.md) 以全局安装 `dotnet-ef` 工具。 从文档可以看出，我们可以使用 `input` 字段指定工具名称，使用 `additionalOptions` 字段指定全局范围：

```json
{
  "run": [
    {
      "comments": "Install the latest version of the .NET Core SDK.",
      "tool": "require-dotnetcoresdk"
    },
    {
      "comments": "Install latest version of the .NET Entity Framework Core Tools CLI.",
      "tool": "dotnet-toolinstall",
      "input": "dotnet-ef",
      "additionalOptions": "--global"
    }
  ]
}
```

最后，将添加 [`choco-install`](tool-choco-install.md) 以安装 `sql-server-express` 包。

```json
{
  "run": [
    {
      "comments": "Install the latest version of the .NET Core SDK.",
      "tool": "require-dotnetcoresdk"
    },
    {
      "comments": "Install latest version of the .NET Entity Framework Core Tools CLI.",
      "tool": "dotnet-toolinstall",
      "input": "dotnet-ef",
      "additionalOptions": "--global"
    },
    {
      "comments": "Install SQL Server 2019 Express",
      "tool": "choco-install",
      "input": "sql-server-express"
    }
  ]
}
```

现在 `.devinit.json` 已完成，我们可以处理将负责运行 devinit 和更新本地数据库的安装脚本。

## <a name="step-3-the-setup-script"></a>步骤 3：安装脚本

若要同时运行 devinit 和更新本地数据库，将创建执行所需命令的脚本。 在纯出口根路径中创建空的 PowerShell 脚本，名为 `PostCloneSetup.ps1`。 首先，将添加对 `devinit init` 的调用：

```powershell
devinit init
```

执行时，`devinit init` 将运行在 `.devinit.json` 的 `run` 部分中定义的所有工具。

最后，我们想要调用 `dotnet ef database update` 来更新本地数据库：

```powershell
devinit init
dotnet ef database update -c catalogcontext -p src\Infrastructure\Infrastructure.csproj -s src\Web\Web.csproj
dotnet ef database update -c appidentitydbcontext -p src\Infrastructure\Infrastructure.csproj -s src\Web\Web.csproj
```

现在，安装脚本已完成，我们需要添加将在 codespace 安装中执行的 `.devcontainer.json` 文件。

## <a name="step-4-the-devcontainerjson"></a>步骤 4：.devcontainer.json

为了确保安装脚本在 codespace 创建期间运行，我们将使用 `.devcontainer.json` 文件。 与其他文件类似，应将其放在存储库根路径中。

在 `.devcontainer.json` 文件中，只需调用安装脚本作为 `postCreateCommand` 的一部分。 这将作为 codespace 创建过程的一部分执行：

```json
{
  "postCreateCommand": "Powershell.exe -ExecutionPolicy unrestricted -File .\\PostCloneSetup.ps1"
}
```

大功告成！

## <a name="step-5-trying-it-out"></a>步骤 5：测试

现在，安装步骤已就绪，让我们使用[实际存储库](https://github.com/andysterland/eShopOnWeb)在实时 codespace 中进行测试吧。

首先，将使用 Visual Studio 创建 codespace：

:::image type="content" source="media/eshoponweb-github-codespaces-prompt.png" alt-text="创建 codespace":::

开始创建 codespace 后，可以在 `C:\.vsonline\.vsoshared\vmTerminal.dat` 中观看安装进程的进度：

:::image type="content" source="media/eshoponweb-watching-progress.png" alt-text="观看安装进度":::

完成后，通过 `Web.csproj` 运行程序以确保一切正常运行：

:::image type="content" source="media/eshoponweb-csproj.png" alt-text="运行项目":::

生成并启动应用后，可以在 web 浏览器中看到商店：

:::image type="content" source="media/eshoponweb-live.png" alt-text="查看站点":::

因此，我们的安装过程正常运行，现在可以在 eShopOnWeb 项目中进行开发了！
