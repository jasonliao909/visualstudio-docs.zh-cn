---
title: devinit 配置文件
description: devinit 的 .devinit.json 清单文件的文档。
ms.date: 11/02/2020
ms.topic: reference
author: andysterland
ms.author: andster
manager: jmartens
ms.workload:
- multiple
monikerRange: '>= vs-2019'
ms.prod: visual-studio-windows
ms.technology: devinit
ms.openlocfilehash: 4f94ee609ba4c0783a06648ed037e58d864aa2a9
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "127833051"
---
# <a name="devinit-configuration-file"></a>devinit 配置文件

> [!IMPORTANT]
> 从 2021 年 4 月 12 日开始，将不再支持从 Visual Studio 2019 连接到 GitHub Codespaces，此个人预览版已结束。 我们的工作重点是改进云支持型内部循环和针对多种 Visual Studio 工作负载优化的 VDI 解决方案的体验。 建议参与 Visual Studio 的开发人员社区论坛，了解未来要推出的预览版和路线图信息。

`.devinit.json` 文件定义应用程序运行和生成所需的系统范围的依赖项。 系统范围的依赖项包括 Node.js、SQL Server、IIS、RabbitMQ、Docker 等。这些是你通常会在开发工具包上安装但不是由特定存储库安装的内容。 它不是像在 NuGet 或 NPM 等包管理器中那样定义应用程序特定的依赖项的地方。 然而，它是定义你需要那些包管理器的地方。

## <a name="file-location"></a>文件位置

`devinit init` 命令通过 `.devinit.json` 文件驱动。 默认情况下，`devinit` 在以下位置查找该文件：

* {current-directory}\\.devinit.json
* {current-directory}\\devinit.json
* {current-directory}\\.devinit\\.devinit.json
* {current-directory}\\.devinit\\devinit.json
* {current-directory}\\devinit\\.devinit.json
* {current-directory}\\devinit\\devinit.json
* {current-directory}\\.devcontainer\\.devinit.json
* {current-directory}\\.devcontainer\\devinit.json

> [!NOTE]
> 如果找到多个默认文件，则 devinit 将使用上面列表中第一个出现的文件。

也可通过 `--file`/`-f` 选项显式指定 `.devinit.json` 文件。

### <a name="directories-and-relative-paths"></a>目录和相对路径

路径相对于 devinit 运行的位置。 这通常是从中执行 `devinit` 的当前工作目录。

## <a name="file-format"></a>文件格式
在 `.devinit.json` 中，可以指定多个要运行的工具。 在 `run` 部分中，可以放入任意数目的对象。 在我们的示例 [.devinit.json](sample-all-tool.md) 中可以看到这方面的一个示例，其中包含我们的所有工具。

```json
{
    "$schema": "https://json.schemastore.org/devinit.schema-3.0",
    "comments": "string",
    "run": [
        {
            "comments": "string",
            "tool": "string",
            "input": "string|null|undefined",
            "additionalOptions": "string|null|undefined"
        }
    ]
}
```

### <a name="property-values"></a>属性值

| 名称         | 类型   | 必须 | 值                              |
|--------------|--------|----------|------------------------------------|
| **注释** | 字符串型 | 否       | 文件的注释。             |
| **run**      | array  | 是      | [RunTool 对象](#run-tool-object) |

#### <a name="run-tool-object"></a>运行工具对象

| 名称                  | 类型   | 必须 | 值                                                                                                      |
|-----------------------|--------|----------|------------------------------------------------------------------------------------------------------------|
| **注释**          | 字符串型 | 否       | 工具条目的注释。                                                                               |
| **tool**              | 字符串 | 是      | 工具名称。 有关可用工具的列表，请参阅 `devinit list` 命令。                            |
| **input**             | 字符串型 | 否       | 工具输入。 因工具而异。 例如，所需的版本、包 ID、文件名或文件夹。|
| **additionalOptions** | 字符串型 | 否       | 要传递给工具的其他命令行参数。                                                |

## <a name="examples"></a>示例

有关使用 devinit 的更多示例，请参阅[示例部分](sample-readme.md)。
