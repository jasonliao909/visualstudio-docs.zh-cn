---
title: set-env
description: devinit 工具 require-set-env。
ms.date: 11/20/2020
ms.topic: reference
author: andysterland
ms.author: andster
manager: jmartens
ms.workload:
- multiple
monikerRange: '>= vs-2019'
ms.prod: visual-studio-windows
ms.technology: devinit
ms.openlocfilehash: 86e6f7c22ac75d976050858eb2853f9036377fee
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "127832979"
---
# <a name="set-env"></a>set-env

> [!IMPORTANT]
> 从 2021 年 4 月 12 日开始，将不再支持从 Visual Studio 2019 连接到 GitHub Codespaces，此个人预览版已结束。 我们专注于为云支持的内部循环和 VDI 解决方案提供不断发展的体验，这些解决方案针对一组广泛的Visual Studio工作负载进行优化。 作为此和 `devinit` 关联工具的一部分，将不再可用。 建议参与 Visual Studio 的开发人员社区论坛，了解未来要推出的预览版和路线图信息。

`set-env`该工具可用于设置环境变量，以用于当前进程。 环境变量仅在当前进程中设置，如果其他工具在该进程中运行 `devinit` ，则它们将被其他工具使用。

此工具使用 .NET Core `Environment.SetEnvironment` API，并且具有与该 API 相同的限制。 有关详细信息，请参阅 [的文档](/dotnet/api/system.environment.setenvironmentvariable?view=netcore-3.1&preserve-view=true) `Environment.SetEnvironment` 。

## <a name="usage"></a>使用情况

| 名称                                         | 类型   | 必须 | 值                                                                       |
|----------------------------------------------|--------|----------|-----------------------------------------------------------------------------|
| **注释**                                 | 字符串型 | 否       | 可选注释属性。 未使用。                                       |
| [**输入**](#input)                          | 字符串型 | 否       | 工具的输入。 有关详细信息 [，](#input) 请参阅下面的输入。               |
| [**additionalOptions**](#additional-options) | 字符串型 | 否       | 有关详细信息 [，请参阅](#additional-options) 下面的其他选项。            |

### <a name="input"></a>输入

该工具 `set-env` 使用单个字符串作为 属性的 `input` 输入。 字符串的格式应为分号 (;) 分隔键值对 (name=value) ，以及基于 属性的值的四个可能 `input` 操作。

| 操作       | 输入            | 说明                                                                                                                                                              | 示例             |
|--------------|------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------------|
| **全部列出** | 空或省略 | 列出所有当前环境变量。                                                                                                                           | `"input":""`        |
| **list one** | 字符串           | 按名称列出特定环境变量的值。                                                                                                               | `"input":"foo"`     |
| **add**      | 字符串           | 将环境变量的值设置为键值对。 添加一个新的环境变量（如果尚未存在）或设置现有环境变量的值 | `"input":"foo=bar"` |
| **delete**   | 字符串           | 通过传递空值字符串删除现有环境变量。                                                                                            | `"input":"foo="`    |

字符串 `input` 可以包含环境变量扩展，例如 `%userprofile%` ，在读取值时将展开该扩展。

### <a name="additional-options"></a>附加选项

 `--user``--process`可以包括 `--machine` 、 或 以指定在何处设置环境变量。 默认情况下，我们以用户为目标。 有关环境变量的可能目标详细信息，请参阅 [EnvironmentVariableTarget](https://docs.microsoft.com/dotnet/api/system.environmentvariabletarget)。

### <a name="default-behavior"></a>默认行为

该工具的默认 `set-env` 行为是列出所有当前环境变量。

## <a name="usage-in-a-codespace"></a>codespace 中的用法

如果使用的是 codespace，可以通过在 文件中自定义 属性来设置在 codespace `remoteEnv` 中使用的环境 [`.devcontainer.json`](https://code.visualstudio.com/docs/remote/devcontainerjson-reference) 变量。

## <a name="example-usage"></a>用法示例
下面是如何使用 运行 `set-env` 的示例 `.devinit.json` 。

#### <a name="devinitjson-that-will-set-an-environment-variable-foo-to-value-bar"></a>将环境变量 设置为值 的 .devinit.json： `foo` `bar`
```json
{
  "$schema": "https://json.schemastore.org/devinit.schema-3.0",
  "run": [
    {
      "tool": "set-env",
      "input": "foo=bar",
    }
  ]
}
```

#### <a name="devinitjson-that-will-set-an-environment-variable-foo-to-value-bar-stored-in-the-environment-block-associated-with-the-current-process"></a>.devinit.json，它将环境变量 设置为值 ，存储在与当前进程 `foo` `bar` 关联的环境块中：
```json
{
  "$schema": "https://json.schemastore.org/devinit.schema-3.0",
  "run": [
    {
      "tool": "set-env",
      "input": "foo=bar",
      "additionalOptions": "--process",
    }
  ]
}
```

#### <a name="devinitjson-that-will-display-the-value-of-an-environment-variable"></a>将显示环境变量值的 .devinit.json：
```json
{
  "$schema": "https://json.schemastore.org/devinit.schema-3.0",
  "run": [
    {
      "tool": "set-env",
      "input": "foo",
    }
  ]
}
```

#### <a name="devinitjson-that-will-list-all-the-environment-variables"></a>将列出所有环境变量的 .devinit.json：
```json
{
  "$schema": "https://json.schemastore.org/devinit.schema-3.0",
  "run": [
    {
      "tool": "set-env",
    }
  ]
}
```

#### <a name="devinitjson-that-will-delete-an-environment-variable"></a>将删除环境变量的 .devinit.json：
```json
{
  "$schema": "https://json.schemastore.org/devinit.schema-3.0",
  "run": [
    {
      "tool": "set-env",
      "input": "foo=",
    }
  ]
}
```


#### <a name="devinitjson-that-will-use-environment-variable-expansion"></a>将使用环境变量扩展的 .devinit.json：
```json
{
  "$schema": "https://json.schemastore.org/devinit.schema-3.0",
  "run": [
    {
      "tool": "set-env",
      "input": "_savedPath=%path%",
    }
  ]
}
```

#### <a name="devinitjson-that-will-set-an-environment-variable-value-using-path-manipulation"></a>.devinit.json，它将使用路径操作设置环境变量值：
```json
{
  "$schema": "https://json.schemastore.org/devinit.schema-3.0",
  "run": [
    {
      "tool": "set-env",
      "input": "path=%path%;%userprofile%\\CustomFolder",
    }
  ]
}
```

#### <a name="devinitjson-that-will-restore-path-from-saved-copy"></a>.devinit.json，它将从保存的副本还原路径：
```json
{
  "$schema": "https://json.schemastore.org/devinit.schema-3.0",
  "run": [
    {
      "tool": "set-env",
      "input": "path=%_savedPath%",
    }
  ]
}
```
