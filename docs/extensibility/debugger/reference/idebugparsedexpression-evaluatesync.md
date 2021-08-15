---
description: 此方法计算分析后的表达式，并选择性地将结果转换为另一种数据类型。
title: IDebugParsedExpression：： EvaluateSync |Microsoft Docs
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
ms.openlocfilehash: c01f674a6bda3ee1dfb229fdabc3123085f7ed466a034880f5fecbed9d89ccc5
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121416997"
---
# <a name="idebugparsedexpressionevaluatesync"></a>IDebugParsedExpression::EvaluateSync
此方法计算分析后的表达式，并选择性地将结果转换为另一种数据类型。

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
中用于控制如何计算表达式的 [EVALFLAGS](../../../extensibility/debugger/reference/evalflags.md) 常量的组合。

`dwTimeout`\
中指定从此方法返回之前要等待的最长时间（以毫秒为单位）。 使用 `INFINITE` 无限期等待。

`pSymbolProvider`\
中符号提供程序，表示为 [IDebugSymbolProvider](../../../extensibility/debugger/reference/idebugsymbolprovider.md) 接口。

`pAddress`\
中方法中的当前执行位置，表示为 [IDebugAddress](../../../extensibility/debugger/reference/idebugaddress.md) 接口。

`pBinder`\
中联编程序，表示为 [IDebugBinder](../../../extensibility/debugger/reference/idebugbinder.md) 接口。

`bstrResultType`\
中结果应强制转换为的类型。 此参数可以为 null 值。

`ppResult`\
弄返回表示求值结果的 [IDebugProperty2](../../../extensibility/debugger/reference/idebugproperty2.md) 接口。

## <a name="return-value"></a>返回值
 如果成功， `S_OK` 则返回; 否则返回错误代码。

## <a name="remarks"></a>备注
 表达式求值上下文是由提供的，这样就可以 `pAddress` 确定包含方法，然后使用语言范围规则确定表达式中的符号值。

## <a name="see-also"></a>另请参阅
- [IDebugSymbolProvider](../../../extensibility/debugger/reference/idebugsymbolprovider.md)
- [IDebugBinder](../../../extensibility/debugger/reference/idebugbinder.md)
- [IDebugAddress](../../../extensibility/debugger/reference/idebugaddress.md)
- [IDebugProperty2](../../../extensibility/debugger/reference/idebugproperty2.md)
- [IDebugParsedExpression](../../../extensibility/debugger/reference/idebugparsedexpression.md)
