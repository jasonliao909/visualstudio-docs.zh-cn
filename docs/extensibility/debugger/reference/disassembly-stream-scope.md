---
description: 指定反汇编流的作用域。
title: DISASSEMBLY_STREAM_SCOPE |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- DISASSEMBLY_STREAM_SCOPE
helpviewer_keywords:
- DISASSEMBLY_STREAM_SCOPE enumeration
ms.assetid: 43e2b364-cbbe-4755-a7e6-a03f3054c965
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: f33c8489746f857ebb7c9225af6dce73161edad5
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122073079"
---
# <a name="disassembly_stream_scope"></a>DISASSEMBLY_STREAM_SCOPE
指定反汇编流的作用域。

## <a name="syntax"></a>语法

```cpp
enum enum_DISASSEMBLY_STREAM_SCOPE {
    DSS_HUGE     = 0x10000000,
    DSS_FUNCTION = 0x0001,
    DSS_MODULE   = (DSS_HUGE) | 0x0002,
    DSS_ALL      = (DSS_HUGE) | 0x0003
};
typedef DWORD DISASSEMBLY_STREAM_SCOPE;
```

```csharp
public enum enum_DISASSEMBLY_STREAM_SCOPE {
    DSS_HUGE     = 0x10000000,
    DSS_FUNCTION = 0x0001,
    DSS_MODULE   = (DSS_HUGE) | 0x0002,
    DSS_ALL      = (DSS_HUGE) | 0x0003
};
```

## <a name="fields"></a>字段
`DSS_HUGE`\
指定反汇编代码上下文生成的输出比客户端通常在单个调用中检索的输出要多。

`DSS_FUNCTION`\
指定应反汇编代码上下文包含的函数。 指定反汇编流表示由 [GetScope](../../../extensibility/debugger/reference/idebugdisassemblystream2-getscope.md) 方法返回的函数。

`DSS_MODULE`\
由 方法 `IDebugDisassemblyStream2::GetScope` 返回时， 指定反汇编流表示模块。

`DSS_ALL`\
指定整个地址空间的反汇编。

## <a name="remarks"></a>备注
作为参数传递给 [GetDisassemblyStream](../../../extensibility/debugger/reference/idebugprogram2-getdisassemblystream.md) 方法，由 [GetScope](../../../extensibility/debugger/reference/idebugdisassemblystream2-getscope.md) 方法返回。

这些值可以与位 合并 `OR` 。

## <a name="requirements"></a>要求
标头：msdbg.h

命名空间：Microsoft.VisualStudio.Debugger.Interop

程序集：Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>请参阅
- [枚举](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)
- [GetDisassemblyStream](../../../extensibility/debugger/reference/idebugprogram2-getdisassemblystream.md)
- [GetScope](../../../extensibility/debugger/reference/idebugdisassemblystream2-getscope.md)
