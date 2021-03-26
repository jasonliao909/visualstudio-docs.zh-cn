---
description: 删除断点。
title: IDebugBoundBreakpoint2：:D e) |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugBoundBreakpoint2::Delete
helpviewer_keywords:
- Delete method
- IDebugBoundBreakpoint2::Delete method
ms.assetid: 7088dc66-f24a-446f-a52a-397d02457a41
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: a6dbe1877144813ab36c437f8163dc64fcdcc78d
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/25/2021
ms.locfileid: "105088960"
---
# <a name="idebugboundbreakpoint2delete"></a>IDebugBoundBreakpoint2::Delete
删除断点。

## <a name="syntax"></a>语法

```cpp
HRESULT Delete( 
    void 
);
```

```csharp
int Delete();
```

## <a name="return-value"></a>返回值
如果成功， `S_OK` 则返回; 否则返回错误代码。 `E_BP_DELETED`如果绑定断点对象的状态设置为 `BPS_DELETED` [BP_STATE](../../../extensibility/debugger/reference/bp-state.md)枚举)  (部分，则返回。

## <a name="example"></a>示例
下面的示例演示如何为 `CBoundBreakpoint` 公开 [IDebugBoundBreakpoint2](../../../extensibility/debugger/reference/idebugboundbreakpoint2.md) 接口的简单对象实现此方法。

```
HRESULT CBoundBreakpoint::Delete(void)
{
    HRESULT hr;

    // Verify that the bound breakpoint has not been
    // deleted. If deleted, then return hr = E_BP_DELETED.
    if (m_state != BPS_DELETED)
    {
        m_pInterp->RemoveBreakpoint(m_sbstrDoc, this);

        // Change the state of the breakpoint to BPS_DELETED.
        m_state = BPS_DELETED;
        hr = S_OK;
    }
    else
    {
        hr = E_BP_DELETED;
    }

    return hr;
}
```

## <a name="see-also"></a>另请参阅
- [IDebugBoundBreakpoint2](../../../extensibility/debugger/reference/idebugboundbreakpoint2.md)
- [BP_STATE](../../../extensibility/debugger/reference/bp-state.md)
