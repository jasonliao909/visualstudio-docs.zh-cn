---
title: SetNotificationForWaitCompletion 方法 |Microsoft Docs
description: 了解调试器如何使用状态位来帮助跳出用于实现承诺样式的任务的异步方法主体。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- SetNotificationForWaitCompletion method, Task class [.NET Framework debug engines]
ms.assetid: da149c9a-20f4-4543-a29e-429c8c1d2e19
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 2418e958c027fea7fd39c93b0d5abbd95d64435b
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2021
ms.locfileid: "99960787"
---
# <a name="setnotificationforwaitcompletion-method"></a>SetNotificationForWaitCompletion 方法
设置或清除 TASK_STATE_WAIT_COMPLETION_NOTIFICATION 状态位。

 **命名空间：** <xref:System.Threading.Tasks?displayProperty=fullName>

 **Assembly：** mscorlib (*mscorlib.dll*) 

## <a name="syntax"></a>语法

```vb
internal void SetNotificationForWaitCompletion(bool enabled)
```

### <a name="parameters"></a>parameters
 `enabled`

 `true` 设置位;取消 `false` 设置此位。

## <a name="exceptions"></a>例外

## <a name="remarks"></a>备注
 调试器将此位设置为帮助跳出异步方法体。 如果 `enabled` 为 `true` ，则必须仅对尚未完成的任务调用此方法。 如果 `enabled` 为 `false` ，则可以对已完成的任务调用此方法。 在这两种情况下，它只应用于承诺样式任务。

## <a name="requirements"></a>要求

## <a name="see-also"></a>另请参阅
- [Task 类](../../extensibility/debugger/task-class-internal-members.md)
