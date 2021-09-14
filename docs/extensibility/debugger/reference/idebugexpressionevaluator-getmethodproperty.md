---
description: 此方法获取一个属性对象，该对象包含方法的局部变量、参数和其他属性。
title: IDebugExpressionEvaluator：：GetMethodProperty |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugExpressionEvaluator::GetMethodProperty
helpviewer_keywords:
- IDebugExpressionEvaluator::GetMethodProperty method
ms.assetid: c394fe4d-eeb6-4feb-828c-098d84a6f1ba
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 0d6ecc116719d37337e127c56a2a026ce5af21c7
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126664518"
---
# <a name="idebugexpressionevaluatorgetmethodproperty"></a>IDebugExpressionEvaluator::GetMethodProperty
此方法获取一个属性对象，该对象包含方法的局部变量、参数和其他属性。

## <a name="syntax"></a>语法

```cpp
HRESULT GetMethodProperty( 
   IDebugSymbolProvider* pSymbolProvider,
   IDebugAddress*        pAddress,
   IDebugBinder*         pBinder,
   BOOL                  fIncludeHiddenLocals,
   IDebugProperty2**     ppProperty
);
```

```csharp
int GetMethodProperty(
   IDebugSymbolProvider pSymbolProvider,
   IDebugAddress        pAddress,
   IDebugBinder         pBinder,
   int                  fIncludeHiddenLocals,
   out IDebugProperty2  ppProperty
);
```

## <a name="parameters"></a>parameters
`pSymbolProvider`\
[in]要使用的符号提供程序，以 [IDebugSymbolProvider](../../../extensibility/debugger/reference/idebugsymbolprovider.md) 对象表示。

`pAddress`\
[in]代码中的地址，以 [IDebugAddress](../../../extensibility/debugger/reference/idebugaddress.md) 对象表示，应解析为最近的包含函数。

`pBinder`\
[in]要使用的联编程序，以 [IDebugBinder](../../../extensibility/debugger/reference/idebugbinder.md) 对象表示。

`fIncludeHiddenLocals`\
[in]非零 () 包括隐藏的局部区域;零表示 () `TRUE` `FALSE` 隐藏局部区域

`ppProperty`\
[out]返回表示 [方法的 IDebugProperty2](../../../extensibility/debugger/reference/idebugproperty2.md) 对象。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK` ;否则返回错误代码。

## <a name="remarks"></a>备注
 隐藏局部变量通常是编译器生成的变量。

## <a name="see-also"></a>另请参阅
- [IDebugExpressionEvaluator](../../../extensibility/debugger/reference/idebugexpressionevaluator.md)
- [IDebugSymbolProvider](../../../extensibility/debugger/reference/idebugsymbolprovider.md)
- [IDebugAddress](../../../extensibility/debugger/reference/idebugaddress.md)
- [IDebugBinder](../../../extensibility/debugger/reference/idebugbinder.md)
- [IDebugProperty2](../../../extensibility/debugger/reference/idebugproperty2.md)
