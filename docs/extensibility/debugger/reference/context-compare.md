---
description: 指定比较两个内存上下文的条件。
title: CONTEXT_COMPARE |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- CONTEXT_COMPARE
helpviewer_keywords:
- CONTEXT_COMPARE enumeration
ms.assetid: 701ed61c-a320-4c20-a335-0b840024abc0
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 49c8975a93d54d9138cbdcf510e7ee18d5bc55d2
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126664612"
---
# <a name="context_compare"></a>CONTEXT_COMPARE
指定比较两个内存上下文的条件。

## <a name="syntax"></a>语法

```cpp
enum enum_CONTEXT_COMPARE {
    CONTEXT_EQUAL                 = 0x0001,
    CONTEXT_LESS_THAN             = 0x0002,
    CONTEXT_GREATER_THAN          = 0x0003,
    CONTEXT_LESS_THAN_OR_EQUAL    = 0x0004,
    CONTEXT_GREATER_THAN_OR_EQUAL = 0x0005,
    CONTEXT_SAME_SCOPE            = 0x0006,
    CONTEXT_SAME_FUNCTION         = 0x0007,
    CONTEXT_SAME_MODULE           = 0x0008,
    CONTEXT_SAME_PROCESS          = 0x0009
};
typedef DWORD CONTEXT_COMPARE;
```

```csharp
public enum enum_CONTEXT_COMPARE {
    CONTEXT_EQUAL                 = 0x0001,
    CONTEXT_LESS_THAN             = 0x0002,
    CONTEXT_GREATER_THAN          = 0x0003,
    CONTEXT_LESS_THAN_OR_EQUAL    = 0x0004,
    CONTEXT_GREATER_THAN_OR_EQUAL = 0x0005,
    CONTEXT_SAME_SCOPE            = 0x0006,
    CONTEXT_SAME_FUNCTION         = 0x0007,
    CONTEXT_SAME_MODULE           = 0x0008,
    CONTEXT_SAME_PROCESS          = 0x0009
};
```

## <a name="fields"></a>字段
`CONTEXT_EQUAL`\
查找列表中与目标内存上下文相等的第一个内存上下文。

`CONTEXT_LESS_THAN`\
查找列表中小于目标内存上下文的第一个内存上下文。

`CONTEXT_GREATER_THAN`\
查找列表中大于目标内存上下文的第一个内存上下文。

`CONTEXT_LESS_THAN_OR_EQUAL`\
查找列表中小于或等于目标内存上下文的第一个内存上下文。

`CONTEXT_GREATER_THAN_OR_EQUAL`\
查找列表中大于或等于目标内存上下文的第一个内存上下文。

`CONTEXT_SAME_SCOPE`\
查找列表中与目标内存上下文位于同一作用域的第一个内存上下文。

`CONTEXT_SAME_FUNCTION`\
查找列表中与目标内存范围位于同一函数中的第一个内存上下文。

`CONTEXT_SAME_MODULE`\
查找列表中与目标内存上下文位于同一模块的第一个内存上下文。

`CONTEXT_SAME_PROCESS`\
查找列表中与目标内存上下文位于同一进程中的第一个内存上下文。

## <a name="remarks"></a>备注
作为参数传递给 [Compare](../../../extensibility/debugger/reference/idebugmemorycontext2-compare.md) 方法。

这些值用于查找列表中满足指定比较条件的第一个内存上下文。 为内存上下文提供一个内存上下文列表，以通过 方法与自身 `IDebugMemoryContext2::Compare` 进行比较。 然后返回列表中要返回比较运算符的第 `true` 一个内存上下文。

## <a name="requirements"></a>要求
标头：msdbg.h

命名空间：Microsoft.VisualStudio.Debugger.Interop

程序集：Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>请参阅
- [枚举](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)
- [比较](../../../extensibility/debugger/reference/idebugmemorycontext2-compare.md)
