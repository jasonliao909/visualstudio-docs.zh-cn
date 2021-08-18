---
description: 从当前上下文减去指定值并返回新上下文。
title: IDebugMemoryContext2：：Subtract |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugMemoryContext2::Subtract
helpviewer_keywords:
- Subtract method
- IDebugMemoryContext2::Subtract method
ms.assetid: 63df14c7-8d7e-47c1-afa7-5a1ab5d8eaba
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: b25e58fed406863009b72220fad4ba04b0d3b1e0
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122118666"
---
# <a name="idebugmemorycontext2subtract"></a>IDebugMemoryContext2::Subtract
从当前上下文减去指定值并返回新上下文。

## <a name="syntax"></a>语法

```cpp
HRESULT Subtract( 
   UINT64                 dwCount,
   IDebugMemoryContext2** ppMemCxt
);
```

```csharp
int Subtract(
   ulong                    dwCount,
   out IDebugMemoryContext2 ppMemCxt
);
```

## <a name="parameters"></a>参数
`dwCount`\
[in]要减量的内存字节数。

`ppMemCxt`\
[out]返回新的 [IDebugMemoryContext2](../../../extensibility/debugger/reference/idebugmemorycontext2.md) 对象。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK` ;否则返回错误代码。

## <a name="remarks"></a>备注
 内存上下文是一个地址，因此从地址中减去值会生成需要新上下文接口的新地址。

 此方法必须始终生成新上下文，即使生成的地址位于与此上下文关联的内存空间之外。 唯一的例外是，无法为新上下文分配内存，或者 如果 为 null 值， (`ppMemCxt` 错误) 。

## <a name="see-also"></a>请参阅
- [IDebugMemoryContext2](../../../extensibility/debugger/reference/idebugmemorycontext2.md)
