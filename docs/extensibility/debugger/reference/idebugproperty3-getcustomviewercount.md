---
description: 获取可用于此属性的自定义查看器数。
title: IDebugProperty3：：GetCustomViewerCount |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProperty3::GetCustomViewerCount
helpviewer_keywords:
- IDebugProperty3::GetCustomViewerCount
ms.assetid: dc5bb3e4-dc85-46e4-98fa-c6be8583b985
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: eb438b6c7585446a7343f01a33c869ac3da508ada0d8f1f9423aa7348a7dcf19
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121415944"
---
# <a name="idebugproperty3getcustomviewercount"></a>IDebugProperty3::GetCustomViewerCount
获取可用于此属性的自定义查看器数。

## <a name="syntax"></a>语法

```cpp
HRESULT GetCustomViewerCount(
    ULONG* pcelt
);
```

```csharp
int GetCustomViewerCount(
    out uint pcelt
);
```

## <a name="parameters"></a>参数
`pcelt`\
[out]可用于此属性的自定义查看器数。

## <a name="return-value"></a>返回值
如果成功，则返回 `S_OK` ;否则返回错误代码。

## <a name="remarks"></a>备注
为了支持类型可视化工具，此方法将调用转发到 [GetCustomViewerCount](../../../extensibility/debugger/reference/ieevisualizerservice-getcustomviewercount.md) 方法。 如果表达式评估器还支持此属性类型的自定义查看器，则此方法会将自定义查看器的数量添加到返回的值中。

有关类型可视化工具与自定义查看器之间的差异的详细信息，请参阅 [类型可视化工具与自定义查看器](../../../extensibility/debugger/type-visualizer-and-custom-viewer.md)。

## <a name="example"></a>示例
下面的示例演示如何为公开 [IDebugProperty3](../../../extensibility/debugger/reference/idebugproperty3.md)接口的 **CProperty** 对象实现此方法。

```cpp
STDMETHODIMP CProperty::GetCustomViewerCount(ULONG* pcelt)
{
    if (pcelt == NULL)
    {
        return E_POINTER;
    }

    if (GetVisualizerService())
    {
        return m_pIEEVisualizerService->GetCustomViewerCount(pcelt);
    }
    else
    {
        return E_NOTIMPL;
    }
}
```

## <a name="see-also"></a>另请参阅
- [IDebugProperty3](../../../extensibility/debugger/reference/idebugproperty3.md)
- [GetCustomViewerCount](../../../extensibility/debugger/reference/ieevisualizerservice-getcustomviewercount.md)
- [类型可视化工具和自定义查看器](../../../extensibility/debugger/type-visualizer-and-custom-viewer.md)
