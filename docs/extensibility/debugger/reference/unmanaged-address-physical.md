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
ms.openlocfilehash: b9c9b3b0759d5a1831525708b5ae4915d063ca801a9e2c998ccaa0d1655b788e
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121388885"
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
 物理地址空间的 64 位偏移量。

## <a name="remarks"></a>备注
 当 结构的 字段[设置为](../../../extensibility/debugger/reference/debug-address-union.md)从 ADDRESS_KIND 枚举值 (时，此结构是 DEBUG_ADDRESS_UNION 结构中联合的 `dwKind` `DEBUG_ADDRESS_UNION` `ADDRESS_KIND_UNMANAGED_PHYSICAL` 一) 。 [](../../../extensibility/debugger/reference/address-kind.md)

## <a name="requirements"></a>要求
 标头：sh.h

 命名空间：Microsoft.VisualStudio.Debugger.Interop

 程序集：Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>请参阅
- [结构和联合](../../../extensibility/debugger/reference/structures-and-unions.md)
- [DEBUG_ADDRESS_UNION](../../../extensibility/debugger/reference/debug-address-union.md)
