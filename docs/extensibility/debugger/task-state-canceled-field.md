---
description: 任务在达到运行状态之前已取消，或者已确认其取消并完成，无异常。
title: TASK_STATE_CANCELED字段|Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- TASK_STATE_CANCELED field, Task class [.NET Framework debug engines]
ms.assetid: f4f5a96a-8230-493d-9696-8d2716bda261
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
ms.openlocfilehash: c6e20f40111f88ad304e5ce86cf4f60a8449418b7d83b6ae9879c6598f0c7f0a
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121338080"
---
# <a name="task_state_canceled-field"></a>TASK_STATE_CANCELED字段
任务在达到运行状态之前已取消，或者已确认其取消并完成，无异常。

 **命名空间：** <xref:System.Threading.Tasks?displayProperty=fullName>

 **程序集：mscorlib** (mscorlib.dll) 

 由于无法从 CIL 访问此内部成员.NET Framework，因此在 CIL (中提供了以下) 。

## <a name="syntax"></a>语法

```csharp
.field static assembly literal int32 TASK_STATE_CANCELED = int32(0x00800000)
```

## <a name="remarks"></a>备注
 如果m_stateFlags [包含](../../extensibility/debugger/m-stateflags-field.md) 此值，则 <xref:System.Threading.Tasks.Task.Status%2A> 属性返回 <xref:System.Threading.Tasks.TaskStatus?displayProperty=fullName> 。

## <a name="see-also"></a>请参阅
- [Task 类](../../extensibility/debugger/task-class-internal-members.md)
