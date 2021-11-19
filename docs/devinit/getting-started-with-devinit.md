---
title: devinit 入门指南
description: devinit 的入门指南。
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
ms.openlocfilehash: 660bb5a2c3d235a347e478d55ae8176e87c5d626
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "127833048"
---
# <a name="getting-started-with-devinit"></a>devinit 入门指南

> [!IMPORTANT]
> 从 2021 年 4 月 12 日开始，将不再支持从 Visual Studio 2019 连接到 GitHub Codespaces，此个人预览版已结束。 我们的工作重点是改进云支持型内部循环和针对多种 Visual Studio 工作负载优化的 VDI 解决方案的体验。 在此期间，`devinit` 和关联工具将不再可用。 建议参与 Visual Studio 的开发人员社区论坛，了解未来要推出的预览版和路线图信息。

devinit 是一个工具，你可以用它来使任何人在你的存储库中通过运行简单的命令来访问代码并提高效率。 你可以使用 devinit 来定义存储库所需的所有系统范围的依赖项，例如 SQL Server、Node.js、Docker 或 IIS。 Devinit 可以调用其他工具和包管理器来安装存储库所需的内容。 你需要在名为 [.devinit.json](devinit-json.md) 的 JSON 文件中定义这些依赖项，然后使用存储库的下一个用户只需运行 [`devinit init`](devinit-commands.md#init) 即可安装所有这些依赖项。 因此，可以在几分钟内完成，而不用为加入一个新的存储库花费半天时间。

devinit 本身不是一个包管理器或一个虚拟机 (VM) 配置工具。 它是一个名为 [.devinit.json](devinit-json.md) 的清单文件的任务运行程序，用于定义应用程序所需的系统范围的依赖项。 为了安装这些依赖项，devinit 利用了你可能已在使用的工具，如 [Chocolatey](https://chocolatey.org)。 你可以在[完整列表](devinit-tool-list.md)中查看可用的工具。 通过使用这些工具而不是直接分发软件，devinit 使你可以方便地使用所选的工具，并使你能够使用现有配置，例如，用于 Chocolatey 的 [packages.config](https://chocolatey.org/docs/commands-install#packagesconfig) 文件。  

## <a name="step-1-get-devinit"></a>步骤 1：获取 devinit

devinit 目前仅在使用 Visual Studio 时作为 GitHub Codespaces 的一部分提供，并且可从 Visual Studio 中的集成终端进行访问。 将来，devinit 将作为 Visual Studio 的一部分提供。

## <a name="step-2-define-your-environment"></a>步骤 2：定义环境

最重要的步骤是在 [.devinit.json 文件](devinit-json.md)中定义“开发”环境。 当你运行 `devinit init` 时，devinit 将使用此文件来创建环境。

对于这一步，请考虑你要让某人启动并运行项目存储库的说明。 例如，是否需要安装 SQL？ .NET Core 的特定版本？ 依此类推。 然后，对于每个依赖项，在[工具列表](devinit-tool-list.md)中查找相应的 devinit 工具，并将其添加到存储库的 `.devinit.json` 文件中。

你还可以在[示例文档](sample-readme.md)中查看选择的示例，或者查看[教程](tutorial.md)。

## <a name="step-3-enjoy"></a>步骤 3：请尽情体验吧！

现在有人在克隆你的存储库后所要做的就是运行 `devinit init`。

```console
devinit init
```

如果你使用的是 [GitHub Codespaces](https://github.com/features/codespaces)，可以将 `devinit init` 配置为在 codespace 预配完成时自动运行。 若要了解详细信息，请参阅 [devinit 和 GitHub Codespaces 文档](devinit-and-codespaces.md)。
