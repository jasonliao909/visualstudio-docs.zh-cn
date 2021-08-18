---
description: 创建基元数据对象，如简单整数。
title: IDebugFunctionObject：：CreatePrimitiveObject |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugFunctionObject::CreatePrimitiveObject
helpviewer_keywords:
- IDebugFunctionObject::CreatePrimitiveObject method
ms.assetid: 6e9dc8b6-b4e1-4abf-b6e0-e885910775bc
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 372275ec5623b8bf52a682c1240e5dcb76d4f837
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122088713"
---
# <a name="idebugfunctionobjectcreateprimitiveobject"></a>IDebugFunctionObject::CreatePrimitiveObject
创建基元数据对象，如简单整数。

## <a name="syntax"></a>语法

```cpp
HRESULT CreatePrimitiveObject( 
   OBJECT_TYPE    ot,
   IDebugObject** ppObject
);
```

```csharp
int CreatePrimitiveObject(
   enum_OBJECT_TYPE ot,
   out IDebugObject ppObject
);
```

## <a name="parameters"></a>参数
`ot`\
[in]一个来自 [OBJECT_TYPE](../../../extensibility/debugger/reference/object-type.md) 枚举的值，该值表示要创建的基元的类型。

`ppObject`\
[out]返回表示[新创建的 对象的 IDebugObject。](../../../extensibility/debugger/reference/idebugobject.md)

## <a name="return-value"></a>返回值
 如果成功，则返回S_OK;否则，返回错误代码。

## <a name="remarks"></a>备注
 调用此方法以创建一个 对象，该对象表示基元对象，该对象是由 [IDebugFunctionObject](../../../extensibility/debugger/reference/idebugfunctionobject.md) 接口表示的函数的参数。 例如，如果表达式字符串为"myString (5) "，则此方法用于创建表示整数 5 的对象。

## <a name="see-also"></a>请参阅
- [IDebugFunctionObject](../../../extensibility/debugger/reference/idebugfunctionobject.md)
