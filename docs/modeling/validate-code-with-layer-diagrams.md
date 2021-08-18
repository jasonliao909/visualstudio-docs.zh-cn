---
title: 使用依赖项关系图验证代码
description: 了解，若要确保代码不与设计冲突，应在代码中使用依赖项关系图验证Visual Studio。
ms.custom: SEO-VS-2020
ms.date: 09/28/2018
ms.topic: conceptual
helpviewer_keywords:
- dependency diagrams, validating
- validation, dependency diagrams
- validation, code
- code exploration, validating
- architecture, validating
- Visual Studio Ultimate, validating code
- validation, architecture
- validation, dependencies
- MSBuild, tasks
- MSBuild, dependency diagrams
- MSBuild, validating code
author: mgoertz-msft
ms.author: mgoertz
manager: jmartens
ms.technology: vs-ide-modeling
ms.workload:
- multiple
ms.openlocfilehash: 3bb9aeadd0e511ce5ed770eb56f0a2f02bf26542
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122123510"
---
# <a name="validate-code-with-dependency-diagrams"></a>使用依赖项关系图验证代码

## <a name="why-use-dependency-diagrams"></a>为何使用依赖项关系图？

若要确保代码不与设计冲突，请用代码中的依赖项关系图Visual Studio。 这可帮助你：

- 查找代码中的依赖项与依赖项关系图上的依赖项之间的冲突。

- 查找建议的更改可能会影响的依赖项。

   例如，可以编辑依赖项关系图以显示潜在的体系结构更改，然后验证代码以查看受影响的依赖项。

- 将代码重构或迁移到其他设计。

   查找在将代码移动到其他体系结构时需要工作的代码或依赖项。

**惠?**

- Visual Studio

  若要为 .NET Core 项目创建依赖项关系图，Visual Studio 2019 版本 16.2 或更高版本。

- 具有具有依赖项关系图的建模项目的解决方案。 此依赖项关系图必须链接到 C# 中的项目或Visual Basic要验证的项目。 请参阅 [从代码 创建依赖项关系图](../modeling/create-layer-diagrams-from-your-code.md)。

若要查看支持此功能的 Visual Studio 的版本，请参阅 [体系结构和建模工具的版本支持](../modeling/analyze-and-model-your-architecture.md#VersionSupport)。

可以在命令提示符下从打开的依赖项关系图Visual Studio验证代码。 还可以在运行本地生成或生成时自动Azure Pipelines代码。 请参阅 [第 9 频道视频：使用依赖项关系图设计和验证体系结构](https://channel9.msdn.com/Series/Visual-Studio-2012-Premium-and-Ultimate-Overview/Visual-Studio-Ultimate-2012-Using-layer-diagrams-to-design-and-validate-your-architecture)。

> [!IMPORTANT]
> 如果要使用 TFS Team Foundation Server (运行) 验证，还必须在生成服务器上安装Visual Studio版本。

## <a name="live-dependency-validation"></a>实时依赖项验证

依赖项验证实时发生，错误列表 会立即 **显示错误**。

* C# 和 Visual Basic 支持实时验证。

* 若要在使用实时依赖项验证时启用完整解决方案分析，请从"错误列表"中出现的黄金栏中打开 **选项设置**。

  - 如果对解决方案中所有体系结构问题不感兴趣，可以永久消除黄金条。
  - 如果未启用完整解决方案分析，则仅对正在编辑的文件执行分析。

* 升级项目以启用实时验证时，会显示转换进度对话框。

* 更新项目进行实时依赖项验证时，NuGet包的版本将升级为所有项目的相同，并且是使用的最高版本。

* 添加新的依赖项验证项目会触发项目更新。

## <a name="see-if-an-item-supports-validation"></a>查看项是否支持验证

可以将层链接到在多个应用Office共享的项目中的网站、文档、纯文本文件和文件，但验证过程不会包括它们。 如果引用的项目或程序集链接到单独的层，而且这些层之间没有依赖关系出现，则将不会出现验证错误。 除非代码使用此类引用，否则这些引用不被视为依赖项。

1. 在依赖项关系图上，选择一个或多个层，右键单击所选内容，然后单击"查看 **链接"。**

2. 在 **层资源管理器** 中，查看" **支持验证"** 列。 如果该值为 false，则项不支持验证。

## <a name="include-other-net-assemblies-and-projects-for-validation"></a>包括其他 .NET 程序集和项目以进行验证

将项拖动到依赖项关系图时，对相应 .NET 程序集或项目的引用会自动添加到建模项目中的"层引用"文件夹。 此文件夹包含对验证过程中分析的程序集和项目的引用。 可以包括其他 .NET 程序集和项目进行验证，而无需手动将它们拖动到依赖项关系图。

1. 在 **解决方案资源管理器** 中，右键单击建模项目或"层引用 **"文件夹，** 然后单击"添加 **引用"。**

2. 在"**添加引用**"对话框中，选择程序集或项目，然后单击"确定 **"。**

## <a name="validate-code-manually"></a>手动验证代码

如果有一个链接到解决方案项的打开依赖项关系图，可以从该关系图运行 **"** 验证快捷方式"命令。 还可使用命令提示符运行 **msbuild** 命令，将 **/p：ValidateArchitecture** 自定义属性设置为 **True。** 例如，在对代码进行更改时，请定期执行层验证以便能够提前捕获依赖项冲突。

### <a name="validate-code-from-an-open-dependency-diagram"></a>验证打开的依赖项关系图中的代码

1. 右键单击关系图图面，然后单击"**验证体系结构"。**

    > [!NOTE]
    > 默认情况下，依赖项关系图 (.layerdiagram) 的"生成操作"属性设置为 **"** 验证"，以便验证过程中包含关系图。

     " **错误列表** "窗口报告发生的任何错误。 有关验证错误的详细信息，请参阅 [排查层验证问题](#troubleshoot-layer-validation-issues)。

2. 若要查看每个错误的源，请在"错误列表"窗口中双击 **该** 错误。

    > [!NOTE]
    > Visual Studio可能显示代码图，而不是错误源。 当代码依赖于依赖项关系图未指定的程序集，或者代码缺少依赖项关系图指定的依赖项时，将发生这种情况。 检查代码映射或代码，以确定此依赖关系是否应该存在。 有关代码图的更多信息，请参阅 [映射解决方案中的依赖项](../modeling/map-dependencies-across-your-solutions.md)。

3. 若要管理错误，请参阅 [解决层验证错误](#resolve-layer-validation-errors)。

### <a name="validate-code-at-the-command-prompt"></a>在命令提示符下验证代码

1. 打开Visual Studio提示符。

2. 选择以下选项之一：

   - 若要根据解决方案中的特定建模项目验证代码，MSBuild自定义属性运行代码。

       ```
       msbuild <FilePath+ModelProjectFileName>.modelproj /p:ValidateArchitecture=true
       ```

     - 或 -

       浏览到包含建模项目 (.modelproj) 文件和依赖项关系图的文件夹，然后MSBuild自定义属性运行以下自定义属性：

       ```
       msbuild /p:ValidateArchitecture=true
       ```

   - 若要针对解决方案中所有建模项目验证代码，MSBuild以下自定义属性运行代码：

       ```
       msbuild <FilePath+SolutionName>.sln /p:ValidateArchitecture=true
       ```

     - 或 -

       浏览到解决方案文件夹，该文件夹必须包含一个包含依赖项关系图的建模项目，然后MSBuild以下自定义属性运行解决方案：

       ```
       msbuild /p:ValidateArchitecture=true
       ```

     将列出发生的任何错误。 有关任务MSBuild，[请参阅](../msbuild/msbuild.md)MSBuild 和[MSBuild 任务](../msbuild/msbuild-task.md)。

   有关验证错误的详细信息，请参阅 [排查层验证问题](#troubleshoot-layer-validation-issues)。

### <a name="manage-validation-errors"></a>管理验证错误

在开发过程中，你可能需要在验证期间禁止显示报告的某些冲突。 例如，你可能希望禁止显示你已解决或与特定情形不相关的错误。 禁止显示错误时，最佳做法是在 Team Foundation 中记录工作项。

> [!WARNING]
> 必须已连接到 TFS 源代码管理 (SCC) 才可创建或链接到工作项。 如果尝试打开到其他 TFS SCC 的连接，则 Visual Studio 会自动关闭当前解决方案。 请先确保已连接到相应的 SCC，然后再尝试创建或链接到工作项。 在更高版本的 Visual Studio 中，如果未连接到 SCC，则菜单命令不可用。

#### <a name="create-a-work-item-for-a-validation-error"></a>为验证错误创建工作项

- 在"**错误列表**"窗口中，右键单击错误，指向"创建工作项"，然后单击要创建的工作项的类型。

使用这些任务在"错误列表"窗口中 **管理验证** 错误：

|**To**|**需要遵循的步骤**|
|-|-|
|禁止在验证过程中显示选定的错误|右键单击一个或多个所选错误，指向"**管理验证错误**"，然后单击"**禁止显示错误"。**<br /><br /> 禁止显示的错误在显示时均带有删除线格式。 在你下次运行验证时，这些错误将不会显示。<br /><br /> 在相应的依赖项关系图文件的 .suppresss 文件中跟踪抑制的错误。|
|停止禁止显示选定的错误|右键单击选定的抑制错误，指向"**管理验证错误**"，然后单击"停止 **禁止显示错误"。**<br /><br /> 在你下次运行验证时，这些所选的禁止显示的错误将会显示。|
|还原"错误列表"窗口中 **所有禁止显示** 的错误|右键单击"错误列表"窗口中 **的任意位置，** 指向"**管理验证错误**"，然后单击"显示 **所有禁止显示的错误"。**|
|从"错误列表"窗口中隐藏 **所有禁止显示** 的错误|右键单击"错误列表"窗口中 **的任意位置，** 指向"**管理验证错误**"，然后单击"隐藏 **所有禁止显示的错误"。**|

## <a name="validate-code-automatically"></a>自动验证代码

每次运行本地生成时，都可以执行层验证。 如果团队使用Azure DevOps，可以使用门控签入执行层验证，可以通过创建自定义 MSBuild 任务来指定该验证，并使用生成报告来收集验证错误。 若要创建封闭签入版本，请参阅 [TFVC 封闭签入](/azure/devops/pipelines/build/triggers)。

### <a name="to-validate-code-automatically-during-a-local-build"></a>在本地生成期间自动验证代码

使用文本编辑器打开建模项目 (.modelproj) 文件，然后包括以下属性：

```xml
<ValidateArchitecture>true</ValidateArchitecture>
```

\- 或 -

1. 在 **解决方案资源管理器** 中，右键单击包含依赖关系图或关系图的建模项目，然后单击 " **属性**"。

2. 在 " **属性** " 窗口中，将建模项目的 " **验证体系结构** " 属性设置为 " **True**"。

    这将在验证过程中包括建模项目。

3. 在 **解决方案资源管理器** 中，单击要用于验证的 ( microsoft.visualstudio.teamarchitect.layerdesigner.diagrams.layerdiagram.show) 的依赖项关系图。

4. 在 " **属性** " 窗口中，确保已将关系图的 " **生成操作** " 属性设置为 " **验证**"。

    这包括验证过程中的依赖关系图。

若要在错误列表 "窗口中管理错误，请参阅 [解决层验证错误](#resolve-layer-validation-errors)。

## <a name="troubleshoot-layer-validation-issues"></a>层验证问题疑难解答

下表描述了层验证问题及其解决方法。 这些问题不同于代码与设计发生冲突而导致出现的错误。 有关这些错误的详细信息，请参阅 [排除层验证问题](#troubleshoot-layer-validation-issues)。

|**问题**|**可能的原因**|**分辨率**|
|-|-|-|
|验证错误不按预期发生。|验证不适用于从解决方案资源管理器中的其他依赖关系图复制到同一建模项目中的依赖关系图。 以这种方式复制的依赖项关系图包含与原始依赖关系图相同的引用。|将新的依赖关系图添加到建模项目。<br /><br /> 将源依赖关系图中的元素复制到新关系图中。|

## <a name="resolve-layer-validation-errors"></a>解决层验证错误

根据依赖关系图验证代码时，如果代码与设计发生冲突，则会发生验证错误。 例如，以下情况可能导致发生验证错误：

- 将项目指派给了错误的层。 在这种情况下，请移动项目。

- 项目（例如类）以与你的体系结构相冲突的方式使用了其他类。 在这种情况下，请重构代码以移除依赖关系。

若要解决这些错误，请更新代码，直至验证过程中不出现其他错误为止。 可以反复执行此任务。

以下各节描述这些错误中使用的语法，解释了这些错误的含义，并提供了纠正或管理这些错误的方法。

|**语法**|**说明**|
|-|-|
|*ArtifactN* (*ArtifactTypeN*) |*ArtifactN* 是与依赖关系图上的层关联的项目。<br /><br /> *ArtifactTypeN* 是 *ArtifactN* 的类型，例如 **类** 或 **方法**，例如：<br /><br /> MySolution.MyProject.MyClass.MyMethod(Method)|
|*NamespaceNameN*|命名空间的名称。|
|*LayerNameN*|依赖关系图层的名称。|
|*DependencyType*|*Artifact1* 和 *Artifact2* 之间的依赖关系的类型。 例如， *Artifact1* 具有与 *Artifact2* 的 **调用** 关系。|

| **错误语法** | 错误说明 |
|-|-|
| DV0001： **依赖关系无效** | 当映射到层 (命名空间、类型、成员) 的代码元素引用映射到另一层的代码元素时，将报告此问题，但在包含此层的依赖项验证关系图中，这些层之间没有依赖项箭头。 这是依赖项约束冲突。 |
| DV1001： **无效的命名空间名称** | 此问题将在与 "允许的命名空间名称" 属性不包含定义此代码元素的命名空间的层关联的代码元素上报告。 这是一个命名约束冲突。 请注意，"允许的命名空间名称" 的语法应为命名空间的分号列表，在这些命名空间中，将允许定义与关联的代码元素。 |
| DV1002： **依赖不可引用命名空间** | 此问题在与层关联的代码元素上报告，并引用在层的 "不可引用 Namespace" 属性中定义的命名空间中定义的另一个代码元素。 这是一个命名约束冲突。 请注意，"不可引用命名空间" 属性定义为不应在与此层关联的代码元素中引用的以分号分隔的命名空间列表。 |
| DV1003：不 **允许的命名空间名称** | 此问题将在与 "不允许的命名空间名称" 属性包含定义此代码元素的命名空间的层关联的代码元素上报告。 这是一个命名约束冲突。 请注意，"不允许的命名空间名称" 属性定义为分号分隔的命名空间列表，其中不应定义与此层关联的代码元素。 |
| DV2001： **层关系图存在** | 此问题在不包含依赖关系关系图文件的项目上报告，但引用依赖项验证分析器。 如果未使用依赖项验证，则可以直接从解决方案资源管理器中移除 "DependencyValidation" 或取消显示此警告。 若要添加依赖关系图，请参阅 [从代码创建依赖项关系](../modeling/create-layer-diagrams-from-your-code.md)图。 |
| DV2002：未 **映射的类型基** | 当代码元素未映射到任何层时，会报告此问题。 |
| DV3001： **缺少链接** | 层 "*LayerName*" 链接到了找不到的 "*项目*"。 是否缺少程序集引用? |
| DV9001： **体系结构分析找到内部错误** | 结果可能不完整。 有关详细信息，请参阅详细的生成事件日志或输出窗口。 |

## <a name="see-also"></a>请参阅

- [Visual Studio 中的实时依赖项验证](https://devblogs.microsoft.com/devops/live-dependency-validation-in-visual-studio-2017/)
- [在开发过程中验证系统](../modeling/validate-your-system-during-development.md)
- [视频：实时验证你的体系结构依赖项](https://sec.ch9.ms/sessions/69613110-c334-4f25-bb36-08e5a93456b5/170ValidateArchitectureDependenciesWithVisualStudio.mp4)
