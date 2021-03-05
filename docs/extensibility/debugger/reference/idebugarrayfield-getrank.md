---
description: 获取数组的秩或维度数。
title: IDebugArrayField：： GetRank |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugArrayField::GetRank
helpviewer_keywords:
- IDebugArrayField::GetRank method
ms.assetid: 2364b876-5be1-4bab-9b8f-3b6121da35c6
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: d9e3d822bac6fa16314f5d2962d69adbf74d0bc3
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2021
ms.locfileid: "102143709"
---
# <a name="idebugarrayfieldgetrank"></a>IDebugArrayField::GetRank
获取数组的秩或维度数。

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
 数组的秩对应于维数。 在 c + + 和 c # 中，多维数组实际上是数组的数组，因此可以只将一维数组视为 (并且 `GetRank` 方法始终返回 1) 。 另一方面，在中， [!INCLUDE[vbprvb](../../../code-quality/includes/vbprvb_md.md)] 多维数组的处理方式不同，此类数组的秩反映 (的维数， `GetRank` 方法始终返回) 的维度数。

## <a name="see-also"></a>另请参阅
- [IDebugArrayField](../../../extensibility/debugger/reference/idebugarrayfield.md)
