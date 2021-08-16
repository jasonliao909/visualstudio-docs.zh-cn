---
description: 为 方法的参数创建枚举器。
title: IDebugMethodField：：EnumParameters |Microsoft Docs
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
ms.technology: vs-ide-debug
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 01b326b70eb0a91b1f59b2abf051741b6b44d49695f0fcaa0881e342fce30034
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121433692"
---
# <a name="idebugmethodfieldenumparameters"></a>IDebugMethodField::EnumParameters
为 方法的参数创建枚举器。

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
[out]返回一 [个 IEnumDebugFields](../../../extensibility/debugger/reference/ienumdebugfields.md) 对象，该对象表示方法的参数列表;否则，如果没有参数，则 返回 null 值。

## <a name="return-value"></a>返回值
 如果成功，则S_OK，或者S_FALSE参数时返回值。 否则，返回错误代码。

## <a name="remarks"></a>备注
 每个元素都是表示不同类型的参数的 [IDebugField](../../../extensibility/debugger/reference/idebugfield.md) 对象。 在每个 [对象上调用 GetKind](../../../extensibility/debugger/reference/idebugfield-getkind.md) 方法，以精确确定对象表示的参数类型。

 参数包括其变量名称和类型。 类方法的第一个参数通常是"this"指针。

 如果只需要参数的类型，请调用 [EnumArguments](../../../extensibility/debugger/reference/idebugmethodfield-enumarguments.md) 方法。

## <a name="see-also"></a>另请参阅
- [IDebugMethodField](../../../extensibility/debugger/reference/idebugmethodfield.md)
- [IEnumDebugFields](../../../extensibility/debugger/reference/ienumdebugfields.md)
- [IDebugField](../../../extensibility/debugger/reference/idebugfield.md)
- [EnumArguments](../../../extensibility/debugger/reference/idebugmethodfield-enumarguments.md)
