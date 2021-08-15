---
description: 使表达式计算器 (企业版) 指定调试器引擎 (DE) 用于读取指标设置的回调接口。
title: IDebugExpressionEvaluator2：： SetCallback |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- IDebugExpressionEvaluator2::SetCallback
- SetCallback
ms.assetid: 31e3a99e-e784-44a3-8b19-cc5ef31ed546
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: cba32a5ab0b934a1ba2426f8b731247bad2598cd77b4ae794e9f682f3c617bde
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121417296"
---
# <a name="idebugexpressionevaluator2setcallback"></a>IDebugExpressionEvaluator2::SetCallback
使表达式计算器 (企业版) 指定调试器引擎 (DE) 用于读取指标设置的回调接口。

## <a name="syntax"></a>语法

```cpp
HRESULT SetCallback (
    IDebugSettingsCallback2* pCallback
);
```

```csharp
int SetCallback (
    IDebugSettingsCallback2 pCallback
);
```

## <a name="parameters"></a>参数
`pCallback`\
中用于设置回调的接口。

## <a name="return-value"></a>返回值
如果成功， `S_OK` 则返回; 否则返回错误代码。

## <a name="remarks"></a>备注
此方法为会话调试管理器提供一个接口，表达式计算器可以使用该接口来读取指标设置。 这对于在计算机上读取度量值非常有用 [!INCLUDE[vsprvs](../../../code-quality/includes/vsprvs_md.md)] 。

## <a name="example"></a>示例
下面的示例演示如何为公开 [IDebugSettingsCallback2](../../../extensibility/debugger/reference/idebugsettingscallback2.md)接口的 **CEE** 对象实现此方法。

```cpp
HRESULT CEE::SetCallback(IDebugSettingsCallback2* in_pCallback)
{
    // precondition
    INVARIANT( this );

    // function body
    if (NULL != this->m_LanguageSpecificUseCases.pfSetCallback)
    {
        EEDomain::fSetCallback DomainVal =
        {
            in_pCallback
        };

        BOOL bSuccess = (*this->m_LanguageSpecificUseCases.pfSetCallback)(DomainVal);
        ENSURE( bSuccess );
    }

    // postcondition
    INVARIANT( this );

    return S_OK;
}
```

## <a name="see-also"></a>另请参阅
- [IDebugExpressionEvaluator2](../../../extensibility/debugger/reference/idebugexpressionevaluator2.md)
