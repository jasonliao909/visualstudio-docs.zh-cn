---
description: IDebugFunctionObject2：：Evaluate 调用 函数，并返回结果值作为 对象。
title: IDebugFunctionObject2：：Evaluate |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- IDebugFunctionObject2::Evaluate
ms.assetid: bc54c652-904b-4297-a6db-faa329684881
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 0d83ca6ffb7899d6a144dc823a5849a41c6188c7569256446ca3688771facfae
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121389795"
---
# <a name="idebugfunctionobject2evaluate"></a>IDebugFunctionObject2::Evaluate
调用 函数，将结果值作为 对象返回。

## <a name="syntax"></a>语法

```cpp
HRESULT Evaluate (
   IDebugObject** ppParams,
   DWORD          dwParams,
   DWORD          dwEvalFlags,
   DWORD          dwTimeout,
   IDebugObject** ppResult
);
```

```csharp
int Evaluate (
   IDebugObject     ppParams,
   uint             dwParams,
   uint             dwEvalFlags,
   uint             dwTimeout,
   out IDebugObject ppResult
);
```

## <a name="parameters"></a>参数
`ppParams`\
[in]表示 [输入参数的 IDebugObject](../../../extensibility/debugger/reference/idebugobject.md) 对象的数组。 每个参数都使用此接口中的 Create 方法之一创建。

`dwParams`\
[in]数组中的参数 `ppParams` 数。

`dwEvalFlags`\
[in] [来自 EVALFLAGS](../../../extensibility/debugger/reference/evalflags.md) 枚举的标志的组合，用于指定如何执行计算。

`dwTimeout`\
[in]指定在从此方法返回之前等待的最大时间（以毫秒为单位）。 使用 **INFINITE** 无限期等待。

`ppResult`\
[out]返回 **一个 IDebugObject，该 IDebugObject** 将函数的值表示为 对象。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK` ;否则返回错误代码。

## <a name="see-also"></a>另请参阅
- [IDebugFunctionObject2](../../../extensibility/debugger/reference/idebugfunctionobject2.md)
