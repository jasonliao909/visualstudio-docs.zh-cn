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
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 0293ebb0d83d0201c669a2d7c8ce1ac7773ec40dffae53d1e2b274def4a75bb0
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121307175"
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
