---
title: TaskScheduler 类-内部成员 |Microsoft Docs
description: 了解帮助您实现自定义调试器的 TaskScheduler 类的内部成员。
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
ms.technology: vs-ide-debug
ms.workload:
- vssdk
ms.openlocfilehash: 02897900a9117eee3d9a917b2e86580d21980345
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126600810"
---
# <a name="taskscheduler-class---internal-members"></a>TaskScheduler 类-内部成员
本文介绍 <xref:System.Threading.Tasks.TaskScheduler?displayProperty=fullName> 可帮助你实现自定义调试器的类的内部成员。 有关此类的常规信息，请参阅 <xref:System.Threading.Tasks.TaskScheduler> 参考文章。

 **命名空间：** <xref:System.Threading.Tasks?displayProperty=fullName>

 **Assembly：** mscorlib (*mscorlib.dll*) 

 由于不能从 .NET Framework 访问这些内部成员，因此在公共中间语言 (CIL) 中提供了以下语法。

## <a name="syntax"></a>语法

```csharp
.class public abstract auto ansi beforefieldinit System.Threading.Tasks.TaskScheduler
       extends System.Object
```

## <a name="members"></a>成员

### <a name="methods"></a>方法

|名称|说明|
|----------|-----------------|
|[GetScheduledTasksForDebugger](../../extensibility/debugger/getscheduledtasksfordebugger-method.md)|检索所有计划任务的数组。|
|[GetTaskSchedulersForDebugger](../../extensibility/debugger/gettaskschedulersfordebugger-method.md)|检索 <xref:System.Threading.Tasks.TaskScheduler> 当前处于活动状态的所有对象的数组。|

## <a name="remarks"></a>备注

## <a name="see-also"></a>另请参阅
- <xref:System.Threading.Tasks.TaskScheduler?displayProperty=fullName>
- [.NET Framework 的并行扩展内部机制](../../extensibility/debugger/parallel-extension-internals-for-the-dotnet-framework.md)
