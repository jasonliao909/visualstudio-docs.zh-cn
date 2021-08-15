---
title: 工作区中的Visual Studio |Microsoft Docs
description: 了解如何Visual Studio工作区来表示"打开文件夹"中的文件集合，包括工作区提供程序和服务。
ms.custom: SEO-VS-2020
ms.date: 02/21/2018
ms.topic: conceptual
author: vukelich
ms.author: svukel
manager: viveis
ms.workload:
- vssdk
ms.openlocfilehash: 95b2df98d3a06e4a2e2b667b8158c310a07d2c27dfe3bf33c9869ec5b138f45f
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121447592"
---
# <a name="workspaces"></a>工作区

工作区是指Visual Studio文件夹 的任何文件集合，它由 类型[](../ide/develop-code-in-visual-studio-without-projects-or-solutions.md) <xref:Microsoft.VisualStudio.Workspace.IWorkspace> 表示。 工作区本身不了解文件夹中与文件相关的内容或功能。 相反，它为功能和扩展提供了一组常规 API，以生成和使用其他人可以处理的数据。 生成者通过使用各种导出属性[Managed Extensibility Framework (](https://github.com/Microsoft/vs-mef/blob/master/doc/index.md) MEF) 组成。

## <a name="workspace-providers-and-services"></a>工作区提供程序和服务

工作区提供程序和服务提供数据和功能来响应工作区的内容。 它们可能会提供上下文文件信息、源文件中的符号或生成功能。

这两个 [概念都](https://en.wikipedia.org/wiki/Factory_method_pattern) 使用工厂模式，并通过工作区通过 MEF 导入。 所有导出属性都实现 或 ，但扩展应该将具体类型 `IProviderMetadataBase` `IWorkspaceServiceFactoryMetadata` 用于导出的类型。

提供程序和服务之间的一个区别在于它们与工作区的关系。 工作区可以具有许多特定类型的提供程序，但每个工作区只创建一个特定类型的服务。 例如，工作区有许多文件扫描程序提供程序，但每个工作区只有一个索引服务。

另一个关键区别是使用来自提供程序和服务的数据。 由于几个原因，工作区是从提供程序获取数据的入口点。 首先，提供程序通常有一些他们创建的窄数据集。 数据可能是 C# 源文件的符号，或者为 C# 源文件的 _生成CMakeLists.txt上下文_ 。 工作区将使用者的请求与元数据与请求一致的提供程序匹配。 其次，某些方案允许许多提供程序参与请求，而其他方案使用优先级最高的提供程序。

相比之下，扩展可以获取 的实例并直接与工作区服务交互。 上的扩展 `IWorkspace` 方法可用于由 Visual Studio提供的服务，例如 <xref:Microsoft.VisualStudio.Workspace.WorkspaceServiceHelper.GetFileWatcherService%2A> 。 扩展可能会为扩展中的组件或其他扩展使用提供工作区服务。 使用者应该 <xref:Microsoft.VisualStudio.Workspace.WorkspaceServiceHelper.GetServiceAsync%2A> 使用 或你在类型上提供的扩展 `IWorkspace` 方法。

>[!WARNING]
> 请勿创作与服务冲突Visual Studio。 这可能导致意外问题。

## <a name="disposal-on-workspace-closure"></a>工作区关闭时处置

关闭工作区时，扩展程序可能需要释放但调用异步代码。 <xref:Microsoft.VisualStudio.Threading.IAsyncDisposable>可以使用 接口轻松编写此代码。

## <a name="related-types"></a>相关类型

- <xref:Microsoft.VisualStudio.Workspace.IWorkspace> 是打开的工作区（如打开的文件夹）的中心实体。
- <xref:Microsoft.VisualStudio.Workspace.IWorkspaceProviderFactory`1> 为每个实例化工作区创建一个提供程序。
- <xref:Microsoft.VisualStudio.Workspace.IWorkspaceServiceFactory> 为每个实例化工作区创建一个服务。
- <xref:Microsoft.VisualStudio.Threading.IAsyncDisposable> 应在处置过程中需要运行异步代码的提供程序和服务上实现 。
- <xref:Microsoft.VisualStudio.Workspace.WorkspaceServiceHelper> 提供用于访问已知服务或任意服务的帮助程序方法。

## <a name="workspace-settings"></a>工作区设置

工作区具有 <xref:Microsoft.VisualStudio.Workspace.Settings.IWorkspaceSettingsManager> 对工作区的简单但功能强大的控制服务。 有关设置的基本概述，请参阅 [自定义生成和调试任务](../ide/customize-build-and-debug-tasks-in-visual-studio.md)。

设置类型的 `SettingsType` 类型是 _.json_ 文件，例如VSWorkspaceSettings.js _on_ 和 _tasks.vs.json。_

工作区设置功能围绕"范围"，这些范围只是工作区中的路径。 使用者调用 时，将聚合包含请求的路径和设置 <xref:Microsoft.VisualStudio.Workspace.Settings.IWorkspaceSettingsManager.GetAggregatedSettings%2A> 类型的所有作用域。 范围聚合优先级如下所示：

1. "本地设置"，通常是工作区根目录 `.vs` 。
1. 请求的路径本身。
1. 所请求路径的父目录。
1. 工作区根目录及包括工作区根目录的所有其他父目录。
1. "全局设置"，位于用户目录中。

结果是 的实例 <xref:Microsoft.VisualStudio.Workspace.Settings.IWorkspaceSettings> 。 此对象保存特定类型的设置，并可以查询其设置存储为 的键名称 `string` 。 <xref:Microsoft.VisualStudio.Workspace.Settings.IWorkspaceSettings.GetProperty%2A>方法和 <xref:Microsoft.VisualStudio.Workspace.Settings.WorkspaceSettingsExtensions> 扩展方法要求调用方知道所请求的设置值的类型。 由于大多数设置文件都保留为 _.json_ 文件，因此许多调用将使用 `string` 这些类型的 `bool` `int` 、、 和 数组。 还支持对象类型。 在这种情况下，可以使用自身 `IWorkspaceSettings` 作为类型参数。 例如：

```json
{
  "intValue": 1,
  "stringValue": "s",
  "boolValue": true,
  "stringArray": [
    "s1",
    "s2"
  ],
  "nestedIWorkspaceSettings": {
    "nestedString": "ns"
  }
}
```

假设这些设置位于用户对VSWorkspaceSettings.js _中，_ 则数据可以访问为：

```csharp
using System.Collections.Generic;
using Microsoft.VisualStudio.Workspace;
using Microsoft.VisualStudio.Workspace.Settings;

private static void ReadSettings(IWorkspace workspace)
{
    IWorkspaceSettingsManager settingsManager = workspace.GetSettingsManager();
    IWorkspaceSettings settings = settingsManager.GetAggregatedSettings(SettingsTypes.Generic);

    // result == WorkspaceSettingsResult.Success
    WorkspaceSettingsResult result = settings.GetProperty("intValue", out int intValue);
    result = settings.GetProperty("stringValue", out string stringValue);
    result = settings.GetProperty("boolValue", out bool boolValue);
    result = settings.GetProperty("stringArray", out string[] stringArray);
    result = settings.GetProperty("nestedIWorkspaceSettings", out IWorkspaceSettings nestedIWorkspaceSettings);
    result = nestedIWorkspaceSettings.GetProperty("nestedString", out string nestedString);

    // Extension method alternative using default values.
    int intValueOrDefault = settings.Property("intValue", /* default */ 42);

    // Missing key. result == WorkspaceSettingsResult.Undefined
    result = settings.GetProperty("missing", out string missing);

    // Wrong type for a key. result == WorkspaceSettingsResult.Error
    result = settings.GetProperty("intValue", out IWorkspaceSettings notSettings);

    // Special ability to union "stringArray" across all scopes.
    IEnumerable<string> allStringArray = settings.UnionPropertyArray<string>("stringArray");
}
```

>[!NOTE]
>这些设置 API 与 命名空间中提供的 `Microsoft.VisualStudio.Settings` API 无关。 工作区设置与主机无关，并且使用特定于工作区的设置文件或动态设置提供程序。

### <a name="providing-dynamic-settings"></a>提供动态设置

扩展可以提供 <xref:Microsoft.VisualStudio.Workspace.Settings.IWorkspaceSettingsProvider> 。 这些内存中提供程序允许扩展添加设置或替代其他设置。

导出 `IWorkspaceSettingsProvider` 不同于其他工作区提供程序。 工厂不为 `IWorkspaceProviderFactory` ，并且没有特殊属性类型。 请改为实现 <xref:Microsoft.VisualStudio.Workspace.Settings.IWorkspaceSettingsProviderFactory> 并使用 `[Export(typeof(IWorkspaceSettingsProviderFactory))]` 。

```csharp
// Common workspace provider factory pattern
[ExportFeatureProvider(some, args, to, export)]
internal class MyProviderFactory : IWorkspaceProviderFactory<IFeatureProvider>
{
     IFeatureProvider CreateProvider(IWorkspace workspace) => new Provider(workspace);
}

// IWorkspaceSettingsProvider pattern
[Export(typeof(IWorkspaceSettingsProviderFactory))]
internal class MySettingsProviderFactory : IWorkspaceSettingsProviderFactory
{
    // 100 is typically the value used by built-in settings providers. Lower value is higher priority.
    int Priority => 100;

    IWorkspaceSettingsProvider CreateSettingsProvider(IWorkspace workspace) => new MySettingsProvider(workspace);
}
```

>[!TIP]
>实现返回 (`IWorkspaceSettingsSource` 方法时 `IWorkspaceSettingsProvider.GetSingleSettings`) ，返回 的实例 `IWorkspaceSettings` 而不是 `IWorkspaceSettingsSource` 。 `IWorkspaceSettings` 提供了可在某些设置聚合过程中有用的详细信息。

### <a name="settings-related-apis"></a>设置相关的 API

- <xref:Microsoft.VisualStudio.Workspace.Settings.IWorkspaceSettingsManager> 读取和聚合工作区的设置。
- <xref:Microsoft.VisualStudio.Workspace.WorkspaceServiceHelper.GetSettingsManager%2A> 获取 `IWorkspaceSettingsManager` 工作区的 。
- <xref:Microsoft.VisualStudio.Workspace.Settings.IWorkspaceSettingsManager.GetAggregatedSettings%2A> 获取跨所有重叠范围聚合的给定范围的设置。
- <xref:Microsoft.VisualStudio.Workspace.Settings.IWorkspaceSettings> 包含特定范围的设置。

## <a name="workspace-suggested-practices"></a>工作区建议的做法

- 从或 `IWorkspaceProviderFactory.CreateProvider` 类似的 API 返回对象，这些 API 在创建 `Workspace` 时记住其上下文。 编写提供程序接口需要创建时保留此对象。
- 将特定于工作区的缓存或设置保存在工作区的"本地设置"路径中。 在 `Microsoft.VisualStudio.Workspace.WorkspaceHelper.MakeRootedUnderWorkingFolder` 2017 版本 15.6 Visual Studio使用 为文件创建路径。 对于版本 15.6 之前的版本，请使用以下代码片段：

```csharp
using System.IO;
using Microsoft.VisualStudio.Workspace;
using Microsoft.VisualStudio.Workspace.Settings;

private static string MakeRootedUnderWorkingFolder(IWorkspace workspace, string relativePath)
{
    string workingFolder = workspace.GetSettingsManager().GetAggregatedSettings(SettingsTypes.WorkspaceControlSettings).Property<string>("WorkingFolder");
    return Path.Combine(workingFolder, relativePath);
}
```

## <a name="solution-events-and-package-auto-load"></a>解决方案事件和包自动加载

加载的包可以实现 `IVsSolutionEvents7` 和调用 `IVsSolution.AdviseSolutionEvents` 。 它包括在打开和关闭文件夹中的文件夹时Visual Studio。

UI 上下文可用于自动加载包。 该值为 `4646B819-1AE0-4E79-97F4-8A8176FDD664`。

## <a name="troubleshooting"></a>故障排除

### <a name="the-sourceexplorerpackage-package-did-not-load-correctly"></a>SourceExplorerPackage 包未正确加载

工作区扩展性高度基于 MEF，组合错误将导致承载 Open Folder 的包无法加载。 例如，如果扩展使用 导出类型，但该类型仅实现 ，则尝试在 中打开文件夹 `ExportFileContextProviderAttribute` `IWorkspaceProviderFactory<IFileContextActionProvider>` 时Visual Studio。

::: moniker range="vs-2017"

可以在 _%LOCALAPPDATA%\Microsoft\VisualStudio\15.0_id\ComponentModelCache\Microsoft.VisualStudio.Default.err_ 中找到错误详细信息。 解决扩展实现的类型的任何错误。

::: moniker-end

::: moniker range=">=vs-2019"

可以在 _%LOCALAPPDATA%\Microsoft\VisualStudio\16.0_id\ComponentModelCache\Microsoft.VisualStudio.Default.err_ 中找到错误详细信息。 解决扩展实现的类型的任何错误。

::: moniker-end

## <a name="next-steps"></a>后续步骤

* [文件上下文](workspace-file-contexts.md) - 文件上下文提供程序为"打开文件夹"工作区提供代码智能。
* [索引](workspace-indexing.md) - 工作区索引收集并保存有关工作区的信息。
