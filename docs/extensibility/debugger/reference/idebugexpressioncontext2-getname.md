---
description: 检索计算上下文的名称。
title: IDebugExpressionContext2：： GetName |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugExpressionContext2::GetName
helpviewer_keywords:
- IDebugExpressionContext2::GetName
ms.assetid: c2b70d22-17af-4986-a7e3-930910367216
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: d53463bdda25a7338aa2aa61db80d022ade4b74e
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126664535"
---
# <a name="idebugexpressioncontext2getname"></a>IDebugExpressionContext2::GetName
检索计算上下文的名称。

## <a name="syntax"></a>语法

```cpp
HRESULT GetName( 
   BSTR* pbstrName
);
```

```csharp
int GetName( 
   out string pbstrName
);
```

## <a name="parameters"></a>parameters
`pbstrName`\
弄返回计算上下文的名称。

## <a name="return-value"></a>返回值
 如果成功， `S_OK` 则返回; 否则返回错误代码。

## <a name="remarks"></a>备注
 名称是此计算上下文的说明。 它通常是指可通过引用此确切计算上下文的表达式计算器来分析的内容。 例如，在 c + + 中，名称如下：

```
"{ function-name, source-file-name, module-file-name }"
```

## <a name="see-also"></a>另请参阅
- [IDebugExpressionContext2](../../../extensibility/debugger/reference/idebugexpressioncontext2.md)
