---
description: 使调试引擎能够远程读取指标设置。
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
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122126253"
---
# <a name="idebugsettingscallback2"></a>IDebugSettingsCallback2
使调试引擎能够远程读取指标设置。

## <a name="syntax"></a>语法

```
IDebugSettingsCallback2D : IUnknown
```

## <a name="notes-for-implementers"></a>实现者说明
此接口由会话调试管理器的事件回调实现，由调试引擎使用。 还可以在本地使用，而不是 Dbgmetric[d].lib。

## <a name="methods"></a>方法
下表显示了 的方法 `IDebugSettingsCallback2` 。

|方法|说明|
|------------|-----------------|
|[EnumEEs](../../../extensibility/debugger/reference/idebugsettingscallback2-enumees.md)|枚举给定语言和供应商标识符的可用表达式评估器。|
|[GetEELocalObject](../../../extensibility/debugger/reference/idebugsettingscallback2-geteelocalobject.md)|根据给定的指标检索表达式计算器本地对象。|
|[GetEEMetricDword](../../../extensibility/debugger/reference/idebugsettingscallback2-geteemetricdword.md)|检索与表达式计算程序指定指标相对应的值。|
|[GetEEMetricFile](../../../extensibility/debugger/reference/idebugsettingscallback2-geteemetricfile.md)|根据给定的名称或指标检索表达式评估器指标文件。|
|[GetEEMetricGuid](../../../extensibility/debugger/reference/idebugsettingscallback2-geteemetricguid.md)|根据表达式评估器指标的名称检索其唯一标识符。|
|[GetEEMetricString](../../../extensibility/debugger/reference/idebugsettingscallback2-geteemetricstring.md)|根据表达式评估器指标的名称检索其值字符串。|
|[GetMetricDword](../../../extensibility/debugger/reference/idebugsettingscallback2-getmetricdword.md)|根据指标的名称检索指标的值。|
|[GetMetricGuid](../../../extensibility/debugger/reference/idebugsettingscallback2-getmetricguid.md)|根据指标的名称检索指标的唯一标识符。|
|[GetMetricString](../../../extensibility/debugger/reference/idebugsettingscallback2-getmetricstring.md)|根据指标的名称检索指标的值字符串。|

## <a name="requirements"></a>要求
标头：Msdbg.h

命名空间：Microsoft.VisualStudio.Debugger.Interop

程序集：Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="example"></a>示例
下面的示例演示一个函数，该函数采用 **IDebugSettingsCallback2** 对象作为参数。

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
