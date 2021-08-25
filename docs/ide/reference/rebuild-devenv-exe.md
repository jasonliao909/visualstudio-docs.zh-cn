---
title: -Rebuild (devenv.exe)
description: 了解如何使用 Rebuild devenv 命令行开关来执行清理，然后生成指定的解决方案配置。
ms.custom: SEO-VS-2020
ms.date: 12/10/2018
ms.topic: reference
helpviewer_keywords:
- Devenv, /rebuild switch
- Rebuild Devenv switch (/Rebuild)
- projects [Visual Studio], rebuilding
- /Rebuild Devenv switch
- applications [Visual Studio], rebuilding
ms.assetid: c5a8a4bf-0e2b-46eb-a44a-8aeb29b92c32
author: TerryGLee
ms.author: tglee
manager: jmartens
ms.technology: vs-ide-general
ms.workload:
- multiple
ms.openlocfilehash: c787cb853ce259f9aec7cf932d0f9e59d0b595c1
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122117158"
---
# <a name="rebuild-devenvexe"></a>/Rebuild (devenv.exe)

清理然后生成指定解决方案配置。

## <a name="syntax"></a>语法

```shell
devenv SolutionName /Rebuild [SolnConfigName [/Project ProjName [/ProjectConfig ProjConfigName]] [/Out OutputFilename]]
```

## <a name="arguments"></a>自变量

- *SolutionName*

  必需。 解决方案文件的完整路径和名称。

- *SolnConfigName*

  可选。 要用于重新生成 SolutionName 中命名的解决方案的解决方案配置的名称（如 `Debug` 或 `Release`）。 如果有多个解决方案平台可用，还必须指定平台（例如，`Debug|Win32`）。 如果未指定此参数或字符串为空 (`""`)，工具便会使用解决方案的有效配置。

- `/Project` *项目名称*

  可选。 解决方案中项目文件的路径和名称。 可以将项目在 SolutionName 文件夹中的显示名称或相对路径输入到项目文件中。 也可以输入项目文件的完整路径和名称。

-  ProjConfigName`/ProjectConfig` 

  可选。 要在重新生成已命名 `/Project` 时使用的项目生成配置的名称（如 `Debug` 或 `Release`）。 如果有多个解决方案平台可用，还必须指定平台（例如，`Debug|Win32`）。 如果此开关已指定，它会替代 SolnConfigName 参数。

- `/Out` *OutputFilename*

  可选。 要将工具输出发送到的文件的文件名。 如果文件已有，工具将输出追加到文件末尾。

## <a name="remarks"></a>注解

- 在 IDE 中，此开关执行与“重新生成解决方案”菜单命令相同的功能。

- 用双引号将含有空格的字符串引起来。

- 与清理和生成相关的摘要信息（包括错误）可以显示在“命令”窗口中，也可以显示在使用 [/Out](out-devenv-exe.md) 开关指定的任何日志文件中。

## <a name="example"></a>示例

下面的示例使用 `MySolution` 中的 `Debug` 项目生成配置来清理和重新生成项目 `CSharpWinApp`。

```shell
devenv "%USERPROFILE%\source\repos\MySolution\MySolution.sln" /rebuild Debug /project "CSharpWinApp\CSharpWinApp.csproj" /projectconfig Debug
```

## <a name="see-also"></a>另请参阅

- [Devenv 命令行开关](../../ide/reference/devenv-command-line-switches.md)
- [/Build (devenv.exe)](../../ide/reference/build-devenv-exe.md)
- [/Clean (devenv.exe)](../../ide/reference/clean-devenv-exe.md)
- [/Out (devenv.exe)](../../ide/reference/out-devenv-exe.md)
