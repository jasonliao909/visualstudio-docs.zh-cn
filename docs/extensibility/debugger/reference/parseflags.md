---
description: 指定如何分析表达式。
title: PARS并AGS |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- PARSEFLAGS
helpviewer_keywords:
- PARSEFLAGS enumeration
ms.assetid: 47943f0a-54cb-4493-a62e-5dba97bd4c35
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: fd615c80c23ce3714208b7b09d1de8480698f52c
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122034690"
---
# <a name="parseflags"></a>PARSEFLAGS
指定如何分析表达式。

## <a name="syntax"></a>语法

```cpp
enum enum_PARSEFLAGS { 
   PARSE_EXPRESSION            = 0x0001,
   PARSE_FUNCTION_AS_ADDRESS   = 0x0002,
   PARSE_DESIGN_TIME_EXPR_EVAL = 0x1000
};
typedef DWORD PARSEFLAGS;
```

```csharp
public enum enum_PARSEFLAGS { 
   PARSE_EXPRESSION            = 0x0001,
   PARSE_FUNCTION_AS_ADDRESS   = 0x0002,
   PARSE_DESIGN_TIME_EXPR_EVAL = 0x1000
};
```

## <a name="fields"></a>字段
 `PARSE_EXPRESSION`\
 指示表达式不是 语句。

 `PARSE_FUNCTION_AS_ADDRESS`\
 指示表达式将按地址 (，) 计算结果。

 `PARSE_DESIGN_TIME_EXPR_EVAL`\
 指示在设计时分析表达式 (，即设计器打开时) 。

## <a name="remarks"></a>备注
 作为参数传递给 [ParseText](../../../extensibility/debugger/reference/idebugexpressioncontext2-parsetext.md) 和 [Parse](../../../extensibility/debugger/reference/idebugexpressionevaluator-parse.md) 方法。

## <a name="requirements"></a>要求
 标头：msdbg.h

 命名空间：Microsoft.VisualStudio.Debugger.Interop

 程序集：Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>请参阅
- [枚举](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)
- [ParseText](../../../extensibility/debugger/reference/idebugexpressioncontext2-parsetext.md)
- [Parse](../../../extensibility/debugger/reference/idebugexpressionevaluator-parse.md)
