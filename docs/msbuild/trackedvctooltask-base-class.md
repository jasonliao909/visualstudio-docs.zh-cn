---
title: TrackedVCToolTask 类 |Microsoft Docs
description: 了解 TrackedVCToolTask 基类向继承自它的任务添加的参数。
ms.custom: SEO-VS-2020
ms.date: 03/10/2019
ms.topic: reference
dev_langs:
- VB
- CSharp
- C++
- jsharp
author: ghogen
ms.author: ghogen
ms.workload:
- multiple
ms.openlocfilehash: 01b55e0ad88cb520078479217306bac948e6cd60
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126640557"
---
# <a name="trackedvctooltask-base-class"></a>TrackedVCToolTask 基类

许多任务最终继承自 <xref:Microsoft.Build.Utilities.Task> 类和 [ToolTask](/dotnet/api/microsoft.build.utilities.tooltask) 类。 此类会向派生自 [VCToolTask](../msbuild/vctooltask-base-class.md) 的任务添加几个参数。 本文档中列出了这些参数。

## <a name="parameters"></a>参数

下表介绍了 TrackedVCToolTask 基类的参数。

|参数|说明|
|---------------|-----------------|
|**DeleteOutputOnExecute**|可选的 bool  参数。|
|**EnableExecuteTool**|可选的 bool  参数。|
|**ExcludedInputPaths**|可选的 **ITaskItem[]** 参数。|
|**MinimalRebuildFromTracking**|可选的 bool  参数。|
|**PathOverride**|可选的 string  参数。|
|**PostBuildTrackingCleanup**|可选的 bool  参数。|
|**RootSource**|可选的 string  参数。|
|**SkippedExecution**|可选的 bool 输出参数。|
|**SourcesCompiled**|可选的 **ITaskItem[]** 输出参数。|
|**TLogCommandFile**|可选的 ITaskItem 参数。|
|**TLogReadFiles**|可选的 **ITaskItem[]** 参数。|
|**TLogWriteFiles**|可选的 **ITaskItem[]** 参数。|
|**ToolArchitecture**|可选的 string  参数。|
|**TrackCommandLines**|可选的 bool  参数。|
|**TrackFileAccess**|可选的 bool  参数。|
|**TrackedInputFilesToIgnore**|可选的 **ITaskItem[]** 参数。|
|**TrackedOutputFilesToIgnore**|可选的 **ITaskItem[]** 参数。|
|**TrackerFrameworkPath**|可选的 string  参数。|
|**TrackerSdkPath**|可选的 string  参数。|

## <a name="see-also"></a>另请参阅

[任务参考](../msbuild/msbuild-task-reference.md)<br/>
[任务](../msbuild/msbuild-tasks.md)
