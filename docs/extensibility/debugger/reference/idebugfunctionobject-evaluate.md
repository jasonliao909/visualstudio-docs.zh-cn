---
description: IDebugFunctionObject：：Evaluate 调用 函数，并返回结果值作为 对象。
title: IDebugFunctionObject：：Evaluate |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugFunctionObject::Evaluate
helpviewer_keywords:
- IDebugFunctionObject::Evaluate method
ms.assetid: 29349ea3-d5c1-4135-aa76-ced073ab9683
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 4bd3d7cae43ce8f49bdae121aca156490d5a197ebdb46c068c6167e79c2e6137
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121451986"
---
# <a name="idebugfunctionobjectevaluate"></a>IDebugFunctionObject::Evaluate
调用 函数，将结果值作为 对象返回。

## <a name="syntax"></a>语法

```cpp
HRESULT Evaluate( 
   IDebugObject** ppParams,
   DWORD          dwParams,
   DWORD          dwTimeout,
   IDebugObject** ppResult
);
```

```csharp
int Evaluate(
   IDebugObject[]   ppParams,
   IntPtr           dwParams,
   uint             dwTimeout,
   out IDebugObject ppResult
);
```

## <a name="parameters"></a>参数
`ppParams`\
[in]表示 [输入参数的 IDebugObject](../../../extensibility/debugger/reference/idebugobject.md) 对象的数组。 每个参数都使用 `Create` [IDebugFunctionObject](../../../extensibility/debugger/reference/idebugfunctionobject.md) 接口中的方法之一创建。

`dwParams`\
[in]数组中的参数 `ppParams` 数。

`dwTimeout`\
[in]指定在从此方法返回之前等待的最大时间（以毫秒为单位）。 使用 `INFINITE` 无限期等待。

`ppResult`\
[out]返回 [一个 IDebugObject，](../../../extensibility/debugger/reference/idebugobject.md) 它以 对象表示函数的值。

## <a name="return-value"></a>返回值
 如果成功，则返回S_OK;否则，返回错误代码。

## <a name="remarks"></a>备注
 此方法设置并执行对 [IDebugFunctionObject](../../../extensibility/debugger/reference/idebugfunctionobject.md) 对象表示的函数的调用。

## <a name="see-also"></a>请参阅
- [IDebugFunctionObject](../../../extensibility/debugger/reference/idebugfunctionobject.md)
