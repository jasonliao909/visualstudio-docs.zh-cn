---
description: 此方法将表达式字符串转换为已分析的表达式。
title: IDebugExpressionEvaluator：:P arse |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugExpressionEvaluator::Parse
helpviewer_keywords:
- IDebugExpressionEvaluator::Parse method
ms.assetid: e6e31b3a-63a7-4293-bcda-267eb78dffb6
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: ac8b2c7a74801925775642bca9738865c207d14d
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126664517"
---
# <a name="idebugexpressionevaluatorparse"></a>IDebugExpressionEvaluator::Parse
此方法将表达式字符串转换为已分析的表达式。

## <a name="syntax"></a>语法

```cpp
HRESULT Parse( 
   LPCOLESTR                upstrExpression,
   PARSEFLAGS               dwFlags,
   UINT                     nRadix,
   BSTR*                    pbstrError,
   UINT*                    pichError,
   IDebugParsedExpression** ppParsedExpression
);
```

```csharp
int Parse(
   string                     upstrExpression,
   enum_PARSEFLAGS            dwFlags,
   uint                       nRadix,
   out string                 pbstrError,
   out uint                   pichError,
   out IDebugParsedExpression ppParsedExpression
);
```

## <a name="parameters"></a>parameters
`upstrExpression`\
[in]要分析的表达式字符串。

`dwFlags`\
[in] [PARS一系列 PARS一AGAGS](../../../extensibility/debugger/reference/parseflags.md) 常量，用于确定如何分析表达式。

`nRadix`\
[in]用于解释任何数值信息的基数。

`pbstrError`\
[out]将错误作为可读文本返回。

`pichError`\
[out]返回表达式字符串中错误开头的字符位置。

`ppParsedExpression`\
[out]返回 [IDebugParsedExpression 对象中已分析的](../../../extensibility/debugger/reference/idebugparsedexpression.md) 表达式。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK` ;否则返回错误代码。

## <a name="remarks"></a>备注
 此方法生成已分析的表达式，而不是实际值。 已分析的表达式已准备好进行计算，即转换为值。

## <a name="see-also"></a>另请参阅
- [IDebugExpressionEvaluator](../../../extensibility/debugger/reference/idebugexpressionevaluator.md)
- [IDebugParsedExpression](../../../extensibility/debugger/reference/idebugparsedexpression.md)
- [PARSEFLAGS](../../../extensibility/debugger/reference/parseflags.md)
