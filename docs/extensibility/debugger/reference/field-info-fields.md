---
description: 指定要检索有关 IDebugField 对象的信息。
title: FIELD_INFO_FIELDS |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- FIELD_INFO_FIELDS
helpviewer_keywords:
- FIELD_INFO_FIELDS enumeration
ms.assetid: a69487d2-e701-4165-804a-8a011df9a3bd
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 03b89d7337888033b2a2ce02e71d37a1340a4580
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122073027"
---
# <a name="field_info_fields"></a>FIELD_INFO_FIELDS
指定要检索有关 [IDebugField](../../../extensibility/debugger/reference/idebugfield.md) 对象的信息。

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
初始化/使用 `bstrFullName` 结构FIELD_INFO字段。 [](../../../extensibility/debugger/reference/field-info.md)

`FIF_NAME`\
初始化/使用 `bstrName` 结构中的 `FIELD_INFO` 字段。

`FIF_TYPE`\
初始化/使用 `bstrType` 结构中的 `FIELD_INFO` 字段。

`FIF_MODIFIERS`\
初始化/使用 `bstrModifiers` 结构中的 `FIELD_INFO` 字段。

## <a name="remarks"></a>备注
这些值也作为参数传递给[GetInfo](../../../extensibility/debugger/reference/idebugfield-getinfo.md)方法，以指定要初始化FIELD_INFO的字段。 [](../../../extensibility/debugger/reference/field-info.md)

这些值还用于 结构的成员， `dwFields` `FIELD_INFO` 以指示使用哪些字段并且有效。

这些标志可以与位 合并 `OR` 。

## <a name="requirements"></a>要求
标头：sh.h

命名空间：Microsoft.VisualStudio.Debugger.Interop

程序集：Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>请参阅
- [枚举](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)
- [FIELD_INFO](../../../extensibility/debugger/reference/field-info.md)
- [IDebugField](../../../extensibility/debugger/reference/idebugfield.md)
- [GetInfo](../../../extensibility/debugger/reference/idebugfield-getinfo.md)
