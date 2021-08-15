---
description: 按比较标志指示的方式将内存上下文与给定数组中的每个上下文进行比较，并返回匹配的第一个上下文的索引。
title: IDebugMemoryContext2：：Compare |Microsoft Docs
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
ms.openlocfilehash: dbf7260bfa0119bf4ffe4ba9ea06c1a59e76fdbaa83d54a3696fdf9d3e34c894
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121342162"
---
# <a name="idebugmemorycontext2compare"></a>IDebugMemoryContext2::Compare
按比较标志指示的方式将内存上下文与给定数组中的每个上下文进行比较，并返回匹配的第一个上下文的索引。

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
[in]一个来自 [CONTEXT_COMPARE](../../../extensibility/debugger/reference/context-compare.md) 值，该值确定比较的类型。

`rgpMemoryContextSet`\
[in]对要比较的 [IDebugMemoryContext2](../../../extensibility/debugger/reference/idebugmemorycontext2.md) 对象的引用数组。

`dwMemoryContextSetLen`\
[in]数组中的上下文 `rgpMemoryContextSet` 数。

`pdwMemoryContext`\
[out]返回满足比较的第一个内存上下文的索引。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK` ;否则返回错误代码。 如果 `E_COMPARE_CANNOT_COMPARE` 无法比较这两个上下文，则返回 。

## <a name="remarks"></a>备注
 调试引擎 (DE) 不一定要支持所有类型的比较，但它必须至少支持 `CONTEXT_EQUAL` 、 `CONTEXT_LESS_THAN` 和 `CONTEXT_GREATER_THAN` `CONTEXT_SAME_SCOPE` 。

## <a name="see-also"></a>另请参阅
- [IDebugMemoryContext2](../../../extensibility/debugger/reference/idebugmemorycontext2.md)
- [CONTEXT_COMPARE](../../../extensibility/debugger/reference/context-compare.md)
