---
description: 任务在达到 "正在运行" 状态之前已被取消，或已确认取消并完成，但未发生异常。
title: TASK_STATE_CANCELED 字段 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- TASK_STATE_CANCELED field, Task class [.NET Framework debug engines]
ms.assetid: f4f5a96a-8230-493d-9696-8d2716bda261
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: e02bd5c81fea58e49eca0909d53d2fe68269b72d
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/25/2021
ms.locfileid: "105079262"
---
# <a name="task_state_canceled-field"></a>TASK_STATE_CANCELED 字段
任务在达到 "正在运行" 状态之前已被取消，或已确认取消并完成，但未发生异常。

 **命名空间：** <xref:System.Threading.Tasks?displayProperty=fullName>

 **Assembly：** mscorlib (mscorlib.dll) 

 由于无法从 .NET Framework 访问此内部成员，因此在公共中间语言 (CIL) 中提供了以下语法。

## <a name="syntax"></a>语法

```csharp
.field static assembly literal int32 TASK_STATE_CANCELED = int32(0x00800000)
```

## <a name="remarks"></a>备注
 如果 [m_stateFlags](../../extensibility/debugger/m-stateflags-field.md) 字段包含此值，则 <xref:System.Threading.Tasks.Task.Status%2A> 属性将返回 <xref:System.Threading.Tasks.TaskStatus?displayProperty=fullName> 。

## <a name="see-also"></a>另请参阅
- [Task 类](../../extensibility/debugger/task-class-internal-members.md)
