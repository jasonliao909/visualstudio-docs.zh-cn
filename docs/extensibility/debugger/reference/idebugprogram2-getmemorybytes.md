---
description: 检索程序占用的内存字节数。
title: IDebugProgram2：： GetMemoryBytes |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProgram2::GetMemoryBytes
helpviewer_keywords:
- IDebugProgram2::GetMemoryBytes
ms.assetid: 1cdedb47-caf8-468e-aaf4-163f16afb403
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: e63d25807e6a434066c7fc3bb860e9657faadf15
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2021
ms.locfileid: "102165990"
---
# <a name="idebugprogram2getmemorybytes"></a>IDebugProgram2::GetMemoryBytes
检索程序占用的内存字节数。

## <a name="syntax"></a>语法

```cpp
HRESULT GetMemoryBytes( 
   IDebugMemoryBytes2** ppMemoryBytes
);
```

```csharp
int GetMemoryBytes( 
   out IDebugMemoryBytes2 ppMemoryBytes
);
```

## <a name="parameters"></a>参数
`ppMemoryBytes`\
弄返回一个 [IDebugMemoryBytes2](../../../extensibility/debugger/reference/idebugmemorybytes2.md) 对象，该对象表示程序的内存字节。

## <a name="return-value"></a>返回值
 如果成功， `S_OK` 则返回; 否则返回错误代码。

## <a name="remarks"></a>备注
 [IDebugMemoryBytes2](../../../extensibility/debugger/reference/idebugmemorybytes2.md)对象所表示的内存字节用于内存中程序的映像，而不是在执行程序时分配的任何内存。

## <a name="see-also"></a>另请参阅
- [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)
- [IDebugMemoryBytes2](../../../extensibility/debugger/reference/idebugmemorybytes2.md)
