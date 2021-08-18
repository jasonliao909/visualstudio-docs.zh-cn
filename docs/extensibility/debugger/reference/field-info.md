---
description: 此结构描述局部变量、参数或其他字段。
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
ms.openlocfilehash: a9b2a07611a3bae712f714c318cf5f3e4446235e
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122072923"
---
# <a name="field_info"></a>FIELD_INFO
此结构描述局部变量、参数或其他字段。

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
集合中标志的组合 [FIELD_INFO_FIELDS](../../../extensibility/debugger/reference/field-info-fields.md) 枚举，用于指定填充哪些成员。

`bstrFullName`\
字段的全名。

`bstrName`\
字段的短名称。

`bstrType`\
字段的类型。

`dwModifiers`\
描述字段的FIELD_MODIFIERS集合中的[](../../../extensibility/debugger/reference/field-modifiers.md)标志组合。

## <a name="remarks"></a>备注
此结构将传递到 [GetInfo](../../../extensibility/debugger/reference/idebugfield-getinfo.md) 方法中填充它。

## <a name="requirements"></a>要求
标头：sh.h

命名空间：Microsoft.VisualStudio.Debugger.Interop

程序集：Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>请参阅
- [结构和联合](../../../extensibility/debugger/reference/structures-and-unions.md)
- [FIELD_INFO_FIELDS](../../../extensibility/debugger/reference/field-info-fields.md)
- [FIELD_MODIFIERS](../../../extensibility/debugger/reference/field-modifiers.md)
- [GetInfo](../../../extensibility/debugger/reference/idebugfield-getinfo.md)
