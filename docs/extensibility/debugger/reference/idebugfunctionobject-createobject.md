---
description: 使用构造函数创建 对象。
title: IDebugFunctionObject：：CreateObject |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugFunctionObject::CreateObject
helpviewer_keywords:
- IDebugFunctionObject::CreateObject method
ms.assetid: c4c99dd5-609a-4e7c-8f29-eb728f57e995
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: d5385aff3c0b50239192a95efcf4789cc2f0900c
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122088726"
---
# <a name="idebugfunctionobjectcreateobject"></a>IDebugFunctionObject::CreateObject
使用构造函数创建 对象。

## <a name="syntax"></a>语法

```cpp
HRESULT CreateObject( 
   IDebugFunctionObject* pConstructor,
   DWORD                 dwArgs,
   IDebugObject*         pArgs[],
   IDebugObject**        ppObject
);
```

```csharp
int CreateObject(
   IDebugFunctionObject pConstructor,
   uint                 dwArgs,
   IDebugObject[]       pArgs,
   out IDebugObject     ppObject
);
```

## <a name="parameters"></a>参数
`pConstructor`\
[in]一 [个 IDebugFunctionObject](../../../extensibility/debugger/reference/idebugfunctionobject.md) 对象，表示要创建的对象的构造函数。

`dwArgs`\
[in]数组中的参数 `pArg` 数。 表示传递给构造函数的参数数。

`pArg`\
[in] [IDebugObject 对象的数组](../../../extensibility/debugger/reference/idebugobject.md) ，表示传递给构造函数的参数。

`ppObject`\
[out]返回 `IDebugObject` 一个 ，它表示新创建的 对象。

## <a name="return-value"></a>返回值
 如果成功，则返回S_OK;否则，返回错误代码。

## <a name="remarks"></a>备注
 调用此方法以创建一个对象，该对象表示类 (或其他需要构造函数) 且该构造函数是函数的参数（由 [IDebugFunctionObject](../../../extensibility/debugger/reference/idebugfunctionobject.md) 接口表示）的实例。

 如果对象参数不需要构造函数，请调用 [CreateObjectNoConstructor](../../../extensibility/debugger/reference/idebugfunctionobject-createobjectnoconstructor.md) 方法。

## <a name="see-also"></a>请参阅
- [IDebugFunctionObject](../../../extensibility/debugger/reference/idebugfunctionobject.md)
- [CreateObjectNoConstructor](../../../extensibility/debugger/reference/idebugfunctionobject-createobjectnoconstructor.md)
