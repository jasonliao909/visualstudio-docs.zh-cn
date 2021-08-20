---
description: 指定断点解析位置的结构。
title: BP_RESOLUTION_LOCATION |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- BP_RESOLUTION_LOCATION
helpviewer_keywords:
- BP_RESOLUTION_LOCATION structure
ms.assetid: 21dc5246-69c1-43e3-855c-9cd4e596c0e6
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: b433f7b58753408c916074539d9d0b6275d1ce17
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122145817"
---
# <a name="bp_resolution_location"></a>BP_RESOLUTION_LOCATION
指定断点解析位置的结构。

## <a name="syntax"></a>语法

```cpp
struct _BP_RESOLUTION_LOCATION {
    BP_TYPE bpType;
    union {
        BP_RESOLUTION_CODE bpresCode;
        BP_RESOLUTION_DATA bpresData;
        int                unused;
    } bpResLocation;
} BP_RESOLUTION_LOCATION;
```

```csharp
public struct BP_RESOLUTION_LOCATION {
    public uint   bpType;
    public IntPtr unionmember1;
    public IntPtr unionmember2;
    public IntPtr unionmember3;
    public uint   unionmember4;
};
```

## <a name="members"></a>成员
`bpType`\
一个来自 [BP_TYPE](../../../extensibility/debugger/reference/bp-type.md) 枚举的值，该值指定如何解释 `bpResLocation` 联合或 `unionmemberX` 成员。

`bpResLocation.bpresCode`\
[仅 C++]如果 为[，BP_RESOLUTION_CODE](../../../extensibility/debugger/reference/bp-resolution-code.md)结构 `bpType`  =  `BPT_CODE` 。

`bpResLocation.bpresData`\
[仅 C++]如果 为[，BP_RESOLUTION_DATA](../../../extensibility/debugger/reference/bp-resolution-data.md)结构 `bpType`  =  `BPT_DATA` 。

`bpResLocation.unused`\
[仅 C++]占位符。

`unionmember1`\
[仅 C# ]请参阅有关解释方式的备注。

`unionmember2`\
[仅 C# ]请参阅有关解释方式的备注。

`unionmember3`\
[仅 C# ]请参阅有关解释方式的备注。

`unionmember4`\
[仅 C# ]请参阅有关解释方式的备注。

## <a name="remarks"></a>备注
此结构是 BP_ERROR_RESOLUTION_INFO[和](../../../extensibility/debugger/reference/bp-error-resolution-info.md)BP_RESOLUTION_INFO[的成员。](../../../extensibility/debugger/reference/bp-resolution-info.md)

 [仅 C# ] `unionmemberX` 成员根据下表进行解释。 在左侧列中查找值，然后跨 ， `bpType` 以确定每个成员表示 `unionmemberX` 什么，并相应地 `unionmemberX` 封送 。 有关在 C# 中解释此结构的方法，请参阅示例。

|`bpLocationType`|`unionmember1`|`unionmember2`|`unionmember3`|`unionmember4`|
|----------------------|--------------------|--------------------|--------------------|--------------------|
|`BPT_CODE`|[IDebugCodeContext2](../../../extensibility/debugger/reference/idebugcodecontext2.md)|-|-|-|
|`BPT_DATA`|`string` (数据表达式) |`string` (函数名称) |`string` (映像名称) |`enum_BP_RES_DATA_FLAGS`|

## <a name="example"></a>示例
此示例演示如何在 `BP_RESOLUTION_LOCATION` C# 中解释 结构。

```csharp
using System;
using System.Runtime.Interop.Services;
using Microsoft.VisualStudio.Debugger.Interop;

namespace MyPackage
{
    public class MyClass
    {
        public void Interpret(BP_RESOLUTION_LOCATION bprl)
        {
            if (bprl.bpType == (uint)enum_BP_TYPE.BPT_CODE)
            {
                IDebugCodeContext2 pContext = (IDebugCodeContext2)Marshal.GetObjectForIUnknown(bp.unionmember1);
            }
            else if (bprl.bpType == (uint)enum_BP_TYPE.BPT_DATA)
            {
                string dataExpression = Marshal.PtrToStringBSTR(bp.unionmember3);
                string functionName = Marshal.PtrToStringBSTR(bp.unionmember2);
                string imageName = Marshal.PtrToStringBSTR(bp.unionmember3);
                enum_BP_RES_DATA_FLAGS numElements = (enum_BP_RES_DATA_FLAGS)bp.unionmember4;
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
- [BP_TYPE](../../../extensibility/debugger/reference/bp-type.md)
- [BP_ERROR_RESOLUTION_INFO](../../../extensibility/debugger/reference/bp-error-resolution-info.md)
- [BP_RESOLUTION_INFO](../../../extensibility/debugger/reference/bp-resolution-info.md)
- [BP_RESOLUTION_CODE](../../../extensibility/debugger/reference/bp-resolution-code.md)
- [BP_RESOLUTION_DATA](../../../extensibility/debugger/reference/bp-resolution-data.md)
- [BP_RES_DATA_FLAGS](../../../extensibility/debugger/reference/bp-res-data-flags.md)
