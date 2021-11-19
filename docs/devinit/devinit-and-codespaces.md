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
> 从 2021 年 4 月 12 日开始，将不再支持从 Visual Studio 2019 连接到 GitHub Codespaces，此个人预览版已结束。 我们将重点放在针对广泛的 Visual Studio 工作负荷进行优化的云驱动内部循环和 VDI 解决方案的不断变化方面。 作为此 `devinit` 和相关工具的一部分将不再可用。 建议参与 Visual Studio 的开发人员社区论坛，了解未来要推出的预览版和路线图信息。

devinit 是[GitHub Codespaces](https://github.com/features/codespaces)和 devinit 的出色补充，可用于获取 codespace 的设置，以便参与者可以立即生成、运行和调试。

> [!IMPORTANT]
> 将 devinit 与 codespace 集成之前，首先需要确保具有 `.devinit.json` 定义依赖项的文件。 有关如何创建的详细信息 `.devinit.json` ，请阅读 [入门文档](getting-started-with-devinit.md)。

在 GitHub Codespace 内部，你的应用程序在云中生成并运行。 在云中，这意味着你的应用程序无权访问计算机上的本地资源。 其中包括本地安装的工具或程序。 如果你的应用程序需要安装或配置任何系统范围的依赖项，则需要在每个 codespace 上完成此操作。 实现此目的的最简单方法是使用 `.devinit.json` 文件。

若要确保使用应用程序所需的依赖项创建 codespace， `devinit` 需要在创建 codespace 时运行。 为此，可以 `devinit init` 从 `postCreateCommand` 存储在存储库根中的文件中的定义 `.devcontainer.json` 。  (中) 的字符串在 `postCreateCommand` codespace 中克隆存储库后，在默认 shell 中执行。 有关详细信息，请参阅 `postCreateCommand` GitHub Codespaces[自定义文档](https://docs.github.com/github/developing-online-with-codespaces/configuring-codespaces-for-your-project)。 若要添加 `devinit` 命令，你可以将添加 `devinit init` 到 `postCreateCommand` 中，如下面的示例中所示。

`devinit init -f <path to .devinit.json>`连接到 codespace 后，也可以从 Visual Studio 集成终端执行。

## <a name="examples"></a>示例

在以下两个示例中， `.devinit.json` 都位于存储库根路径中 `.devcontainer.json` 。

### <a name="with-a-devcontainerjson-file"></a>使用 devcontainer 文件

在此示例中， `.devcontainer.json` 下面的文件与文件一起放置在存储库根路径中 `.devinit.json` 。 文件也可以放在 `.devcontainer` 目录中。

```json
{
  "postCreateCommand": "devinit init"
}
```

如果 `.devinit.json` 在另一个目录中，则可以使用-f 标志。

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

你可以在我们的[文档](sample-all-tool.md)和 GitHub 的[.net Core 示例](https://github.com/microsoft/devinit-example-dotnet-core)和[Node.js 示例](https://github.com/microsoft/devinit-example-nodejs)存储库中找到更多有关使用 devinit 的示例。

### <a name="as-commands"></a>As 命令

在此示例中，下面的文件位于存储库 `.devcontainer.json` 根中，并 `devinit run` 从命令行直接调用以运行单个工具。  

```json
{
  "postCreateCommand": ["devinit run –t require-dotnetcoresdk"]
}
```

### <a name="from-a-terminal-prompt"></a>从终端提示符

当前工作目录包含 `.devinit.json` 文件时。

```console
devinit init
```

如果位于 `.devinit.json` 另一个目录中。

```console
devinit init -f path/to/.devinit.json
```
