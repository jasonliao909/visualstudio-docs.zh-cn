---
title: SetNotificationForWaitCompletion 方法|Microsoft Docs
description: 了解调试器如何使用状态位来帮助从异步方法主体中逐步执行承诺样式任务。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- SetNotificationForWaitCompletion method, Task class [.NET Framework debug engines]
ms.assetid: da149c9a-20f4-4543-a29e-429c8c1d2e19
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
ms.openlocfilehash: 88a0140ce27816592a7c43f1304f16638a2935b2
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126600831"
---
# <a name="setnotificationforwaitcompletion-method"></a>SetNotificationForWaitCompletion 方法
设置或清除TASK_STATE_WAIT_COMPLETION_NOTIFICATION位。

 **命名空间：** <xref:System.Threading.Tasks?displayProperty=fullName>

 **程序集：mscorlib** (*mscorlib.dll*) 

## <a name="syntax"></a>语法

```vb
internal void SetNotificationForWaitCompletion(bool enabled)
```

### <a name="parameters"></a>parameters
 `enabled`

 `true` 若要设置位，为 ; `false` 若要取消设置位，为 。

## <a name="exceptions"></a>例外

## <a name="remarks"></a>备注
 调试器设置此位以帮助逐步退出异步方法主体。 如果 `enabled` `true` 为 ，则只能对尚未完成的任务调用此方法。 当 `enabled` 为 `false` 时，可以在已完成的任务上调用此方法。 在任一事件中，它应仅用于承诺样式的任务。

## <a name="requirements"></a>要求

## <a name="see-also"></a>另请参阅
- [Task 类](../../extensibility/debugger/task-class-internal-members.md)
