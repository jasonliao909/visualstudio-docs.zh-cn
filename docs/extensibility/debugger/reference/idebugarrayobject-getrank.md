---
description: 获取数组的秩，即维度的数目。
title: IDebugArrayObject：： GetRank |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugArrayObject::GetRank
helpviewer_keywords:
- IDebugArrayObject::GetRank method
ms.assetid: 9948551a-e334-4ff6-979c-08dab633b9b6
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 1440ff2fa82c8296bf54b106b622556a8eebb611
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/25/2021
ms.locfileid: "105094323"
---
# <a name="idebugarrayobjectgetrank"></a>IDebugArrayObject::GetRank
获取数组的秩，即维度的数目。

## <a name="syntax"></a>语法

```cpp
HRESULT GetRank( 
   DWORD* pdwRank
);
```

```csharp
int GetRank(
   out uint pdwRank
);
```

## <a name="parameters"></a>参数
`pdwRank`\
弄返回秩。

## <a name="return-value"></a>返回值
 如果成功，将返回 S_OK;否则，将返回错误代码。

## <a name="remarks"></a>备注
 使用 [GetDimensions](../../../extensibility/debugger/reference/idebugarrayobject-getdimensions.md) 方法可检索数组对象的每个维度的大小。

## <a name="see-also"></a>另请参阅
- [IDebugArrayObject](../../../extensibility/debugger/reference/idebugarrayobject.md)
