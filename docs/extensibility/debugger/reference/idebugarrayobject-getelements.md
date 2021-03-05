---
description: 获取数组的所有元素的枚举器。
title: IDebugArrayObject：： GetElements |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugArrayObject::GetElements
helpviewer_keywords:
- IDebugArrayObject::GetElements method
ms.assetid: f6a6262f-5183-46ce-8a45-33ef46088b98
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 33840f3f5d5a65cf1ed929049f0b85801724a5c9
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2021
ms.locfileid: "102158548"
---
# <a name="idebugarrayobjectgetelements"></a>IDebugArrayObject::GetElements
获取数组的所有元素的枚举器。

## <a name="syntax"></a>语法

```cpp
HRESULT GetElements( 
   IEnumDebugObjects** ppEnum
);
```

```csharp
int GetElements(
   out IEnumDebugObjects ppEnum
);
```

## <a name="parameters"></a>参数
`ppEnum`\
弄返回一个 [IEnumDebugObjects](../../../extensibility/debugger/reference/ienumdebugobjects.md) 对象，该对象允许枚举所有元素。

## <a name="return-value"></a>返回值
 如果成功，将返回 S_OK;否则，将返回错误代码。

## <a name="remarks"></a>备注
 作为替代方法，使用 [GetCount](../../../extensibility/debugger/reference/idebugarrayobject-getcount.md) 和 [GetElement](../../../extensibility/debugger/reference/idebugarrayobject-getelement.md) 方法循环访问元素。

## <a name="see-also"></a>另请参阅
- [IDebugArrayObject](../../../extensibility/debugger/reference/idebugarrayobject.md)
