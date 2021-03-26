---
description: 删除 IDE 为特定运行时体系结构或语言设置的异常列表。
title: IDebugEngine2：： RemoveAllSetExceptions |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugEngine2::RemoveAllSetExceptions
helpviewer_keywords:
- IDebugEngine2::RemoveAllSetExceptions
ms.assetid: 165fbe89-802d-4d99-85ca-c10fd6cccc09
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: b40da7391fc360b68da70f02f4d32afb92e83a58
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/25/2021
ms.locfileid: "105087933"
---
# <a name="idebugengine2removeallsetexceptions"></a>IDebugEngine2::RemoveAllSetExceptions
删除 IDE 为特定运行时体系结构或语言设置的异常列表。

## <a name="syntax"></a>语法

```cpp
HRESULT RemoveAllSetExceptions( 
   REFGUID guidType
);
```

```csharp
int RemoveAllSetExceptions( 
   ref Guid guidType
);
```

## <a name="parameters"></a>参数
`guidType`\
中语言的 GUID 或特定于运行时体系结构的调试引擎的 GUID。

## <a name="return-value"></a>返回值
 如果成功， `S_OK` 则返回; 否则返回错误代码。

## <a name="remarks"></a>备注
 此方法删除的异常由先前对 [SetException](../../../extensibility/debugger/reference/idebugengine2-setexception.md) 方法的调用设置。

 若要删除特定的异常，请调用 [RemoveSetException](../../../extensibility/debugger/reference/idebugengine2-removesetexception.md) 方法。

## <a name="see-also"></a>另请参阅
- [IDebugEngine2](../../../extensibility/debugger/reference/idebugengine2.md)
- [IDebugEngine2](../../../extensibility/debugger/reference/idebugengine2.md)
- [RemoveSetException](../../../extensibility/debugger/reference/idebugengine2-removesetexception.md)
