---
description: 检索当前处于活动状态的所有 TaskScheduler 对象的数组。
title: GetTaskSchedulersForDebugger 方法 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- GetTaskSchedulersForDebugger method, TaskScheduler class [.NET Framework debug engines]
ms.assetid: 58aa236a-5ab8-4695-b303-89dffdbcd946
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
ms.openlocfilehash: 04cc9a685554971e4e4065dba95bb1ac3118f56d470c82da474fe8349769c8dd
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121417790"
---
# <a name="gettaskschedulersfordebugger-method"></a>GetTaskSchedulersForDebugger 方法
检索 <xref:System.Threading.Tasks.TaskScheduler> 当前处于活动状态的所有对象的数组。

 **命名空间：** <xref:System.Threading.Tasks?displayProperty=fullName>

 **Assembly：** mscorlib (*mscorlib.dll*) 

 由于无法从 .NET Framework 访问此内部成员，因此在公共中间语言 (CIL) 中提供了以下语法。

## <a name="syntax"></a>语法

```csharp
.method assembly hidebysig static class System.Threading.Tasks.TaskScheduler[] GetTaskSchedulersForDebugger() cil managed
```

## <a name="return-value"></a>返回值
 <xref:System.Threading.Tasks.TaskScheduler>此中当前处于活动状态的所有对象的数组 <xref:System.AppDomain> 。

## <a name="remarks"></a>备注
 此方法不是线程安全的，不应同时与的其他实例一起使用 <xref:System.Threading.Tasks.TaskScheduler> 。 仅当调试器挂起了所有其他线程时，才从调试器调用此方法。

## <a name="see-also"></a>请参阅
- [TaskScheduler 类](../../extensibility/debugger/taskscheduler-class-internal-members.md)
