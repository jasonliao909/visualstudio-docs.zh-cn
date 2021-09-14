---
description: 获取数组中元素的计数。
title: IDebugArrayObject：：GetCount |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugArrayObject::GetCount
helpviewer_keywords:
- IDebugArrayObject::GetCount method
ms.assetid: 7931f3f7-033c-4bf8-8abd-95183952ebb0
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 402a73f6e9f0b866c661b5508d6c785e29d6236f
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126600948"
---
# <a name="idebugarrayobjectgetcount"></a>IDebugArrayObject::GetCount
获取数组中元素的计数。

## <a name="syntax"></a>语法

```cpp
HRESULT GetCount( 
   DWORD* pdwElements
);
```

```csharp
int GetCount(
   out uint pdwElements
);
```

## <a name="parameters"></a>parameters
`pdwElements`\
[out]返回计数。

## <a name="return-value"></a>返回值
 如果成功，则返回S_OK;否则，返回错误代码。

## <a name="remarks"></a>备注
 此方法将数组对象的所有元素视为一维数组，即使数组对象是多维的。 例如，给定数组 `myarray[3][2][6]` ，此方法将在 参数中返回 36。 `pdwElements` 使用 [GetElement](../../../extensibility/debugger/reference/idebugarrayobject-getelement.md) 方法一次检索单个元素。

## <a name="see-also"></a>另请参阅
- [IDebugArrayObject](../../../extensibility/debugger/reference/idebugarrayobject.md)
