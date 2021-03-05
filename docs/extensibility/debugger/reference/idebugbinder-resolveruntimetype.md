---
description: 此方法确定对象的运行时类型。
title: IDebugBinder：： ResolveRuntimeType |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugBinder::ResolveRuntimeType
helpviewer_keywords:
- IDebugBinder::ResolveRuntimeType method
ms.assetid: 6456ab3e-1c03-4f3c-91f9-16797ab7f5e7
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 19e7285dd25009e7fe4aeb92974c70ce4109502c
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2021
ms.locfileid: "102143631"
---
# <a name="idebugbinderresolveruntimetype"></a>IDebugBinder::ResolveRuntimeType
此方法确定对象的运行时类型。

## <a name="syntax"></a>语法

```cpp
HRESULT ResolveRuntimeType( 
   IDebugObject* pObject,
   IDebugField** ppResolved
);
```

```csharp
int ResolveRuntimeType(
   IDebugObject     pObject,
   out IDebugField  ppResolved
);
```

## <a name="parameters"></a>参数
`pObject`\
中要解析的 [IDebugObject](../../../extensibility/debugger/reference/idebugobject.md) 。

`ppResolved`\
弄以 [IDebugField](../../../extensibility/debugger/reference/idebugfield.md)的形式返回对象的类型。

## <a name="return-value"></a>返回值
 如果成功， `S_OK` 则返回; 否则返回错误代码。

## <a name="remarks"></a>备注
 对象的运行时类型在编译时并非始终是已知的。 例如，使用多态性，可以将参数作为其基类（如 button 类）传递给函数。 实参可以是派生类，如单选按钮类。

## <a name="see-also"></a>另请参阅
- [IDebugBinder](../../../extensibility/debugger/reference/idebugbinder.md)
- [IDebugObject](../../../extensibility/debugger/reference/idebugobject.md)
- [IDebugField](../../../extensibility/debugger/reference/idebugfield.md)
