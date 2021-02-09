---
title: IDebugFunctionObject2：： CreateObject |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- IDebugFunctionObject2::CreateObject
- CreateObject
ms.assetid: 148de615-941e-4b64-ab11-75b692aae465
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 424599d322c2c8dd4db8ff4e19bab60eceaefc08
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2021
ms.locfileid: "99920989"
---
# <a name="idebugfunctionobject2createobject"></a>IDebugFunctionObject2::CreateObject
创建一个对象，该对象使用给定了计算标志设置和超时值的构造函数。

## <a name="syntax"></a>语法

```cpp
HRESULT CreateObject (
   IDebugFunctionObject* pConstructor,
   DWORD                 dwArgs,
   IDebugObject*         pArgs[],
   DWORD                 dwEvalFlags,
   DWORD                 dwTimeout,
   IDebugObject**        ppObject
);
```

```csharp
int CreateObject (
   IDebugFunctionObject pConstructor,
   uint                 dwArgs,
   IDebugObject[]       pArgs,
   uint                 dwEvalFlags,
   uint                 dwTimeout,
   out IDebugObject**   ppObject
);
```

## <a name="parameters"></a>parameters
`pConstructor`\
中一个 [IDebugFunctionObject](../../../extensibility/debugger/reference/idebugfunctionobject.md) 对象，表示要创建的对象的构造函数。

`dwArgs`\
中数组中参数的数目 `pArg` 。 表示传递给构造函数的参数的数目。

`pArgs`\
中 [IDebugObject](../../../extensibility/debugger/reference/idebugobject.md) 对象的数组，这些对象表示传递给构造函数的参数。

`dwEvalFlags`\
中 [EVALFLAGS](../../../extensibility/debugger/reference/evalflags.md) 枚举中的标志的组合，该枚举指定如何执行计算。

`dwTimeout`\
中从此方法返回前等待的最长时间（以毫秒为单位）。 使用 **无限大** 无限期等待。

`ppObject`\
弄返回表示新创建的对象的 **IDebugObject** 。

## <a name="return-value"></a>返回值
 如果成功， `S_OK` 则返回; 否则返回错误代码。

## <a name="remarks"></a>备注
 调用此方法可创建一个对象，该对象表示类的实例，或者需要构造函数的其他复杂类型，即参数。

## <a name="see-also"></a>另请参阅
- [IDebugFunctionObject2](../../../extensibility/debugger/reference/idebugfunctionobject2.md)
