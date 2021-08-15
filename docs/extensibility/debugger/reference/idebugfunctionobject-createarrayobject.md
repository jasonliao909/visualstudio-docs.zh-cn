---
description: 创建数组对象。
title: IDebugFunctionObject：：CreateArrayObject |Microsoft Docs
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
ms.openlocfilehash: 822a00dcfb4b4ba6a5b9739135ae756f92d2fe7437d8f9dcc8407fd17624a2fc
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121417257"
---
# <a name="idebugfunctionobjectcreatearrayobject"></a>IDebugFunctionObject::CreateArrayObject
创建数组对象。 此数组可以包含基元或对象实例值。

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
[in]指定来自 OBJECT_TYPE [枚举的值](../../../extensibility/debugger/reference/object-type.md) ，该值指示新数组对象的类型。

`pClassField`\
[in]一 [个 IDebugField](../../../extensibility/debugger/reference/idebugfield.md) 对象，表示对象的类（如果创建对象实例值的数组）。 如果创建基元对象的数组，则此参数为 null 值。

`dwRank`\
[in]数组的排名或维数。

`dwDims`\
[in]数组的每个维度的大小。

`dwLowBounds`\
[in]每个维度的原 (通常为 0 或 1) 。

`ppObject`\
[out]返回表示 [新创建的数组的 IDebugObject](../../../extensibility/debugger/reference/idebugobject.md) 对象。 这实际上是一个 [IDebugArrayObject](../../../extensibility/debugger/reference/idebugarrayobject.md) 对象。

## <a name="return-value"></a>返回值
 如果成功，则返回S_OK;否则，返回错误代码。

## <a name="remarks"></a>备注
 调用此方法以创建一个 对象，该对象表示由 [IDebugFunctionObject 接口表示的函数的数组](../../../extensibility/debugger/reference/idebugfunctionobject.md) 参数。

## <a name="see-also"></a>另请参阅
- [IDebugFunctionObject](../../../extensibility/debugger/reference/idebugfunctionobject.md)
