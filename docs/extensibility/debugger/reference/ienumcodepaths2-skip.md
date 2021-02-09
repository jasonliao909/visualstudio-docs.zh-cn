---
title: IEnumCodePaths2：： Skip |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IEnumCodePaths2::Skip
helpviewer_keywords:
- IEnumCodePaths2::Skip
ms.assetid: 356472d8-68b2-4b7e-b5f0-1f16d4ee80af
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 75b5e75362330def308bc3b0b836d22807aea66a
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2021
ms.locfileid: "99912723"
---
# <a name="ienumcodepaths2skip"></a>IEnumCodePaths2::Skip
跳过指定数目的元素。

## <a name="syntax"></a>语法

```cpp
HRESULT Skip(
   ULONG celt
);
```

```csharp
int Skip(
   uint celt
);
```

## <a name="parameters"></a>parameters
`celt`\
中要跳过的元素数。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK`。 `S_FALSE`如果 `celt` 大于剩余元素的数目，则返回; 否则返回错误代码。

## <a name="remarks"></a>备注
 如果 `celt` 指定的值大于剩余元素的数目，则枚举将设置为 end，并 `S_FALSE` 返回。

## <a name="see-also"></a>另请参阅
- [IEnumCodePaths2](../../../extensibility/debugger/reference/ienumcodepaths2.md)
