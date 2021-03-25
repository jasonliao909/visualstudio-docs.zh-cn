---
description: 为此类的构造函数创建一个枚举器。
title: IDebugClassField：： EnumConstructors |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugClassField::EnumConstructors
helpviewer_keywords:
- IDebugClassField::EnumConstructors method
ms.assetid: 66a250b2-75a0-45aa-8d58-40f91cc4bf7b
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 8efba9ecb25259b6aa4998a1f22fedf443c1281a
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/25/2021
ms.locfileid: "105084969"
---
# <a name="idebugclassfieldenumconstructors"></a>IDebugClassField::EnumConstructors
为此类的构造函数创建一个枚举器。

## <a name="syntax"></a>语法

```cpp
HRESULT EnumConstructors( 
   CONSTRUCTOR_ENUM   cMatch,
   IEnumDebugFields** ppEnum
);
```

```csharp
int EnumConstructors(
   CONSTRUCTOR_ENUM     cMatch,
   out IEnumDebugFields ppEnum
);
```

## <a name="parameters"></a>参数
`cMatch`\
中 [CONSTRUCTOR_ENUM](../../../extensibility/debugger/reference/constructor-enum.md) 枚举中的一个值，该值指定要枚举的构造函数的类型。

`ppEnum`\
弄返回表示构造函数列表的 [IEnumDebugFields](../../../extensibility/debugger/reference/ienumdebugfields.md) 对象。 如果没有构造函数，则返回 null 值。

## <a name="return-value"></a>返回值
 如果成功，则返回 S_OK 或返回 S_FALSE （如果没有任何构造函数）。 否则，返回错误代码。

## <a name="remarks"></a>备注
 枚举的每个元素都是一个描述构造函数方法的 [IDebugMethodField](../../../extensibility/debugger/reference/idebugmethodfield.md) 对象。

 构造函数的列表通常不包含编译器提供的默认构造函数。

## <a name="see-also"></a>另请参阅
- [IDebugClassField](../../../extensibility/debugger/reference/idebugclassfield.md)
- [IEnumDebugFields](../../../extensibility/debugger/reference/ienumdebugfields.md)
- [IDebugMethodField](../../../extensibility/debugger/reference/idebugmethodfield.md)
- [CONSTRUCTOR_ENUM](../../../extensibility/debugger/reference/constructor-enum.md)
