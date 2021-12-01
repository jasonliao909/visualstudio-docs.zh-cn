---
title: .NET Core 应用
description: 使用 devinit 安装特定 .NET Core SDK 的示例存储库。
ms.date: 11/04/2020
ms.topic: reference
author: andysterland
ms.author: andster
manager: jmartens
ms.workload:
- multiple
monikerRange: '>= vs-2019'
ms.prod: visual-studio-windows
ms.technology: devinit
ms.openlocfilehash: b3e25835f305a96b2205fc96cc0200d68ad033af
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "127833031"
---
# <a name="net-core-app"></a>.NET Core 应用

> [!IMPORTANT]
> 从 2021 年 4 月 12 日开始，将不再支持从 Visual Studio 2019 连接到 GitHub Codespaces，此个人预览版已结束。 我们的工作重点是改进云支持型内部循环和针对多种 Visual Studio 工作负载优化的 VDI 解决方案的体验。 在此期间，`devinit` 和关联工具将不再可用。 建议参与 Visual Studio 的开发人员社区论坛，了解未来要推出的预览版和路线图信息。

有关使用 devinit 在 Codespaces 中安装所需 .NET Core SDK 版本的完整示例，请参阅 [devinit-example-dotnet-core](https://github.com/microsoft/devinit-example-dotnet-core) 存储库。

## <a name="devinitjson"></a>.devinit.json

存储库根中的 .devinit.json 文件的内容。

```json
{
  "$schema": "https://json.schemastore.org/devinit.schema-2.0",
  "run": [
    {
      "comments": "Installs the .NET Core SDK specified in the global.json file.",
      "tool": "require-dotnetcoresdk"
    }
  ]
}
```

## <a name="devcontainerjson"></a>.devcontainer.json

存储库根中的 .devcontainer.json 文件的内容。

```json
{
  "postCreateCommand": "devinit init"
}
```

## <a name="globaljson"></a>global.json

存储库根中的 global.json 文件的内容。

```json
{
  "sdk": {
    "version": "3.1.302"
  }
}
```
