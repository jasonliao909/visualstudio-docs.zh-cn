---
description: 检索当前处于活动状态的所有 System.Threading.Tasks.TaskScheduler 对象的数组。
title: GetTaskSchedulersForDebugger 方法|Microsoft Docs
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
ms.openlocfilehash: edcaa82677bf2b107c3a9dcc3f12ef9af05208be
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122153491"
---
# <a name="gettaskschedulersfordebugger-method"></a>GetTaskSchedulersForDebugger 方法
检索当前处于活动状态 <xref:System.Threading.Tasks.TaskScheduler> 的所有 对象的数组。

 **命名空间：** <xref:System.Threading.Tasks?displayProperty=fullName>

 **程序集：mscorlib** (*mscorlib.dll*) 

 由于无法从 CIL 访问此内部成员，因此.NET Framework CIL 语言中的公共中间语言 (语法) 。

## <a name="syntax"></a>语法

```csharp
.method assembly hidebysig static class System.Threading.Tasks.TaskScheduler[] GetTaskSchedulersForDebugger() cil managed
```

## <a name="return-value"></a>返回值
 此 中 <xref:System.Threading.Tasks.TaskScheduler> 当前处于活动状态的所有 对象的数组 <xref:System.AppDomain> 。

## <a name="remarks"></a>备注
 此方法不是线程安全的，不应同时与 的其他实例一起使用 <xref:System.Threading.Tasks.TaskScheduler> 。 仅在调试器挂起所有其他线程时，才从调试器调用此方法。

## <a name="see-also"></a>请参阅
- [TaskScheduler 类](../../extensibility/debugger/taskscheduler-class-internal-members.md)
