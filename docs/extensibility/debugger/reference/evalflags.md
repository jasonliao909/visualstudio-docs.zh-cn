---
description: 指定控制表达式计算的标志。
title: EVALFLAGS |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- EVALFLAGS
helpviewer_keywords:
- EVALFLAGS enumeration
ms.assetid: 7b2cb14a-511a-4fef-9e4f-308139719fba
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 00b025ac3d14ee9c2d6bd767ff45c28222c71009ffe6702e183ffe705e3eaf31
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121390289"
---
# <a name="evalflags"></a>EVALFLAGS
指定控制表达式计算的标志。

## <a name="syntax"></a>语法

```cpp
enum enum_EVALFLAGS {
    EVAL_RETURNVALUE = 0x0002,
    EVAL_NOSIDEEFFECTS = 0x0004,
    EVAL_ALLOWBPS = 0x0008,
    EVAL_ALLOWERRORREPORT = 0x0010,
    EVAL_FUNCTION_AS_ADDRESS = 0x0040,
    EVAL_NOFUNCEVAL = 0x0080,
    EVAL_NOEVENTS = 0x1000
};
typedef DWORD EVALFLAGS;
```

```csharp
public enum enum_EVALFLAGS {
    EVAL_RETURNVALUE = 0x0002,
    EVAL_NOSIDEEFFECTS = 0x0004,
    EVAL_ALLOWBPS = 0x0008,
    EVAL_ALLOWERRORREPORT = 0x0010,
    EVAL_FUNCTION_AS_ADDRESS = 0x0040,
    EVAL_NOFUNCEVAL = 0x0080,
    EVAL_NOEVENTS = 0x1000
}
```

## <a name="fields"></a>字段
`EVAL_RETURNVALUE`\
指定将计算返回值（如果有）。

`EVAL_NOSIDEEFFECTS`\
指定不允许副作用。

`EVAL_ALLOWBPS`\
指定在断点处停止。

`EVAL_ALLOWERRORREPORT`\
指定将错误报告给允许的主机。 主要用于 Internet Explorer 中的脚本中的表达式计算。

`EVAL_FUNCTION_AS_ADDRESS`\
强制将函数作为地址进行计算，而不是调用函数。

`EVAL_NOFUNCEVAL`\
禁止计算函数。 例如，请考虑 `int` 表达式中的标记 `myExpression(int) + 10` 。 此函数可以正确地作为地址进行计算，但不能作为值来计算。

`EVAL_NOEVENTS`\
一个标志，用于指示在表达式计算过程中发生的事件不应发送到会话调试管理器 (SDM) 或 IDE。

## <a name="remarks"></a>备注
这些标志作为参数传递给 [EvaluateAsync](../../../extensibility/debugger/reference/idebugexpression2-evaluateasync.md) 和 [EvaluateSync](../../../extensibility/debugger/reference/idebugexpression2-evaluatesync.md) 方法。

这些标志可以与按位 "或" 组合在一起。

## <a name="requirements"></a>要求
标头： msdbg

命名空间： VisualStudio

程序集： Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>请参阅
- [枚举](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)
- [EvaluateAsync](../../../extensibility/debugger/reference/idebugexpression2-evaluateasync.md)
- [EvaluateSync](../../../extensibility/debugger/reference/idebugexpression2-evaluatesync.md)
