---
title: Visual Studio 2022 预览版中的中断性 API 更改
description: 了解将扩展迁移到 2022 预览版时导致现有 VS 扩展无法Visual Studio的 API 更改。
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
ms.openlocfilehash: 2e206c6c87c8861f4f0e14bc6a5b7dc518010456
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122110249"
---
# <a name="breaking-api-changes-in-visual-studio-2022"></a>2022 年 Visual Studio 中的中断性 API 更改

[!INCLUDE [preview-note](../includes/preview-note.md)]

如果要将扩展迁移到 2022 Visual Studio，则此处列出的中断性变更可能会影响你。

## <a name="reference-assemblies-no-longer-installed"></a>不再安装引用程序集

你可能一直在引用的许多程序集MSBuild不再Visual Studio目录中解析的程序集。 应该使用 NuGet 获取Visual Studio SDK ref 程序集。 有关 [执行此操作的详细](update-visual-studio-extension.md#modernize-your-vsix-project) 步骤，请参阅现代化项目。

## <a name="removed-apis"></a>已删除的 API

在 Visual Studio 2022 年 1 月，许多 API 在继续迁移时Visual Studio一部分。 可在"已删除的 API 列表"页上找到已删除 [API](removed-api-list.md) 的列表。

## <a name="interop-breaking-changes"></a>互操作中断性变更

我们的许多 API 在 2022 Visual Studio发生了更改，通常只需进行简单的更改，代码就很容易适应。

为了管理中断性变更，我们计划为互操作程序集的分发提供新的机制。 具体而言，对于 Visual Studio 2022 及Visual Studio，我们提供一个互操作程序集，该程序集具有许多常见公共Visual Studio接口的定义。 该程序集包含许多接口的托管Visual Studio从多个互操作程序集移开。 新的互操作程序集通过 NuGet `Microsoft.VisualStudio.Interop` 分发。

但是，Visual Studio主要在本机上下文中使用且具有大量中断性变更的组件将继续具有其自己的互操作程序集 (例如，调试器程序集仍将是 VisualStudio.Debugger.Interop.dll，就像) 。 在任何情况下，都可以从应用程序引用程序集，就像现在一样。

这是一项重大更改，这意味着使用此新方法中和程序集中的 API 和程序集的扩展与旧版 Visual Studio使用以前的互操作程序集不兼容。

这具有一些非常重要的优势，可以更轻松地将扩展更新到 Visual Studio 2022：

- 任何损坏的 API 都将成为生成时间错误，使其更易于查找和修复。
- 只需更新使用 2022 年 1 月中断的 API Visual Studio代码。
- 你将无法意外使用旧的、现已损坏的 API。

从整体上来说，这些更改将为所有用户Visual Studio稳定版本。 此方法的主要缺点是，如果不针对每个目标 Visual Studio 版本编译代码一次，托管程序集将无法在 Visual Studio 2019 和 Visual Studio 2022 中运行。

处理由于 Visual Studio 2019 和 Visual Studio 2022 之间的 API 差异而出现编译错误时，你可能会发现下面列出的 API 或模式，并提供了有关如何修复该错误的指南。

### <a name="int-or-uint-where-intptr-is-expected"></a>`int`或 `uint` 应 `IntPtr`

我们预计这是一个很常见的错误。 若要Visual Studio 2022 年 64 位进程，必须修复某些互操作 API，其中假定指针可以容纳 32 位整数，才能实际使用指针大小的值。

示例错误：

> 参数 3：无法从"out uint"转换为"out System.IntPtr"

只需更新代码，以提供或 `IntPtr` `UIntPtr` 用于解决中断 `int` 的 `uint` 或 。

示例修复：

```diff
-shell.LoadLibrary(myGuid, myFlags, out uint ptrLib);
+shell.LoadLibrary(myGuid, myFlags, out IntPtr ptrLib);
```

### <a name="an-interop-type-defined-in-two-assemblies"></a>在两个程序集中定义的互操作类型

当 C# 编译器报告错误，指出你使用的类型在两个程序集中定义时，你可能正在引用 SDK Visual Studio 2019 版本中不应再引用的程序集。

示例错误：

> 错误 CS0433：类型"IVsDpiAware"存在于"Microsoft.VisualStudio.Interop" Version=17.0.0.0， Culture=neutral， PublicKeyToken=b03f5f7f11d50a3a' 和 'Microsoft.VisualStudio.Shell.Interop.16.0.DesignTime， Version=16.0.0.0， Culture=neutral， PublicKeyToken=b03f5f7f11d50a3a'

请参阅引用[程序集重新映射表](migrated-assemblies.md)，了解哪个程序集名称是 2022 年 1 月Visual Studio名称。
考虑到上述示例错误中命名的两个程序集，并查看此表，请注意 `Microsoft.VisualStudio.Interop` ，这是新的程序集名称。 然后，解决方法是从项目中删除 `Microsoft.VisualStudio.Shell.Interop.16.0.DesignTime` 对 的引用。

在某些情况下，我们为包含类型Visual Studio的已弃用程序集提供 2022 版本版本包。 如果可用，可以选择升级对 Visual Studio 2022 版本的包引用，而不是删除它。  类型转发器将解决编译器的错误。

请记住，有时这些引用可能通过可传递的包引用进行，因此比在项目文件中直接引用更难以删除。 在这种情况下，请确保所有直接包引用都使用 Visual Studio 2022 SDK 包本身。 可以参考 *project.assets.js* 来标识负责引入已弃用程序集的包链。 更新对 2022 Visual Studio的可传递包引用与直接引用一样简单。

例如，如果无法更改依赖关系树 (，因为它涉及第三方依赖项) ，可以将直接包引用添加到 Visual Studio 2022 之前包，并添加元数据到该项以解决 `ExcludeAssets="compile"` `PackageReference` 编译器错误。 但请记住，通过此方法，扩展可能会保留对 2022 Visual Studio的依赖项，并且扩展可能会在运行时发生故障。

### <a name="missing-reference-to-an-interop-assembly"></a>缺少对互操作程序集的引用

引用针对 2022 SDK Visual Studio的程序集时，可能会收到有关缺少程序集引用的错误。

示例错误：

> 错误 CS0012 类型"IVsTextViewFilter"在未引用的程序集中定义。 必须添加对程序集"Microsoft.VisualStudio.TextManager.Interop， Version=7.1.40304.0， Culture=neutral， PublicKeyToken=b03f5f7f11d50a3a" 的引用

使用 [引用程序集重新映射表](migrated-assemblies.md)，可以确认请求的程序集实际上不是必须引用的程序集。

最佳解决方法是，将依赖项更新为针对 Visual Studio 2022 SDK 编译的版本，以便编译器不再请求已删除的互操作程序集。

在某些情况下，我们为包含类型Visual Studio的已弃用程序集提供 2022 版本版本包。 如果可用，可以选择向已过时包的 Visual Studio 2022 版本添加包引用，以便类型转发器从编译器解决错误。

### <a name="iasyncserviceprovider-is-missing"></a>`IAsyncServiceProvider` 缺少

此接口有两个定义，在两个命名空间中。 其中只有一个旨在托管使用。

Visual Studio 2019 命名空间 | Visual Studio 2022 命名空间 | 预期用途
--|--|--
Microsoft.VisualStudio.Shell.IAsyncServiceProvider | Microsoft.VisualStudio.Shell.IAsyncServiceProvider | 托管代码消耗
Microsoft.VisualStudio.Shell.Interop.IAsyncServiceProvider | Microsoft.VisualStudio.Shell.COMAsyncServiceProvider.IAsyncServiceProvider | 仅低级别互操作

如果看到有关 的错误，可能是你使用了用于本机代码的代码， (第 `IAsyncServiceProvider` 二行) 。 
如果是这样，可以更新到新命名空间，或切换到更具托管友好性接口。

### <a name="dte-and-_dte-type-cast-failures"></a>`DTE``_DTE`和 类型强制转换失败

`DTE``_DTE`和 都是接口。 一个派生自另一个。 但在 Visual Studio 2022 中，将交换基类型和派生类型。
这会使某些类型分配或强制转换失败。

这也意味着，在以前使用 `new DTE()` 的地方，现在必须使用 `new _DTE()` 。

若要缓解大多数此类问题，请 `DTE2` 改为从 `EnvDTE80` 命名空间使用 。

### <a name="missing-argument-on-a-method-invocation"></a>方法调用中缺少参数

一些方法不再为互操作 API 中的可选参数声明默认参数。
如果收到有关 COM 互操作调用缺少参数的错误，并且参数调用了类型，则定义的 `object` Visual Studio 2019 互操作 API 以前的默认值可能是 ，因此请考虑添加 作为参数来解决编译 `""` `""` 错误。

如果对默认参数过去是什么有疑问，请尝试将语言服务上下文从 Visual Studio 2022 切换为 Visual Studio 2019，以便使用较旧的互操作程序集获取 Intellisense 以查看默认参数是什么，然后将它显式添加到代码中。 在针对 2019 年 1 月编译时，它将继续Visual Studio，但现在将在 2022 年 1 月Visual Studio编译。

示例修复：

```diff
-process4.Attach2();
+process4.Attach2("");
```
