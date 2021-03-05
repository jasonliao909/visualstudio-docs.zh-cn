---
description: 从当前上下文中减去指定的值并返回一个新的上下文。
title: IDebugMemoryContext2：：减法 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugMemoryContext2::Subtract
helpviewer_keywords:
- Subtract method
- IDebugMemoryContext2::Subtract method
ms.assetid: 63df14c7-8d7e-47c1-afa7-5a1ab5d8eaba
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 7d77a0fcd4d791eefe98ae908bdf86ba49bec519
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2021
ms.locfileid: "102165002"
---
# <a name="idebugmemorycontext2subtract"></a>IDebugMemoryContext2::Subtract
从当前上下文中减去指定的值并返回一个新的上下文。

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
中要递减的内存字节数。

`ppMemCxt`\
弄返回一个新的 [IDebugMemoryContext2](../../../extensibility/debugger/reference/idebugmemorycontext2.md) 对象。

## <a name="return-value"></a>返回值
 如果成功， `S_OK` 则返回; 否则返回错误代码。

## <a name="remarks"></a>备注
 内存上下文是一个地址，因此，从地址中减去值将产生一个新地址，该地址需要新的上下文接口。

 此方法必须始终生成新的上下文，即使生成的地址超出与此上下文关联的内存空间。 唯一的例外是，如果不能为新上下文分配任何内存，或者如果 `ppMemCxt` 是 null 值，则为 null 值 (这是) 错误。

## <a name="see-also"></a>另请参阅
- [IDebugMemoryContext2](../../../extensibility/debugger/reference/idebugmemorycontext2.md)
