---
description: 为与堆栈帧关联的属性创建一个枚举器，如局部变量。
title: IDebugStackFrame2：： EnumProperties |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugStackFrame2::EnumProperties
helpviewer_keywords:
- IDebugStackFrame2::EnumProperties
ms.assetid: 334bb95e-c7e0-4008-9f06-8c3999e47ee8
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 40298e505f0d3ccbba200c5487a1bf1d6723f5b2
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2021
ms.locfileid: "102145958"
---
# <a name="idebugstackframe2enumproperties"></a>IDebugStackFrame2::EnumProperties
为与堆栈帧关联的属性创建一个枚举器，如局部变量。

## <a name="syntax"></a>语法

```cpp
HRESULT EnumProperties ( 
   DEBUGPROP_INFO_FLAGS      dwFieldSpec,
   UINT                      nRadix,
   REFIID                    refiid,
   DWORD                     dwTimeout,
   ULONG*                    pcelt,
   IEnumDebugPropertyInfo2** ppEnum
);
```

```csharp
int EnumProperties ( 
   enum_DEBUGPROP_INFO_FLAGS   dwFieldSpec,
   uint                        nRadix,
   ref Guid                    refiid,
   uint                        dwTimeout,
   out uint                    pcelt,
   out IEnumDebugPropertyInfo2 ppEnum
);
```

## <a name="parameters"></a>参数
`dwFieldSpec`\
中 [DEBUGPROP_INFO_FLAGS](../../../extensibility/debugger/reference/debugprop-info-flags.md) 枚举中的标志的组合，用于指定要在枚举的 [DEBUG_PROPERTY_INFO](../../../extensibility/debugger/reference/debug-property-info.md) 结构中填充的字段。

`nRadix`\
中用于设置任何数字信息格式的基数。

`refiid`\
中用于选择要枚举的 [DEBUG_PROPERTY_INFO](../../../extensibility/debugger/reference/debug-property-info.md) 结构的筛选器的 GUID，例如 `guidFilterLocals` 。

`dwTimeout`\
中从此方法返回前等待的最长时间（以毫秒为单位）。 使用 `INFINITE` 无限期等待。

`pcelt`\
弄返回枚举的属性数。 这与调用 [GetCount](../../../extensibility/debugger/reference/ienumdebugpropertyinfo2-getcount.md) 方法相同。

`ppEnum`\
弄返回一个 [IEnumDebugPropertyInfo2](../../../extensibility/debugger/reference/ienumdebugpropertyinfo2.md) 对象，该对象包含所需属性的列表。

## <a name="return-value"></a>返回值
 如果成功， `S_OK` 则返回; 否则返回错误代码。

## <a name="remarks"></a>备注
 由于此方法允许使用单个调用来检索所有选定的属性，因此它比按顺序调用 [GetDebugProperty](../../../extensibility/debugger/reference/idebugstackframe2-getdebugproperty.md) 和 [EnumChildren](../../../extensibility/debugger/reference/idebugproperty2-enumchildren.md) 方法快。

## <a name="see-also"></a>另请参阅
- [IDebugStackFrame2](../../../extensibility/debugger/reference/idebugstackframe2.md)
- [DEBUGPROP_INFO_FLAGS](../../../extensibility/debugger/reference/debugprop-info-flags.md)
- [IEnumDebugPropertyInfo2](../../../extensibility/debugger/reference/ienumdebugpropertyinfo2.md)
- [GetCount](../../../extensibility/debugger/reference/ienumdebugpropertyinfo2-getcount.md)
- [GetDebugProperty](../../../extensibility/debugger/reference/idebugstackframe2-getdebugproperty.md)
- [EnumChildren](../../../extensibility/debugger/reference/idebugproperty2-enumchildren.md)
