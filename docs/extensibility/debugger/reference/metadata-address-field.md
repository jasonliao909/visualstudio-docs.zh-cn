---
description: 此结构表示类或结构的字段的地址。
title: METADATA_ADDRESS_FIELD |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- METADATA_ADDRESS_FIELD
helpviewer_keywords:
- METADATA_ADDRESS_FIELD structure
ms.assetid: 15ab45fe-6b3b-4e09-880b-31b34f523607
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 9757f42022cf5b590385151fc1346ad75ce8cdd3
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122152557"
---
# <a name="metadata_address_field"></a>METADATA_ADDRESS_FIELD

此结构表示类或结构的字段的地址。

## <a name="syntax"></a>语法

```cpp
typedef struct _tagMETADATA_ADDRESS_FIELD {
    _mdToken tokField;
} METADATA_ADDRESS_FIELD
```

```csharp
public struct METADATA_ADDRESS_FIELD {
    public int tokField;
}
```

## <a name="members"></a>成员

`tokField`\
字段标记的 ID。

[C++] `_mdToken` 是 `typedef` 32 位 的 `int` 。

## <a name="remarks"></a>备注

当 结构的 字段[设置为](../../../extensibility/debugger/reference/debug-address-union.md)从 ADDRESS_KIND 枚举值 (时，此结构是 DEBUG_ADDRESS_UNION 结构中联合的 `dwKind` `DEBUG_ADDRESS_UNION` `ADDRESS_KIND_FIELD` 一) 。 [](../../../extensibility/debugger/reference/address-kind.md)

## <a name="requirements"></a>要求

标头：sh.h

命名空间：Microsoft.VisualStudio.Debugger.Interop

程序集：Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>请参阅

- [结构和联合](../../../extensibility/debugger/reference/structures-and-unions.md)
- [DEBUG_ADDRESS_UNION](../../../extensibility/debugger/reference/debug-address-union.md)
- [ADDRESS_KIND](../../../extensibility/debugger/reference/address-kind.md)
