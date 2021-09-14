---
title: Visual Studio 2022 预览版中删除的 api
description: 了解 Visual Studio 2022 预览版中删除的 VS SDK api，适用于扩展创作者更新其扩展以使用 Visual Studio 2022 preview。
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
ms.openlocfilehash: 4501fdb465452eff1623e39c50e8c97f3bb5ca5b
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126665309"
---
# <a name="visual-studio-2022-sdk-removed-apis"></a>Visual Studio 2022 SDK 已删除 api

[!INCLUDE [preview-note](../includes/preview-note.md)]

以下 api 已从 Visual Studio SDK 中删除，不能再使用，有关如何更新代码的详细信息，请参阅每个部分。

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

正在 `IVsImageService` Visual Studio 2022 中移除。 `IVsImageService`应改为转到的所有用户 `IVsImageService2` 。

### <a name="recommended-updates"></a>建议的更新

如果使用，则将对 `IVsImageService` 其方法的调用替换为对的等效方法的调用 `IVsImageService2` ：

| **IVsImageService 方法** | **等效的 IVsImageService2 方法** |
|----------------------------|----------------------------------------|
| 添加                        | AddCustomImage                         |
| 获取                        | GetImage                               |
| GetIconForFile             | GetImageMonikerForFile                 |
| GetIconForFileEx           | GetImageMonikerForFile                 |

`IVsImageService`通过名称引用自定义图像的 Add 和 Get 方法 (字符串) 而不是名字对象。  更可取的方法是将代码切换为仅使用名字对象来引用自定义映像，但如果这种证明不切实际，则 `IVsImageService2` 有几种方法可以使名称与名字对象关联：

* `TryAssociateNameWithMoniker`
* `GetImageMonikerForName`

使用这两种方法，你可以继续按名称引用映像。

## <a name="iblockcontextprovider"></a>IBlockContextProvider

`IBlockContextProvider`在 Visual Studio 2022 中将删除和相关类型。 `IBlockContextProvider`应改为转到的所有用户 `IStructureContextSourceProvider` 。

### <a name="recommended-updates"></a>建议的更新

的用户 `IBlockContextProvider` 应该改用 `IStructureContextSourceProvider` ([文档](/dotnet/api/microsoft.visualstudio.text.adornments.istructurecontextsourceprovider)) 。

## <a name="itooltipprovider"></a>IToolTipProvider

`IToolTipProvider`在 Visual Studio 2022 中将删除和相关类型。 `IToolTipProvider`应改为转到的所有用户 `IToolTipService` 。

### <a name="recommended-updates"></a>建议的更新

的用户 `IToolTipProvider` 应该改用 `IToolTipService` ([文档](/dotnet/api/microsoft.visualstudio.text.adornments.itooltipservice)) 。

## <a name="ivstextscanner-and-ivsfulltextscanner"></a>IVsTextScanner 和 IVsFullTextScanner

`IVsTextScanner` `IVsFullTextScanner` Visual Studio 2022 中将删除和。 或的所有 `IVsTextScanner` 用户 `IVsFullTextScanner` 应改为转到 `IVsTextLines` 。

### <a name="recommended-updates"></a>建议的更新

或的 `IVsTextScanner` 用户 `IVsFullTextScanner` 应该改用 `IVsTextLines` ([文档](/dotnet/apimicrosoft.visualstudio.textmanager.interop.ivstextlines.getlinetext)) 。

## <a name="asynchronous-solution-load-and-lightweight-solution-load"></a>异步解决方案加载和轻型解决方案加载

Visual Studio 2022 中将删除异步解决方案加载 (ASL) 和轻型解决方案加载 (LSL) 功能，因为这样做会删除以下方法：

### <a name="interfaces"></a>接口

* `IVsSolution4` -方法： `IsBackgroundSolutionLoadEnabled` 、 `EnsureProjectsAreLoaded` 、 `EnsureProjectIsLoaded` 、 `EnsureSolutionIsLoaded`
* `IVsSolutionLoadEvents` -方法： `OnBeforeBackgroundSolutionLoadBegins` 、 `OnQueryBackgroundLoadProjectBatch` 、 `OnBeforeLoadProjectBatch` 、 `OnAfterLoadProjectBatch`
* `IVsSolutionLoadManagerSupport` -整个接口
* `IVsSolutionLoadManager` -整个接口
* `IVsSccManager3`  -整个接口
* `IVsAsynchronousProjectCreate` -整个接口
* `IVsAsynchronousProjectCreateUI` -整个接口

### <a name="enums-properties-and-ui-contexts"></a>枚举、属性和 UI 上下文

* `VSHPROPID_ProjectUnloadStatus` 枚举 `UNLOADSTATUS_LoadPendingIfNeeded`
* `VSHPROPID_DemandLoadDependencies`
* `VSHPROPID_IsProjectProvisioned`
* `VSPROPID_IsInBackgroundIdleLoadProjectBatch`
* `VSPROPID_IsInSyncDemandLoadProjectBatch`
* `VSPROPID_ActiveSolutionLoadManager`
* `UICONTEXT_BackgroundProjectLoad`

### <a name="recommended-updates"></a>建议的更新

无。

## <a name="ivsdummy"></a>IVsDummy

正在 `IVsDummy` Visual Studio 2022 中删除，不会将其替换。 

### <a name="recommended-updates"></a>建议的更新

无。 但是，这不会产生任何影响，因为 API 未执行任何操作。

## <a name="microsoftvisualstudioshelltask"></a>VisualStudio。

`Microsoft.VisualStudio.Shell.Task`类已重命名为， `Microsoft.VisualStudio.Shell.TaskListItem` 因此不会与非常流行的类冲突 `System.Threading.Tasks.Task` 。

## <a name="open-from-source-safe"></a>从源安全打开

正在删除对从 "源安全" 打开解决方案的支持，如以下方法、事件、和等。

## <a name="interfaces"></a>接口

* `IVsSCCProvider3` -整个接口

### <a name="recommended-updates"></a>建议的更新

无。

## <a name="new-wpf-xaml-designer-for-net-framework"></a>面向 .NET Framework 的新版 WPF XAML 设计器

已弃用 .NET Framework 的当前 wpf XAML 设计器，并将根据用于 .net 的 wpf XAML 设计器 ( .net Core) 的相同体系结构替换为新的 wpf XAML 设计器 .NET Framework。 这也意味着 WPF .NET Framework 基于 design.dll 和 Microsoft 的扩展性模型。Windows。设计：不再支持扩展性。 .NET Framework 的新 wpf XAML 设计器将为 .net ( .net Core) 提供与 WPF XAML 设计器相同的扩展性模型。 如果已为 .NET ( .NET Core) 创建了. designtools.dll 扩展，则该相同扩展将适用于 .NET Framework 的新 WPF XAML 设计器。 请参阅下面的迁移链接，了解有关如何迁移到 WPF 平台的新扩展性模型的详细信息 (.NET Framework 和 .net Core) 和 UWP 平台向后移动。 

### <a name="recommended-updates"></a>建议的更新

请参阅 [XAML 设计器扩展性迁移](https://github.com/microsoft/xaml-designer-extensibility/blob/main/documents/xaml-designer-extensibility-migration.md)。
