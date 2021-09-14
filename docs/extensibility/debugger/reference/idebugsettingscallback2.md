---
description: 启用调试引擎以远程读取指标设置。
title: IDebugSettingsCallback2 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- IDebugSettingsCallback2 interface
ms.assetid: 7e525d0b-7d7a-4d1c-8b78-e1398fa922f2
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
ms.openlocfilehash: babc486a4c8d683a3557b602273bc2e165a49420
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126664452"
---
# <a name="idebugsettingscallback2"></a>IDebugSettingsCallback2
启用调试引擎以远程读取指标设置。

## <a name="syntax"></a>语法

```
IDebugSettingsCallback2D : IUnknown
```

## <a name="notes-for-implementers"></a>实施者注意事项
此接口由会话调试管理器的事件回调实现，由调试引擎使用。 它还可以在本地使用，而不是在 Dbgmetric [d] .lib 中使用。

## <a name="methods"></a>方法
下表显示的方法 `IDebugSettingsCallback2` 。

|方法|说明|
|------------|-----------------|
|[EnumEEs](../../../extensibility/debugger/reference/idebugsettingscallback2-enumees.md)|根据语言和供应商标识符枚举可用的表达式计算器。|
|[GetEELocalObject](../../../extensibility/debugger/reference/idebugsettingscallback2-geteelocalobject.md)|检索给定度量值的表达式计算器本地对象。|
|[GetEEMetricDword](../../../extensibility/debugger/reference/idebugsettingscallback2-geteemetricdword.md)|检索一个值，该值对应于表达式计算器的指定指标。|
|[GetEEMetricFile](../../../extensibility/debugger/reference/idebugsettingscallback2-geteemetricfile.md)|检索给定名称或度量值的表达式计算器度量值文件。|
|[GetEEMetricGuid](../../../extensibility/debugger/reference/idebugsettingscallback2-geteemetricguid.md)|根据给定的名称检索表达式计算器度量值的唯一标识符。|
|[GetEEMetricString](../../../extensibility/debugger/reference/idebugsettingscallback2-geteemetricstring.md)|根据给定的名称检索表达式计算器指标的值字符串。|
|[GetMetricDword](../../../extensibility/debugger/reference/idebugsettingscallback2-getmetricdword.md)|根据给定的名称检索度量值。|
|[GetMetricGuid](../../../extensibility/debugger/reference/idebugsettingscallback2-getmetricguid.md)|根据给定的名称检索指标的唯一标识符。|
|[GetMetricString](../../../extensibility/debugger/reference/idebugsettingscallback2-getmetricstring.md)|根据给定的名称检索指标的值字符串。|

## <a name="requirements"></a>要求
标头： Msdbg

命名空间： VisualStudio

程序集： Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="example"></a>示例
下面的示例演示了一个将 **IDebugSettingsCallback2** 对象作为参数的函数。

```cpp
HRESULT GetDebugSettingsCallback (IDebugSettingsCallback2 **ppCallback)
{
    HRESULT hRes = E_FAIL;

    if ( ppCallback )
    {
        if ( EVAL(m_pdec) )
            hRes = m_pdec->QueryInterface(IID_IDebugSettingsCallback2, (void **)ppCallback);
        else
            hRes = E_FAIL;
    }
    else
        hRes = E_INVALIDARG;

    return ( hRes );
}
```
