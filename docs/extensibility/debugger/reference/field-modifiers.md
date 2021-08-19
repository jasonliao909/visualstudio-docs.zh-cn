---
description: 指定字段类型的修饰符。
title: FIELD_MODIFIERS |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- FIELD_MODIFIERS
helpviewer_keywords:
- FIELD_MODIFIERS enumeration
ms.assetid: 1e44681c-1f03-41a9-9c04-b79f231b0822
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 8e74dec064f2603fa19745ec0abab8b7a402307a
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122119966"
---
# <a name="field_modifiers"></a>FIELD_MODIFIERS
指定字段类型的修饰符。

## <a name="syntax"></a>语法

```cpp
enum enum_FIELD_MODIFIERS {
    FIELD_MOD_NONE             = 0x00000000,

    // Modifier of the field
    FIELD_MOD_ACCESS_NONE      = 0x00000001,
    FIELD_MOD_ACCESS_PUBLIC    = 0x00000002,
    FIELD_MOD_ACCESS_PROTECTED = 0x00000004,
    FIELD_MOD_ACCESS_PRIVATE   = 0x00000008,

    // Storage modifier of the field
    FIELD_MOD_NOMODIFIERS      = 0x00000010,
    FIELD_MOD_STATIC           = 0x00000020,
    FIELD_MOD_CONSTANT         = 0x00000040,
    FIELD_MOD_TRANSIENT        = 0x00000080,
    FIELD_MOD_VOLATILE         = 0x00000100,
    FIELD_MOD_ABSTRACT         = 0x00000200,
    FIELD_MOD_NATIVE           = 0x00000400,
    FIELD_MOD_SYNCHRONIZED     = 0x00000800,
    FIELD_MOD_VIRTUAL          = 0x00001000,
    FIELD_MOD_INTERFACE        = 0x00002000,
    FIELD_MOD_FINAL            = 0x00004000,
    FIELD_MOD_SENTINEL         = 0x00008000,
    FIELD_MOD_INNERCLASS       = 0x00010000,
    FIELD_TYPE_OPTIONAL        = 0x00020000,
    FIELD_MOD_BYREF            = 0x00040000,
    FIELD_MOD_HIDDEN           = 0x00080000,
    FIELD_MOD_MARSHALASOBJECT  = 0x00100000,
    FIELD_MOD_SPECIAL_NAME     = 0x00200000,
    FIELD_MOD_HIDEBYSIG        = 0x00400000,

    FIELD_MOD_WRITEONLY        = 0x80000000,
    FIELD_MOD_ACCESS_MASK      = 0x000000ff,
    FIELD_MOD_MASK             = 0xffffff00,
    FIELD_MOD_ALL              = 0x7fffffff
};
typedef DWORD FIELD_MODIFIERS;
```

```csharp
public enum enum_FIELD_MODIFIERS {
    FIELD_MOD_NONE             = 0x00000000,

    // Modifier of the field
    FIELD_MOD_ACCESS_NONE      = 0x00000001,
    FIELD_MOD_ACCESS_PUBLIC    = 0x00000002,
    FIELD_MOD_ACCESS_PROTECTED = 0x00000004,
    FIELD_MOD_ACCESS_PRIVATE   = 0x00000008,

    // Storage modifier of the field
    FIELD_MOD_NOMODIFIERS      = 0x00000010,
    FIELD_MOD_STATIC           = 0x00000020,
    FIELD_MOD_CONSTANT         = 0x00000040,
    FIELD_MOD_TRANSIENT        = 0x00000080,
    FIELD_MOD_VOLATILE         = 0x00000100,
    FIELD_MOD_ABSTRACT         = 0x00000200,
    FIELD_MOD_NATIVE           = 0x00000400,
    FIELD_MOD_SYNCHRONIZED     = 0x00000800,
    FIELD_MOD_VIRTUAL          = 0x00001000,
    FIELD_MOD_INTERFACE        = 0x00002000,
    FIELD_MOD_FINAL            = 0x00004000,
    FIELD_MOD_SENTINEL         = 0x00008000,
    FIELD_MOD_INNERCLASS       = 0x00010000,
    FIELD_TYPE_OPTIONAL        = 0x00020000,
    FIELD_MOD_BYREF            = 0x00040000,
    FIELD_MOD_HIDDEN           = 0x00080000,
    FIELD_MOD_MARSHALASOBJECT  = 0x00100000,
    FIELD_MOD_SPECIAL_NAME     = 0x00200000,
    FIELD_MOD_HIDEBYSIG        = 0x00400000,

    FIELD_MOD_WRITEONLY        = 0x80000000,
    FIELD_MOD_ACCESS_MASK      = 0x000000ff,
    FIELD_MOD_MASK             = 0xffffff00,
    FIELD_MOD_ALL              = 0x7fffffff
};
```

## <a name="fields"></a>字段
`FIELD_MOD_ACCESS_TYPE`\
指示无法访问该字段。

`FIELD_MOD_ACCESS_PUBLIC`\
指示字段具有公共访问权限。

`FIELD_MOD_ACCESS_PROTECTED`\
指示字段具有受保护的访问权限。

`FIELD_MOD_ACCESS_PRIVATE`\
指示字段具有专用访问权限。

`FIELD_MOD_NOMODIFIERS`\
指示字段没有修饰符。

`FIELD_MOD_STATIC`\
指示字段是静态的。

`FIELD_MOD_CONSTANT`\
指示字段是常量。

`FIELD_MOD_TRANSIENT`\
指示该字段是暂时性的。

`FIELD_MOD_VOLATILE`\
指示字段是可变的。

`FIELD_MOD_ABSTRACT`\
指示字段是抽象的。

`FIELD_MOD_NATIVE`\
指示该字段为本机字段。

`FIELD_MOD_SYNCHRONIZED`\
指示字段已同步。

`FIELD_MOD_VIRTUAL`\
指示该字段是虚拟的。

`FIELD_MOD_INTERFACE`\
指示字段是接口。

`FIELD_MOD_FINAL`\
指示字段是最终字段。

`FIELD_MOD_SENTINEL`\
指示字段是 sentinel。

`FIELD_MOD_INNERCLASS`\
指示字段是内部类。

`FIELD_TYPE_OPTIONAL`\
指示字段是可选的。

`FIELD_MOD_BYREF`\
指示字段是引用参数。 这专门用于方法参数。

`FIELD_MOD_HIDDEN`\
指示字段必须隐藏或在另一个上下文中显示;例如， [!INCLUDE[vbprvb](../../../code-quality/includes/vbprvb_md.md)] 静态局部变量。

`FIELD_MOD_MARSHALASOBJECT`\
指示字段表示具有接口 `IUnknown` 的对象。

`FIELD_MOD_SPECIAL_NAME`\
指示字段具有一个特殊名称，例如，仅 (`.ctor` [!INCLUDE[vbprvb](../../../code-quality/includes/vbprvb_md.md)] 构造函数) 。

`FIELD_MOD_HIDEBYSIG`\
指示字段具有应用于 `Overloads` 该字段的关键字 ([!INCLUDE[vbprvb](../../../code-quality/includes/vbprvb_md.md)] 仅) 。

`FIELD_MOD_WRITEONLY`\
指示该字段是只写的。 此值不包括在 `FIELD_MOD_ALL` 中，因为此类仅写字段的唯一用途是进行函数计算。 用户必须显式请求 `FIELD_MOD_WRITEONLY` 字段。

`FIELD_MOD_ACCESS_MASK`\
指示用于字段访问的掩码。

`FIELD_MOD_MASK`\
指示字段修饰符的掩码。

## <a name="remarks"></a>备注
用于 `dwModifiers` 结构FIELD_INFO成员。 [](../../../extensibility/debugger/reference/field-info.md)

这些值还会传递给 [EnumFields](../../../extensibility/debugger/reference/idebugcontainerfield-enumfields.md) 方法，以筛选特定字段。

## <a name="requirements"></a>要求
标头：sh.h

命名空间：Microsoft.VisualStudio.Debugger.Interop

程序集：Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>请参阅
- [枚举](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)
- [FIELD_INFO](../../../extensibility/debugger/reference/field-info.md)
- [EnumFields](../../../extensibility/debugger/reference/idebugcontainerfield-enumfields.md)
