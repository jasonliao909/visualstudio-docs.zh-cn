---
description: 根据给定的唯一标识符检索服务对象。
title: IDebugExpressionEvaluator2：： GetService |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- IDebugExpressionEvaluator2::GetService
- GetService
ms.assetid: f8988a9e-9d18-42af-84a7-55f41e9adf63
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 34a432be96d0511128a5466c2fd771f0682129bb3ddf4087a129831ace8be491
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121360425"
---
# <a name="idebugexpressionevaluator2getservice"></a>IDebugExpressionEvaluator2::GetService
根据给定的唯一标识符检索服务对象。

## <a name="syntax"></a>语法

```cpp
HRESULT GetService (
   GUID        uid,
   IUnknown ** ppService
);
```

```csharp
int GetService (
   Guid       uid,
   out object ppService
);
```

## <a name="parameters"></a>参数
`uid`\
中要检索的服务的唯一标识符。

`ppService`\
弄返回表示服务的对象。

## <a name="return-value"></a>返回值
 如果成功， `S_OK` 则返回; 否则返回错误代码。

## <a name="remarks"></a>备注
 第三方表达式计算器可以使用此方法从其他表达式计算器获取服务。 例如，此方法可用于从默认表达式计算器获取可视化工具服务的接口。 第三方表达式计算器不太可能需要实现此接口。

## <a name="see-also"></a>请参阅
- [IDebugExpressionEvaluator2](../../../extensibility/debugger/reference/idebugexpressionevaluator2.md)
