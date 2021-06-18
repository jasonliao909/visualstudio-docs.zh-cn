---
title: Visual Studio 2022 预览版中的重大 API 更改
description: 了解将扩展迁移到 Visual Studio 2022 Preview 时导致现有 VS 扩展无法编译的 API 更改。
ms.date: 06/08/2021
ms.topic: reference
author: leslierichardson95
ms.author: lerich
manager: jmartens
monikerRange: vs-2022
ms.workload:
- vssdk
ms.openlocfilehash: 9427b7a75ad53fc9a0795b249d96431113aba36d
ms.sourcegitcommit: 5fb4a67a8208707e79dc09601e8db70b16ba7192
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/17/2021
ms.locfileid: "112308557"
---
# <a name="breaking-api-changes-in-visual-studio-2022"></a>在 Visual Studio 2022 中中断 API 更改

[!INCLUDE [preview-note](../includes/preview-note.md)]

如果要将扩展迁移到 Visual Studio 2022，这里列出的重大更改可能会影响你。

## <a name="reference-assemblies-no-longer-installed"></a>不再安装引用程序集

许多程序集可能已引用从 Visual Studio 安装目录解析的 MSBuild。 应该使用 NuGet 来获取所需的 Visual Studio SDK ref 程序集。 有关执行此操作的详细步骤，请参阅 [现代化项目](update-visual-studio-extension.md#modernize-your-vsix-project) 。

## <a name="removed-apis"></a>删除的 Api

在 Visual Studio 2022 中，已在迁移 Visual Studio 的过程中删除了许多 Api。 可以在 [删除的 Api 列表](removed-api-list.md) 页上找到已删除 api 的列表。

## <a name="interop-breaking-changes"></a>互操作中断性变更

许多 Api 在 Visual Studio 2022 中发生了更改，通常使用简单的更改，可以方便地适应代码。

为了管理重大更改，我们计划为互操作程序集分配提供一种新机制。 具体而言，对于 Visual Studio 2022 和更高版本，我们会提供单个互操作程序集，其中包含许多常见公共 Visual Studio 接口的定义。 该程序集包含从多个互操作程序集移出的许多 Visual Studio 接口的托管定义。 新的互操作程序集通过 `Microsoft.VisualStudio.Interop` NuGet 包分发。

但是，Visual Studio 组件主要用于本机上下文并且具有较少的重大更改，这将继续具有自己的互操作程序集 (例如，调试器程序集仍将 VisualStudio.Debugger.Interop.dll，就像当前) 。 在任何情况下，都可以从应用程序中引用程序集，就像现在一样。

这是一项重大更改，这意味着使用此新方法的中的 Api 和程序集的扩展不与使用以前的互操作程序集的早期版本的 Visual Studio 兼容。

这具有几个非常重要的优点，使你可以更轻松地将扩展更新为 Visual Studio 2022：

- 任何损坏的 Api 将成为生成时错误，使其更易于查找和修复。
- 只需更新使用在 Visual Studio 2022 中已损坏的 API 的代码。
- 您将不会意外使用旧的、现在损坏的 API。

总体而言，这些更改将导致为所有用户提供更稳定的 Visual Studio 版本。 此方法的主要缺点是，如果不为每个目标 Visual Studio 版本编译代码一次，则托管程序集将不能在 Visual Studio 2019 和 Visual Studio 2022 中运行。

当你通过 Visual Studio 2019 和 Visual Studio 2022 之间的 API 差异来处理编译错误时，你可能会发现以下所列的 API 或模式，其中包含了有关如何解决该问题的指南。

### <a name="int-or-uint-where-intptr-is-expected"></a>`int` 或 `uint` `IntPtr` 应为何处

预计这会是一个非常常见的错误。 若要使 Visual Studio 2022 成为64位进程，必须修复其中一些互操作 Api，在这种情况下，它们假定在32位整数中使用指针大小的值。

示例错误：

> 参数3：无法从 "out uint" 转换为 "out system.exception"

只需将代码更新为 "预期" 或 "提供" 或 "或" 以 `IntPtr` `UIntPtr` `int` `uint` 解析中断。

示例修复：

```diff
-shell.LoadLibrary(myGuid, myFlags, out uint ptrLib);
+shell.LoadLibrary(myGuid, myFlags, out IntPtr ptrLib);
```

### <a name="an-interop-type-defined-in-two-assemblies"></a>在两个程序集中定义的互操作类型

当 c # 编译器报告在两个程序集中定义所使用的类型的错误时，您可能会从 SDK 的 Visual Studio 2019 版本中引用不应再引用的程序集。

示例错误：

> 错误 CS0433：类型 "IVsDpiAware" 同时存在于 "VisualStudio，Version = 17.0.0.0，Culture = 中立，PublicKeyToken = b03f5f7f11d50a3a" 和 "VisualStudio，Version = 16.0，Culture = 中立，PublicKeyToken = DesignTime" 中

请参阅我们的 [引用程序集重映射表](migrated-assemblies.md) ，以查看在 Visual Studio 2022 中哪个程序集名称是首选名称。
考虑上述示例错误中命名的两个程序集并查看此表，请注意， `Microsoft.VisualStudio.Interop` 是新的程序集名称。 然后，修复方法是从项目中删除对的引用 `Microsoft.VisualStudio.Shell.Interop.16.0.DesignTime` 。

在某些情况下，我们为包含类型转发器的不推荐使用的程序集提供了 Visual Studio 2022 版本的包。 如果可用，可以选择将包引用 *升级* 到 Visual Studio 2022 版本，而不是将其删除。 类型转发器将从编译器解析此错误。

请记住，有时这些引用可以通过可传递的包引用来实现，因此可能更难删除，而不是在项目文件中进行直接引用。 在这种情况下，请确保所有直接包引用均使用 Visual Studio 2022 SDK 包本身。 您可以参考 *project.assets.js* 来确定负责引入不推荐使用的程序集的包链。 将可传递包引用更新为 Visual Studio 2022 版本非常简单，只需将其安装为直接引用即可。

如果无法更改依赖关系树 (例如，因为它涉及第三方依赖项) ，你可以将直接包引用添加到预 Visual Studio 2022 包，并向 `ExcludeAssets="compile"` 该项目添加元数据 `PackageReference` 以解决编译器错误。 但请记住，使用此方法时，扩展可能会保留对 Visual Studio 2022 程序集的依赖关系，并且扩展在运行时可能会发生故障。

### <a name="missing-reference-to-an-interop-assembly"></a>缺少对互操作程序集的引用

当你引用为 Visual Studio 2022 SDK 预编译的程序集时，可能会收到有关缺少程序集引用的错误。

示例错误：

> 错误 CS0012 在未被引用的程序集中定义了类型 "IVsTextViewFilter"。 必须添加对程序集 "VisualStudio，Version = 7.1.40304.0，Culture = 中立，PublicKeyToken = b03f5f7f11d50a3a" 的引用

使用 [引用程序集重新映射表](migrated-assemblies.md)，你可以确认所请求的程序集实际上不是你应该引用的程序集。

最好的解决方法是将依赖项更新为针对 Visual Studio 2022 SDK 编译的版本，以便编译器不再请求已删除的互操作程序集。

在某些情况下，我们为包含类型转发器的不推荐使用的程序集提供了 Visual Studio 2022 版本的包。 当此功能可用时，您可以选择添加对过时包的 Visual Studio 2022 版本的包引用，使类型转发器可以从编译器解析错误。

### <a name="iasyncserviceprovider-is-missing"></a>`IAsyncServiceProvider` 缺少

此接口在两个命名空间中有两个定义。 其中只有一个用于托管使用。

Visual Studio 2019 命名空间 | Visual Studio 2022 命名空间 | 预期用途
--|--|--
VisualStudio. IAsyncServiceProvider | VisualStudio. IAsyncServiceProvider | 托管代码消耗
VisualStudio. IAsyncServiceProvider。 | VisualStudio. COMAsyncServiceProvider. IAsyncServiceProvider | 仅低级别互操作

如果出现有关的错误 `IAsyncServiceProvider` ， *可能* 是因为 (第二行) 使用的是本机代码。
如果是这样，则可以更新为新的命名空间，或切换到更易于管理的接口。

### <a name="dte-and-_dte-type-cast-failures"></a>`DTE` 和 `_DTE` 类型强制转换失败

`DTE` 和 `_DTE` 都是接口。 一个派生自另一个。 但是，在 Visual Studio 2022 中，基类型和派生类型是交换的。
这会使某些类型赋值或强制转换失败。

这也意味着使用的位置 `new DTE()` ，您现在必须使用 `new _DTE()` 。

### <a name="missing-argument-on-a-method-invocation"></a>方法调用中缺少参数

一些方法不再为互操作 API 中的可选参数声明默认参数。
如果收到有关 COM 互操作调用的缺少参数的错误，并且参数调用 `object` 类型，则 Visual Studio 2019 互操作 API 定义的以前的默认值可能已为 `""` ，因此，请考虑添加 `""` 作为参数以解决编译错误。

当不确定所用的默认参数时，请尝试将您的语言服务上下文从 Visual Studio 2022 切换到 Visual Studio 2019，以便您可以使用较旧的互操作程序集获取 Intellisense，以查看默认参数是什么，然后将其显式添加到您的代码中。 在针对 Visual Studio 2019 编译时，它将继续正常运行，但现在将针对 Visual Studio 2022 进行编译。

示例修复：

```diff
-process4.Attach2();
+process4.Attach2("");
```
