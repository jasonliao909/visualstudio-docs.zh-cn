---
title: 解决方案 (。Sln) 文件
description: 了解 .sln 文件，该文件是维护项目中项目的状态信息Visual Studio。
ms.custom: SEO-VS-2020
ms.date: 03/15/2019
ms.topic: conceptual
helpviewer_keywords:
- sln files, VSPackages
- solutions, .sln files
- .sln files, VSPackages
ms.assetid: 7d7ef539-2e4b-4637-b853-8ec7626609df
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: 5c036504bd5a7b881edab2d2bf4ef373706d65f9
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122062740"
---
# <a name="solution-sln-file"></a>解决方案 (.sln) 文件

解决方案是一种结构，用于组织项目中Visual Studio。 该解决方案在两个文件中维护项目的状态信息：

- .sln 文件 (基于文本的共享) 

- .suo 文件 (特定于用户的二进制解决方案选项) 

有关 .suo 文件的详细信息，请参阅解决方案 [用户选项 (。Suo) 文件](../../extensibility/internals/solution-user-options-dot-suo-file.md)。

如果 VSPackage 由于在 .sln 文件中被引用而加载，则环境将调用 以 <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistSolutionProps.ReadSolutionProps%2A> 读取 .sln 文件。

.sln 文件包含环境用于查找和加载持久数据及其引用的项目 VSPackages 的名称值参数的基于文本的信息。 当用户打开解决方案时，环境会循环访问 .sln 文件中 、 和 信息，以加载解决方案、解决方案中的项目以及附加到解决方案 `preSolution` `Project` 的任何持久 `postSolution` 化信息。

每个项目的 文件都包含环境读取的其他信息，以使用该项目的项填充层次结构。 层次结构数据持久性由项目控制。 数据通常不存储在 .sln 文件中，不过，如果选择这样做，你可以有意将项目信息写入 .sln 文件。 有关持久性详细信息，[请参阅暂留](../../extensibility/internals/project-persistence.md)Project打开和保存Project[项](../../extensibility/internals/opening-and-saving-project-items.md)。

## <a name="file-header"></a>文件头

.sln 文件的标头如下所示：

::: moniker range="vs-2017"

```
Microsoft Visual Studio Solution File, Format Version 12.00
# Visual Studio 15
VisualStudioVersion = 15.0.26730.15
MinimumVisualStudioVersion = 10.0.40219.1
```

### <a name="definitions"></a>定义

`Microsoft Visual Studio Solution File, Format Version 12.00`\
定义文件格式版本的标准标头。

`# Visual Studio 15`\
最近一次Visual Studio保存 (文件) 版本。 此信息控制解决方案图标中的版本号。

`VisualStudioVersion = 15.0.26730.15`\
最近一次Visual Studio保存 (的完整) 版本。 如果解决方案文件由具有相同主版本的较新版本的 Visual Studio保存，则此值不会更新，以减少解决方案文件中流失。

`MinimumVisualStudioVersion = 10.0.40219.1`\
可以 (此解决方案) Visual Studio版本的最低版本。

::: moniker-end

::: moniker range=">=vs-2019"

```
Microsoft Visual Studio Solution File, Format Version 12.00
# Visual Studio Version 16
VisualStudioVersion = 16.0.28701.123
MinimumVisualStudioVersion = 10.0.40219.1
```

### <a name="definitions"></a>定义

`Microsoft Visual Studio Solution File, Format Version 12.00`\
定义文件格式版本的标准标头。

`# Visual Studio Version 16`\
最近一次Visual Studio保存 (文件) 版本。 此信息控制解决方案图标中的版本号。

`VisualStudioVersion = 16.0.28701.123`\
最近一次Visual Studio保存 (的完整) 版本。 如果解决方案文件由具有相同主Visual Studio版本的较新版本保存，则此值不会更新，以减少该文件中的改动。

`MinimumVisualStudioVersion = 10.0.40219.1`\
可以 (此解决方案) Visual Studio版本的最低版本。

::: moniker-end

## <a name="file-body"></a>文件正文

.sln 文件的正文由多个标记为 的部分 `GlobalSection` 组成，如下所示：

```
Project("{F184B08F-C81C-45F6-A57F-5ABD9991F28F}") = "Project1", "Project1.vbproj", "{8CDD8387-B905-44A8-B5D5-07BB50E05BEA}"
EndProject
Global
  GlobalSection(SolutionNotes) = postSolution
  EndGlobalSection
  GlobalSection(SolutionConfiguration) = preSolution
       ConfigName.0 = Debug
       ConfigName.1 = Release
  EndGlobalSection
  GlobalSection(ProjectDependencies) = postSolution
  EndGlobalSection
  GlobalSection(ProjectConfiguration) = postSolution
   {8CDD8387-B905-44A8-B5D5-07BB50E05BEA}.Debug.ActiveCfg = Debug|x86
   {8CDD8387-B905-44A8-B5D5-07BB50E05BEA}.Debug.Build.0 = Debug|x86
   {8CDD8387-B905-44A8-B5D5-07BB50E05BEA}.Release.ActiveCfg = Release|x86
   {8CDD8387-B905-44A8-B5D5-07BB50E05BEA}.Release.Build.0 = Release|x86
  EndGlobalSection
  GlobalSection(ExtensibilityGlobals) = postSolution
  EndGlobalSection
  GlobalSection(ExtensibilityAddIns) = postSolution
  EndGlobalSection
EndGlobal
```

若要加载解决方案，环境将执行以下任务序列：

1. 环境读取 .sln 文件的"全局"部分，并处理标记为 的所有部分 `preSolution` 。 在此示例文件中，有一个这样的语句：

   ```
   GlobalSection(SolutionConfiguration) = preSolution
        ConfigName.0 = Debug
        ConfigName.1 = Release
   ```

   当环境读取 `GlobalSection('name')` 标记时，它会使用注册表将名称映射到 VSPackage。 密钥名称应存在于 [HKLM<\\ 应用程序 ID 注册表根 \> \SolutionPersistence\AggregateGUIDs] 下的注册表中。 密钥的默认值是用于 (REG_SZ) 项的 VSPackage 的包 GUID 名称。

2. 环境加载 VSPackage，对接口的 VSPackage 调用 ，然后使用 节中的数据调用 方法，以便 `QueryInterface` <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistSolutionProps> <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistSolutionProps.ReadSolutionProps%2A> VSPackage 可以存储数据。 环境对每个部分重复此过程 `preSolution` 。

3. 环境会访问项目持久性块。 在这种情况下，有一个项目。

   ```
   Project("{F184B08F-C81C-45F6-A57F-5ABD9991F28F}") = "Project1",
   "Project1.vbproj", "{8CDD8387-B905-44A8-B5D5-07BB50E05BEA}"
   EndProject
   ```

   此语句包含唯一项目 GUID 和项目类型 GUID。 环境使用此信息查找属于解决方案的项目文件或文件，以及每个项目所需的 VSPackage。 将项目 GUID 传递给 以加载与项目相关的特定 <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectFactory> VSPackage，然后 VSPackage 加载该项目。 在这种情况下，将加载此项目加载的 VSPackage Visual Basic。

   每个项目都可以保留唯一的项目实例 ID，以便解决方案中其他项目能够根据需要访问它。 理想情况下，如果解决方案和项目受源代码控制，则项目的路径应相对于解决方案的路径。 首次加载解决方案时，项目文件不能位于用户计算机上。 通过使项目文件相对于解决方案文件存储在服务器上，找到项目文件并复制到用户计算机相对简单。 然后，它复制并加载项目所需的其余文件。

4. 环境根据 .sln 文件的项目部分中包含的信息加载每个项目文件。 然后，项目本身负责填充项目层次结构并加载任何嵌套项目。

5. 处理 .sln 文件的所有部分后，解决方案将显示在解决方案资源管理器中，可供用户修改。

如果解决方案中实现项目的任何 VSPackage 无法加载，将调用 方法，并且解决方案中的所有其他项目有机会忽略它在加载过程中 <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistSolutionProps.OnProjectLoadFailure%2A> 可能所做的更改。 如果分析错误发生，解决方案文件会保留尽可能多的信息，并且环境会显示一个对话框，警告用户解决方案已损坏。

保存或关闭解决方案时，将调用 方法并传递给层次结构，以查看是否对需要输入 <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistSolutionProps.QuerySaveSolutionProps%2A> 到 .sln 文件中的解决方案进行了更改。 在 中传入的 null 值 `QuerySaveSolutionProps` <xref:Microsoft.VisualStudio.Shell.Interop.VSQUERYSAVESLNPROPS> 指示正在为解决方案保留信息。 如果值不为 null，则持久化信息适用于特定项目，由指向接口的指针 <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy> 确定。

如果有要保存的信息，则使用指向 方法 <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionPersistence> 的指针调用 <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistSolutionProps.SaveSolutionProps%2A> 接口。 然后，环境调用 方法，从接口检索名称/值对，然后将 <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistSolutionProps.WriteSolutionProps%2A> `IPropertyBag` 信息写入 .sln 文件。

`SaveSolutionProps` 环境以递归方法调用 和 对象，以检索从接口保存的信息，直到所有更改都输入 `WriteSolutionProps` `IPropertyBag` 到 .sln 文件中。 这样，就可以确保信息将随解决方案一起保留，并且下次打开解决方案时可用。

枚举每个加载的 VSPackage，以查看其是否具有要保存到 .sln 文件的内容。 仅在加载时查询注册表项。 环境知道所有已加载的包，因为它们在保存解决方案时位于内存中。

只有 .sln 文件包含 和 `preSolution` 节中 `postSolution` 的条目。 .suo 文件中没有类似的部分，因为解决方案需要此信息来正确加载。 .suo 文件包含用户特定的选项，例如私有便笺，这些选项不应共享或置于源代码控制下。

## <a name="see-also"></a>请参阅

- <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistSolutionProps>
- [解决方案用户选项 (.Suo) 文件](../../extensibility/internals/solution-user-options-dot-suo-file.md)
- [解决方案](../../extensibility/internals/solutions-overview.md)
