---
description: 启用表达式计算 (企业版) 指定调试器引擎在 DE (将) 用于读取指标设置的回调接口。
title: IDebugExpressionEvaluator2：：SetCallback |Microsoft Docs
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
ms.openlocfilehash: 66d69dc119b23f06efebb9c8d87cf96792118bd1
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122138661"
---
# <a name="idebugexpressionevaluator2setcallback"></a>IDebugExpressionEvaluator2::SetCallback
启用表达式计算 (企业版) 指定调试器引擎在 DE (将) 用于读取指标设置的回调接口。

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
[in]用于设置回调的接口。

## <a name="return-value"></a>返回值
如果成功，则返回 `S_OK` ;否则返回错误代码。

## <a name="remarks"></a>备注
此方法为会话调试管理器提供接口，表达式评估程序可以使用该接口读取指标设置。 它在远程调试中可用于读取计算机上 [!INCLUDE[vsprvs](../../../code-quality/includes/vsprvs_md.md)] 的指标。

## <a name="example"></a>示例
以下示例演示如何为公开 [IDebugSettingsCallback2](../../../extensibility/debugger/reference/idebugsettingscallback2.md)接口的 **CEE** 对象实现此方法。

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

## <a name="see-also"></a>请参阅
- [IDebugExpressionEvaluator2](../../../extensibility/debugger/reference/idebugexpressionevaluator2.md)
