---
description: 获取数组中元素的计数。
title: IDebugArrayObject：： GetCount |Microsoft Docs
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
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: c3a5d052fcb2c40f9dad76791aa992dbfbde72b0
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/25/2021
ms.locfileid: "105058893"
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

## <a name="parameters"></a>参数
`pdwElements`\
弄返回计数。

## <a name="return-value"></a>返回值
 如果成功，将返回 S_OK;否则，将返回错误代码。

## <a name="remarks"></a>备注
 此方法将数组对象的所有元素视为一维数组，即使数组对象是多维的。 例如，给定数组 `myarray[3][2][6]` ，此方法将在参数中返回 36 `pdwElements` 。 使用 [GetElement](../../../extensibility/debugger/reference/idebugarrayobject-getelement.md) 方法每次检索一个元素。

## <a name="see-also"></a>另请参阅
- [IDebugArrayObject](../../../extensibility/debugger/reference/idebugarrayobject.md)
