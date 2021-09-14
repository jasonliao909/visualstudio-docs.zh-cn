---
description: 此结构表示作用域内局部变量的地址 (函数或方法) 。
title: METADATA_ADDRESS_LOCAL |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- METADATA_ADDRESS_LOCAL
helpviewer_keywords:
- METADATA_ADDRESS_LOCAL structure
ms.assetid: 635f6bc5-c486-4e0e-83db-36f15e543843
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 71b8b4ef578646a63ec64fbbde506dd71984fe35
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126665395"
---
# <a name="metadata_address_local"></a>METADATA_ADDRESS_LOCAL

此结构表示作用域内局部变量的地址 (函数或方法) 。

## <a name="syntax"></a>语法

```cpp
typedef struct _tagMETADATA_ADDRESS_LOCAL {
    _mdToken  tokMethod;
    IUnknown* pLocal;
    DWORD     dwIndex;
} METADATA_ADDRESS_LOCAL;
```

```csharp
public struct METADATA_ADDRESS_LOCAL {
    public int    tokMethod;
    public object pLocal;
    public uint   dwIndex;
}
```

## <a name="members"></a>成员

`tokMethod`\
局部变量所包含的方法或函数的 ID。

[C++] `_mdToken` 是 `typedef` 32 位 的 `int` 。

`pLocal`\
此 结构表示其地址的标记。

`dwIndex`\
可以是方法或函数中此局部变量的索引，或特定于语言 (的一) 。

## <a name="remarks"></a>备注

当 结构的 字段设置为从 DEBUG_ADDRESS_UNION[](../../../extensibility/debugger/reference/debug-address-union.md)枚举值中 (时，此结构是 ADDRESS_KIND 联合的 `dwKind` `DEBUG_ADDRESS_UNION` `ADDRESS_KIND_LOCAL` 一) 。 [](../../../extensibility/debugger/reference/address-kind.md)

> [!WARNING]
> [仅 C++]如果 不为 null，则必须在标记指针上调用 ， (`pLocal` `Release` `addr` 是以下DEBUG_ADDRESS中的) ： [](../../../extensibility/debugger/reference/debug-address.md)
>
> ```cpp
> if (addr.dwKind == ADDRESS_KIND_METADATA_LOCAL && addr.addr.addrLocal.pLocal != NULL)
> {
>     addr.addr.addrLocal.pLocal->Release();
> }
> ```

## <a name="requirements"></a>要求

标头：sh.h

命名空间：Microsoft.VisualStudio.Debugger.Interop

程序集：Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>另请参阅

- [结构和联合](../../../extensibility/debugger/reference/structures-and-unions.md)
- [DEBUG_ADDRESS_UNION](../../../extensibility/debugger/reference/debug-address-union.md)
- [DEBUG_ADDRESS](../../../extensibility/debugger/reference/debug-address.md)
- [ADDRESS_KIND](../../../extensibility/debugger/reference/address-kind.md)
