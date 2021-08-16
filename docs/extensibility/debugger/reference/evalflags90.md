---
description: 枚举控制表达式计算的标志的有效值。
title: EVALFLAGS90 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- EVALFLAGS90 enumeration
ms.assetid: 64fb0139-8b04-4726-b52c-db2e04d65498
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: c935059fc7af18563cc203c5d79ee5887675d1663f94d2b06a99a2233bd89f8e
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121434342"
---
# <a name="evalflags90"></a>EVALFLAGS90
枚举控制表达式计算的标志的有效值。 此枚举扩展了 [EVALFLAGS](../../../extensibility/debugger/reference/evalflags.md) 枚举。

## <a name="syntax"></a>语法

```cpp
enum enum_EVALFLAGS90
{
    // VS 8.0 values
    EVAL90_RETURNVALUE                 = 0x0002,
    EVAL90_NOSIDEEFFECTS               = 0x0004,
    EVAL90_ALLOWBPS                    = 0x0008,
    EVAL90_ALLOWERRORREPORT            = 0x0010,
    EVAL90_FUNCTION_AS_ADDRESS         = 0x0040,
    EVAL90_NOFUNCEVAL                  = 0x0080,
    EVAL90_NOEVENTS                    = 0x1000,
    EVAL90_DESIGN_TIME_EXPR_EVAL       = 0x2000,
    EVAL90_ALLOW_IMPLICIT_VARS         = 0x4000,

    // Values added in VS 9.0
    EVAL90_FORCE_EVALUATION_NOW        = 0x8000
};
typedef DWORD EVALFLAGS90;
```

```csharp
public enum enum_EVALFLAGS90
{
    // VS 8.0 values
    EVAL90_RETURNVALUE                 = 0x0002,
    EVAL90_NOSIDEEFFECTS               = 0x0004,
    EVAL90_ALLOWBPS                    = 0x0008,
    EVAL90_ALLOWERRORREPORT            = 0x0010,
    EVAL90_FUNCTION_AS_ADDRESS         = 0x0040,
    EVAL90_NOFUNCEVAL                  = 0x0080,
    EVAL90_NOEVENTS                    = 0x1000,
    EVAL90_DESIGN_TIME_EXPR_EVAL       = 0x2000,
    EVAL90_ALLOW_IMPLICIT_VARS         = 0x4000,

    // Values added in VS 9.0
    EVAL90_FORCE_EVALUATION_NOW        = 0x8000
};
```

## <a name="fields"></a>字段
`EVAL90_RETURNVALUE`\
指定将计算返回值（如果有）。

`EVAL90_NOSIDEEFFECTS`\
指定不允许副作用。

`EVAL90_ALLOWBPS`\
指定在断点处停止。

`EVAL90_ALLOWERRORREPORT`\
指定将错误报告给允许的主机。 主要用于 Internet Explorer 中的脚本中的表达式计算。

`EVAL90_FUNCTION_AS_ADDRESS`\
强制将函数作为地址进行计算，而不是调用函数。

`EVAL90_NOFUNCEVAL`\
禁止计算函数。 例如，请考虑 `int` 表达式中的标记 `myExpression(int) + 10` 。 此函数可以正确地作为地址进行计算，但不能作为值来计算。

`EVAL90_NOEVENTS`\
一个标志，用于指示在表达式计算过程中发生的事件不应发送到会话调试管理器 (SDM) 或 IDE。

`EVAL90_DESIGN_TIME_EXPR_EVAL`\
启用设计时表达式计算。

`EVAL90_ALLOW_IMPLICIT_VARS`\
允许隐式变量创建。

`EVAL90_FORCE_EVALUATION_NOW`\
强制立即执行计算。 这在处理请求（如用户请求）时很有用。

## <a name="requirements"></a>要求
标头： Msdbg90

命名空间： VisualStudio

程序集： Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>请参阅
- [枚举](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)
