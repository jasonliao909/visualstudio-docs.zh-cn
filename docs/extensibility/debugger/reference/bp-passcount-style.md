---
description: 指定与导致断点被发射的断点传递计数关联的条件。
title: BP_PASSCOUNT_STYLE |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- BP_PASSCOUNT_STYLE
helpviewer_keywords:
- BP_PASSCOUNT_STYLE structure
ms.assetid: 0a647047-e2d5-4724-a0b8-68108425ecad
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 02aae6a4ef4939660639004602b539b0f68c4fa2
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122145908"
---
# <a name="bp_passcount_style"></a>BP_PASSCOUNT_STYLE
指定与导致断点被发射的断点传递计数关联的条件。

## <a name="syntax"></a>语法

```cpp
enum enum_BP_PASSCOUNT_STYLE {
    BP_PASSCOUNT_NONE             = 0x0000,
    BP_PASSCOUNT_EQUAL            = 0x0001,
    BP_PASSCOUNT_EQUAL_OR_GREATER = 0x0002,
    BP_PASSCOUNT_MOD              = 0x0003
};
typedef DWORD BP_PASSCOUNT_STYLE;
```

```csharp
public enum enum_BP_PASSCOUNT_STYLE {
    BP_PASSCOUNT_NONE             = 0x0000,
    BP_PASSCOUNT_EQUAL            = 0x0001,
    BP_PASSCOUNT_EQUAL_OR_GREATER = 0x0002,
    BP_PASSCOUNT_MOD              = 0x0003
};
```

## <a name="fields"></a>字段
`BP_PASSCOUNT_NONE`\
指定无断点传递计数样式。

`BP_PASSCOUNT_EQUAL`\
将断点传递计数样式设置为相等。 当断点命中次数等于通过计数时，将触发断点。

`BP_PASSCOUNT_EQUAL_OR_GREATER`\
将断点传递计数样式设置为等于或大于。 断点在命中断点次数等于或大于通过计数时触发。

`BP_PASSCOUNT_MOD`\
指定模数传递计数。 例如，如果传递计数的类型为 ，并且传递计数值为 4，则每次命中计数为 4 的倍数时都会触发 `BP_PASSCOUNT_MOD` 断点。

## <a name="remarks"></a>备注
用于 `stylePassCount` 结构的成员[，BP_PASSCOUNT](../../../extensibility/debugger/reference/bp-passcount.md)[](../../../extensibility/debugger/reference/bp-request-info.md)结构的成员，而该结构又成为BP_REQUEST_INFO BP_REQUEST_INFO2的成员。 [](../../../extensibility/debugger/reference/bp-request-info2.md)

## <a name="requirements"></a>要求
标头：msdbg.h

命名空间：Microsoft.VisualStudio.Debugger.Interop

程序集：Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>请参阅
- [枚举](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)
- [BP_PASSCOUNT](../../../extensibility/debugger/reference/bp-passcount.md)
- [BP_REQUEST_INFO](../../../extensibility/debugger/reference/bp-request-info.md)
- [BP_REQUEST_INFO2](../../../extensibility/debugger/reference/bp-request-info2.md)
