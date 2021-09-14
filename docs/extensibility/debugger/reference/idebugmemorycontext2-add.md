---
description: 将指定的值添加到当前上下文，并返回新的上下文。
title: IDebugMemoryContext2：： Add |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugMemoryContext2::Add
helpviewer_keywords:
- IDebugMemoryContext2::Add method
- Add method
ms.assetid: 3c47e646-ce9e-4dd3-8f1a-6dbd3827d407
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 3d3926b151cc078dc879ebbe44ba3b902919bca3
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126600885"
---
# <a name="idebugmemorycontext2add"></a>IDebugMemoryContext2::Add
将指定的值添加到当前上下文，并返回新的上下文。

## <a name="syntax"></a>语法

```cpp
HRESULT Add( 
   UINT64                 dwCount,
   IDebugMemoryContext2** ppMemCxt
);
```

```csharp
int Add(
   ulong                    dwCount,
   out IDebugMemoryContext2 ppMemCxt
);
```

## <a name="parameters"></a>parameters
`dwCount`\
中要添加到当前上下文中的值。

`ppMemCxt`\
弄返回一个新的 [IDebugMemoryContext2](../../../extensibility/debugger/reference/idebugmemorycontext2.md) 对象。

## <a name="return-value"></a>返回值
 如果成功， `S_OK` 则返回; 否则返回错误代码。

## <a name="remarks"></a>备注
 内存上下文是一个地址，因此向地址添加值将产生一个新地址，该地址需要新的上下文接口。

 此方法必须始终生成新的上下文，即使生成的地址超出与此上下文关联的内存空间。 唯一的例外是，如果不能为新上下文分配任何内存，或者如果 `ppMemCxt` 是 null 值，则为 null 值 (这是) 错误。

## <a name="see-also"></a>另请参阅
- [IDebugMemoryContext2](../../../extensibility/debugger/reference/idebugmemorycontext2.md)
