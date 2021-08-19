---
description: 指定 IDebugField 对象中包含的字段类型。
title: FIELD_KIND |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- FIELD_KIND
helpviewer_keywords:
- FIELD_KIND enumeration
ms.assetid: fd522b9c-52e2-42fa-939d-343347d5c3b1
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 9429f3637172b8797eb700717383786e51be8354
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122072883"
---
# <a name="field_kind"></a>FIELD_KIND
指定 [IDebugField](../../../extensibility/debugger/reference/idebugfield.md) 对象中包含的字段类型。

## <a name="syntax"></a>语法

```cpp
enum enum_FIELD_KIND {
    FIELD_KIND_NONE       = 0x00000000,

    // Type of field
    FIELD_KIND_TYPE       = 0x00000001,
    FIELD_KIND_SYMBOL     = 0x00000002,

    // Storage type of the field
    FIELD_TYPE_PRIMITIVE  = 0x00000010,
    FIELD_TYPE_STRUCT     = 0x00000020,
    FIELD_TYPE_CLASS      = 0x00000040,
    FIELD_TYPE_INTERFACE  = 0x00000080,
    FIELD_TYPE_UNION      = 0x00000100,
    FIELD_TYPE_ARRAY      = 0x00000200,
    FIELD_TYPE_METHOD     = 0x00000400,
    FIELD_TYPE_BLOCK      = 0x00000800,
    FIELD_TYPE_POINTER    = 0x00001000,
    FIELD_TYPE_ENUM       = 0x00002000,
    FIELD_TYPE_LABEL      = 0x00004000,
    FIELD_TYPE_TYPEDEF    = 0x00008000,
    FIELD_TYPE_BITFIELD   = 0x00010000,
    FIELD_TYPE_NAMESPACE  = 0x00020000,
    FIELD_TYPE_MODULE     = 0x00040000,
    FIELD_TYPE_DYNAMIC    = 0x00080000,
    FIELD_TYPE_PROP       = 0x00100000,
    FIELD_TYPE_INNERCLASS = 0x00200000,
    FIELD_TYPE_REFERENCE  = 0x00400000,
    FIELD_TYPE_EXTENDED   = 0x00800000,

    // Specific information about symbols
    FIELD_SYM_MEMBER      = 0x01000000,
    FIELD_SYM_LOCAL       = 0x02000000,
    FIELD_SYM_PARAM       = 0x04000000,
    FIELD_SYM_THIS        = 0x08000000,
    FIELD_SYM_GLOBAL      = 0x10000000,
    FIELD_SYM_PROP_GETTER = 0x20000000,
    FIELD_SYM_PROP_SETTER = 0x40000000,
    FIELD_SYM_EXTENDED    = 0x80000000,

    FIELD_KIND_MASK       = 0x0000000f,
    FIELD_TYPE_MASK       = 0x00fffff0,
    FIELD_SYM_MASK        = 0xff000000,

    FIELD_KIND_ALL        = 0xffffffff
};
typedef DWORD FIELD_KIND;
```

```csharp
public enum enum_FIELD_KIND {
    FIELD_KIND_NONE       = 0x00000000,

    // Type of field
    FIELD_KIND_TYPE       = 0x00000001,
    FIELD_KIND_SYMBOL     = 0x00000002,

    // Storage type of the field
    FIELD_TYPE_PRIMITIVE  = 0x00000010,
    FIELD_TYPE_STRUCT     = 0x00000020,
    FIELD_TYPE_CLASS      = 0x00000040,
    FIELD_TYPE_INTERFACE  = 0x00000080,
    FIELD_TYPE_UNION      = 0x00000100,
    FIELD_TYPE_ARRAY      = 0x00000200,
    FIELD_TYPE_METHOD     = 0x00000400,
    FIELD_TYPE_BLOCK      = 0x00000800,
    FIELD_TYPE_POINTER    = 0x00001000,
    FIELD_TYPE_ENUM       = 0x00002000,
    FIELD_TYPE_LABEL      = 0x00004000,
    FIELD_TYPE_TYPEDEF    = 0x00008000,
    FIELD_TYPE_BITFIELD   = 0x00010000,
    FIELD_TYPE_NAMESPACE  = 0x00020000,
    FIELD_TYPE_MODULE     = 0x00040000,
    FIELD_TYPE_DYNAMIC    = 0x00080000,
    FIELD_TYPE_PROP       = 0x00100000,
    FIELD_TYPE_INNERCLASS = 0x00200000,
    FIELD_TYPE_REFERENCE  = 0x00400000,
    FIELD_TYPE_EXTENDED   = 0x00800000,

    // Specific information about symbols
    FIELD_SYM_MEMBER      = 0x01000000,
    FIELD_SYM_LOCAL       = 0x02000000,
    FIELD_SYM_PARAM       = 0x04000000,
    FIELD_SYM_THIS        = 0x08000000,
    FIELD_SYM_GLOBAL      = 0x10000000,
    FIELD_SYM_PROP_GETTER = 0x20000000,
    FIELD_SYM_PROP_SETTER = 0x40000000,
    FIELD_SYM_EXTENDED    = 0x80000000,

    FIELD_KIND_MASK       = 0x0000000f,
    FIELD_TYPE_MASK       = 0x00fffff0,
    FIELD_SYM_MASK        = 0xff000000,

    FIELD_KIND_ALL        = 0xffffffff
};
```

## <a name="fields"></a>字段
`FIELD_KIND_TYPE`\
指示该字段仅为类型。

`FIELD_KIND_SYMBOL`\
指示字段是一个符号，包含类型、名称和其他信息。

`FIELD_TYPE_PRIMITIVE`\
指示字段是基元数据类型。

`FIELD_TYPE_STRUCT`\
指示字段是结构。

`FIELD_TYPE_CLASS`\
指示字段是类。

`FIELD_TYPE_INTERFACE`\
指示字段是接口。

`FIELD_TYPE_UNION`\
指示字段是联合。

`FIELD_TYPE_ARRAY`\
指示字段是数组。

`FIELD_TYPE_METHOD`\
指示字段是方法。

`FIELD_TYPE_BLOCK`\
指示字段是块。

`FIELD_TYPE_POINTER`\
指示字段是指针。

`FIELD_TYPE_ENUM`\
指示字段是枚举数据类型。

`FIELD_TYPE_LABEL`\
指示字段是标签。

`FIELD_TYPE_TYPEDEF`\
指示字段是 typedef。

`FIELD_TYPE_BITFIELD`\
指示字段是位域。

`FIELD_TYPE_NAMESPACE`\
指示字段是命名空间。

`FIELD_TYPE_MODULE`\
指示字段是模块。

`FIELD_TYPE_DYNAMIC`\
指示字段是动态的。

`FIELD_TYPE_PROP`\
指示字段是属性。

`FIELD_TYPE_INNERCLASS`\
指示字段是内部类。

`FIELD_TYPE_REFERENCE`\
指示字段是引用。

`FIELD_TYPE_EXTENDED`\
保留供将来使用。

`FIELD_SYM_MEMBER`\
指示字段是成员。

`FIELD_SYM_LOCAL`\
指示该字段是本地的。

`FIELD_SYM_PARAMETER`\
指示字段是参数。

`FIELD_SYM_THIS`\
指示字段是"this"指针。

`FIELD_SYM_GLOBAL`\
指示该字段是全局字段。

`FIELD_SYM_PROP_GETTER`\
指示字段检索属性。

`FIELD_SYM_PROP_SETTER`\
指示字段设置属性。

`FIELD_SYM_EXTENDED`\
保留供将来使用。

`FIELD_KIND_MASK`\
指示字段类型的掩码。

`FIELD_TYPE_MASK`\
指示字段类型的掩码。

`FIELD_SYM_MASK`\
指示符号信息的掩码。

## <a name="remarks"></a>备注
从调用 [GetKind 方法返回](../../../extensibility/debugger/reference/idebugfield-getkind.md) 。

根据字段类型，可以在[IDebugField](../../../extensibility/debugger/reference/idebugfield.md)接口上为更具体的接口形式调用[QueryInterface。](/cpp/atl/queryinterface) 例如，如果 [GetKind](../../../extensibility/debugger/reference/idebugfield-getkind.md) 返回 `FIELD_TYPE_METHOD` ，则你可以调用 `QueryInterface` I 以获取 `DebugField` [IDebugMethodField](../../../extensibility/debugger/reference/idebugmethodfield.md) 接口。

## <a name="requirements"></a>要求
标头：sh.h

命名空间：Microsoft.VisualStudio.Debugger.Interop

程序集：Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>请参阅
- [枚举](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)
- [FIELD_MODIFIERS](../../../extensibility/debugger/reference/field-modifiers.md)
- [GetKind](../../../extensibility/debugger/reference/idebugfield-getkind.md)
- [IDebugField](../../../extensibility/debugger/reference/idebugfield.md)
