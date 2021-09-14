---
description: 返回线程枚举中的下一组元素。
title: IEnumDebugThreads2：：Next |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IEnumDebugThreads2::Next
helpviewer_keywords:
- IEnumDebugThreads2::Next
ms.assetid: bcffd954-3c67-4867-96f3-041ddb3e34d4
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 08ee68932b0bff150f57debb05a5e3b2c866d5d9
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126602594"
---
# <a name="ienumdebugthreads2next"></a>IEnumDebugThreads2::Next
返回 枚举中的下一组元素。

## <a name="syntax"></a>语法

```cpp
HRESULT Next(
   ULONG           celt,
   IDebugThread2** rgelt,
   ULONG*          pceltFetched
);
```

```csharp
int Next(
   uint            celt,
   IDebugThread2[] rgelt,
   ref uint        pceltFetched
);
```

## <a name="parameters"></a>parameters
`celt`\
[in]要检索的元素数。 还指定数组的最大 `rgelt` 大小。

`rgelt`\
[in， out]要填充 [的 IDebugThread2](../../../extensibility/debugger/reference/idebugthread2.md) 元素的数组。

`pceltFetched`\
[out]返回 中实际返回的元素数 `rgelt` 。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK`。 如果可能返回的元素数少于请求的元素数，则返回 `S_FALSE` ;否则返回错误代码。

## <a name="see-also"></a>另请参阅
- [IEnumDebugThreads2](../../../extensibility/debugger/reference/ienumdebugthreads2.md)
- [IDebugThread2](../../../extensibility/debugger/reference/idebugthread2.md)
