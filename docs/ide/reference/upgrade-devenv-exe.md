---
title: -Upgrade (devenv.exe)
description: 了解如何使用 Upgrade devenv 命令行开关将解决方案文件及其所有项目文件或指定的项目文件更新为这些文件的当前 Visual Studio 格式。
ms.custom: SEO-VS-2020
ms.date: 12/10/2018
ms.topic: reference
helpviewer_keywords:
- /upgrade Devenv switch
- Devenv, /upgrade switch
- upgrade Devenv switch
ms.assetid: 3468045c-5cc9-4157-9a9d-622452145d27
author: TerryGLee
ms.author: tglee
manager: jmartens
ms.technology: vs-ide-general
ms.workload:
- multiple
ms.openlocfilehash: b82eb2d9be21464b0f160a114972ab6ae7df4d0b
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126735734"
---
# <a name="upgrade-devenvexe"></a>/Upgrade (devenv.exe)

将解决方案文件及其所有项目文件或指定的项目文件更新为，这些文件的当前 Visual Studio 格式。

## <a name="syntax"></a>语法

```shell
devenv {SolutionFile|ProjectFile} /Upgrade [/Out OutputFilename]
```

## <a name="arguments"></a>参数

- SolutionFile

  若要升级整个解决方案及其项目，此为必需参数。 解决方案文件的路径和名称。 可以只输入解决方案文件的名称，也可以输入解决方案文件的完整路径和名称。 如果已命名的文件夹或文件尚不存在，便会进行创建。

- ProjectFile

  若要升级一个项目，此为必需参数。 解决方案中项目文件的路径和名称。 可以只输入项目文件的名称，也可以输入项目文件的完整路径和名称。 如果已命名的文件夹或文件尚不存在，便会进行创建。

- `/Out` *OutputFilename*

  可选。 要将工具输出发送到的文件的文件名。 如果文件已有，工具将输出追加到文件末尾。

## <a name="remarks"></a>注解

备份自动创建，并复制到在当前目录中创建的“备份”目录中。

要升级源代码控制的解决方案或项目，必须先将其签出。

使用 `/Upgrade` 开关不会打开 Visual Studio。 可在解决方案或项目的开发语言的“升级报告”中看到升级结果。 不会返回任何错误或使用情况信息。 若要详细了解如何在 Visual Studio 中升级项目，请参阅[移植、迁移和升级 Visual Studio 项目](../../porting/port-migrate-and-upgrade-visual-studio-projects.md)。

## <a name="example"></a>示例

下面的示例升级名为“MyProject.sln”的解决方案文件。

```shell
devenv "%USERPROFILE%\source\repos\MyProject\MyProject.sln" /upgrade
```

## <a name="see-also"></a>另请参阅

- [Devenv 命令行开关](../../ide/reference/devenv-command-line-switches.md)
