---
description: 此方法获取用于创建函数参数的 IDebugFunctionObject 对象。
title: IDebugBinder：：GetFunctionObject |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugBinder::GetFunctionObject
helpviewer_keywords:
- IDebugBinder::GetFunctionObject method
ms.assetid: 8fb789df-8f30-420d-8ca5-bb496a6738f1
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 5fbd978bf415565c4fab016d08bbe50729124fb2683141acdcba611659bd07a1
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121342591"
---
# <a name="idebugbindergetfunctionobject"></a>IDebugBinder::GetFunctionObject
此方法获取用于创建 [函数参数的 IDebugFunctionObject](../../../extensibility/debugger/reference/idebugfunctionobject.md) 对象。

## <a name="syntax"></a>语法

```cpp
HRESULT GetFunctionObject( 
   IDebugFunctionObject **ppFunction
);
```

```csharp
int GetFunctionObject(
   out IDebugFunctionObject ppFunction
);
```

## <a name="parameters"></a>参数
`ppFunction`\
[out]返回用于创建函数参数的 [IDebugFunctionObject](../../../extensibility/debugger/reference/idebugfunctionobject.md) 接口。

## <a name="return-value"></a>返回值
 如果成功，则返回S_OK;否则，返回错误代码。

## <a name="see-also"></a>另请参阅
- [IDebugBinder](../../../extensibility/debugger/reference/idebugbinder.md)
- [IDebugFunctionObject](../../../extensibility/debugger/reference/idebugfunctionobject.md)
