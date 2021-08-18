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
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 037fabf80a10a9b5af69c8827cf1c39d3b3651b6df8e59bf342d8133120572f1
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121433705"
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

## <a name="see-also"></a>请参阅
- [IDebugMethodField](../../../extensibility/debugger/reference/idebugmethodfield.md)
- [IDebugClassField](../../../extensibility/debugger/reference/idebugclassfield.md)
