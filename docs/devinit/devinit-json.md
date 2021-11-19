---
title: devinit 配置文件
description: 用于 devinit 的 .devinit.json 清单文件的文档。
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
> 从 2021 年 4 月 12 日开始，将不再支持从 Visual Studio 2019 连接到 GitHub Codespaces，此个人预览版已结束。 我们专注于为云支持的内部循环和 VDI 解决方案提供不断发展的体验，这些解决方案针对一组广泛的Visual Studio工作负载进行优化。 建议参与 Visual Studio 的开发人员社区论坛，了解未来要推出的预览版和路线图信息。

`.devinit.json`文件定义应用程序运行和生成所需的系统范围的依赖项。 系统范围的依赖项包括 Node.js、SQL Server、IIS、RabbitMQ、Docker 等。这些是通常在开发框上安装的、未由特定存储库安装的信息。 不能像在包管理器（如应用程序管理器或 NPM）中一样定义特定于NuGet依赖项。 但是，这是一个定义需要这些包管理器的位置。

## <a name="file-location"></a>文件位置

`devinit init`该命令通过 文件 `.devinit.json` 驱动。 默认情况下，`devinit` 在以下位置查找该文件：

* {current-directory}\\.devinit.json
* {current-directory} \\devinit.json
* {current-directory} \\ 。devinit \\ .devinit.json
* {current-directory} \\ 。devinit \\ devinit.json
* {current-directory} \\devinit \\ .devinit.json
* {current-directory} \\devinit \\ devinit.json
* {current-directory} \\ 。devcontainer \\ .devinit.json
* {current-directory} \\ 。devcontainer \\ devinit.json

> [!NOTE]
> 如果找到多个默认文件，则 devinit 将使用上面列表中首先显示的文件。

`.devinit.json`也可通过 选项显式指定 `--file` / `-f` 文件。

### <a name="directories-and-relative-paths"></a>目录和相对路径

路径相对于 devinit 运行的位置。 这通常是从中执行的当前 `devinit` 工作目录。

## <a name="file-format"></a>文件格式
在 `.devinit.json` 中，可以指定多个要运行的工具。 在 `run` 部分中，可以放入任意数目的对象。 使用所有工具的示例 [.devinit.json](sample-all-tool.md) 中提供了一个示例。

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
| **运行**      | array  | 是      | [RunTool 对象](#run-tool-object) |

#### <a name="run-tool-object"></a>运行工具对象

| 名称                  | 类型   | 必须 | 值                                                                                                      |
|-----------------------|--------|----------|------------------------------------------------------------------------------------------------------------|
| **注释**          | 字符串型 | 否       | 工具条目的注释。                                                                               |
| **工具**              | 字符串 | 是      | 工具名称。 有关 `devinit list` 可用工具列表，请参阅 命令。                            |
| **input**             | 字符串型 | 否       | 工具输入。 因工具而异。 例如，所需的版本、包 ID、文件名或文件夹。|
| **additionalOptions** | 字符串型 | 否       | 要传递给工具的其他命令行参数。                                                |

## <a name="examples"></a>示例

有关使用 devinit 的更多示例，请参阅 [示例部分](sample-readme.md)。
