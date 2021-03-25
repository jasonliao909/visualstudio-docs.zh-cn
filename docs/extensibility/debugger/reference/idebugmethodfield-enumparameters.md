---
description: 为方法的参数创建枚举器。
title: IDebugMethodField：： EnumParameters |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugMethodField::EnumParameters
helpviewer_keywords:
- IDebugMethodField::EnumParameters method
ms.assetid: d77b1197-deb6-4144-8d1b-8b09949ccfac
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 0f2085b6a2aff6b41456f47a01c446b1c646f353
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/25/2021
ms.locfileid: "105058386"
---
# <a name="idebugmethodfieldenumparameters"></a>IDebugMethodField::EnumParameters
为方法的参数创建枚举器。

## <a name="syntax"></a>语法

```cpp
HRESULT EnumParameters( 
   IEnumDebugFields** ppParams
);
```

```csharp
int EnumParameters(
   out IEnumDebugFields ppParams
);
```

## <a name="parameters"></a>参数
`ppParams`\
弄返回表示方法的参数列表的 [IEnumDebugFields](../../../extensibility/debugger/reference/ienumdebugfields.md) 对象;否则，如果没有参数，则返回 null 值。

## <a name="return-value"></a>返回值
 如果成功，则返回 S_OK 或返回 S_FALSE （如果没有参数）。 否则，返回错误代码。

## <a name="remarks"></a>备注
 每个元素都是一个 [IDebugField](../../../extensibility/debugger/reference/idebugfield.md) 对象，表示不同类型的参数。 对每个对象调用 [GetKind](../../../extensibility/debugger/reference/idebugfield-getkind.md) 方法，以确定对象表示的参数类型。

 参数包括其变量名称和类型。 类方法的第一个参数通常是 "this" 指针。

 如果只需要参数类型，请调用 [EnumArguments](../../../extensibility/debugger/reference/idebugmethodfield-enumarguments.md) 方法。

## <a name="see-also"></a>另请参阅
- [IDebugMethodField](../../../extensibility/debugger/reference/idebugmethodfield.md)
- [IEnumDebugFields](../../../extensibility/debugger/reference/ienumdebugfields.md)
- [IDebugField](../../../extensibility/debugger/reference/idebugfield.md)
- [EnumArguments](../../../extensibility/debugger/reference/idebugmethodfield-enumarguments.md)
