---
description: 指定启动进程进行调试的原因。
title: DEBUG_REASON |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- DEBUG_REASON
helpviewer_keywords:
- DEBUG_REASON enumeration
ms.assetid: ad2ee898-8648-4671-9078-d32873862346
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 790dbcf8988af2751a8ce2eafda854797c89538ff3ca425b1bc11b9e53c9c795
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121378037"
---
# <a name="debug_reason"></a>DEBUG_REASON
指定启动进程进行调试的原因。

## <a name="syntax"></a>语法

```cpp
enum enum_DEBUG_REASON {
    DEBUG_REASON_ERROR         = 0,
    DEBUG_REASON_USER_LAUNCHED = 1,
    DEBUG_REASON_USER_ATTACHED = 2,
    DEBUG_REASON_AUTO_ATTACHED = 3,
    DEBUG_REASON_CAUSALITY     = 4
};
typedef DWORD DEBUG_REASON;
```

```csharp
public enum enum_DEBUG_REASON {
    DEBUG_REASON_ERROR         = 0,
    DEBUG_REASON_USER_LAUNCHED = 1,
    DEBUG_REASON_USER_ATTACHED = 2,
    DEBUG_REASON_AUTO_ATTACHED = 3,
    DEBUG_REASON_CAUSALITY     = 4
};
```

## <a name="fields"></a>字段
`DEBUG_REASON_ERROR`\
出现非特定错误 (当其他任何原因都不符合条件时，此错误用作默认) 。

`DEBUG_REASON_USER_LAUNCHED`\
进程是在用户请求时启动的。

`DEBUG_REASON_USER_ATTACHED`\
已运行的进程已由用户附加到 。

`DEBUG_REASON_AUTO_ATTACHED`\
进程在启动时自动附加到 。

`DEBUG_REASON_CAUSALITY`\
由于实时运行 JIT  (调试事件) 进程。

## <a name="remarks"></a>备注
从 [GetDebugReason 方法](../../../extensibility/debugger/reference/idebugprocess3-getdebugreason.md) 返回。

## <a name="requirements"></a>要求
标头：msdbg.h

命名空间：Microsoft.VisualStudio.Debugger.Interop

程序集：Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>请参阅
- [枚举](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)
- [GetDebugReason](../../../extensibility/debugger/reference/idebugprocess3-getdebugreason.md)
