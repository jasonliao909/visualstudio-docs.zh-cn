---
description: 在调试引擎的地址空间中创建托管对象的副本。
title: IDebugObject：：GetManagedDebugObject |Microsoft Docs
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
ms.openlocfilehash: a3aa4089a22988bc6a64ca8928dfd7a2b24e300438337ee8646634a4d34b2ae4
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121307253"
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
[out]返回表示 [新创建的托管对象的 IDebugManagedObject](../../../extensibility/debugger/reference/idebugmanagedobject.md) 对象。

## <a name="return-value"></a>返回值
 如果成功，则返回S_OK;否则，返回错误代码。 如果E_FAIL [IDebugObject](../../../extensibility/debugger/reference/idebugobject.md) 不表示托管值类实例，则返回值。

## <a name="remarks"></a>备注
 此 [IDebugObject](../../../extensibility/debugger/reference/idebugobject.md) 对象必须表示托管值类实例，例如 `System.Decimal` 实例。 通过具有本地副本，消除了调用 Evaluate [的](../../../extensibility/debugger/reference/idebugfunctionobject-evaluate.md) 开销。

## <a name="see-also"></a>另请参阅
- [IDebugObject](../../../extensibility/debugger/reference/idebugobject.md)
- [IDebugManagedObject](../../../extensibility/debugger/reference/idebugmanagedobject.md)
