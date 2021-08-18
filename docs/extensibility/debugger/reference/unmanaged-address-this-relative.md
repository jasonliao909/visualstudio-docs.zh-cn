---
description: 此结构表示一个地址，该地址相对于此指针在 (Me Visual Basic) 。
title: UNMANAGED_ADDRESS_THIS_RELATIVE |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- UNMANAGED_ADDRESS_THIS_RELATIVE
helpviewer_keywords:
- UNMANAGED_ADDRESS_THIS_RELATIVE structure
ms.assetid: e6a91ace-2d47-4ff9-aefb-8d8b68eab0b2
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: ae93e6438c476ce34a6287ba2f35bf6a78e6ac2a
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122110717"
---
# <a name="unmanaged_address_this_relative"></a>UNMANAGED_ADDRESS_THIS_RELATIVE
此结构表示一个地址，该地址相对于 (`this` `Me` 中的指针Visual Basic) 。

## <a name="syntax"></a>语法

```cpp
typedef struct _tagUNMANAGED_THIS_RELATIVE {
   DWORD dwOffset;
   DWORD dwBitOffset;
   DWORD dwBitLength;
} UNMANAGED_ADDRESS_THIS_RELATIVE;
```

```csharp
public struct UNMANAGED_THIS_RELATIVE {
   public uint dwOffset;
   public uint dwBitOffset;
   public uint dwBitLength;
}
```

## <a name="members"></a>成员
 `dwOffset`\
 基位置的字节偏移量 (例如，类 vtable) 。

 `dwBitOffset`\
 从基位置偏移的位 (始终为 0，除非引用位字段) 。

 `dwBitLength`\
 表示地址的位数 (始终为 0，除非引用位域) 。

## <a name="remarks"></a>备注
 当 结构的 字段[设置为](../../../extensibility/debugger/reference/debug-address-union.md)从 ADDRESS_KIND 枚举值 (时，此结构是 DEBUG_ADDRESS_UNION 结构中联合的 `dwKind` `DEBUG_ADDRESS_UNION` `ADDRESS_KIND_UNMANAGED_THIS_RELATIVE` 一) 。 [](../../../extensibility/debugger/reference/address-kind.md)

## <a name="requirements"></a>要求
 标头：sh.h

 命名空间：Microsoft.VisualStudio.Debugger.Interop

 程序集：Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>请参阅
- [结构和联合](../../../extensibility/debugger/reference/structures-and-unions.md)
- [DEBUG_ADDRESS_UNION](../../../extensibility/debugger/reference/debug-address-union.md)
