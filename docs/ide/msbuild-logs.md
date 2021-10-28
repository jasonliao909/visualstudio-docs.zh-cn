---
title: 对 MSBuild 问题进行故障排除并为其创建日志
description: 了解如何诊断 Visual Studio 项目中的生成问题，并在必要时创建日志以发送给 Microsoft 进行调查。
ms.custom: SEO-VS-2020
ms.date: 02/08/2021
ms.technology: vs-ide-compile
ms.topic: troubleshooting
helpviewer_keywords:
- msbuild logs"
author: corob-msft
ms.author: corob
manager: jmartens
dev_langs:
- CSharp
- VB
- CPP
ms.workload:
- multiple
ms.description: Generate build logs for msbuild projects to collect helpful information when troubleshooting issues.
ms.openlocfilehash: 3496eb5a0e8f699a994037ccc853a76e4f93e4ee
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126736714"
---
# <a name="troubleshoot-and-create-logs-for-msbuild-problems"></a>对 MSBuild 问题进行故障排除并为其创建日志

以下过程可以帮助你诊断 Visual Studio 项目中的生成问题，并在必要时创建日志以发送给 Microsoft 进行调查。

## <a name="a-property-value-is-ignored"></a>一个属性值被忽略

如果项目属性看上去设置为特定值，但对生成没有影响，请按照下列步骤进行操作：

1. 打开与你的 Visual Studio 版本对应的 Visual Studio 开发人员命令提示符。
1. 在替换解决方案路径、配置和项目名称的值后，运行以下命令：

    ```cmd
    msbuild /p:SolutionDir="c:\MySolutionDir\";Configuration="MyConfiguration";Platform="Win32" /pp:out.xml MyProject.vcxproj
    ```

    此命令将生成一个“预处理”msbuild 项目文件 (out.xml)。 你可以在该文件中搜索特定属性以查看其定义位置。

属性的最后一个定义是生成使用了什么。 如果设置了两次属性，则第二个值将覆盖第一个值。 此外，MSBuild 还会评估多个传递中的项目：

- PropertyGroups 和 Imports
- ItemDefinitionGroups
- ItemGroups
- 目标

因此，给定以下顺序：

```xml
<PropertyGroup>
   <MyProperty>A</MyProperty>
</PropertyGroup>
<ItemGroup>
   <MyItems Include="MyFile.txt"/>
</ItemGroup>
<ItemDefinitionGroup>
  <MyItems>
      <MyMetadata>$(MyProperty)</MyMetadata>
  </MyItems>
</ItemDefinitionGroup>
<PropertyGroup>
   <MyProperty>B</MyProperty>
</PropertyGroup>
```

在生成期间，“MyFile.txt”项的“MyMetadata”值将评估为“B”（不是“A”，也不是空）

## <a name="incremental-build-is-building-more-than-it-should"></a>增量生成的生成超出预期

如果 MSBuild 不必要地重新生成项目或项目项，请创建详细的生成日志或二进制生成日志。 你可以在该日志中搜索不必要地生成或编译的文件。 输出的内容与以下类似：

```output
  Task "CL"

  Using cached input dependency table built from:

  F:\test\Project1\Project1\Debug\Project1.tlog\CL.read.1.tlog

  Outputs for F:\TEST\PROJECT1\PROJECT1\PROJECT1.CPP:
  F:\TEST\PROJECT1\PROJECT1\DEBUG\PROJECT1.OBJ
  Project1.cpp will be compiled because F:\TEST\PROJECT1\PROJECT1\PROJECT1.H was modified at 6/5/2019 12:37:09 PM.

  Outputs for F:\TEST\PROJECT1\PROJECT1\PROJECT1.CPP:
  F:\TEST\PROJECT1\PROJECT1\DEBUG\PROJECT1.OBJ

  Write Tracking Logs:
  Debug\Project1.tlog\CL.write.1.tlog
```

如果是在 Visual Studio IDE 中生成（输出窗口详细程度为详细），输出窗口将显示每个项目不是最新的原因：

```output
1>------ Up-To-Date check: Project: Project1, Configuration: Debug Win32 ------

1>Project is not up-to-date: build input 'f:\test\project1\project1\project1.h' was modified after the last build finished.
```

## <a name="create-a-binary-msbuild-log-at-the-command-prompt"></a>在命令提示符下创建二进制 MSBuild 日志

1. 打开你的 Visual Studio 版本的开发人员命令提示符

1. 从命令提示符中运行以下命令之一。 （记得使用你的实际项目和配置值。）：

   ```cmd
   Msbuild /p:Configuration="MyConfiguration";Platform="x86" /bl MySolution.sln
   ```

   or

   ```cmd
   Msbuild /p:SolutionDir="c:\MySolutionDir\";Configuration="MyConfiguration";Platform="Win32" /bl MyProject.vcxproj
   ```

将在运行 MSBuild 的目录中创建 msbuild.binlog 文件。

## <a name="create-a-binary-msbuild-log-by-using-the-project-system-tools-extension"></a>使用项目系统工具扩展创建二进制 MSBuild 日志

1. 下载并安装[项目系统工具扩展](https://marketplace.visualstudio.com/items?itemName=VisualStudioProductTeam.ProjectSystemTools)。

1. 安装扩展后，某些新项将显示在“查看” > “其他窗口”菜单中。

   ![“其他窗口”菜单](../ide/media/view-menu.png)

1. 选择“查看” > “其他窗口” > “生成日志记录”，以在 Visual Studio 中显示“生成日志记录”窗口。 选择第一个工具栏图标，在项目系统中开始记录常规和设计时生成。

   ![“生成日志”窗口](../ide/media/build-logging-click-to-record.png)

1. 记录生成后，它将显示在“生成日志”窗口中。 右键单击该项，然后在上下文菜单中选择“保存日志”以保存 .binlog 文件。

   ![“生成日志”上下文菜单](../ide/media/build-logging-context-menu.png)

可以使用 [MSBuild 结构化日志查看器](http://www.msbuildlog.com/)查看和搜索 .binlog 文件。

## <a name="create-a-detailed-log"></a>创建详细的日志

1. 从 Visual Studio 主菜单中，转到“工具” > “选项” > “项目和解决方案” >“生成并运行”。
1. 在两个组合框中，将“Msbuild 项目生成详细程度”设置为“详细”。 上面的组合框控制“输出窗口”中的生成详细程度，第二个组合框控制生成期间在每个项目的中间目录中创建的 \<projectname\>.log 文件中的生成详细程度。
2. 从 Visual Studio 开发人员命令提示符中，输入以下命令之一，替换你的实际路径和配置值：

    ```cmd
    Msbuild /p:Configuration="MyConfiguration";Platform="x86" /fl MySolution.sln
    ```

    or

    ```cmd
    Msbuild /p:/p:SolutionDir="c:\MySolutionDir\";Configuration="MyConfiguration";Platform="Win32" /fl MyProject.vcxproj
    ```

    将在运行 msbuild 的目录中创建 Msbuild.log 文件。

## <a name="see-also"></a>请参阅

- [Visual Studio 故障排除](/troubleshoot/visualstudio/welcome-visual-studio/)
