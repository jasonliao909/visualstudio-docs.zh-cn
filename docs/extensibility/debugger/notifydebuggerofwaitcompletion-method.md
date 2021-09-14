---
title: NotifyDebuggerOfWaitCompletion 方法|Microsoft Docs
description: 了解 NotifyDebuggerOfWaitCompletion 方法，该方法是调试器用作断点目标的占位符。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- NotifyDebuggerOfWaitCompletion method, Task class [.NET Framework debug engines]
ms.assetid: 841c5908-4f3f-400b-a7b0-96a95f362817
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
ms.openlocfilehash: f4ba75017e277f12c6d3727ddc3d14a7dfd3483a
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126664860"
---
# <a name="notifydebuggerofwaitcompletion-method"></a>NotifyDebuggerOfWaitCompletion 方法
调试器用作断点目标的占位符方法。 此方法不得是内向或优化的。

 **命名空间：** <xref:System.Threading.Tasks?displayProperty=fullName>

 **程序集：mscorlib** (*mscorlib.dll*) 

## <a name="syntax"></a>语法

```vb
private void NotifyDebuggerOfWaitCompletion()
```

## <a name="remarks"></a>备注
 如果设置了任务的调试器通知位，则具有任务的所有联接操作都应调用此方法。

## <a name="requirements"></a>要求

## <a name="see-also"></a>另请参阅
- [Task 类](../../extensibility/debugger/task-class-internal-members.md)
