---
description: 枚举 IDebugField 对象可以包含的其他类型的字段。
title: FIELD_KIND_EX |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- FIELD_KIND_EX enumeration
ms.assetid: 922c3208-1e94-485f-b70a-3bc96affeff8
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 158ebeea620ebb66be02d6b707d326d727411012f79abd91b4b1578be048a0ad
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121452311"
---
# <a name="field_kind_ex"></a>FIELD_KIND_EX
枚举 [IDebugField](../../../extensibility/debugger/reference/idebugfield.md) 对象可以包含的其他类型的字段。 此枚举扩展了 [FIELD_KIND](../../../extensibility/debugger/reference/field-kind.md) 枚举。

## <a name="syntax"></a>语法

```cpp
enum enum_FIELD_KIND_EX
{
    FIELD_KIND_EX_NONE = 0,
    FIELD_TYPE_EX_METHODVAR = 0x1,
    FIELD_TYPE_EX_CLASSVAR = 0x2
};
typedef DWORD FIELD_KIND_EX;
```

```csharp
public enum enum_FIELD_KIND_EX
{
    FIELD_KIND_EX_NONE = 0,
    FIELD_TYPE_EX_METHODVAR = 0x1,
    FIELD_TYPE_EX_CLASSVAR = 0x2
};
```

## <a name="fields"></a>字段
`FIELD_KIND_EX_NONE`\
字段不包含扩展类型。

`FIELD_TYPE_EX_METHODVAR`\
字段包含方法变量。

`FIELD_TYPE_EX_CLASSVAR`\
字段包含类变量。

## <a name="requirements"></a>要求
标头：Sh.h

命名空间：Microsoft.VisualStudio.Debugger.Interop

程序集：Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>请参阅
- [枚举](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)
- [GetExtendedKind](../../../extensibility/debugger/reference/idebugextendedfield-getextendedkind.md)
