---
description: 获取此断点请求的断点位置类型。
title: IDebugBreakpointRequest2：： GetLocationType |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugBreakpointRequest2::GetLocationType
helpviewer_keywords:
- IDebugBreakpointRequest2::GetLocationType
ms.assetid: b6d14c59-d3aa-48ff-8278-f6b5bba9c2f3
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 888d17e7616162120835ef77cee47a24e149b5cf4902b78b5a819c8f451b6b48
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121452273"
---
# <a name="idebugbreakpointrequest2getlocationtype"></a>IDebugBreakpointRequest2::GetLocationType
获取此断点请求的断点位置类型。

## <a name="syntax"></a>语法

```cpp
HRESULT GetLocationType(
    BP_LOCATION_TYPE* pBPLocationType
);
```

```csharp
int GetLocationType(
    out enum_BP_LOCATION_TYPE pBPLocationType
);
```

## <a name="parameters"></a>参数
`pBPLocationType`\
弄返回 [BP_LOCATION_TYPE](../../../extensibility/debugger/reference/bp-location-type.md) 枚举中的一个值，该值描述此断点请求的位置。

## <a name="return-value"></a>返回值
如果成功， `S_OK` 则返回; 否则返回错误代码。 `E_FAIL`如果 `bpLocation` 关联的[BP_REQUEST_INFO](../../../extensibility/debugger/reference/bp-request-info.md)结构中的字段无效，则返回。

## <a name="example"></a>示例
下面的示例演示如何为 `CDebugBreakpointRequest` 公开[IDebugBreakpointRequest2](../../../extensibility/debugger/reference/idebugbreakpointrequest2.md) 接口的简单对象实现此方法。

```
HRESULT CDebugBreakpointRequest::GetLocationType(BP_LOCATION_TYPE* pBPLocationType)
{
    HRESULT hr;

    if (pBPLocationType)
    {
        // Set default BP_LOCATION_TYPE.
        *pBPLocationType = BPLT_NONE;

        // Check if the BPREQI_BPLOCATION flag is set in BPREQI_FIELDS.
        if (IsFlagSet(m_bpRequestInfo.dwFields, BPREQI_BPLOCATION))
        {
            // Get the new BP_LOCATION_TYPE.
            *pBPLocationType = m_bpRequestInfo.bpLocation.bpLocationType;
            hr = S_OK;
        }
        else
        {
            hr = E_FAIL;
        }
    }
    else
    {
        hr = E_INVALIDARG;
    }

    return hr;
}
```

## <a name="see-also"></a>另请参阅
- [IDebugBreakpointRequest2](../../../extensibility/debugger/reference/idebugbreakpointrequest2.md)
- [BP_LOCATION_TYPE](../../../extensibility/debugger/reference/bp-location-type.md)
- [BPREQI_FIELDS](../../../extensibility/debugger/reference/bpreqi-fields.md)
- [BP_REQUEST_INFO](../../../extensibility/debugger/reference/bp-request-info.md)
