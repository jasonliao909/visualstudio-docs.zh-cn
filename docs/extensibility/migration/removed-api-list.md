---
title: 2022 Visual Studio预览版中删除的 API
description: 了解在 Visual Studio 2022 预览版中删除的 VS SDK API，供扩展作者更新其扩展以使用 Visual Studio 2022 预览版。
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
ms.openlocfilehash: 707002e3ec7038b15c7ef813b76e0d9691b264840b4134c701b2fbedbed51df1
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121447917"
---
# <a name="visual-studio-2022-sdk-removed-apis"></a>Visual Studio 2022 SDK 已删除 API

[!INCLUDE [preview-note](../includes/preview-note.md)]

以下 API 已从 Visual Studio SDK 中删除，无法再使用。请参阅每个部分，详细了解如何更新代码。

* [`IVsImageService`](#ivsimageservice)
* [`IBlockContextProvider`](#iblockcontextprovider)
* [`IToolTipProvider`](#itooltipprovider)
* [`IVsTextScanner` 和 `IVsFullTextScanner`](#ivstextscanner-and-ivsfulltextscanner)
* [异步解决方案加载和轻型解决方案加载](#asynchronous-solution-load-and-lightweight-solution-load)
* [`IVsDummy`](#ivsdummy)
* [`Microsoft.VisualStudio.Shell.Task`](#microsoftvisualstudioshelltask)
* [从源安全打开](#open-from-source-safe)
* 面向 .NET Framework 的新版 WPF XAML 设计器

## <a name="ivsimageservice"></a>IVsImageService

正在 `IVsImageService` 2022 Visual Studio中删除 。 的所有用户 `IVsImageService` 都应改为移动到 `IVsImageService2` 。

### <a name="recommended-updates"></a>建议的更新

如果使用 ， `IVsImageService` 请将对 方法的调用替换为对 上的等效方法的调用 `IVsImageService2` ：

| **IVsImageService 方法** | **等效的 IVsImageService2 方法** |
|----------------------------|----------------------------------------|
| 添加                        | AddCustomImage                         |
| 获取                        | GetImage                               |
| GetIconForFile             | GetImageMonikerForFile                 |
| GetIconForFileEx           | GetImageMonikerForFile                 |

`IVsImageService`的 Add 和 Get 方法按名称引用自定义图像 (字符串) ，而不是名字对象。  最好将代码切换为仅使用名字对象来引用自定义图像，但如果这证明不切实际，则有几个方法允许你将名称与名字对象 `IVsImageService2` 关联：

* `TryAssociateNameWithMoniker`
* `GetImageMonikerForName`

使用这两种方法，可以继续按名称引用图像。

## <a name="iblockcontextprovider"></a>IBlockContextProvider

和 `IBlockContextProvider` 相关类型在 2022 Visual Studio中删除。 的所有用户 `IBlockContextProvider` 都应改为移动到 `IStructureContextSourceProvider` 。

### <a name="recommended-updates"></a>建议的更新

的用户 `IBlockContextProvider` 应改为 `IStructureContextSourceProvider` 使用 ([文档) 。](/dotnet/api/microsoft.visualstudio.text.adornments.istructurecontextsourceprovider)

## <a name="itooltipprovider"></a>IToolTipProvider

和 `IToolTipProvider` 相关类型在 2022 Visual Studio中删除。 的所有用户 `IToolTipProvider` 都应改为移动到 `IToolTipService` 。

### <a name="recommended-updates"></a>建议的更新

的用户 `IToolTipProvider` 应改为 `IToolTipService` 使用 ([文档) 。](/dotnet/api/microsoft.visualstudio.text.adornments.itooltipservice)

## <a name="ivstextscanner-and-ivsfulltextscanner"></a>IVsTextScanner 和 IVsFullTextScanner

和 `IVsTextScanner` `IVsFullTextScanner` 在 2022 Visual Studio中删除。 或 的 `IVsTextScanner` 所有用户 `IVsFullTextScanner` 都应改为 `IVsTextLines` 移动到 。

### <a name="recommended-updates"></a>建议的更新

或 `IVsTextScanner` 的用户 `IVsFullTextScanner` 应 `IVsTextLines` 改为使用 ([文档) 。](/dotnet/apimicrosoft.visualstudio.textmanager.interop.ivstextlines.getlinetext)

## <a name="asynchronous-solution-load-and-lightweight-solution-load"></a>异步解决方案加载和轻型解决方案加载

Visual Studio 2022 (中删除异步解决方案加载 (ASL) 和轻型解决方案加载 (LSL) 功能，因此将删除以下方法：

### <a name="interfaces"></a>界面

* `IVsSolution4` - 方法 `IsBackgroundSolutionLoadEnabled` `EnsureProjectsAreLoaded` `EnsureProjectIsLoaded` ：、、、、 `EnsureSolutionIsLoaded`
* `IVsSolutionLoadEvents` - 方法 `OnBeforeBackgroundSolutionLoadBegins` `OnQueryBackgroundLoadProjectBatch` `OnBeforeLoadProjectBatch` ：、、、、 `OnAfterLoadProjectBatch`
* `IVsSolutionLoadManagerSupport` - 整个接口
* `IVsSolutionLoadManager` - 整个接口
* `IVsSccManager3`  - 整个接口
* `IVsAsynchronousProjectCreate` - 整个接口
* `IVsAsynchronousProjectCreateUI` - 整个接口

### <a name="enums-properties-and-ui-contexts"></a>枚举、属性和 UI 上下文

* `VSHPROPID_ProjectUnloadStatus` - 枚举： `UNLOADSTATUS_LoadPendingIfNeeded`
* `VSHPROPID_DemandLoadDependencies`
* `VSHPROPID_IsProjectProvisioned`
* `VSPROPID_IsInBackgroundIdleLoadProjectBatch`
* `VSPROPID_IsInSyncDemandLoadProjectBatch`
* `VSPROPID_ActiveSolutionLoadManager`
* `UICONTEXT_BackgroundProjectLoad`

### <a name="recommended-updates"></a>建议的更新

无。

## <a name="ivsdummy"></a>IVsDu以

`IVsDummy`将在 2022 Visual Studio中删除，并且不会替换。 

### <a name="recommended-updates"></a>建议的更新

无。 但是，它应没有任何影响，因为 API 未执行任何操作。

## <a name="microsoftvisualstudioshelltask"></a>Microsoft.VisualStudio.Shell.Task

`Microsoft.VisualStudio.Shell.Task`类已重命名为 `Microsoft.VisualStudio.Shell.TaskListItem` ，以便不与非常热门的 `System.Threading.Tasks.Task` 类冲突。

## <a name="open-from-source-safe"></a>从源安全打开

将删除对从源安全打开解决方案的支持，因此将删除以下方法、事件和常量。

## <a name="interfaces"></a>界面

* `IVsSCCProvider3` - 整个接口

### <a name="recommended-updates"></a>建议的更新

无。

## <a name="new-wpf-xaml-designer-for-net-framework"></a>面向 .NET Framework 的新版 WPF XAML 设计器

.NET Framework 的当前 WPF XAML 设计器 已弃用，并且将替换为适用于 .NET Framework 的新 WPF XAML 设计器，该体系结构与用于 .NET 的 WPF XAML 设计器 (.NET Core) 的体系结构相同。 这也意味着 WPF .NET Framework和 Microsoft 控制扩展性.design.dll模型。Windows。不再支持 Design.Extensibility。 适用于 XAML 设计器 的新 WPF .NET Framework 将提供与适用于 .NET (.NET Core) 的 WPF XAML 设计器相同的扩展性模型。 如果已创建 .NET .designtools.dll (.NET Core) 的 WPF 扩展，则同一扩展适用于适用于 .NET Framework 的新 WPF XAML 设计器。 请参阅下面的迁移链接，以进一步了解如何迁移到 WPF 平台的新扩展性模型 (.NET Framework以及 .NET Core) 和 UWP 平台。 

### <a name="recommended-updates"></a>建议的更新

请参阅 [XAML 设计器扩展性迁移](https://github.com/microsoft/xaml-designer-extensibility/blob/main/documents/xaml-designer-extensibility-migration.md)。
