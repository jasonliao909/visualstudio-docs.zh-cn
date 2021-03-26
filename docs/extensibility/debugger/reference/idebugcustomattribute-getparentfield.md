---
description: 获取自定义属性附加到的字段。
title: IDebugCustomAttribute：： GetParentField |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugCustomAttribute::GetParentField
helpviewer_keywords:
- IDebugCustomAttribute::GetParentField
ms.assetid: bcdfdf37-bfcf-4988-a7b8-4c731d0af1b0
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 7aaa3ea38e5ed0691b8e335a3d39a8a82b7576ef
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/25/2021
ms.locfileid: "105088050"
---
# <a name="idebugcustomattributegetparentfield"></a>IDebugCustomAttribute::GetParentField
获取自定义属性附加到的字段。

## <a name="syntax"></a>语法

```cpp
HRESULT GetParentField( 
   IDebugField** ppField
);
```

```csharp
int GetParentField(
   out IDebugField ppField
);
```

## <a name="parameters"></a>参数
`ppField`\
弄返回 [IDebugField](../../../extensibility/debugger/reference/idebugfield.md) 对象，该对象表示自定义特性附加到的字段。

## <a name="return-value"></a>返回值
 如果成功，将返回 S_OK;否则，将返回错误代码。

## <a name="remarks"></a>备注
 对返回的[IDebugField](../../../extensibility/debugger/reference/idebugfield.md)对象调用[GetKind](../../../extensibility/debugger/reference/idebugfield-getkind.md)方法，以确定父字段的类型。

## <a name="see-also"></a>另请参阅
- [IDebugCustomAttribute](../../../extensibility/debugger/reference/idebugcustomattribute.md)
- [IDebugField](../../../extensibility/debugger/reference/idebugfield.md)
