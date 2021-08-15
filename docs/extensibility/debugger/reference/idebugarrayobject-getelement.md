---
description: 获取数组的元素。
title: IDebugArrayObject：： GetElement |Microsoft Docs
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
ms.openlocfilehash: 95d910d6ab039a544715a77b68d2f09b4a1478545ef64dd962db8cd5b372f707
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121323867"
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

## <a name="parameters"></a>参数
`dwIndex`\
中元素索引。

`ppElement`\
弄返回表示元素的 [IDebugObject](../../../extensibility/debugger/reference/idebugobject.md) 接口。

## <a name="return-value"></a>返回值
 如果成功，将返回 S_OK;否则，将返回错误代码。

## <a name="remarks"></a>备注
 此方法将数组对象的所有元素视为一维数组，即使数组对象是多维的。 例如，假设数组 `myarray[3][2][6]` 和 `dwIndex` 参数为20，则此方法将返回中的元素 `myarray[1][1][2]` ，而 `dwIndex` 参数21会从返回该元素 `myarray[1][1][3]` 。 使用 [GetCount](../../../extensibility/debugger/reference/idebugarrayobject-getcount.md) 方法来确定数组中的元素总数。

## <a name="see-also"></a>另请参阅
- [IDebugArrayObject](../../../extensibility/debugger/reference/idebugarrayobject.md)
