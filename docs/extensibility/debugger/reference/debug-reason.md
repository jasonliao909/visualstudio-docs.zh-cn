---
description: 指定为调试启动进程的原因。
title: DEBUG_REASON |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- DEBUG_REASON
helpviewer_keywords:
- DEBUG_REASON enumeration
ms.assetid: ad2ee898-8648-4671-9078-d32873862346
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 9404e4b5cfdd1f1690b0fe76d0cd5e98cc90d2a4
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2021
ms.locfileid: "102170544"
---
# <a name="debug_reason"></a>DEBUG_REASON
指定为调试启动进程的原因。

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
发生了非特定的错误 (如果其他原因均不符合) ，则使用此值作为默认条件。

`DEBUG_REASON_USER_LAUNCHED`\
该进程是在用户请求时启动的。

`DEBUG_REASON_USER_ATTACHED`\
用户已将已运行的进程附加到。

`DEBUG_REASON_AUTO_ATTACHED`\
进程在启动时自动附加到。

`DEBUG_REASON_CAUSALITY`\
由于 *实时* (JIT) 调试事件，进程已启动。

## <a name="remarks"></a>备注
从 [GetDebugReason](../../../extensibility/debugger/reference/idebugprocess3-getdebugreason.md) 方法返回。

## <a name="requirements"></a>要求
标头： msdbg

命名空间： VisualStudio

程序集： Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>请参阅
- [枚举](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)
- [GetDebugReason](../../../extensibility/debugger/reference/idebugprocess3-getdebugreason.md)
