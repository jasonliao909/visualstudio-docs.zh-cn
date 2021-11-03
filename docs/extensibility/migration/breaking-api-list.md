---
title: Visual Studio 2022 RC 中的重大 API 更改
description: 了解在将扩展迁移到 Visual Studio 2022 RC 时导致现有 VS 扩展无法编译的 API 更改。
ms.date: 06/08/2021
ms.topic: reference
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
monikerRange: vs-2022
ms.workload:
- vssdk
feedback_system: GitHub
ms.openlocfilehash: 4e7d206ce21a173b9bce8a1e91f898165b6801f7
ms.sourcegitcommit: 7a820b7698a8dcf076eb36e3d766fb0751f56bb1
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/02/2021
ms.locfileid: "131126541"
---
# <a name="breaking-api-changes-in-visual-studio-2022"></a>Visual Studio 2022 中的重大 API 更改

[!INCLUDE [preview-note](../includes/preview-note.md)]

如果要将扩展迁移到 Visual Studio 2022，这里列出的重大更改可能会影响你。

## <a name="reference-assemblies-no-longer-installed"></a>不再安装引用程序集

您可能已引用 MSBuild 从 Visual Studio 安装目录中解决的许多程序集已被安装。 应使用 NuGet 获取所需的 Visual Studio SDK ref 程序集。 有关执行此操作的详细步骤，请参阅 [现代化项目](update-visual-studio-extension.md#modernize-your-vsix-project) 。

## <a name="removed-apis"></a>删除的 Api

在 Visual Studio 2022 中，已删除了许多 api，因为这是向前移动 Visual Studio 的一部分。 可以在 [删除的 Api 列表](removed-api-list.md) 页上找到已删除 api 的列表。

## <a name="interop-breaking-changes"></a>互操作中断性变更

许多 api 在 Visual Studio 2022 中发生了更改，通常使用简单的更改，可以方便地适应代码。

为了管理重大更改，我们计划为互操作程序集分配提供一种新机制。 具体而言，对于 Visual Studio 2022 和更高版本，我们会提供单个互操作程序集，其中包含许多常见公共 Visual Studio 接口的定义。 该程序集包含多个从多个互操作程序集移动的多个 Visual Studio 接口的托管定义。 新的互操作程序集通过 `Microsoft.VisualStudio.Interop` NuGet 包分发。

但是，Visual Studio 主要用于本机上下文并且具有较少重大更改的组件将继续具有其自己的互操作程序集 (例如，调试器程序集仍将 VisualStudio.Debugger.Interop.dll，与今天的) 相同。 在任何情况下，都可以从应用程序中引用程序集，就像现在一样。

这是一项重大更改，这意味着使用此新方法的中的 api 和程序集的扩展与使用以前的互操作程序集的 Visual Studio 的旧版本不兼容。

这具有几个非常重要的优点，将扩展更新 Visual Studio 2022 更简单：

- 任何损坏的 Api 将成为生成时错误，使其更易于查找和修复。
- 只需更新代码，该代码使用的 API 在 Visual Studio 2022 中已损坏。
- 您将不会意外使用旧的、现在损坏的 API。

总体而言，这些更改将导致为所有用户提供更稳定的 Visual Studio 版本。 此方法的主要缺点是，如果不为每个目标 Visual Studio 版本编译代码一次，则托管程序集将不能同时在 Visual Studio 2019 和 Visual Studio 2022 中运行。

当你在执行编译错误时，由于 Visual Studio 2019 和 Visual Studio 2022 之间的 api 差异，你可能会发现下面列出的 api 或模式包含如何修复此问题的指南。

### <a name="int-or-uint-where-intptr-is-expected"></a>`int` 或 `uint` `IntPtr` 应为何处

预计这会是一个非常常见的错误。 若要使 Visual Studio 2022 成为64位进程，必须修复其中的某些互操作 api，因为它们假定在32位整数中使用指针大小的值。

示例错误：

> 参数3：无法从 "out uint" 转换为 "out system.exception"

只需将代码更新为 "预期" 或 "提供" 或 "或" 以 `IntPtr` `UIntPtr` `int` `uint` 解析中断。

示例修复：

```diff
-shell.LoadLibrary(myGuid, myFlags, out uint ptrLib);
+shell.LoadLibrary(myGuid, myFlags, out IntPtr ptrLib);
```

### <a name="an-interop-type-defined-in-two-assemblies"></a>在两个程序集中定义的互操作类型

当 c # 编译器报告在两个程序集中定义你所使用的类型的错误时，可能是因为你不应再引用 SDK 的 Visual Studio 2019 版本的程序集。

示例错误：

> 错误 CS0433：类型 "IVsDpiAware" 同时存在于 "VisualStudio，Version = 17.0.0.0，Culture = 中立，PublicKeyToken = b03f5f7f11d50a3a" 和 "VisualStudio，Version = 16.0，Culture = 中立，PublicKeyToken = DesignTime" 中

请参阅我们的[引用程序集重映射表](migrated-assemblies.md)，以查看哪个程序集名称是 Visual Studio 2022 中的首选名称。
考虑上述示例错误中命名的两个程序集并查看此表，请注意， `Microsoft.VisualStudio.Interop` 是新的程序集名称。 然后，修复方法是从项目中删除对的引用 `Microsoft.VisualStudio.Shell.Interop.16.0.DesignTime` 。

在某些情况下，我们为包含类型转发器的不推荐使用的程序集提供了一个 Visual Studio 2022 版本的包。 当此功能可用时，可以选择将包引用 *升级* 到 Visual Studio 2022 版本，而不是将其删除。 类型转发器将从编译器解析此错误。

请记住，有时这些引用可以通过可传递的包引用来实现，因此可能更难删除，而不是在项目文件中进行直接引用。 在这种情况下，请确保所有直接包引用均使用 Visual Studio 2022 SDK 包本身。 您可以参考 " *项目"。 json* 来确定负责引入不推荐使用的程序集的包链。 将可传递包引用更新为 Visual Studio 2022 版本与将其安装为直接引用非常简单。

如果无法更改依赖关系树 (例如，因为它涉及第三方依赖项) ，你可以将直接包引用添加到预 Visual Studio 2022 包，并向 `ExcludeAssets="compile"` 该项目添加元数据 `PackageReference` 以解决编译器错误。 但请记住，使用此方法时，扩展可能会保留对预 Visual Studio 2022 程序集的依赖项，并且扩展在运行时可能会发生故障。

### <a name="missing-reference-to-an-interop-assembly"></a>缺少对互操作程序集的引用

当你引用针对预 Visual Studio 2022 SDK 编译的程序集时，可能会收到有关缺少程序集引用的错误。

示例错误：

> 错误 CS0012 在未被引用的程序集中定义了类型 "IVsTextViewFilter"。 必须添加对程序集 "VisualStudio，Version = 7.1.40304.0，Culture = 中立，PublicKeyToken = b03f5f7f11d50a3a" 的引用

使用 [引用程序集重新映射表](migrated-assemblies.md)，你可以确认所请求的程序集实际上不是你应该引用的程序集。

最好的解决方法是将依赖项更新为针对 Visual Studio 2022 SDK 编译的版本，以便编译器不再请求已删除的互操作程序集。

在某些情况下，我们为包含类型转发器的不推荐使用的程序集提供了一个 Visual Studio 2022 版本的包。 当此功能可用时，您可以选择添加对过时包的 Visual Studio 2022 版本的包引用，这样，类型转发器将从编译器解析此错误。

### <a name="iasyncserviceprovider-is-missing"></a>`IAsyncServiceProvider` 缺少

此接口在两个命名空间中有两个定义。 其中只有一个用于托管使用。

Visual Studio 2019 命名空间 | Visual Studio 2022 命名空间 | 预期用途
--|--|--
VisualStudio. IAsyncServiceProvider | VisualStudio. IAsyncServiceProvider | 托管代码消耗
VisualStudio. IAsyncServiceProvider。 | VisualStudio. COMAsyncServiceProvider. IAsyncServiceProvider | 仅低级别互操作

如果出现有关的错误 `IAsyncServiceProvider` ， *可能* 是因为 (第二行) 使用的是本机代码。
如果是这样，则可以更新为新的命名空间，或切换到更易于管理的接口。

### <a name="dte-and-_dte-type-cast-failures"></a>`DTE` 和 `_DTE` 类型强制转换失败

`DTE` 和 `_DTE` 都是接口。 一个派生自另一个。 但在 Visual Studio 2022 中，将交换基类型和派生类型。
这会使某些类型赋值或强制转换失败。

这也意味着使用的位置 `new DTE()` ，您现在必须使用 `new _DTE()` 。

若要缓解此问题，请改用 `DTE2` `EnvDTE80` 命名空间中的。

### <a name="missing-argument-on-a-method-invocation"></a>方法调用中缺少参数

一些方法不再为互操作 API 中的可选参数声明默认参数。
如果收到有关 COM 互操作调用的缺少参数的错误，并且参数调用 `object` 类型的默认值，则可能已定义 Visual Studio 2019 互操作 API 之前的默认值 `""` ，因此，请考虑添加 `""` 作为参数以解决编译错误。

当不确定所用的默认参数时，请尝试将语言服务上下文从 Visual Studio 2022 切换到 Visual Studio 2019，以便使用较旧的互操作程序集获取 Intellisense，以查看默认参数是什么，然后将其显式添加到代码中。 为 Visual Studio 2019 进行编译时，它将继续正常工作，但现在将针对 Visual Studio 2022 进行编译。

示例修复：

```diff
-process4.Attach2();
+process4.Attach2("");
```

### <a name="legacy-find-api-deprecation"></a>旧查找 API 弃用

作为我们努力在文件中查找的一项工作，我们在 VS 2022 中为 EnvDTE 接口的以下 Api 提供了不推荐使用的支持。

-   [EditPoint. FindPattern (String，Int32，EditPoint，TextRanges) ](https://docs.microsoft.com/dotnet/api/envdte.editpoint.findpattern?view=visualstudiosdk-2019)
-   [EditPoint. ReplacePattern (TextPoint，String，String，Int32，TextRanges) ](https://docs.microsoft.com/dotnet/api/envdte.editpoint.replacepattern?view=visualstudiosdk-2019)
-   [EditPoint. ReplaceText (Object，String，Int32) ](https://docs.microsoft.com/dotnet/api/envdte.editpoint.replacetext?view=visualstudiosdk-2019)
-   [TextSelection. FindText (String，Int32) ](https://docs.microsoft.com/dotnet/api/envdte.textselection.findtext?view=visualstudiosdk-2019#EnvDTE_TextSelection_FindText_System_String_System_Int32_)
-   [TextSelection. FindPattern (String，Int32，TextRanges) ](https://docs.microsoft.com/dotnet/api/envdte.textselection.findpattern?view=visualstudiosdk-2019)
-   [TextSelection. ReplaceText (String，String，Int32) ](https://docs.microsoft.com/dotnet/api/envdte.textselection.replacetext?view=visualstudiosdk-2019)
-   [TextSelection. ReplacePattern (String，String，Int32，TextRanges) ](https://docs.microsoft.com/dotnet/api/envdte.textselection.replacepattern?view=visualstudiosdk-2019)
-   [TextDocument. ReplacePattern (String，String，Int32，TextRanges) ](https://docs.microsoft.com/dotnet/api/envdte.textdocument.replacepattern?view=visualstudiosdk-2019)
-   [TextDocument. ReplaceText (String，String，Int32) ](https://docs.microsoft.com/dotnet/api/envdte.textdocument.replacetext?view=visualstudiosdk-2019)

在 VS 2022 和更高版本中，这些 Api 将不再工作。 本指南旨在 [ () VisualStudio 中使用 IFinder 接口 ](https://docs.microsoft.com/dotnet/api/microsoft.visualstudio.text.operations.ifinder?view=visualstudiosdk-2019) ，而不是在其上查找和替换方法。 可以通过 [IFindService 方法](https://docs.microsoft.com/dotnet/api/microsoft.visualstudio.text.operations.ifindservice.createfinderfactory?view=visualstudiosdk-2019)获取对实现 IFinder 接口的对象的访问权限。 可在此处找到将第三方扩展迁移到 Visual Studio 从较旧的 api 迁移到新式 IFinder api 的示例：将[Maid 扩展从 EnvDTE 查找并替换为新式 IFinder api](https://github.com/codecadwallader/codemaid/pull/847/commits/12e226a2ad6e9a4ccec4c3fda1a19db63eef6efd)
