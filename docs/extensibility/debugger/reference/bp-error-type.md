---
description: 指定断点的错误类型。
title: BP_ERROR_TYPE |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- BP_ERROR_TYPE
helpviewer_keywords:
- BP_ERROR_TYPE enumeration
ms.assetid: c483eaab-db29-46de-bfdb-5c2a9a9cfb68
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: ddff439aba67248bd2eb706a85c5f91b4bf1628d
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/25/2021
ms.locfileid: "105085281"
---
# <a name="bp_error_type"></a>BP_ERROR_TYPE
指定断点的错误类型。

## <a name="syntax"></a>语法

```cpp
enum enum_BP_ERROR_TYPE {
    BPET_NONE            = 0x00000000,
    BPET_TYPE_WARNING    = 0x00000001,
    BPET_TYPE_ERROR      = 0x00000002,
    BPET_SEV_HIGH        = 0x0F000000,
    BPET_SEV_GENERAL     = 0x07000000,
    BPET_SEV_LOW         = 0x01000000,
    BPET_TYPE_MASK       = 0x0000ffff,
    BPET_SEV_MASK        = 0xffff0000,
    BPET_GENERAL_WARNING = BPET_SEV_GENERAL | BPET_TYPE_WARNING,
    BPET_GENERAL_ERROR   = BPET_SEV_GENERAL | BPET_TYPE_ERROR,
    BPET_ALL             = 0xffffffff
};
typedef DWORD BP_ERROR_TYPE;
```

```csharp
public enum enum_BP_ERROR_TYPE {
    BPET_NONE            = 0x00000000,
    BPET_TYPE_WARNING    = 0x00000001,
    BPET_TYPE_ERROR      = 0x00000002,
    BPET_SEV_HIGH        = 0x0F000000,
    BPET_SEV_GENERAL     = 0x07000000,
    BPET_SEV_LOW         = 0x01000000,
    BPET_TYPE_MASK       = 0x0000ffff,
    BPET_SEV_MASK        = 0xffff0000,
    BPET_GENERAL_WARNING = BPET_SEV_GENERAL | BPET_TYPE_WARNING,
    BPET_GENERAL_ERROR   = BPET_SEV_GENERAL | BPET_TYPE_ERROR,
    BPET_ALL             = 0xffffffff
};
```

## <a name="fields"></a>字段
`BPET_NONE`\
指定无断点错误。

`BPET_TYPE_WARNING`\
指定警告样式断点错误。

`BPET_TYPE_ERROR`\
指定错误样式断点错误。

`BPET_SEV_HIGH`\
指定高严重性断点错误。

`BPET_SEV_GENERAL`\
指定中等严重性断点错误。

`BPET_SEV_LOW`\
指定低严重性断点错误。

`BPET_TYPE_MASK`\
指定掩码样式断点错误。

`BPET_SEV_MASK`\
指定严重性掩码样式断点错误。

`BPET_GENERAL_WARNING`\
指定一般警告样式断点错误。

`BPET_GENERAL_ERROR`\
指定常规错误样式断点错误。

`BPET_ALL`\
指定所有断点错误类型。

## <a name="remarks"></a>备注
这些值可以与按位与 `OR` `dwType` [BP_ERROR_RESOLUTION_INFO](../../../extensibility/debugger/reference/bp-error-resolution-info.md) 结构的成员一起使用。 作为参数传递给 [EnumErrorBreakpoints](../../../extensibility/debugger/reference/idebugpendingbreakpoint2-enumerrorbreakpoints.md) 方法。

断点错误类型由类型和严重性组成。 这意味着断点错误类型永远不只是一种类型 (例如， `BPET_TYPE_ERROR` ) 或严重性 (例如， `BPET_SEV_GENERAL`) 本身。 `BPET_GENERAL_WARNING` 和 `BPET_GENERAL_ERROR` 为常规警告和错误断点提供预定义的值。

## <a name="requirements"></a>要求
标头： msdbg

命名空间： VisualStudio

程序集： Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>请参阅
- [枚举](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)
- [BP_ERROR_RESOLUTION_INFO](../../../extensibility/debugger/reference/bp-error-resolution-info.md)
- [EnumErrorBreakpoints](../../../extensibility/debugger/reference/idebugpendingbreakpoint2-enumerrorbreakpoints.md)
