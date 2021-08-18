---
description: 为与堆栈帧关联的属性（如局部变量）创建枚举器。
title: IDebugStackFrame2：：EnumProperties |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugStackFrame2::EnumProperties
helpviewer_keywords:
- IDebugStackFrame2::EnumProperties
ms.assetid: 334bb95e-c7e0-4008-9f06-8c3999e47ee8
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: b917bc14728ee1f8dd37f28bbec42e395455ee35
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122126201"
---
# <a name="idebugstackframe2enumproperties"></a>IDebugStackFrame2::EnumProperties
为与堆栈帧关联的属性（如局部变量）创建枚举器。

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
[in]来自枚举[DEBUGPROP_INFO_FLAGS标志的组合](../../../extensibility/debugger/reference/debugprop-info-flags.md)，指定要填充枚举DEBUG_PROPERTY_INFO结构中的哪些字段。 [](../../../extensibility/debugger/reference/debug-property-info.md)

`nRadix`\
[in]用于设置任何数值信息格式的基数。

`refiid`\
[in]筛选器的 GUID，用于DEBUG_PROPERTY_INFO枚举哪些[](../../../extensibility/debugger/reference/debug-property-info.md)结构，例如 `guidFilterLocals` 。

`dwTimeout`\
[in]从此方法返回之前等待的最大时间（以毫秒为单位）。 使用 `INFINITE` 无限期等待。

`pcelt`\
[out]返回枚举的属性数。 这与调用 [GetCount 方法相同](../../../extensibility/debugger/reference/ienumdebugpropertyinfo2-getcount.md) 。

`ppEnum`\
[out]返回包含 [所需属性列表的 IEnumDebugPropertyInfo2](../../../extensibility/debugger/reference/ienumdebugpropertyinfo2.md) 对象。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK` ;否则返回错误代码。

## <a name="remarks"></a>备注
 因为此方法允许通过单个调用检索所有选定的属性，所以比按顺序调用 [GetDebugProperty](../../../extensibility/debugger/reference/idebugstackframe2-getdebugproperty.md) 和 [EnumChildren](../../../extensibility/debugger/reference/idebugproperty2-enumchildren.md) 方法更快。

## <a name="see-also"></a>请参阅
- [IDebugStackFrame2](../../../extensibility/debugger/reference/idebugstackframe2.md)
- [DEBUGPROP_INFO_FLAGS](../../../extensibility/debugger/reference/debugprop-info-flags.md)
- [IEnumDebugPropertyInfo2](../../../extensibility/debugger/reference/ienumdebugpropertyinfo2.md)
- [GetCount](../../../extensibility/debugger/reference/ienumdebugpropertyinfo2-getcount.md)
- [GetDebugProperty](../../../extensibility/debugger/reference/idebugstackframe2-getdebugproperty.md)
- [EnumChildren](../../../extensibility/debugger/reference/idebugproperty2-enumchildren.md)
