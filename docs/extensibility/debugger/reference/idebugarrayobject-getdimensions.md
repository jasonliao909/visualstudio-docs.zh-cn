---
description: 获取数组的尺寸。
title: IDebugArrayObject：： GetDimensions |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugArrayObject::GetDimensions
helpviewer_keywords:
- IDebugArrayObject::GetDimensions method
ms.assetid: 113e0aff-9028-49d6-b104-9fe7be4772d7
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 7ba82b8a921a7295b6521622ff45efc84a9b6742
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/25/2021
ms.locfileid: "105058880"
---
# <a name="idebugarrayobjectgetdimensions"></a>IDebugArrayObject::GetDimensions
获取数组的尺寸。

## <a name="syntax"></a>语法

```cpp
HRESULT GetDimensions( 
   DWORD dwCount,
   DWORD dwDimensions[]
);
```

```csharp
int GetDimensions(
   [In] uint    dwCount,
   [Out] uint[] dwDimensions
);
```

## <a name="parameters"></a>参数
`dwCount`\
中要检索的维度数。

`dwDimensions`\
[in，out]用每个维度的大小填充的数组。 `dwCount` 指定数组的最大大小 `dwDimensions` 。

## <a name="return-value"></a>返回值
 如果成功，将返回 S_OK;否则，将返回错误代码。

## <a name="remarks"></a>备注
 多维数组每个维度的大小可以不同。 例如，假设有一个三维数组 `myarray[3][2][6]` ，则此方法会在 `dwDimensions` 参数中按顺序返回3、2和6。

## <a name="see-also"></a>另请参阅
- [IDebugArrayObject](../../../extensibility/debugger/reference/idebugarrayobject.md)
