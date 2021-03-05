---
description: 获取方法的全局容器。
title: IDebugMethodField：： GetGlobalContainer |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugMethodField::GetGlobalContainer
helpviewer_keywords:
- IDebugMethodField::GetGlobalContainer method
ms.assetid: 041ac5aa-0b80-4310-b9ae-b88f8e7e0e5f
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: eb20551d39f3e876a836ac42906ad9c50e3c6419
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2021
ms.locfileid: "102166289"
---
# <a name="idebugmethodfieldgetglobalcontainer"></a>IDebugMethodField::GetGlobalContainer
获取方法的全局容器。

## <a name="syntax"></a>语法

```cpp
HRESULT GetGlobalContainer(
   IDebugClassField** ppClass
);
```

```csharp
int GetGlobalContainer(
   out IDebugClassField ppClass
);
```

## <a name="parameters"></a>参数
`ppClass`\
弄返回一个 [IDebugClassField](../../../extensibility/debugger/reference/idebugclassfield.md) ，它表示在其中定义此方法的模块。

## <a name="return-value"></a>返回值
 如果成功，将返回 S_OK;否则，将返回错误代码。

## <a name="remarks"></a>备注
 返回的 [IDebugClassField](../../../extensibility/debugger/reference/idebugclassfield.md) 对象表示整个模块，是一个人工对象，也就是说，该模块本身不具有实际类，但可以由 `IDebugClassField` 对象表示，从而允许枚举和发现模块的各种元素。

## <a name="see-also"></a>另请参阅
- [IDebugMethodField](../../../extensibility/debugger/reference/idebugmethodfield.md)
- [IDebugClassField](../../../extensibility/debugger/reference/idebugclassfield.md)
