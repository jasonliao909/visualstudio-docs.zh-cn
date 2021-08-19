---
description: 按比较标志所指示的方式，将内存上下文与给定数组中的每个上下文进行比较，并返回第一个匹配的上下文的索引。
title: IDebugMemoryContext2：： Compare |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugMemoryContext2::Compare
helpviewer_keywords:
- IDebugMemoryContext2::Compare method
- Compare method
ms.assetid: c51b5128-848e-4d8e-b2e9-1161339763c3
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 0b0e4e55872da333089d91eddd8edb54d7ce99f5
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122078903"
---
# <a name="idebugmemorycontext2compare"></a>IDebugMemoryContext2::Compare
按比较标志所指示的方式，将内存上下文与给定数组中的每个上下文进行比较，并返回第一个匹配的上下文的索引。

## <a name="syntax"></a>语法

```cpp
HRESULT Compare( 
   CONTEXT_COMPARE        compare,
   IDebugMemoryContext2** rgpMemoryContextSet,
   DWORD                  dwMemoryContextSetLen,
   DWORD*                 pdwMemoryContext
);
```

```csharp
int Compare(
   enum_CONTEXT_COMPARE   compare,
   IDebugMemoryContext2[] rgpMemoryContextSet,
   uint                   dwMemoryContextSetLen,
   out uint               pdwMemoryContext
);
```

## <a name="parameters"></a>参数
`compare`\
中 [CONTEXT_COMPARE](../../../extensibility/debugger/reference/context-compare.md) 枚举中的一个值，该值确定比较的类型。

`rgpMemoryContextSet`\
中对要比较的 [IDebugMemoryContext2](../../../extensibility/debugger/reference/idebugmemorycontext2.md) 对象的引用数组。

`dwMemoryContextSetLen`\
中数组中上下文的数目 `rgpMemoryContextSet` 。

`pdwMemoryContext`\
弄返回满足比较条件的第一个内存上下文的索引。

## <a name="return-value"></a>返回值
 如果成功， `S_OK` 则返回; 否则返回错误代码。 `E_COMPARE_CANNOT_COMPARE`如果无法比较两个上下文，则返回。

## <a name="remarks"></a>备注
 调试引擎 (DE) 不必支持所有类型的比较，但它必须至少支持 `CONTEXT_EQUAL` 、 `CONTEXT_LESS_THAN` `CONTEXT_GREATER_THAN` 和 `CONTEXT_SAME_SCOPE` 。

## <a name="see-also"></a>请参阅
- [IDebugMemoryContext2](../../../extensibility/debugger/reference/idebugmemorycontext2.md)
- [CONTEXT_COMPARE](../../../extensibility/debugger/reference/context-compare.md)
