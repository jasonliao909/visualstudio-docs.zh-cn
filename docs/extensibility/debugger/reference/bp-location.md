---
description: 指定用于描述断点位置的结构类型。
title: BP_LOCATION |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- BP_LOCATION
helpviewer_keywords:
- BP_LOCATION union
ms.assetid: ed1e874c-f289-4c31-8b6c-04dde03ad0f5
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 23319123066e4c78525f2fb57b07da982a8aef1763d97a66a123d44d876e2eba
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121434472"
---
# <a name="bp_location"></a>BP_LOCATION
指定用于描述断点位置的结构类型。

## <a name="syntax"></a>语法

```cpp
typedef struct _BP_LOCATION {
    BP_LOCATION_TYPE bpLocationType;
    union {
        BP_LOCATION_CODE_FILE_LINE   bplocCodeFileLine;
        BP_LOCATION_CODE_FUNC_OFFSET bplocCodeFuncOffset;
        BP_LOCATION_CODE_CONTEXT     bplocCodeContext;
        BP_LOCATION_CODE_STRING      bplocCodeString;
        BP_LOCATION_CODE_ADDRESS     bplocCodeAddress;
        BP_LOCATION_DATA_STRING      bplocDataString;
        BP_LOCATION_RESOLUTION       bplocResolution;
        DWORD                        unused;
    } bpLocation;
} BP_LOCATION;
```

```csharp
public struct BP_LOCATION {
    public uint   bpLocationType;
    public IntPtr unionmember1;
    public IntPtr unionmember2;
    public IntPtr unionmember3;
    public IntPtr unionmember4;
};
```

## <a name="members"></a>成员
`bpLocationType`\
一个来自 [BP_LOCATION_TYPE](../../../extensibility/debugger/reference/bp-location-type.md) 枚举的值，该值用于解释 `bpLocation` 联合或 `unionmemberX` 成员。

`bpLocation`.`bplocCodeFileLine`\
[仅 C++]如果 为[，BP_LOCATION_CODE_FILE_LINE](../../../extensibility/debugger/reference/bp-location-code-file-line.md)结构 `bpLocationType`  =  `BPLT_CODE_FILE_LINE` 。

`bpLocation.bplocCodeFuncOffset`\
[仅 C++]如果 为[，BP_LOCATION_CODE_FUNC_OFFSET](../../../extensibility/debugger/reference/bp-location-code-func-offset.md)结构 `bpLocationType`  =  `BPLT_CODE_FUNC_OFFSET` 。

`bpLocation.bplocCodeContext`\
[仅 C++]如果 为[，BP_LOCATION_CODE_CONTEXT](../../../extensibility/debugger/reference/bp-location-code-context.md)结构 `bpLocationType`  =  `BPLT_CODE_CONTEXT` 。

`bpLocation.bplocCodeString`\
[仅 C++]如果 为[，BP_LOCATION_CODE_STRING](../../../extensibility/debugger/reference/bp-location-code-string.md)结构 `bpLocationType`  =  `BPLT_CODE_STRING` 。

`bpLocation.bplocCodeAddress`\
[仅 C++]如果 为[，BP_LOCATION_CODE_ADDRESS](../../../extensibility/debugger/reference/bp-location-code-address.md)结构 `bpLocationType`  =  `BPLT_CODE_ADDRESS` 。

`bpLocation.bplocDataString`\
[仅 C++]如果 为[，BP_LOCATION_DATA_STRING](../../../extensibility/debugger/reference/bp-location-data-string.md)结构 `bpLocationType`  =  `BPLT_DATA_STRING` 。

`bpLocation.bplocResolution`\
[仅 C++]如果 为[，BP_LOCATION_RESOLUTION](../../../extensibility/debugger/reference/bp-location-resolution.md)结构 `bpLocationType`  =  `BPLT_RESOLUTION` 。

`unionmember1`\
[仅 C# ]请参阅有关解释方式的备注。

`unionmember2`\
[仅 C# ]请参阅有关解释方式的备注。

`unionmember3`\
[仅 C# ]请参阅有关解释方式的备注。

`unionmember4`\
[仅 C# ]请参阅有关解释方式的备注。

## <a name="remarks"></a>备注
此结构是 BP_REQUEST_INFO[和](../../../extensibility/debugger/reference/bp-request-info.md)BP_REQUEST_INFO2[的成员。](../../../extensibility/debugger/reference/bp-request-info2.md)

 [仅 C# ] `unionmemberX` 成员根据下表进行解释。 向下查找值的左列，然后查看其他列以确定每个成员表示 `bpLocationType` `unionmemberX` 什么，并相应地封 `unionmemberX` 送 。 有关在 C# 中解释此结构的一部分的方法，请参阅示例。

|`bpLocationType`|`unionmember1`|`unionmember2`|`unionmember3`|`unionmember4`|
|----------------------|--------------------|--------------------|--------------------|--------------------|
|`BPLT_CODE_FILE_LINE`|`string` (上下文) |[IDebugDocumentPosition2](../../../extensibility/debugger/reference/idebugdocumentposition2.md)|-|-|
|`BPLT_CODE_FUNC_OFFSET`|`string` (上下文) |[IDebugFunctionPosition2](../../../extensibility/debugger/reference/idebugfunctionposition2.md)|-|-|
|`BPLT_CODE_CONTEXT`|[IDebugCodeContext2](../../../extensibility/debugger/reference/idebugcodecontext2.md)|-|-|-|
|`BPLT_CODE_STRING`|`string` (上下文) |`string` (条件表达式) |-|-|
|`BPLT_CODE_ADDRESS`|`string` (上下文) |`string` (模块 URL) |`string` (函数名称) |`string` (地址) |
|`BPLT_DATA_STRING`|[IDebugThread2](../../../extensibility/debugger/reference/idebugthread2.md)|`string` (上下文) |`string` (数据表达式) |`uint` (元素数) |
|`BPLT_RESOLUTION`|[IDebugBreakpointResolution2](../../../extensibility/debugger/reference/idebugbreakpointresolution2.md)|-|-|-|

## <a name="example"></a>示例
此示例演示如何在 `BP_LOCATION` C# 中解释 类型的 `BPLT_DATA_STRING` 结构。 此特定类型演示如何以所有可能的格式解释所有四个成员 (对象、字符串和 `unionmemberX` 数字) 。

```csharp
using System;
using System.Runtime.Interop.Services;
using Microsoft.VisualStudio.Debugger.Interop;

namespace MyPackage
{
    public class MyClass
    {
        public void Interpret(BP_LOCATION bp)
        {
            if (bp.bpLocationType == (uint)enum_BP_LOCATION_TYPE.BPLT_DATA_STRING)
            {
                IDebugThread2 pThread = (IDebugThread2)Marshal.GetObjectForIUnknown(bp.unionmember1);
                string context = Marshal.PtrToStringBSTR(bp.unionmember2);
                string dataExpression = Marshal.PtrToStringBSTR(bp.unionmember3);
                uint numElements = (uint)Marshal.ReadInt32(bp.unionmember4);
            }
        }
    }
}
```

## <a name="requirements"></a>要求
标头：msdbg.h

命名空间：Microsoft.VisualStudio.Debugger.Interop

程序集：Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>请参阅
- [结构和联合](../../../extensibility/debugger/reference/structures-and-unions.md)
- [BP_REQUEST_INFO](../../../extensibility/debugger/reference/bp-request-info.md)
- [BP_LOCATION_CODE_FILE_LINE](../../../extensibility/debugger/reference/bp-location-code-file-line.md)
- [BP_LOCATION_CODE_FUNC_OFFSET](../../../extensibility/debugger/reference/bp-location-code-func-offset.md)
- [BP_LOCATION_CODE_CONTEXT](../../../extensibility/debugger/reference/bp-location-code-context.md)
- [BP_LOCATION_CODE_STRING](../../../extensibility/debugger/reference/bp-location-code-string.md)
- [BP_LOCATION_CODE_ADDRESS](../../../extensibility/debugger/reference/bp-location-code-address.md)
- [BP_LOCATION_DATA_STRING](../../../extensibility/debugger/reference/bp-location-data-string.md)
- [BP_LOCATION_RESOLUTION](../../../extensibility/debugger/reference/bp-location-resolution.md)
