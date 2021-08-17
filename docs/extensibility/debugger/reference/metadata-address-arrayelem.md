---
description: 此结构表示数组中的数组元素。
title: METADATA_ADDRESS_ARRAYELEM |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- METADATA_ADDRESS_ARRAYELEM
helpviewer_keywords:
- METADATA_ADDRESS_ARRAYELEM structure
ms.assetid: 24321be5-7c17-4038-82a1-c20a2b68ff3c
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 5ec0844ce76be009e0111cc5edfc71350f05037d685aaa4d793b7e9446a9b891
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121401812"
---
# <a name="metadata_address_arrayelem"></a>METADATA_ADDRESS_ARRAYELEM

此结构表示数组中的数组元素。

## <a name="syntax"></a>语法

```cpp
typedef struct _tagMETADATA_ADDRESS_ARRAYELEM {
    _mdToken tokMethod;
    DWORD    dwIndex;
} METADATA_ADDRESS_ARRAYELEM;
```

```csharp
public struct METADATA_ADDRESS_ARRAYELEM {
    public int  tokMethod;
    public uint dwIndex;
}
```

## <a name="members"></a>成员

`tokMethod`\
此元素属于的数组的 ID。

[C++] `_mdToken` 是 `typedef` 32 位 的 `int` 。

`dwIndex`\
数组中此元素的索引。

## <a name="remarks"></a>备注
当 结构的 字段[设置为](../../../extensibility/debugger/reference/debug-address-union.md)从 ADDRESS_KIND 枚举值 (时，此结构是 DEBUG_ADDRESS_UNION 结构中联合的 `dwKind` `DEBUG_ADDRESS_UNION` `ADDRESS_KIND_ARRAYELEM` 一) 。 [](../../../extensibility/debugger/reference/address-kind.md)

## <a name="requirements"></a>要求
标头：sh.h

命名空间：Microsoft.VisualStudio.Debugger.Interop

程序集：Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>请参阅

- [结构和联合](../../../extensibility/debugger/reference/structures-and-unions.md)
- [DEBUG_ADDRESS_UNION](../../../extensibility/debugger/reference/debug-address-union.md)
- [ADDRESS_KIND](../../../extensibility/debugger/reference/address-kind.md)
