---
title: 更改生成输出目录
description: 了解如何在预配置的基础上指定项目生成的输出的位置（用于调试、发布或两者）。
ms.custom: contperf-fy22q3
ms.date: 01/15/2022
ms.technology: vs-ide-compile
ms.topic: how-to
helpviewer_keywords:
- output directory, changing
ms.assetid: a8333c89-afb2-4b1d-b2e2-9146da852402
author: ghogen
ms.author: ghogen
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 3b22539cd001c410a03edbe8d973dd676a7010b7
ms.sourcegitcommit: b0ec2d8b7e32a9a6b50e462d588c64d471665533
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/10/2022
ms.locfileid: "139704074"
---
# <a name="how-to-change-the-build-output-directory"></a>如何：更改生成输出目录

可以在预配置的基础上指定项目生成的输出的位置（用于调试、发布或两者）。

## <a name="change-the-build-output-directory"></a>更改生成输出目录

1. 要打开项目的属性页面，右键单击“解决方案资源管理器”中的项目节点，然后选择“属性”。

2. 根据项目类型选择相应的选项卡：

   - 对于 C#，选择“生成”选项卡。
   - 对于 Visual Basic，选择“编译”选项卡。
   - 对于 C++ 或 JavaScript，选择“常规”选项卡。

3. 在顶部的配置下拉列表中，选择你想要更改其输出文件位置的配置（“调试”、“发布”或“所有配置”）。

4. 在页面上找到输出路径条目，路径条目根据项目类型而有所不同：

   - C# 和 JavaScript 项目的输出路径
   - Visual Basic 项目的生成输出路径
   - Visual C++ 项目的输出目录

   键入要生成输出的路径（绝对或相对于根项目目录），或选择“浏览”，浏览到该文件夹。

   ::: moniker range="<=vs-2019"
   ![Visual Studio C# 项目的输出路径属性](media/output-path.png)
   ::: moniker-end
   ::: moniker range=">=vs-2022"
   ![Visual Studio C# 项目的输出路径属性](media/vs-2022/output-path.png)
   ::: moniker-end

   > [!NOTE]
   > 某些项目会默认在生成路径中包括框架和运行时。 若要更改这一点，请在解决方案资源管理器中右键单击项目节点，选择“编辑项目文件”并添加以下内容：

   > ```xml
   > <PropertyGroup>
   >   <AppendTargetFrameworkToOutputPath>false</AppendTargetFrameworkToOutputPath>
   >   <AppendRuntimeIdentifierToOutputPath>false</AppendRuntimeIdentifierToOutputPath>
   > </PropertyGroup>
   > ```

> [!TIP]
> 如果系统未将输出生成到指定位置，请在 Visual Studio 的菜单栏上选择该位置，确保构建相应的配置（例如“调试”或“发布”）。
>
> ::: moniker range="<=vs-2019"
> ![2019 年 1 月Visual Studio配置选取器。](media/build-configuration-chooser.png)
> ::: moniker-end
> ::: moniker range=">=vs-2022"
> ![2022 年 1 月Visual Studio配置选取器。](media/vs-2022/build-configuration-chooser.png)
> ::: moniker-end

## <a name="build-to-a-common-output-directory"></a>生成到公共输出目录

默认情况下，[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 将解决方案中的每个项目生成到其在解决方案中自己的文件夹中。 可以通过更改项目的生成输出路径来强制将所有输出都放到相同的文件夹中。

### <a name="to-place-all-solution-outputs-in-a-common-directory"></a>将所有解决方案输出都放到一个共同目录中

1. 单击解决方案中的项目。

2. 在 **“项目”** 菜单上，单击 **“属性”** 。

3. 根据项目的类型，单击“编译”选项卡或“生成”选项卡，并将“输出路径”设置为适用于解决方案中所有项目的文件夹。

4. 打开项目的项目文件，将以下属性声明添加到第一个属性组。

   ```xml
   <PropertyGroup>
     <!-- existing property declarations are here -->
     <UseCommonOutputDirectory>true</UseCommonOutputDirectory>
   </PropertyGroup>
   ```

   `UseCommonOutputDirectory` `true`设置为 Visual Studio 会告知 (MSBuild) 及其基础生成引擎将多个项目输出放在同一文件夹中，因此 MSBuild 省略了当项目依赖于其他项目时通常会发生的复制步骤。

5. 对解决方案中所有项目重复步骤 1-4。 如果某些异常项目不应使用公共输出目录，可以跳过某些项目。

### <a name="to-set-the-intermediate-output-directory-for-a-project-net-projects"></a>为项目 ( 项目设置中间 A0.NET 目录) 

1. 打开项目文件。

1. 将以下属性声明添加到第一个属性组。

   ```xml
   <PropertyGroup>
     <!-- existing property declarations are here -->
     <IntermediateOutputPath>path</IntermediateOutputPath>
   <PropertyGroup>
   ```

   路径相对于项目文件，或者可以使用绝对路径。 如果要将项目名称放在路径中，可以使用属性 MSBuild引用`$(MSBuildProjectName)`它`$(MSBuildProjectDirectory)`。 有关可以使用的更多属性，MSBuild[保留属性和已知属性](../msbuild/msbuild-reserved-and-well-known-properties.md)。

1. Visual Studio项目文件夹下创建 obj 文件夹，但它为空。 可以在生成过程中将其删除。 为此，一种方式是添加生成后事件以运行以下命令：

   ```cmd
   rd "$(ProjectDir)obj" /s /q
   ```

   请参阅 [指定自定义生成事件](specifying-custom-build-events-in-visual-studio.md)。

   从 MSBuild 命令行生成时，不会创建 obj 文件夹。

## <a name="see-also"></a>另请参阅

- [项目设计器的“生成”页 (C#)](../ide/reference/build-page-project-designer-csharp.md)
- [常规属性页（项目）](/cpp/build/reference/general-property-page-project)
- [编译和生成](../ide/compiling-and-building-in-visual-studio.md)
