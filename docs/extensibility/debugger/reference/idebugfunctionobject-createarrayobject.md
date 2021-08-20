---
description: 创建数组对象。
title: IDebugFunctionObject：： CreateArrayObject |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugFunctionObject::CreateArrayObject
helpviewer_keywords:
- IDebugFunctionObject::CreateArrayObject method
ms.assetid: a380e53c-15f1-401f-927f-f366eea789e6
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 2138a6ae51d24f099665eb2ec0a58aa60437a4d2
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122138323"
---
# <a name="idebugfunctionobjectcreatearrayobject"></a>IDebugFunctionObject::CreateArrayObject
创建数组对象。 此数组可以包含基元或对象实例的值。

## <a name="syntax"></a>语法

```cpp
HRESULT CreateArrayObject( 
   OBJECT_TYPE    ot,
   IDebugField*   pClassField,
   DWORD          dwRank,
   DWORD          dwDims[],
   DWORD          dwLowBounds[],
   IDebugObject** ppObject
);
```

```csharp
int CreateArrayObject(
   enum_OBJECT_TYPE ot,
   IDebugField      pClassField,
   uint             dwRank,
   uint[]           dwDims,
   uint[]           dwLowBounds,
   out IDebugObject ppObject
);
```

## <a name="parameters"></a>参数
`ot`\
中指定 [OBJECT_TYPE](../../../extensibility/debugger/reference/object-type.md) 枚举中的一个值，该值指示新数组对象的类型。

`pClassField`\
中一个 [IDebugField](../../../extensibility/debugger/reference/idebugfield.md) 对象，它表示对象的类（如果创建对象实例值的数组）。 如果创建基元对象的数组，则此参数为 null 值。

`dwRank`\
中数组的秩或维度数。

`dwDims`\
中数组每个维度的大小。

`dwLowBounds`\
中每个维度的原点 (通常为0或 1) 。

`ppObject`\
弄返回一个 [IDebugObject](../../../extensibility/debugger/reference/idebugobject.md) 对象，该对象表示新创建的数组。 这实际上是一个 [IDebugArrayObject](../../../extensibility/debugger/reference/idebugarrayobject.md) 对象。

## <a name="return-value"></a>返回值
 如果成功，将返回 S_OK;否则，将返回错误代码。

## <a name="remarks"></a>备注
 调用此方法可创建一个对象，该对象表示由 [IDebugFunctionObject](../../../extensibility/debugger/reference/idebugfunctionobject.md) 接口表示的函数的数组参数。

## <a name="see-also"></a>请参阅
- [IDebugFunctionObject](../../../extensibility/debugger/reference/idebugfunctionobject.md)
