---
description: 根据服务对象的唯一标识符检索服务对象。
title: IDebugExpressionEvaluator2：：GetService |Microsoft Docs
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
ms.openlocfilehash: 78719dbd33ea20e03fefd44f00cba3dd8b7f28e8
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122088973"
---
# <a name="idebugexpressionevaluator2getservice"></a>IDebugExpressionEvaluator2::GetService
根据服务对象的唯一标识符检索服务对象。

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
[in]要检索的服务的唯一标识符。

`ppService`\
[out]返回表示服务的 对象。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK` ;否则返回错误代码。

## <a name="remarks"></a>备注
 第三方表达式计算程序可以使用此功能从另一个表达式计算程序获取服务。 例如，此方法可用于从默认表达式评估器获取可视化工具服务的接口。 第三方表达式计算程序不太可能需要实现此接口。

## <a name="see-also"></a>请参阅
- [IDebugExpressionEvaluator2](../../../extensibility/debugger/reference/idebugexpressionevaluator2.md)
