---
description: 创建一个对象，该对象使用给定评估标志设置和超时值的构造函数。
title: IDebugFunctionObject2：：CreateObject |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- IDebugFunctionObject2::CreateObject
- CreateObject
ms.assetid: 148de615-941e-4b64-ab11-75b692aae465
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: bb4ea8d82a10eb5ed7dc4e0b427d7b966a30faf3
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122088648"
---
# <a name="idebugfunctionobject2createobject"></a>IDebugFunctionObject2::CreateObject
创建一个对象，该对象使用给定评估标志设置和超时值的构造函数。

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

## <a name="parameters"></a>参数
`pConstructor`\
[in]表示 [要创建的对象的构造函数的 IDebugFunctionObject](../../../extensibility/debugger/reference/idebugfunctionobject.md) 对象。

`dwArgs`\
[in]数组中的参数 `pArg` 数。 表示传递给构造函数的参数数。

`pArgs`\
[in] [IDebugObject](../../../extensibility/debugger/reference/idebugobject.md) 对象的数组，表示传递给构造函数的参数。

`dwEvalFlags`\
[in] [来自 EVALFLAGS](../../../extensibility/debugger/reference/evalflags.md) 枚举的标志的组合，用于指定如何执行计算。

`dwTimeout`\
[in]从此方法返回之前等待的最大时间（以毫秒为单位）。 使用 **INFINITE** 无限期等待。

`ppObject`\
[out]返回表示 **新创建的 对象的 IDebugObject。**

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK` ;否则返回错误代码。

## <a name="remarks"></a>备注
 调用此方法以创建一个对象，该对象表示类的实例或其他需要构造函数（即参数）的复杂类型。

## <a name="see-also"></a>请参阅
- [IDebugFunctionObject2](../../../extensibility/debugger/reference/idebugfunctionobject2.md)
