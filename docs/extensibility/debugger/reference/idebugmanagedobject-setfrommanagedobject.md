---
description: 从作为参数提供的值类的实例设置值类对象实例的值。
title: IDebugManagedObject：：SetFromManagedObject |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugManagedObject::SetFromManagedObject
helpviewer_keywords:
- IDebugManagedObject::SetFromManagedObject method
ms.assetid: 8700ee8d-2704-4580-bccc-046837a24edd
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 58b902732a0dcbfd30c7dd57b5c22a63fbc930ec
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126600897"
---
# <a name="idebugmanagedobjectsetfrommanagedobject"></a>IDebugManagedObject::SetFromManagedObject
从作为参数提供的值类的实例设置值类对象实例的值。

## <a name="syntax"></a>语法

```cpp
HRESULT SetFromManagedObject( 
   IUnknown* pManagedObject
);
```

```csharp
int SetFromManagedObject(
   object pManagedObject
);
```

## <a name="parameters"></a>parameters
`pManagedObject`\
[in]一个接口，表示包含新值的托管对象。

## <a name="return-value"></a>返回值
 如果成功，则返回S_OK;否则，返回错误代码。

## <a name="remarks"></a>备注
 此方法用于更改 [IDebugManagedObject](../../../extensibility/debugger/reference/idebugmanagedobject.md) 对象表示的托管对象。

## <a name="see-also"></a>另请参阅
- [IDebugManagedObject](../../../extensibility/debugger/reference/idebugmanagedobject.md)
