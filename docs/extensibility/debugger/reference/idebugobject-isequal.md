---
description: 将 对象与此 对象进行比较。
title: IDebugObject：：IsEqual |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugObject::IsEqual
helpviewer_keywords:
- IDebugObject::IsEqual method
ms.assetid: 4b76e663-ef2e-41ff-9be1-bf26d666a34a
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 22b5f3a98afa2be496295dd13e8ec1c2b5f08a1b
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122034976"
---
# <a name="idebugobjectisequal"></a>IDebugObject::IsEqual
将 对象与此 对象进行比较。

## <a name="syntax"></a>语法

```cpp
HRESULT IsEqual( 
   IDebugObject* pObject,
   BOOL*         pfIsEqual
);
```

```csharp
int IsEqual(
   IDebugObject pObject,
   out int      pfIsEqual
);
```

## <a name="parameters"></a>参数
`pObject`\
[in]表示 [要比较的对象的 IDebugObject](../../../extensibility/debugger/reference/idebugobject.md) 对象。

`pfIsEqual`\
[out]如果对象的值 () ，则返回非零值;否则 `TRUE` `FALSE` ， () 。

## <a name="return-value"></a>返回值
 如果成功，则返回S_OK;否则，返回错误代码。

## <a name="remarks"></a>备注
 通常，此方法可以比较参数和此 `pObject` [IDebugObject](../../../extensibility/debugger/reference/idebugobject.md) 对象表示的值的地址;如果地址相等，则对象可视为相等。

## <a name="see-also"></a>请参阅
- [IDebugObject](../../../extensibility/debugger/reference/idebugobject.md)
