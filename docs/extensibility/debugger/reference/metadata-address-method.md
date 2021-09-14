---
description: 此结构表示类的方法的地址。
title: METADATA_ADDRESS_METHOD |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- METADATA_ADDRESS_METHOD
helpviewer_keywords:
- METADATA_ADDRESS_METHOD structure
ms.assetid: fc0e5370-1b4f-4867-837f-0d63c4b9dd09
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: b462e63ec64fec9de292ee7f497f8b62333dd7ba
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126665396"
---
# <a name="metadata_address_method"></a>METADATA_ADDRESS_METHOD
此结构表示类的方法的地址。

## <a name="syntax"></a>语法

```cpp
typedef struct _tagMETADATA_ADDRESS_METHOD {
   _mdToken tokMethod;
   DWORD    dwOffset;
   DWORD    dwVersion;
} METADATA_ADDRESS_METHOD;
```

```csharp
public struct METADATA_ADDRESS_METHOD {
   public int  tokMethod;
   public uint dwOffset;
   public uint dwVersion;
}
```

## <a name="members"></a>成员
 `tokMethod`\
 方法的 ID。

 [C++] `_mdToken` 是 `typedef` 32 位 的 `int` 。

 `dwOffset`\
 从 类开始到此方法的偏移量 (表示 vtable) 。

 `dwVersion`\
 此方法的版本 (此值对于符号提供程序唯一) 。

## <a name="remarks"></a>备注
 当 结构的 字段[设置为](../../../extensibility/debugger/reference/debug-address-union.md)从 DEBUG_ADDRESS_UNION 枚举集合中 (值时，此结构是 ADDRESS_KIND 中的联合 `dwKind` `DEBUG_ADDRESS_UNION` `ADDRESS_KIND_METHOD`) 。 [](../../../extensibility/debugger/reference/address-kind.md)

## <a name="requirements"></a>要求
 标头：sh.h

 命名空间：Microsoft.VisualStudio.Debugger.Interop

 程序集：Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>另请参阅
- [结构和联合](../../../extensibility/debugger/reference/structures-and-unions.md)
- [DEBUG_ADDRESS_UNION](../../../extensibility/debugger/reference/debug-address-union.md)
- [ADDRESS_KIND](../../../extensibility/debugger/reference/address-kind.md)
