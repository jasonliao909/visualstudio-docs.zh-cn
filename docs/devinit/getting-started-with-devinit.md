---
title: 入门与 devinit
description: Devinit 入门指南。
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
# <a name="getting-started-with-devinit"></a>入门与 devinit

> [!IMPORTANT]
> 从 2021 年 4 月 12 日开始，将不再支持从 Visual Studio 2019 连接到 GitHub Codespaces，此个人预览版已结束。 我们将重点放在针对广泛的 Visual Studio 工作负荷进行优化的云驱动内部循环和 VDI 解决方案的不断变化方面。 作为此 `devinit` 和相关工具的一部分将不再可用。 建议参与 Visual Studio 的开发人员社区论坛，了解未来要推出的预览版和路线图信息。

devinit 是一种工具，可用于通过运行简单的命令使任何人都能够访问代码并在存储库中提高效率。 你可以使用 devinit 来定义存储库所需的所有系统范围的依赖项，例如 SQL server、Node.js、Docker 或 IIS。 Devinit 可以调用其他工具和包管理器来安装存储库所需的内容。 在名为 [devinit](devinit-json.md) 的 json 文件中定义这些依赖项，然后使用存储库的下一个用户只需运行 [`devinit init`](devinit-commands.md#init) 即可安装所有这些依赖项。 因此，可以在几分钟内完成，而不是在一天中加入到新的存储库。

devinit 不是包管理器或虚拟机 (VM) 配置工具本身。 它是一个名为 [devinit](devinit-json.md)的清单文件的任务运行程序，用于定义应用程序所需的系统范围依赖项。 若要安装这些依赖项，devinit 利用了你可能已在使用的工具，如 [Chocolatey](https://chocolatey.org)。 可以在 [完整列表](devinit-tool-list.md)中查看可用的工具。 通过使用这些工具而不是直接分发软件，devinit 使你可以方便地使用所选的工具，并使你能够使用现有配置，例如，用于 Chocolatey 的 [packages.config](https://chocolatey.org/docs/commands-install#packagesconfig) 文件。  

## <a name="step-1-get-devinit"></a>步骤1：获取 devinit

devinit 当前仅在使用 Visual Studio 时作为 GitHub Codespaces 的一部分提供，并且可从 Visual Studio 中的集成终端进行访问。 将来，devinit 将作为 Visual Studio 的一部分提供。

## <a name="step-2-define-your-environment"></a>步骤2：定义环境

最重要的步骤是在 [devinit 文件](devinit-json.md)中定义 "开发" 环境。 当你运行时，devinit 将使用此文件来创建环境 `devinit init` 。

对于此步骤，请考虑你要让某人获取并运行项目存储库的说明。 例如，是否需要安装 SQL？ .NET Core 的特定版本？ 依此类推。 然后，对于每个依赖项，请在 [工具列表](devinit-tool-list.md) 中查找相应的 devinit 工具，并将其添加到存储库的 `.devinit.json` 文件中。

你还可以在 [示例文档](sample-readme.md)中查看选择的示例，或者查看 [教程](tutorial.md)。

## <a name="step-3-enjoy"></a>步骤3：欣赏！

现在，所有人都必须在克隆存储库后执行操作 `devinit init` 。

```console
devinit init
```

如果使用[GitHub Codespaces](https://github.com/features/codespaces)，则可以将配置 `devinit init` 为在预配 codespace 时自动运行。 若要了解详细信息，请参阅[devinit 和 GitHub Codespaces 文档](devinit-and-codespaces.md)。
