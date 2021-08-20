---
description: 包含实现断点所需的信息。
title: BP_REQUEST_INFO |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- BP_REQUEST_INFO
helpviewer_keywords:
- BP_REQUEST_INFO structure
ms.assetid: 42a31412-5b6b-47fe-a762-0c2bc769e1cc
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: fe85c279173932adc3ccc4dab98cc5b0727d1b3b
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122145882"
---
# <a name="bp_request_info"></a>BP_REQUEST_INFO
包含实现断点所需的信息。

## <a name="syntax"></a>语法

```cpp
typedef struct _BP_REQUEST_INFO {
    BPREQI_FIELDS   dwFields;
    GUID            guidLanguage;
    BP_LOCATION     bpLocation;
    IDebugProgram2* pProgram;
    BSTR            bstrProgramName;
    IDebugThread2*  pThread;
    BSTR            bstrThreadName;
    BP_CONDITION    bpCondition;
    BP_PASSCOUNT    bpPassCount;
    BP_FLAGS        dwFlags;
} BP_REQUEST_INFO;
```

```csharp
public struct BP_REQUEST_INFO {
    public uint           dwFields;
    public Guid           guidLanguage;
    public BP_LOCATION    bpLocation;
    public IDebugProgram2 pProgram;
    public string         bstrProgramName;
    public IDebugThread2  pThread;
    public string         bstrThreadName;
    public BP_CONDITION   bpCondition;
    public BP_PASSCOUNT   bpPassCount;
    public uint           dwFlags;
};
```

## <a name="members"></a>成员
`dwFields`\
[BPREQI_FIELDS](../../../extensibility/debugger/reference/bpreqi-fields.md)枚举中的标志的组合，用于指定要填写的字段。

`guidLanguage`\
语言 GUID。

`bpLocation`\
[BP_LOCATION](../../../extensibility/debugger/reference/bp-location.md)结构，它指定断点位置的类型。

`pProgram`\
[IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)对象，表示在其中发生断点的应用程序。

`bstrProgramName`\
发生断点的应用程序的名称。

`pThread`\
[IDebugThread2](../../../extensibility/debugger/reference/idebugthread2.md)对象，表示在其中发生断点的线程。

`bstrThreadName`\
发生断点的线程的名称。

`bpCondition`\
描述引发断点的条件的 [BP_CONDITION](../../../extensibility/debugger/reference/bp-condition.md) 结构。

`bpPassCount`\
[BP_PASSCOUNT](../../../extensibility/debugger/reference/bp-passcount.md)结构，它包含断点的传递计数信息。

`dwFlags`\
[BP_FLAGS](../../../extensibility/debugger/reference/bp-flags.md)枚举中的标志的组合，该枚举指定请求的断点的标志。

## <a name="remarks"></a>备注
此结构由 [GetRequestInfo](../../../extensibility/debugger/reference/idebugbreakpointrequest2-getrequestinfo.md) 方法返回。

如果需要获取调试引擎供应商 GUID、断点约束或跟踪点，请参阅 [BP_REQUEST_INFO2](../../../extensibility/debugger/reference/bp-request-info2.md) 结构。

## <a name="requirements"></a>要求
标头： msdbg

命名空间： VisualStudio

程序集： Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>请参阅
- [结构和联合](../../../extensibility/debugger/reference/structures-and-unions.md)
- [GetRequestInfo](../../../extensibility/debugger/reference/idebugbreakpointrequest2-getrequestinfo.md)
- [BPREQI_FIELDS](../../../extensibility/debugger/reference/bpreqi-fields.md)
- [BP_LOCATION](../../../extensibility/debugger/reference/bp-location.md)
- [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)
- [IDebugThread2](../../../extensibility/debugger/reference/idebugthread2.md)
- [BP_CONDITION](../../../extensibility/debugger/reference/bp-condition.md)
- [BP_PASSCOUNT](../../../extensibility/debugger/reference/bp-passcount.md)
- [BP_FLAGS](../../../extensibility/debugger/reference/bp-flags.md)
- [BP_REQUEST_INFO2](../../../extensibility/debugger/reference/bp-request-info2.md)
