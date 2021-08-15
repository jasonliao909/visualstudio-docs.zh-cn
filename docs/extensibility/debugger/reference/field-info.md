---
description: 此结构描述本地变量、参数或其他字段。
title: FIELD_INFO |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- FIELD_INFO
helpviewer_keywords:
- FIELD_INFO structure
ms.assetid: bfafef6d-0c83-43d7-a779-1f0d24b166a1
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 2a0d549ef0327b9894e50a7d849be4b6688df83c8e903e14778b3827f7e82f2d
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121360789"
---
# <a name="field_info"></a>FIELD_INFO
此结构描述本地变量、参数或其他字段。

## <a name="syntax"></a>语法

```cpp
typedef struct _tagFieldInfo {
    FIELD_INFO_FIELDS dwFields;
    BSTR              bstrFullName;
    BSTR              bstrName;
    BSTR              bstrType;
    FIELD_MODIFIERS   dwModifiers;
} FIELD_INFO;
```

```csharp
public struct FIELD_INFO {
    public uint   dwFields;
    public string bstrFullName;
    public string bstrName;
    public string bstrType;
    public uint   dwModifiers;
};
```

## <a name="members"></a>成员
`dwFields`\
[FIELD_INFO_FIELDS](../../../extensibility/debugger/reference/field-info-fields.md)枚举中的标志的组合，用于指定要填写的成员。

`bstrFullName`\
字段的全名。

`bstrName`\
字段的短名称。

`bstrType`\
字段的类型。

`dwModifiers`\
描述字段的 [FIELD_MODIFIERS](../../../extensibility/debugger/reference/field-modifiers.md) 枚举中的标志的组合。

## <a name="remarks"></a>备注
此结构被传递给 [GetInfo](../../../extensibility/debugger/reference/idebugfield-getinfo.md) 方法，其中填充了此结构。

## <a name="requirements"></a>要求
标头： sh。h

命名空间： VisualStudio

程序集： Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>另请参阅
- [结构和联合](../../../extensibility/debugger/reference/structures-and-unions.md)
- [FIELD_INFO_FIELDS](../../../extensibility/debugger/reference/field-info-fields.md)
- [FIELD_MODIFIERS](../../../extensibility/debugger/reference/field-modifiers.md)
- [GetInfo](../../../extensibility/debugger/reference/idebugfield-getinfo.md)
