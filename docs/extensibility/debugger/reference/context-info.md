---
description: 此结构描述内存上下文或代码上下文。
title: CONTEXT_INFO |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- CONTEXT_INFO
helpviewer_keywords:
- CONTEXT_INFO structure
ms.assetid: 6b513f4e-e7b0-4969-adf0-2205ccc1e09b
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 1f0e47ae5651f928894d42e2e06c015315fa037a
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122145544"
---
# <a name="context_info"></a>CONTEXT_INFO
此结构描述内存上下文或代码上下文。

## <a name="syntax"></a>语法

```cpp
typedef struct _tagCONTEXT_INFO {
    CONTEXT_INFO_FIELDS dwFields;
    BSTR                bstrModuleUrl;
    BSTR                bstrFunction;
    TEXT_POSITION       posFunctionOffset;
    BSTR                bstrAddress;
    BSTR                bstrAddressOffset;
    BSTR                bstrAddressAbsolute;
} CONTEXT_INFO;
```

```csharp
public struct CONTEXT_INFO {
    public uint          dwFields;
    public string        bstrModuleUrl;
    public string        bstrFunction;
    public TEXT_POSITION posFunctionOffset;
    public string        bstrAddress;
    public string        bstrAddressOffset;
    public string        bstrAddressAbsolute;
};
```

## <a name="members"></a>成员
`dwFields`\
来自该参数的标志 [CONTEXT_INFO_FIELDS](../../../extensibility/debugger/reference/context-info-fields.md) 枚举，用于指定填充哪些字段<strong>。</strong>

`bstrModuleUrl`\
上下文所在的模块的名称。

`bstrFunction`\
上下文所在的函数名称。

`posFunctionOffset`\
一 [TEXT_POSITION](../../../extensibility/debugger/reference/text-position.md) 结构，用于标识与代码上下文关联的函数的行偏移量和列偏移量。

`bstrAddress`\
代码中给定上下文所在的地址。

`bstrAddressOffset`\
给定上下文所在的代码中地址的偏移量。

`bstrAddressAbsolute`\
给定上下文所在的内存中的绝对地址。

## <a name="remarks"></a>备注
此结构从对 [GetInfo](../../../extensibility/debugger/reference/idebugmemorycontext2-getinfo.md) 方法的调用返回。

此结构的典型用途是支持 **内存调试窗口** 。

## <a name="requirements"></a>要求
标头：msdbg.h

命名空间：Microsoft.VisualStudio.Debugger.Interop

程序集：Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>请参阅
- [结构和联合](../../../extensibility/debugger/reference/structures-and-unions.md)
- [GetInfo](../../../extensibility/debugger/reference/idebugmemorycontext2-getinfo.md)
- [CONTEXT_INFO_FIELDS](../../../extensibility/debugger/reference/context-info-fields.md)
- [TEXT_POSITION](../../../extensibility/debugger/reference/text-position.md)
