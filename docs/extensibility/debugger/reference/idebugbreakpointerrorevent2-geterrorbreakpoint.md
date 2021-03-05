---
description: 获取一个 IDebugErrorBreakpoint2 对象，该对象描述未绑定断点的原因。
title: IDebugBreakpointErrorEvent2：： GetErrorBreakpoint |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugBreakpointErrorEvent2::GetErrorBreakpoint
helpviewer_keywords:
- IDebugBreakpointErrorEvent2::GetErrorBreakpoint
ms.assetid: e5acfd19-ac17-47f3-a31a-b2aa8baca36d
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: a71442e25d8da31ed7bed0b6e65ae05692eb1e36
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2021
ms.locfileid: "102143384"
---
# <a name="idebugbreakpointerrorevent2geterrorbreakpoint"></a>IDebugBreakpointErrorEvent2::GetErrorBreakpoint
获取一个 [IDebugErrorBreakpoint2](../../../extensibility/debugger/reference/idebugerrorbreakpoint2.md) 对象，该对象描述未绑定断点的原因。

## <a name="syntax"></a>语法

```cpp
HRESULT GetErrorBreakpoint( 
    IDebugErrorBreakpoint2** ppErrorBP
);
```

```csharp
int GetErrorBreakpoint( 
    out IDebugErrorBreakpoint2 ppErrorBP
);
```

## <a name="parameters"></a>参数
`ppErrorBP`\
弄返回描述警告或错误的 [IDebugErrorBreakpoint2](../../../extensibility/debugger/reference/idebugerrorbreakpoint2.md) 对象。

## <a name="return-value"></a>返回值
如果成功， `S_OK` 则返回; 否则返回错误代码。

## <a name="remarks"></a>备注
`IDebugErrorBreakpoint2`获取接口后，调用[GetBreakpointResolution](../../../extensibility/debugger/reference/idebugerrorbreakpoint2-getbreakpointresolution.md)方法以获取[IDebugErrorBreakpointResolution2](../../../extensibility/debugger/reference/idebugerrorbreakpointresolution2.md)对象。 然后，可以使用 [GetResolutionInfo](../../../extensibility/debugger/reference/idebugerrorbreakpointresolution2-getresolutioninfo.md) 方法来确定无效的位置、无效的表达式或挂起断点未绑定的原因（例如，未加载代码）等。

## <a name="example"></a>示例
下面的示例演示如何为公开 [IDebugBreakpointErrorEvent2](../../../extensibility/debugger/reference/idebugbreakpointerrorevent2.md)接口的 **CBreakpointSetDebugEventBase** 对象实现此方法。

```cpp
STDMETHODIMP CBreakpointErrorDebugEventBase::GetErrorBreakpoint(
    IDebugErrorBreakpoint2 **ppbp)
{
    HRESULT hRes = E_FAIL;

    if ( ppbp )
    {
        if ( m_pError )
        {
            *ppbp = m_pError;

            m_pError->AddRef();

            hRes = S_OK;
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
- [IDebugBreakpointErrorEvent2](../../../extensibility/debugger/reference/idebugbreakpointerrorevent2.md)
- [IDebugErrorBreakpointResolution2](../../../extensibility/debugger/reference/idebugerrorbreakpointresolution2.md)
- [IDebugErrorBreakpoint2](../../../extensibility/debugger/reference/idebugerrorbreakpoint2.md)
