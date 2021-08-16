---
description: 此方法将表达式字符串转换为分析的表达式。
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
ms.openlocfilehash: 75973f94ba1499afbf608bc2e3625f1d27e4460c10c7be516f4d5badb10d21b7
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121389938"
---
# <a name="idebugexpressionevaluatorparse"></a>IDebugExpressionEvaluator::Parse
此方法将表达式字符串转换为分析的表达式。

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

## <a name="parameters"></a>参数
`upstrExpression`\
中要分析的表达式字符串。

`dwFlags`\
中确定如何分析表达式的 [PARSEFLAGS](../../../extensibility/debugger/reference/parseflags.md) 常量的集合。

`nRadix`\
中用于解释任何数值信息的基数。

`pbstrError`\
弄以用户可读的文本形式返回错误。

`pichError`\
弄返回表达式字符串中错误开头的字符位置。

`ppParsedExpression`\
弄返回 [IDebugParsedExpression](../../../extensibility/debugger/reference/idebugparsedexpression.md) 对象中分析的表达式。

## <a name="return-value"></a>返回值
 如果成功， `S_OK` 则返回; 否则返回错误代码。

## <a name="remarks"></a>备注
 此方法生成一个分析的表达式，而不是实际值。 已分析的表达式已准备好进行计算，即转换为值。

## <a name="see-also"></a>另请参阅
- [IDebugExpressionEvaluator](../../../extensibility/debugger/reference/idebugexpressionevaluator.md)
- [IDebugParsedExpression](../../../extensibility/debugger/reference/idebugparsedexpression.md)
- [PARSEFLAGS](../../../extensibility/debugger/reference/parseflags.md)
