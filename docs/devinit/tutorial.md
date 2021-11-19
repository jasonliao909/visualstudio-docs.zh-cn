---
title: 教程
description: Devinit 教程。
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
> 从 2021 年 4 月 12 日开始，将不再支持从 Visual Studio 2019 连接到 GitHub Codespaces，此个人预览版已结束。 我们专注于为云支持的内部循环和 VDI 解决方案提供不断发展的体验，这些解决方案针对一组广泛的Visual Studio工作负载进行优化。 建议参与 Visual Studio 的开发人员社区论坛，了解未来要推出的预览版和路线图信息。

在本教程中，我们将探讨使用 devinit 和 Codespaces 设置 [eShopOnWeb](https://github.com/andysterland/eShopOnWeb) 存储库。 本教程假定 devinit 已可用，如入门 [页 中所述](getting-started-with-devinit.md)。

## <a name="step-1-determining-setup-steps"></a>步骤 1：确定安装步骤

如入门 [页所述](getting-started-with-devinit.md)，第一步是始终确定项目具有的依赖项和设置步骤。 这因特定项目而异，但需要考虑一些问题：

- 项目依赖于哪些运行时或 SDK？
- 项目是否需要任何包 (，例如 Chocolatey) ？
- 安装过程是否需要执行任何 (例如，运行脚本) ？
- 项目是否对随项目一起安装Visual Studio？
  - 如果是，建议同时在 devinit 设置中包括它们。 这样，可以避免与安装Visual Studio耦合。

确定此信息的最佳方法之一是浏览当前为存储库设置的手动设置步骤。 对于 eShopOnWeb，需要处理一些操作：

- 安装最新版本的 .NET Core SDK
- 安装最新版本的 .NET Entity Framework Core 工具 CLI
- 安装 SQL Server 2019 Express
- 使用 .NET 实体框架 CLI 将本地数据库更新为最新迁移

接下来，我们将探讨如何在 devinit 上下文中完成所有这些任务。

## <a name="step-2-the-devinitjson"></a>步骤 2：.devinit.json

首先，我们需要构造 [.devinit.json](devinit-json.md) 文件，并放在存储库的根目录下。 此文件将包含一系列步骤，稍后将作为命令的一部分 `devinit init` 执行。 若要确定文件中包含的内容，可以执行设置步骤列表，并将其与 `.devinit.json` [devinit 工具 的列表进行比较](devinit-tool-list.md)。 现在，让我们使用上述设置步骤来这样做。

| 步骤                                                              | 能否为我们解决此问题？                                                                        |
| :---------------------------------------------------------------- | :----------------------------------------------------------------------------------------------------  |
| 安装最新.NET Core SDK                                      | **是**！ 我们可以使用[ `require-dotnetcoresdk` 该工具](tool-require-dotnetcoresdk.md)                  |
| 安装 .NET Entity Framework Core 工具 CLI                      | **是**！ 我们可以使用[ `dotnet-toolinstall` 该工具](tool-dotnet-toolinstall.md)                        |
| 安装 SQL Server 2019 Express                                   | **是**！ 我们可以使用[ `choco-install` 该工具](tool-choco-install.md)                                  |
| 使用 .NET 数据库更新本地实体框架                 | **否**，但仍通过将 devinit 与脚本相结合来实现此目的！                               |

至此，我们已了解这一点，让我们从一个基本 的 开始 `.devinit.json` 。 我们将包含对架构[ `.devinit.json` 的引用和](https://json.schemastore.org/devinit.schema-2.0)一个空 `run` 部分：

```json
{
  "$schema": "https://json.schemastore.org/devinit.schema-2.0",
  "run": []
}
```

现在，让我们添加一些工具！

首先，我们将添加 [`require-dotnetcoresdk`](tool-require-dotnetcoresdk.md) 。 从该工具的文档中，可以看到默认行为是安装最新的 SDK 版本。 这正是我们想要的，因此让我们将其添加到 中 `.devinit.json` ：

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

其次，我们将添加 [`dotnet-toolinstall`](tool-dotnet-toolinstall.md) 以全局 `dotnet-ef` 安装该工具。 从文档中可以看到，可以使用 字段指定工具名称，使用 字段 `input` `additionalOptions` 指定全局范围：

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

最后，我们将添加 [`choco-install`](tool-choco-install.md) 以安装 `sql-server-express` 包。

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

现在我们已完成，我们可以处理一个安装脚本，该脚本 `.devinit.json` 将负责运行 devinit 和更新本地数据库。

## <a name="step-3-the-setup-script"></a>步骤 3：安装脚本

为了同时处理运行 devinit 和更新本地数据库，我们将创建一个执行所需命令的脚本。 让我们在存储库根目录创建一个名为 的空 PowerShell 脚本 `PostCloneSetup.ps1` 。 首先，我们将添加对 的调用 `devinit init` ：

```powershell
devinit init
```

执行时， `devinit init` 将运行在 的 节中 `run` 定义的所有工具 `.devinit.json` 。

最后，我们想要调用 `dotnet ef database update` 来更新本地数据库：

```powershell
devinit init
dotnet ef database update -c catalogcontext -p src\Infrastructure\Infrastructure.csproj -s src\Web\Web.csproj
dotnet ef database update -c appidentitydbcontext -p src\Infrastructure\Infrastructure.csproj -s src\Web\Web.csproj
```

安装脚本完成后，我们需要添加一个文件，该文件将在 codespace 安装过程中 `.devcontainer.json` 执行。

## <a name="step-4-the-devcontainerjson"></a>步骤 4：.devcontainer.json

为了确保安装脚本在 codespace 创建期间运行，我们将使用 `.devcontainer.json` 文件。 与其他文件类似，这应该放在存储库根目录下。

在 `.devcontainer.json` 文件中，只需调用安装脚本作为 的一部分 `postCreateCommand` 。 这将在 codespace 创建过程中执行：

```json
{
  "postCreateCommand": "Powershell.exe -ExecutionPolicy unrestricted -File .\\PostCloneSetup.ps1"
}
```

大功告成！

## <a name="step-5-trying-it-out"></a>步骤 5：尝试

设置步骤完成后，让我们使用实际存储库 在实时 codespace 中 [尝试此操作](https://github.com/andysterland/eShopOnWeb)。

首先，我们将使用 Visual Studio：

:::image type="content" source="media/eshoponweb-github-codespaces-prompt.png" alt-text="创建 codespace":::

开始创建 codespace 后，我们可以在 中监视安装过程的进度 `C:\.vsonline\.vsoshared\vmTerminal.dat` ：

:::image type="content" source="media/eshoponweb-watching-progress.png" alt-text="监视安装进度":::

完成后，让我们通过 运行应用 `Web.csproj` ，确保一切正常运行：

:::image type="content" source="media/eshoponweb-csproj.png" alt-text="运行项目":::

在应用生成并启动后，我们可以在 Web 浏览器中看到商店：

:::image type="content" source="media/eshoponweb-live.png" alt-text="查看站点":::

因此，我们的安装过程正常运行，现在可以在 eShopOnWeb 项目中进行开发了！
