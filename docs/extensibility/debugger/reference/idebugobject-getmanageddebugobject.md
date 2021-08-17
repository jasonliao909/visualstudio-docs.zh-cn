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
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 688e16b038959e0b1005afcab212687e80047d6e
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122078812"
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

## <a name="see-also"></a>请参阅
- [IDebugObject](../../../extensibility/debugger/reference/idebugobject.md)
- [IDebugManagedObject](../../../extensibility/debugger/reference/idebugmanagedobject.md)
