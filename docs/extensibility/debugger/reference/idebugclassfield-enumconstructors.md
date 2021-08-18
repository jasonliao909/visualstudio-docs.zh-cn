---
description: 为此类的构造函数创建枚举器。
title: IDebugClassField：：EnumConstructors |Microsoft Docs
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
ms.technology: vs-ide-debug
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: a019a55fc9610e0953b6083ad901c16ae73d0907
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122119719"
---
# <a name="idebugclassfieldenumconstructors"></a>IDebugClassField::EnumConstructors
为此类的构造函数创建枚举器。

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
[in]一个来自 [CONSTRUCTOR_ENUM](../../../extensibility/debugger/reference/constructor-enum.md) 值，该值指定要枚举的构造函数的类型。

`ppEnum`\
[out]返回表示 [构造函数列表的 IEnumDebugFields](../../../extensibility/debugger/reference/ienumdebugfields.md) 对象。 如果没有构造函数，则返回 null 值。

## <a name="return-value"></a>返回值
 如果成功，则返回 S_OK，S_FALSE如果没有构造函数，则返回 。 否则，返回错误代码。

## <a name="remarks"></a>备注
 枚举的每个元素都是描述构造函数方法的 [IDebugMethodField](../../../extensibility/debugger/reference/idebugmethodfield.md) 对象。

 构造函数列表通常不包括编译器提供的默认构造函数。

## <a name="see-also"></a>请参阅
- [IDebugClassField](../../../extensibility/debugger/reference/idebugclassfield.md)
- [IEnumDebugFields](../../../extensibility/debugger/reference/ienumdebugfields.md)
- [IDebugMethodField](../../../extensibility/debugger/reference/idebugmethodfield.md)
- [CONSTRUCTOR_ENUM](../../../extensibility/debugger/reference/constructor-enum.md)
