---
title: TaskScheduler 类 - 内部成员|Microsoft Docs
description: 了解 System.Threading.Tasks.TaskScheduler 类的内部成员，这些成员可帮助你实现自定义调试器。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- TaskScheduler class [.NET Framework debug engines]
- debug engines, TaskScheduler class [.NET Framework]
ms.assetid: 87f1c969-0217-4464-8907-7609c1bf61d3
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 58b370a6742387f7493e4c6357cffd05f2bd88a5
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2021
ms.locfileid: "112900143"
---
# <a name="taskscheduler-class---internal-members"></a>TaskScheduler 类 - 内部成员
本文介绍 类的内部成员 <xref:System.Threading.Tasks.TaskScheduler?displayProperty=fullName> ，这些成员可帮助你实现自定义调试器。 有关此类的一般信息，请参阅 <xref:System.Threading.Tasks.TaskScheduler> 参考文章。

 **命名空间：** <xref:System.Threading.Tasks?displayProperty=fullName>

 **程序集：mscorlib** (*mscorlib.dll*) 

 由于无法从 CIL 访问这些内部成员.NET Framework，因此在 CIL (中提供了以下) 。

## <a name="syntax"></a>语法

```csharp
.class public abstract auto ansi beforefieldinit System.Threading.Tasks.TaskScheduler
       extends System.Object
```

## <a name="members"></a>成员

### <a name="methods"></a>方法

|名称|描述|
|----------|-----------------|
|[GetScheduledTasksForDebugger](../../extensibility/debugger/getscheduledtasksfordebugger-method.md)|检索所有计划任务的数组。|
|[GetTaskSchedulersForDebugger](../../extensibility/debugger/gettaskschedulersfordebugger-method.md)|检索当前处于活动状态 <xref:System.Threading.Tasks.TaskScheduler> 的所有 对象的数组。|

## <a name="remarks"></a>备注

## <a name="see-also"></a>另请参阅
- <xref:System.Threading.Tasks.TaskScheduler?displayProperty=fullName>
- [并行扩展插件的内部.NET Framework](../../extensibility/debugger/parallel-extension-internals-for-the-dotnet-framework.md)
