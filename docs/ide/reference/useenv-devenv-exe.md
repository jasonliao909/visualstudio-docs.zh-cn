---
title: -UseEnv (devenv.exe)
description: 了解如何使用 UseEnv devenv 命令行开关启动 Visual Studio 并加载某些环境变量以进行编译。
ms.custom: SEO-VS-2020
ms.date: 01/10/2019
ms.topic: reference
f1_keywords:
- VC.Project.UseEnvVars.ExcludePath
- VC.Project.UseEnvVars.LibraryPath
- VC.Project.UseEnvVars.SourcePath
- VC.Project.UseEnvVars.Include
- VC.Project.UseEnvVars.Path
- VC.Project.UseEnvVars.ReferencePath
helpviewer_keywords:
- UseEnv switch
- /UseEnv Devenv switch
- Devenv, /UseEnv
ms.assetid: 2dd14603-a61b-42d2-ba31-427a0ee8a799
author: TerryGLee
ms.author: tglee
manager: jmartens
ms.technology: vs-ide-general
ms.workload:
- multiple
ms.openlocfilehash: a8a2b8e0ed2c02a4d912eacd93c82236332e72c9
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122123744"
---
# <a name="useenv-devenvexe"></a>/UseEnv (devenv.exe)

启动 Visual Studio，并加载特定环境变量以供编译。

> [!NOTE]
> 此开关与使用 C++ 的桌面开发工作负载一起安装  。

## <a name="syntax"></a>语法

```shell
devenv /UseEnv {SolutionName|ProjectName}
```

## <a name="arguments"></a>自变量

- *SolutionName*

  解决方案文件的完整路径和名称。

- *ProjectName*

  项目文件的完整路径和名称。

## <a name="remarks"></a>备注

此开关通过“VC++ 目录”项目属性影响 Visual Studio IDE。 如果你指定 `/UseEnv` 开关，“VC++目录”节点显示 PATH、INCLUDE、LIBPATH 和 LIB 环境变量的值。 （它还显示“源目录”和“排除目录”的值。）否则，此节点将环境变量替换为五个目录值：“可执行目录”、“包含目录”、“引用目录”、“库目录”和“库 WinRT 目录”。

> [!TIP]
> 若要访问项目属性，请右键单击 C++ 项目，并选择“属性”。 在“属性页”对话框中，依次选择“配置属性”和“VC++ 目录”。

如果项目名称是使用此开关指定，工具显示项目父解决方案中所有项目的环境变量。

## <a name="example"></a>示例

下面的示例启动 Visual Studio，并将环境变量加载到 `MySolution` 解决方案的属性页中。

```shell
devenv.exe /useenv "%USERPROFILE%\source\repos\MySolution\MySolution.sln"
```

## <a name="see-also"></a>另请参阅

- [Devenv 命令行开关](../../ide/reference/devenv-command-line-switches.md)
- [“VC++ 目录”属性页 (Windows)](/cpp/build/reference/vcpp-directories-property-page)
