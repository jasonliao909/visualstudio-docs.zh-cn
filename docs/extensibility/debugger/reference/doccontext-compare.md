---
description: 指定比较两个文档上下文的条件。
title: DOCCONTEXT_COMPARE |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- DOCCONTEXT_COMPARE
helpviewer_keywords:
- DOCCONTEXT_COMPARE enumeration
ms.assetid: ed947c34-b07e-4b69-8381-b6e7cb842862
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 3329c805ab1e5f6f45f82a2789fdec242c83931f18e525a50fd883f3601c63da
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121360815"
---
# <a name="doccontext_compare"></a>DOCCONTEXT_COMPARE
指定比较两个文档上下文的条件。

## <a name="syntax"></a>语法

```cpp
enum enum_DOCCONTEXT_COMPARE {
    DOCCONTEXT_EQUAL         = 0x0001,
    DOCCONTEXT_LESS_THAN     = 0x0002,
    DOCCONTEXT_GREATER_THAN  = 0x0003,
    DOCCONTEXT_SAME_DOCUMENT = 0x0004
};
typedef DWORD DOCCONTEXT_COMPARE;
```

```csharp
enum enum_DOCCONTEXT_COMPARE {
    DOCCONTEXT_EQUAL         = 0x0001,
    DOCCONTEXT_LESS_THAN     = 0x0002,
    DOCCONTEXT_GREATER_THAN  = 0x0003,
    DOCCONTEXT_SAME_DOCUMENT = 0x0004
};
```

## <a name="fields"></a>字段
`DOCCONTEXT_EQUAL`\
查找列表中与目标文档上下文相等的第一个文档上下文。

`DOCCONTEXT_LESS_THAN`\
查找列表中小于目标文档上下文的第一个文档上下文。

`DOCCONTEXT_GREATER_THAN`\
查找列表中大于目标文档上下文的第一个文档上下文。

`DOCCONTEXT_SAME_DOCUMENT`\
查找列表中与目标文档上下文位于同一文档中的第一个文档上下文。

## <a name="remarks"></a>备注
作为参数传递给 [Compare](../../../extensibility/debugger/reference/idebugdocumentcontext2-compare.md) 方法。

这些值用于指定用于查找列表中第一个文档上下文的比较条件。 为文档上下文提供一个文档上下文列表，以通过 方法将其 `IDebugDocumentContext2::Compare` 与自身进行比较。 然后返回列表中要返回比较运算符的第 `true` 一个文档上下文。

## <a name="requirements"></a>要求
标头：msdbg.h

命名空间：Microsoft.VisualStudio.Debugger.Interop

程序集：Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>请参阅
- [枚举](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)
- [比较](../../../extensibility/debugger/reference/idebugdocumentcontext2-compare.md)
