---
description: 检索所有计划任务的数组。
title: GetScheduledTasksForDebugger 方法|Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- GetScheduledTasksForDebugger method, TaskScheduler class [.NET Framework debug engines]
ms.assetid: 7c9b4cde-6e4a-4cef-929f-7d02b1da5762
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 51da481edb636450770d0cff569b9ef411e17cf6
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2021
ms.locfileid: "112900949"
---
# <a name="getscheduledtasksfordebugger-method"></a>GetScheduledTasksForDebugger 方法
检索所有计划任务的数组。

 **命名空间：** <xref:System.Threading.Tasks?displayProperty=fullName>

 **程序集：mscorlib** (*mscorlib.dll*) 

 由于无法从 CIL 访问此内部成员，因此.NET Framework CIL 语言中的公共中间语言 (语法) 。

## <a name="syntax"></a>语法

```csharp
.method assembly hidebysig instance class System.Threading.Tasks.Task[] GetScheduledTasksForDebugger() cil managed
```

## <a name="return-value"></a>返回值
 所有计划任务的数组。 每个任务正在执行或已完成执行。

## <a name="remarks"></a>备注
 此方法不是线程安全的，不应同时与 的其他实例一起使用 <xref:System.Threading.Tasks.TaskScheduler> 。 仅在调试器挂起所有其他线程时，才从调试器调用此方法。

## <a name="see-also"></a>另请参阅
- [TaskScheduler 类](../../extensibility/debugger/taskscheduler-class-internal-members.md)
