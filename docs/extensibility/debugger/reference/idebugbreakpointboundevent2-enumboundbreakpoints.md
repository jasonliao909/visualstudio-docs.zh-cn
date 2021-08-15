---
description: 创建绑定到此事件的断点的枚举器。
title: IDebugBreakpointBoundEvent2：：EnumBoundBreakpoints |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugBreakpointBoundEvent2::EnumBoundBreakpoints
helpviewer_keywords:
- IDebugBreakpointBoundEvent2::EnumBoundBreakpoints
ms.assetid: 1f588feb-522e-488d-be92-7bc19b9e3688
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 68358ca3153ddff04e64ecf7e199616ce5ed8f8caac851c0f3683aa53aa37ead
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121308085"
---
# <a name="idebugbreakpointboundevent2enumboundbreakpoints"></a>IDebugBreakpointBoundEvent2::EnumBoundBreakpoints
创建绑定到此事件的断点的枚举器。

## <a name="syntax"></a>语法

```cpp
HRESULT EnumBoundBreakpoints( 
    IEnumDebugBoundBreakpoints2** ppEnum
);
```

```csharp
int EnumBoundBreakpoints( 
    out IEnumDebugBoundBreakpoints2 ppEnum
);
```

## <a name="parameters"></a>参数
`ppEnum`\
[out]返回一个 [IEnumDebugBoundBreakpoints2](../../../extensibility/debugger/reference/ienumdebugboundbreakpoints2.md) 对象，该对象枚举从此事件绑定的所有断点。

## <a name="return-value"></a>返回值
如果成功，则返回 `S_OK`。 如果没有 `S_FALSE` 绑定断点，则返回 ;否则返回错误代码。

## <a name="remarks"></a>备注
绑定断点列表适用于绑定到此事件的断点，并且可能不是从挂起断点绑定的整个断点列表。 若要获取绑定到挂起断点的所有断点的列表，请调用 [GetPendingBreakpoint](../../../extensibility/debugger/reference/idebugbreakpointboundevent2-getpendingbreakpoint.md) 方法获取关联的 [IDebugPendingBreakpoint2](../../../extensibility/debugger/reference/idebugpendingbreakpoint2.md) 对象，然后调用 [EnumBoundBreakpoints](../../../extensibility/debugger/reference/idebugpendingbreakpoint2-enumboundbreakpoints.md) 方法获取 [IEnumDebugBoundBreakpoints2](../../../extensibility/debugger/reference/ienumdebugboundbreakpoints2.md) 对象，该对象包含挂起断点的所有绑定断点。

## <a name="example"></a>示例
下面的示例演示如何为公开 [IDebugBreakpointBoundEvent2](../../../extensibility/debugger/reference/idebugbreakpointboundevent2.md)接口的 **CBreakpointSetDebugEventBase** 对象实现此方法。

```cpp
STDMETHODIMP CBreakpointSetDebugEventBase::EnumBoundBreakpoints(
    IEnumDebugBoundBreakpoints2 **ppEnum)
{
    HRESULT hRes = E_FAIL;

    if ( ppEnum )
    {
        if ( m_pEnumBound )
        {
            hRes = m_pEnumBound->Clone(ppEnum);

            if ( EVAL(S_OK == hRes) )
                (*ppEnum)->Reset();
        }
        else
            hRes = E_FAIL;
    }
    else
        hRes = E_INVALIDARG;

    return ( hRes );
}
```

## <a name="see-also"></a>另请参阅
- [IDebugBreakpointBoundEvent2](../../../extensibility/debugger/reference/idebugbreakpointboundevent2.md)
- [IEnumDebugBoundBreakpoints2](../../../extensibility/debugger/reference/ienumdebugboundbreakpoints2.md)
- [GetPendingBreakpoint](../../../extensibility/debugger/reference/idebugbreakpointboundevent2-getpendingbreakpoint.md)
- [IDebugPendingBreakpoint2](../../../extensibility/debugger/reference/idebugpendingbreakpoint2.md)
- [EnumBoundBreakpoints](../../../extensibility/debugger/reference/idebugpendingbreakpoint2-enumboundbreakpoints.md)
