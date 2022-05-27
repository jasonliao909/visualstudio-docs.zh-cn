---
title: 解决方案 (.sln) 文件
description: 了解 .sln 文件，该文件是维护Visual Studio中项目的状态信息的文件之一。
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
ms.openlocfilehash: d82a274ae10a3cc95e275fbef8b88c54afd09967
ms.sourcegitcommit: 4264e57e45dede8bf55ddf0f7e81738a42580081
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/20/2022
ms.locfileid: "145183497"
---
# <a name="solution-sln-file"></a>解决方案 (.sln) 文件

 [!INCLUDE [Visual Studio](~/includes/applies-to-version/vs-windows-only.md)]

解决方案是用于组织Visual Studio中的项目的结构。 该解决方案维护两个文件中项目的状态信息：

- .sln 文件 (基于文本的共享) 

- .suo 文件 (二进制、特定于用户的解决方案选项) 

有关 .suo 文件的详细信息，请参阅 [解决方案用户选项 (。Suo) 文件](../../extensibility/internals/solution-user-options-dot-suo-file.md)。

如果 VSPackage 由于在 .sln 文件中被引用而加载，则环境会调用 <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistSolutionProps.ReadSolutionProps%2A> 在 .sln 文件中读取。

.sln 文件包含环境用于查找和加载持久化数据的名称值参数及其引用的项目 VSPackage 的基于文本的信息。 当用户打开解决方案时，环境会循环访问 `preSolution``Project``postSolution` .sln 文件中的信息，以加载解决方案、解决方案中的项目以及附加到解决方案的任何持久信息。

每个项目的文件都包含环境读取的其他信息，以使用该项目的项填充层次结构。 层次结构数据持久性由项目控制。 数据通常不存储在 .sln 文件中，尽管如果选择这样做，可以有意将项目信息写入 .sln 文件。 有关持久性的详细信息，请参阅[Project持久性](../../extensibility/internals/project-persistence.md)和[打开和保存Project项](../../extensibility/internals/opening-and-saving-project-items.md)。

## <a name="file-header"></a>文件标头

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
最近 () 保存此解决方案文件的Visual Studio的主要版本。 此信息控制解决方案图标中的版本号。

`VisualStudioVersion = 15.0.26730.15`\
最近 () 保存解决方案文件的Visual Studio的完整版本。 如果解决方案文件由具有相同主版本的较新版本Visual Studio保存，则此值不会更新，以免在解决方案文件中减少改动。

`MinimumVisualStudioVersion = 10.0.40219.1`\
可打开此解决方案文件的最旧) 版本的Visual Studio的最低 (。

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
最近 () 保存此解决方案文件的Visual Studio的主要版本。 此信息控制解决方案图标中的版本号。

`VisualStudioVersion = 16.0.28701.123`\
最近 () 保存解决方案文件的Visual Studio的完整版本。 如果解决方案文件由具有相同主版本的较新版本Visual Studio保存，则此值不会更新，以免减少文件中的改动。

`MinimumVisualStudioVersion = 10.0.40219.1`\
可打开此解决方案文件的最旧) 版本的Visual Studio的最低 (。

::: moniker-end

## <a name="file-body"></a>文件正文

.sln 文件的正文由多个分区 `GlobalSection`组成，如下所示：

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

1. 环境读取 .sln 文件的全局部分，并处理标记为 `preSolution`的所有节。 在此示例文件中，有一个这样的语句：

   ```
   GlobalSection(SolutionConfiguration) = preSolution
        ConfigName.0 = Debug
        ConfigName.1 = Release
   ```

   当环境读取 `GlobalSection('name')` 标记时，它会使用注册表将名称映射到 VSPackage。 密钥名称应存在于注册表中的 [HKLM\\<应用程序 ID 注册表根\>\SolutionPersistence\AggregateGUIDs]。 密钥的默认值是写入条目的 VSPackage 的包 GUID (REG_SZ) 。

2. 环境加载 VSPackage、对接口的 <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistSolutionProps> VSPackage 调用`QueryInterface`，并使用节中的数据调用<xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistSolutionProps.ReadSolutionProps%2A>方法，以便 VSPackage 可以存储数据。 环境对每个 `preSolution` 部分重复此过程。

3. 环境循环访问项目持久性块。 在这种情况下，有一个项目。

   ```
   Project("{F184B08F-C81C-45F6-A57F-5ABD9991F28F}") = "Project1",
   "Project1.vbproj", "{8CDD8387-B905-44A8-B5D5-07BB50E05BEA}"
   EndProject
   ```

   此语句包含唯一的项目 GUID 和项目类型 GUID。 环境使用此信息查找属于解决方案的项目文件或文件，以及每个项目所需的 VSPackage。 项目 GUID 传递给加载 <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectFactory> 与项目相关的特定 VSPackage，然后由 VSPackage 加载项目。 在这种情况下，为此项目加载的 VSPackage Visual Basic。

   每个项目都可以保留唯一的项目实例 ID，以便解决方案中的其他项目根据需要对其进行访问。 理想情况下，如果解决方案和项目位于源代码控制之下，则项目的路径应相对于解决方案的路径。 首次加载解决方案时，项目文件不能位于用户的计算机上。 通过将项目文件存储在相对于解决方案文件的服务器上，可以比较简单地找到项目文件并将其复制到用户的计算机上。 然后，它会复制并加载项目所需的其余文件。

4. 根据 .sln 文件的项目部分中包含的信息，环境将加载每个项目文件。 然后，项目本身负责填充项目层次结构并加载任何嵌套项目。

5. 处理 .sln 文件的所有部分后，解决方案会显示在解决方案资源管理器中，可供用户修改。

如果在解决方案中实现项目的任何 VSPackage 无法加载， <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistSolutionProps.OnProjectLoadFailure%2A> 则会调用该方法，并且解决方案中的每个其他项目都有机会忽略在加载期间可能所做的更改。 如果发生分析错误，则解决方案文件会保留尽可能多的信息，并且环境会显示一个对话框，警告用户解决方案已损坏。

保存或关闭解决方案时，将 <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistSolutionProps.QuerySaveSolutionProps%2A> 调用该方法并将其传递到层次结构，以查看是否已对需要输入到 .sln 文件中的解决方案进行更改。 传入的 `QuerySaveSolutionProps` <xref:Microsoft.VisualStudio.Shell.Interop.VSQUERYSAVESLNPROPS>null 值指示正在为解决方案保存信息。 如果该值不为 null，则持久化信息适用于由指向 <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy> 接口的指针确定的特定项目。

如果有要保存的信息，则会 <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionPersistence> 使用指向该方法的 <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistSolutionProps.SaveSolutionProps%2A> 指针调用接口。 <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistSolutionProps.WriteSolutionProps%2A>然后，环境调用该方法以从`IPropertyBag`接口检索名称值对，并将信息写入 .sln 文件。

`SaveSolutionProps` 环境 `WriteSolutionProps` 以递归方式调用对象，以检索要从 `IPropertyBag` 接口保存的信息，直到所有更改都输入到 .sln 文件中。 这样，便可以确保信息将随解决方案一起保存，并在下次打开解决方案时可用。

枚举每个加载的 VSPackage，以查看它是否有任何内容要保存到 .sln 文件。 仅在加载时查询注册表项。 环境知道所有已加载的包，因为它们在保存解决方案时处于内存中。

只有 .sln 文件包含节`preSolution``postSolution`中的条目。 .suo 文件中没有类似的部分，因为解决方案需要此信息才能正确加载。 .suo 文件包含用户特定的选项，例如专用笔记，这些选项不打算共享或放置在源代码控制下。

## <a name="see-also"></a>另请参阅

- <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistSolutionProps>
- [解决方案用户选项 (.Suo) 文件](../../extensibility/internals/solution-user-options-dot-suo-file.md)
- [解决方案](../../extensibility/internals/solutions-overview.md)
