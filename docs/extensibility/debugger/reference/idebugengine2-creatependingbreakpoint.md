---
description: 在调试引擎中创建挂起的断点 (DE) 。
title: IDebugEngine2：：CreatePendingBreakpoint |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugEngine2::CreatePendingBreakpoint
helpviewer_keywords:
- IDebugEngine2::CreatePendingBreakpoint
ms.assetid: 92e85b90-a931-48d9-89a7-a6edcb83ae5a
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 31a138104cbaeea8eb0a2313956f5d1bba34db28
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126665422"
---
# <a name="idebugengine2creatependingbreakpoint"></a>IDebugEngine2::CreatePendingBreakpoint
在调试引擎中创建挂起的断点 (DE) 。

## <a name="syntax"></a>语法

```cpp
HRESULT CreatePendingBreakpoint(
    IDebugBreakpointRequest2*  pBPRequest,
    IDebugPendingBreakpoint2** ppPendingBP
);
```

```csharp
int CreatePendingBreakpoint(
    IDebugBreakpointRequest2     pBPRequest,
    out IDebugPendingBreakpoint2 ppPendingBP
);
```

## <a name="parameters"></a>parameters
`pBPRequest`\
[in]描述 [要创建的挂起断点的 IDebugBreakpointRequest2](../../../extensibility/debugger/reference/idebugbreakpointrequest2.md) 对象。

`ppPendingBP`\
[out]返回表示 [挂起断点的 IDebugPendingBreakpoint2](../../../extensibility/debugger/reference/idebugpendingbreakpoint2.md) 对象。

## <a name="return-value"></a>返回值
如果成功，则返回 `S_OK` ;否则返回错误代码。 如果参数无效或不完整，则通常返回 ;如果 参数与 的 DE 支持的任何语言 `E_FAIL` `pBPRequest` 不匹配， `pBPRequest` 则返回 。

## <a name="remarks"></a>备注
挂起的断点实质上是将断点绑定到代码所需的全部信息的集合。 在调用 [Bind](../../../extensibility/debugger/reference/idebugpendingbreakpoint2-bind.md) 方法之前，从此方法返回的挂起断点不会绑定到代码。

对于用户设置的每个挂起断点，会话调试管理器 (SDM) 在每个附加的 DE 中调用此方法。 由 DE 负责验证断点是否对在 DE 中运行的程序有效。

当用户在代码行上设置断点时，DE 可以随意将断点绑定到文档中对应于此代码的最近行。 这样，用户就有可能在多行语句的第一行上设置断点，但将其绑定到最后一行 (其中的所有代码均在调试信息中) 。

## <a name="example"></a>示例
下面的示例演示如何为简单 对象实现 `CProgram` 此方法。 然后，DE 的 实现 `IDebugEngine2::CreatePendingBreakpoint` 可以转发每个程序中方法的此实现的所有调用。

```
HRESULT CProgram::CreatePendingBreakpoint(IDebugBreakpointRequest2* pBPRequest, IDebugPendingBreakpoint2** ppPendingBP)
{
    // Create and initialize the CPendingBreakpoint object.
    CComObject<CPendingBreakpoint> *pPending;
    CComObject<CPendingBreakpoint>::CreateInstance(&pPending);
    pPending->Initialize(pBPRequest, m_pInterp, m_pCallback, m_pEngine);
    return pPending->QueryInterface(ppPendingBP);
}
```

## <a name="see-also"></a>另请参阅
- [IDebugEngine2](../../../extensibility/debugger/reference/idebugengine2.md)
- [绑定](../../../extensibility/debugger/reference/idebugpendingbreakpoint2-bind.md)
- [IDebugBreakpointRequest2](../../../extensibility/debugger/reference/idebugbreakpointrequest2.md)
- [IDebugPendingBreakpoint2](../../../extensibility/debugger/reference/idebugpendingbreakpoint2.md)
