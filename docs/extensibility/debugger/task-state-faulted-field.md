---
description: 由于未处理异常的原因而完成的任务。
title: TASK_STATE_FAULTED字段|Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- TASK_STATE_FAULTED field, Task class [.NET Framework debug engines]
ms.assetid: ced826ae-09a9-4acf-af00-a2343d396bb8
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
ms.openlocfilehash: 7a603ace4218acfeb412fc50389c8484cdcdb3a6ce79eacb347e9c8957590a53
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121432938"
---
# <a name="task_state_faulted-field"></a>TASK_STATE_FAULTED字段
由于未处理异常的原因而完成的任务。

 **命名空间：** <xref:System.Threading.Tasks?displayProperty=fullName>

 **程序集：mscorlib** (*mscorlib.dll*) 

 由于无法从 CIL 访问此内部成员，因此.NET Framework CIL 语言中的公共中间语言 (语法) 。

## <a name="syntax"></a>语法

```csharp
.field static assembly literal int32 TASK_STATE_FAULTED = int32(0x00400000)
```

## <a name="remarks"></a>备注
 如果m_stateFlags [字段](../../extensibility/debugger/m-stateflags-field.md) 包含此值，则 <xref:System.Threading.Tasks.Task.Status%2A> 属性返回 <xref:System.Threading.Tasks.TaskStatus?displayProperty=fullName> 。

## <a name="see-also"></a>请参阅
- [Task 类](../../extensibility/debugger/task-class-internal-members.md)
