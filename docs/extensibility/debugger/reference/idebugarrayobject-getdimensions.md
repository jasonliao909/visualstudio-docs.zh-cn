---
description: 获取数组的维度。
title: IDebugArrayObject：：GetDimensions |Microsoft Docs
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
ms.technology: vs-ide-debug
ms.workload:
- vssdk
ms.openlocfilehash: e637f1139de8ee6caebea92cc5ca1fe494c206e6
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122080008"
---
# <a name="idebugarrayobjectgetdimensions"></a>IDebugArrayObject::GetDimensions
获取数组的维度。

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
[in]要检索的维度数。

`dwDimensions`\
[in， out]用每个维度的大小填充的数组。 `dwCount` 指定数组的最大 `dwDimensions` 大小。

## <a name="return-value"></a>返回值
 如果成功，则返回S_OK;否则，返回错误代码。

## <a name="remarks"></a>备注
 多维数组可以具有每个维度的不同大小。 例如，给定三维数组 ，此方法将按该顺序在 参数中返回 `myarray[3][2][6]` 3、2 `dwDimensions` 和 6。

## <a name="see-also"></a>请参阅
- [IDebugArrayObject](../../../extensibility/debugger/reference/idebugarrayobject.md)
