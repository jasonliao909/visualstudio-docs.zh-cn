---
description: 获取数组的所有元素的枚举数。
title: IDebugArrayObject：：GetElements |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugArrayObject::GetElements
helpviewer_keywords:
- IDebugArrayObject::GetElements method
ms.assetid: f6a6262f-5183-46ce-8a45-33ef46088b98
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 72f3ec74ccb8eae959f3a12b9233bb329c0f72c3
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126600942"
---
# <a name="idebugarrayobjectgetelements"></a>IDebugArrayObject::GetElements
获取数组的所有元素的枚举数。

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

## <a name="parameters"></a>parameters
`ppEnum`\
[out]返回一个 [IEnumDebugObjects](../../../extensibility/debugger/reference/ienumdebugobjects.md) 对象，该对象允许枚举所有元素。

## <a name="return-value"></a>返回值
 如果成功，则返回S_OK;否则，返回错误代码。

## <a name="remarks"></a>备注
 或者，使用 [GetCount](../../../extensibility/debugger/reference/idebugarrayobject-getcount.md) 和 [GetElement](../../../extensibility/debugger/reference/idebugarrayobject-getelement.md) 方法来访问元素。

## <a name="see-also"></a>另请参阅
- [IDebugArrayObject](../../../extensibility/debugger/reference/idebugarrayobject.md)
