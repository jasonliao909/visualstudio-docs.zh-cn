---
description: 此方法确定此对象或父容器的 "编辑并继续" 状态是否过时。
title: IDebugObject2：： IsEncOutdated |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugObject2::IsEncOutdated
helpviewer_keywords:
- IDebugObject2::IsEncOutdated method
ms.assetid: d3a8c02d-895b-478c-9957-d663130f308e
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 583b77ed4f3fbfc81bb595ddde025b8c08f169dd
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2021
ms.locfileid: "102170011"
---
# <a name="idebugobject2isencoutdated"></a>IDebugObject2::IsEncOutdated
此方法确定此对象或父容器的 "编辑并继续" 状态是否过时。 自定义表达式计算器不实现此方法并始终返回 `E_NOTIMPL` 。

## <a name="syntax"></a>语法

```cpp
HRESULT IsEncOutdated(
   BOOL* pfEncOutdated
);
```

```csharp
int IsEncOutdated(
   out int pfEncOutdated
);
```

## <a name="parameters"></a>参数
`pfEncOutdated`\
弄 `TRUE` 如果 "编辑并继续" 状态为 "过期"，则为非零 () ， `FALSE` 如果不是，则 () 。

## <a name="return-value"></a>返回值
 如果成功， `S_OK` 则返回; 否则返回错误代码。

> [!NOTE]
> 自定义表达式计算器应该总是返回 `E_NOTIMPL` 。

## <a name="see-also"></a>另请参阅
- [IDebugObject2](../../../extensibility/debugger/reference/idebugobject2.md)
