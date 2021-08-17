---
description: 描述错误断点（包括位置、程序、线程）的解决方法。
title: BP_ERROR_RESOLUTION_INFO |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- BP_ERROR_RESOLUTION_INFO
helpviewer_keywords:
- BP_ERROR_RESOLUTION_INFO structure
ms.assetid: a6b83242-5728-4716-80f3-840c96d59c6c
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 3e678d3089032d93eb2974123d9a5c2153c97e95
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122073170"
---
# <a name="bp_error_resolution_info"></a>BP_ERROR_RESOLUTION_INFO
描述错误断点（包括位置、程序、线程）的解决方法。

## <a name="syntax"></a>语法

```cpp
typedef struct _BP_ERROR_RESOLUTION_INFO {
    BPERESI_FIELDS         dwFields;
    BP_RESOLUTION_LOCATION bpResLocation;
    IDebugProgram2*        pProgram;
    IDebugThread2*         pThread;
    BSTR                   bstrMessage;
    BP_ERROR_TYPE          dwType;
} BP_ERROR_RESOLUTION_INFO;
```

```csharp
public struct BP_ERROR_RESOLUTION_INFO {
    public uint                   dwFields;
    public BP_RESOLUTION_LOCATION bpResLocation;
    public IDebugProgram2         pProgram;
    public IDebugThread2          pThread;
    public string                 bstrMessage;
    public uint                   dwType;
};
```

## <a name="members"></a>成员
`dwFields`\
指定填充此结构的BPERESI_FIELDS枚举[](../../../extensibility/debugger/reference/bperesi-fields.md)中的值的组合。

`bpResLocation`\
BP_RESOLUTION_LOCATION [联合](../../../extensibility/debugger/reference/bp-resolution-location.md) ，指定断点解析位置。

`pProgram`\
[IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)对象，表示发生断点错误的应用程序。

`pThread`\
[IDebugThread2](../../../extensibility/debugger/reference/idebugthread2.md)对象，表示生成断点错误的应用程序正在其上运行的线程。

`bstrMessage`\
一个字符串，其中包含由此错误解决方法导致的任何警告或错误消息。

`dwType`\
指定断 [点BP_ERROR_TYPE](../../../extensibility/debugger/reference/bp-error-type.md) 类型的值。

## <a name="remarks"></a>备注
此结构从 [GetResolutionInfo 方法](../../../extensibility/debugger/reference/idebugerrorbreakpointresolution2-getresolutioninfo.md) 返回。

## <a name="requirements"></a>要求
标头：msdbg.h

命名空间：Microsoft.VisualStudio.Debugger.Interop

程序集：Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>请参阅
- [结构和联合](../../../extensibility/debugger/reference/structures-and-unions.md)
- [GetResolutionInfo](../../../extensibility/debugger/reference/idebugerrorbreakpointresolution2-getresolutioninfo.md)
- [BPRESI_FIELDS](../../../extensibility/debugger/reference/bpresi-fields.md)
- [BP_RESOLUTION_LOCATION](../../../extensibility/debugger/reference/bp-resolution-location.md)
- [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)
- [IDebugThread2](../../../extensibility/debugger/reference/idebugthread2.md)
- [BP_ERROR_TYPE](../../../extensibility/debugger/reference/bp-error-type.md)
