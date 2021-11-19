---
title: devinit 命令
description: 有关如何使用 devinit 命令安装组件的详细信息。
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
ms.openlocfilehash: d6c8f487fcb35fc210db57f0c8a49a2a86f909e9
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "127833127"
---
# <a name="devinit-commands"></a>devinit 命令

> [!IMPORTANT]
> 从 2021 年 4 月 12 日开始，将不再支持从 Visual Studio 2019 连接到 GitHub Codespaces，此个人预览版已结束。 我们的工作重点是改进云支持型内部循环和针对多种 Visual Studio 工作负载优化的 VDI 解决方案的体验。 在此期间，`devinit` 和关联工具将不再可用。 建议参与 Visual Studio 的开发人员社区论坛，了解未来要推出的预览版和路线图信息。

## <a name="init"></a>Init

```console
devinit init
```

通过运行 [.devinit.json](devinit-json.md) 文件中指定的工具来初始化环境。

### <a name="options-for-init"></a>init 选项

`devinit init` 命令的可选选项。

| 参数             | 必需 | 说明                                                               |
|----------------------|----------|---------------------------------------------------------------------------|
| -f、--file            | 否       | 指向 `.devinit.json` 文件的路径。                                         |
| --error-action       | 否       | 指定如何处理错误。 选项：停止、忽略、继续（默认）。|
| -v、--verbose         | 否       | 发出详细输出。                                                      |
| -n、--dry-run         | 否       | 试运行。                                                                  |

#### <a name="--file-argument"></a>--file 参数

指定 devinit.json 文件的路径。 如果不指定 --file，我们将在以下位置搜索默认文件：

* {current-directory}\\.devinit.json
* {current-directory}\\devinit.json
* {current-directory}\\.devinit\\.devinit.json
* {current-directory}\\.devinit\\devinit.json
* {current-directory}\\devinit\\.devinit.json
* {current-directory}\\devinit\\devinit.json
* {current-directory}\\.devcontainer\\.devinit.json
* {current-directory}\\.devcontainer\\devinit.json

> [!NOTE]
> 如果找到多个默认文件，devinit 将使用上面列表中第一个出现的文件。

#### <a name="--error-action-argument"></a>--error-action 参数

请参阅[下文](#options-for-run)。

#### <a name="--verbose-switch"></a>--verbose 开关

请参阅[下文](#options-for-run)。

#### <a name="--dry-run-switch"></a>--dry-run 开关

请参阅[下文](#options-for-run)。

## <a name="run"></a>运行

```console
devinit run -t <toolname>
```

运行特定工具，参数如下。 有关每个工具的特定用法，请参阅[文档](devinit-tool-list.md)。

### <a name="options-for-run"></a>运行选项

`devinit run` 命令选项。

| 参数                                      | 必需 | 说明                                                                          |
|-----------------------------------------------|----------|--------------------------------------------------------------------------------------|
| -t、--tool                                     | 是      | 必需。 工具名称。                                                             |
| -i、--input                                    | 否       | 工具输入值。 例如，文件名、包或名称。                     |
| --error-action                                | 否       | 指定如何处理工具错误：停止、忽略、继续。 默认为停止。 |
| -v、--verbose                                  | 否       | 发出详细输出。                                                                 |
| -n、--dry-run                                  | 否       | 试运行。                                                                             |
| --&lt;arg1&gt; &lt;arg2&gt; ... &lt;argN&gt;  | 否       | 工具的其他命令行参数。                                       |

#### <a name="--error-action-argument"></a>--error-action 参数

指定工具返回非零退出代码时要执行的操作。 有效值为：

| 参数 | 说明                                                                                                                                                                                                                                                                           |
|----------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| continue | 在向标准错误发出错误后，继续处理其他工具。 devinit.exe 退出代码为非零（失败）。 此行为类似于“停止”错误操作，但会继续处理。 `continue` 是 init 命令的默认 error-action。              |
| ignore   | 在向标准输出发出警告后，继续处理其他工具。 DevInit 进程退出代码应始终为零（成功）。 `ignore` 设置将忽略所有错误。                                                                                                      |
| stop     | 向标准错误发出错误并停止处理工具。 devinit.exe 退出代码为非零（失败）。 这类似于继续错误操作，但处理在遇到第一个错误时暂停。 `stop` 是除 init 之外的所有命令的默认 error-action。 |

#### <a name="--dry-run-switch"></a>--dry-run 开关

将运行的回显工具命令。 某些工具可能会采取针对该工具记录的进一步操作。 

#### <a name="--verbose-switch"></a>--verbose 开关

向标准输出发出详细输出。 如果要执行的工具支持 verbose 选项，则将 verbose 开关传播到该工具。

#### <a name="--dry-run-switch"></a>--dry-run 开关

将运行但不执行任何工具的回显工具命令。

#### <a name="additional-command-line-arguments"></a>其他命令行参数

使用在其值中包含空格的 `<arg>` 时，必须包含一对额外的转义引号。

```console
devinit run -t <toolname> -<somearg> "<some value>"
```

用于将 dotnet 安装到特定目录 `C:\Program Files\dotnet` 中：

```console
devinit run -t require-dotnetcoresdk --"-InstallDir \"C:\Program Files\dotnet\""
```

## <a name="list"></a>列出

```console
devinit list
```

打印所有可用工具的列表。

## <a name="show"></a>显示

```console
devinit show -t <toolname>
```

| 参数       | 必需 | 说明                                                                          |
|----------------|----------|--------------------------------------------------------------------------------------|
| -t、--tool      | 是      | 必需。 工具名称。                                                             |

打印给定工具的帮助信息。

## <a name="version"></a>Version

```console
devinit version
```

打印用于 devinit 的当前版本信息。

## <a name="help"></a>帮助

```console
devinit help
devinit help list
```

打印用于 devinit 或特定命令 `devinit <command>` 的帮助文本。
 
