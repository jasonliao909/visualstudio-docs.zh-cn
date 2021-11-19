---
title: devinit 和 GitHub Codespaces
description: 了解如何使用 devinit 为 Visual Studio 自定义 codespace。
ms.date: 08/28/2020
ms.topic: reference
author: andysterland
ms.author: andster
manager: jmartens
ms.workload:
- multiple
monikerRange: '>= vs-2019'
ms.prod: visual-studio-windows
ms.technology: devinit
ms.openlocfilehash: c98c00e0b62d3a2a755790b07621d717abcb41c1
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "127833070"
---
# <a name="devinit-and-github-codespaces"></a>devinit 和 GitHub Codespaces

> [!IMPORTANT]
> 从 2021 年 4 月 12 日开始，将不再支持从 Visual Studio 2019 连接到 GitHub Codespaces，此个人预览版已结束。 我们的工作重点是改进云支持型内部循环和针对多种 Visual Studio 工作负载优化的 VDI 解决方案的体验。 在此期间，`devinit` 和关联工具将不再可用。 建议参与 Visual Studio 的开发人员社区论坛，了解未来要推出的预览版和路线图信息。

devinit 是 [GitHub Codespaces](https://github.com/features/codespaces) 和 devinit 的有效补充，可用于获取 codespace 设置，以便参与者可以立即生成、运行和调试。

> [!IMPORTANT]
> 将 devinit 与 codespace 集成之前，首先需要确保具有定义依赖项的 `.devinit.json` 文件。 有关如何创建 `.devinit.json` 的详细信息，请阅读[入门文档](getting-started-with-devinit.md)。

在 GitHub Codespace 内部，应用程序在云中生成并运行。 在云中，这意味着你的应用程序无权访问计算机上的本地资源。 其中包括本地安装的工具或程序。 如果你的应用程序需要安装或配置任何系统范围的依赖项，则需要在每个 codespace 上完成此操作。 实现此目的的最简单方法是使用 `.devinit.json` 文件。

若要确保使用应用程序所需的依赖项创建 codespace，`devinit` 需要在创建 codespace 时运行。 为此，可以从放置在存储库根路径中的 `.devcontainer.json` 文件中定义的 `postCreateCommand` 调用 `devinit init`。 在 codespace 中克隆存储库后，`postCreateCommand` 中的字符串在默认 shell 中执行。 有关 `postCreateCommand` 的详细信息，请参阅 GitHub Codespaces [自定义文档](https://docs.github.com/github/developing-online-with-codespaces/configuring-codespaces-for-your-project)。 若要添加 `devinit` 命令，你可以将 `devinit init` 添加到 `postCreateCommand` 中，如以下示例所示。

连接到 codespace 后，也可以从 Visual Studio 集成终端执行 `devinit init -f <path to .devinit.json>`。

## <a name="examples"></a>示例

在以下两个示例中，`.devinit.json` 与 `.devcontainer.json` 一起位于存储库根路径中。

### <a name="with-a-devcontainerjson-file"></a>使用 .devcontainer.json 文件

在此示例中，下面的 `.devcontainer.json` 文件与 `.devinit.json` 文件一起放置在存储库根路径中。 文件也可以放在 `.devcontainer` 目录中。

```json
{
  "postCreateCommand": "devinit init"
}
```

如果 `.devinit.json` 在另一个目录中，则可以使用 -f 标记。

```json
{
  "postCreateCommand": "devinit init -f path\\to\\.devinit.json"
}

```

```json
{
  "postCreateCommand": ["<some other command>", "devinit init"]
}
```

你可以在我们的[文档](sample-all-tool.md)和 GitHub 的 [.NET Core 示例](https://github.com/microsoft/devinit-example-dotnet-core)以及 [Node.js 示例](https://github.com/microsoft/devinit-example-nodejs)存储库中找到更多有关使用 devinit 的示例。

### <a name="as-commands"></a>As 命令

在此示例中，下面的 `.devcontainer.json` 文件位于存储库根路径中，并从命令行直接调用 `devinit run` 以运行单个工具。  

```json
{
  "postCreateCommand": ["devinit run –t require-dotnetcoresdk"]
}
```

### <a name="from-a-terminal-prompt"></a>终端提示

当前工作目录包含 `.devinit.json` 文件时。

```console
devinit init
```

当 `.devinit.json` 位于另一个目录中。

```console
devinit init -f path/to/.devinit.json
```
