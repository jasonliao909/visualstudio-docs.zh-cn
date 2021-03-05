---
description: 在调试引擎的地址空间中创建托管对象的副本。
title: IDebugObject：： GetManagedDebugObject |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugObject::GetManagedDebugObject
helpviewer_keywords:
- IDebugObject::GetManagedDebugObject method
ms.assetid: cb89692e-7657-47ff-846d-311943521951
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 87956b3630f9d152ecdda7754623e7257cf0a01a
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2021
ms.locfileid: "102164756"
---
# <a name="idebugobjectgetmanageddebugobject"></a>IDebugObject::GetManagedDebugObject
在调试引擎的地址空间中创建托管对象的副本。

## <a name="syntax"></a>语法

```cpp
HRESULT GetManagedDebugObject( 
   IDebugManagedObject** ppObject
);
```

```csharp
int GetManagedDebugObject(
   out IDebugManagedObject ppObject
);
```

## <a name="parameters"></a>参数
`ppObject`\
弄返回表示新创建的托管对象的 [IDebugManagedObject](../../../extensibility/debugger/reference/idebugmanagedobject.md) 对象。

## <a name="return-value"></a>返回值
 如果成功，将返回 S_OK;否则，将返回错误代码。 如果此 [IDebugObject](../../../extensibility/debugger/reference/idebugobject.md) 不表示托管值类实例，则返回 E_FAIL。

## <a name="remarks"></a>备注
 此 [IDebugObject](../../../extensibility/debugger/reference/idebugobject.md) 对象必须表示托管值类实例，如 `System.Decimal` 实例。 通过使用本地副本，可消除调用 [计算](../../../extensibility/debugger/reference/idebugfunctionobject-evaluate.md) 的开销。

## <a name="see-also"></a>另请参阅
- [IDebugObject](../../../extensibility/debugger/reference/idebugobject.md)
- [IDebugManagedObject](../../../extensibility/debugger/reference/idebugmanagedobject.md)
