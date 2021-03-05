---
description: 指定要检索的有关 IDebugField 对象的信息。
title: FIELD_INFO_FIELDS |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- FIELD_INFO_FIELDS
helpviewer_keywords:
- FIELD_INFO_FIELDS enumeration
ms.assetid: a69487d2-e701-4165-804a-8a011df9a3bd
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 024c12d5112398e055141a8db4995f2801ca5401
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2021
ms.locfileid: "102170284"
---
# <a name="field_info_fields"></a>FIELD_INFO_FIELDS
指定要检索的有关 [IDebugField](../../../extensibility/debugger/reference/idebugfield.md) 对象的信息。

## <a name="syntax"></a>语法

```cpp
enum enum_FIELD_INFO_FIELDS { 
    FIF_FULLNAME  = 0x0001,
    FIF_NAME      = 0x0002,
    FIF_TYPE      = 0x0004,
    FIF_MODIFIERS = 0x0008,
    FIF_ALL       = 0xffffffff,
    FIF_NONE      = 0x0000
};
typedef DWORD FIELD_INFO_FIELDS;
```

```csharp
public enum enum_FIELD_INFO_FIELDS {
    FIF_FULLNAME  = 0x0001,
    FIF_NAME      = 0x0002,
    FIF_TYPE      = 0x0004,
    FIF_MODIFIERS = 0x0008,
    FIF_ALL       = 0xffffffff,
    FIF_NONE      = 0x0000
};
```

## <a name="fields"></a>字段
`FIF_FULLNAME`\
初始化/使用 `bstrFullName` [FIELD_INFO](../../../extensibility/debugger/reference/field-info.md) 结构中的字段。

`FIF_NAME`\
初始化/使用 `bstrName` 结构中的字段 `FIELD_INFO` 。

`FIF_TYPE`\
初始化/使用 `bstrType` 结构中的字段 `FIELD_INFO` 。

`FIF_MODIFIERS`\
初始化/使用 `bstrModifiers` 结构中的字段 `FIELD_INFO` 。

## <a name="remarks"></a>备注
还会将这些值作为参数传递给 [GetInfo](../../../extensibility/debugger/reference/idebugfield-getinfo.md) 方法，以指定要初始化 [FIELD_INFO](../../../extensibility/debugger/reference/field-info.md) 结构的哪些字段。

还在结构的成员中使用这些值 `dwFields` `FIELD_INFO` 来指示使用和有效的字段。

这些标志可以与按位组合 `OR` 。

## <a name="requirements"></a>要求
标头： sh。h

命名空间： VisualStudio

程序集： Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>请参阅
- [枚举](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)
- [FIELD_INFO](../../../extensibility/debugger/reference/field-info.md)
- [IDebugField](../../../extensibility/debugger/reference/idebugfield.md)
- [GetInfo](../../../extensibility/debugger/reference/idebugfield-getinfo.md)
