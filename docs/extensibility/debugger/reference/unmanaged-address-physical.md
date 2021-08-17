---
description: 此结构表示物理地址。
title: UNMANAGED_ADDRESS_PHYSICAL |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- UNMANAGED_ADDRESS_PHYSICAL
helpviewer_keywords:
- UNMANAGED_ADDRESS_PHYSICAL structure
ms.assetid: fed09686-caa6-4efc-851e-a0432019e9d0
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: e2abfd4bd36ef8e3f278c6df610cd7bb495c36ab
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122087361"
---
# <a name="unmanaged_address_physical"></a>UNMANAGED_ADDRESS_PHYSICAL
此结构表示物理地址。

## <a name="syntax"></a>语法

```cpp
typedef struct _tagUNMANAGED_ADDRESS_PHYSICAL {
   ULONGLONG offset;
} UNMANAGED_ADDRESS_PHYSICAL;
```

```csharp
public struct UNMANAGED_ADDRESS_PHYSICAL {
   public ulong offset;
}
```

## <a name="members"></a>成员
 `offset`\
 物理地址空间的64位偏移量。

## <a name="remarks"></a>备注
 当结构的[](../../../extensibility/debugger/reference/debug-address-union.md) `dwKind` 字段 `DEBUG_ADDRESS_UNION` 设置为 `ADDRESS_KIND_UNMANAGED_PHYSICAL` 从[ADDRESS_KIND](../../../extensibility/debugger/reference/address-kind.md)枚举) 中的值 (时，此结构是 DEBUG_ADDRESS_UNION 结构中联合的一部分。

## <a name="requirements"></a>要求
 标头： sh。h

 命名空间： VisualStudio

 程序集： Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>请参阅
- [结构和联合](../../../extensibility/debugger/reference/structures-and-unions.md)
- [DEBUG_ADDRESS_UNION](../../../extensibility/debugger/reference/debug-address-union.md)
