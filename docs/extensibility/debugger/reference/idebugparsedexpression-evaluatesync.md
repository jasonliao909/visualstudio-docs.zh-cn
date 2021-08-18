---
description: 此方法计算已分析的表达式，并选择性地将结果强制转换到另一种数据类型。
title: IDebugParsedExpression：：EvaluateSync |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugParsedExpression::EvaluateSync
helpviewer_keywords:
- IDebugParsedExpression::EvaluateSync method
ms.assetid: 0ea04cfa-de87-4b6c-897e-4572c1a28942
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 192ad990d0f5ad3a12fddc0cc9a56a5c92700d5a
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122153272"
---
# <a name="idebugparsedexpressionevaluatesync"></a>IDebugParsedExpression::EvaluateSync
此方法计算已分析的表达式，并选择性地将结果强制转换到另一种数据类型。

## <a name="syntax"></a>语法

```cpp
HRESULT EvaluateSync( 
   DWORD                 dwEvalFlags,
   DWORD                 dwTimeout,
   IDebugSymbolProvider* pSymbolProvider,
   IDebugAddress*        pAddress,
   IDebugBinder*         pBinder,
   BSTR                  bstrResultType,
   IDebugProperty2**     ppResult
);
```

```csharp
int EvaluateSync(
   uint                 dwEvalFlags,
   uint                 dwTimeout,
   IDebugSymbolProvider pSymbolProvider,
   IDebugAddress        pAddress,
   IDebugBinder         pBinder,
   string               bstrResultType,
   out IDebugProperty2  ppResult
);
```

## <a name="parameters"></a>参数
`dwEvalFlags`\
[in] [用于控制表达式计算方式的 EVALFLAGS](../../../extensibility/debugger/reference/evalflags.md) 常量的组合。

`dwTimeout`\
[in]指定在从此方法返回之前等待的最大时间（以毫秒为单位）。 使用 `INFINITE` 无限期等待。

`pSymbolProvider`\
[in]符号提供程序，以 [IDebugSymbolProvider](../../../extensibility/debugger/reference/idebugsymbolprovider.md) 接口表示。

`pAddress`\
[in]方法中的当前执行位置，以 [IDebugAddress](../../../extensibility/debugger/reference/idebugaddress.md) 接口表示。

`pBinder`\
[in]绑定器，表示为 [IDebugBinder](../../../extensibility/debugger/reference/idebugbinder.md) 接口。

`bstrResultType`\
[in]结果应强制转换到的类型。 此参数可以是 null 值。

`ppResult`\
[out]返回表示计算结果的 [IDebugProperty2](../../../extensibility/debugger/reference/idebugproperty2.md) 接口。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK` ;否则返回错误代码。

## <a name="remarks"></a>备注
 表达式计算上下文由 提供，因此可以确定包含的方法，然后使用语言范围规则来确定表达式中 `pAddress` 符号的值。

## <a name="see-also"></a>请参阅
- [IDebugSymbolProvider](../../../extensibility/debugger/reference/idebugsymbolprovider.md)
- [IDebugBinder](../../../extensibility/debugger/reference/idebugbinder.md)
- [IDebugAddress](../../../extensibility/debugger/reference/idebugaddress.md)
- [IDebugProperty2](../../../extensibility/debugger/reference/idebugproperty2.md)
- [IDebugParsedExpression](../../../extensibility/debugger/reference/idebugparsedexpression.md)
