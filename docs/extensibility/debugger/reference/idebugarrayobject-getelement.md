---
description: 获取数组的元素。
title: IDebugArrayObject：：GetElement |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugArrayObject::GetElement
helpviewer_keywords:
- IDebugArrayObject::GetElement method
ms.assetid: 08b44341-7bf1-4a8c-8b79-98ae5785b195
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 8bc91b0576e98b5c27659ca9ae90ef37001e790c
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126600943"
---
# <a name="idebugarrayobjectgetelement"></a>IDebugArrayObject::GetElement
获取数组的元素。

## <a name="syntax"></a>语法

```cpp
HRESULT GetElement( 
   DWORD          dwIndex,
   IDebugObject** ppElement
);
```

```csharp
int GetElement(
   [In] uint dwIndex,
   out IDebugObject ppElement
);
```

## <a name="parameters"></a>parameters
`dwIndex`\
[in]元素索引。

`ppElement`\
[out]返回表示 [元素的 IDebugObject](../../../extensibility/debugger/reference/idebugobject.md) 接口。

## <a name="return-value"></a>返回值
 如果成功，则返回S_OK;否则，返回错误代码。

## <a name="remarks"></a>备注
 此方法将数组对象的所有元素视为一维数组，即使数组对象是多维的。 例如，给定数组 `myarray[3][2][6]` 和参数 20，此方法将返回 中的 元素，参数 `dwIndex` `myarray[1][1][2]` `dwIndex` 21 将返回 中的 元素 `myarray[1][1][3]` 。 使用 [GetCount](../../../extensibility/debugger/reference/idebugarrayobject-getcount.md) 方法确定数组中的元素总数。

## <a name="see-also"></a>另请参阅
- [IDebugArrayObject](../../../extensibility/debugger/reference/idebugarrayobject.md)
