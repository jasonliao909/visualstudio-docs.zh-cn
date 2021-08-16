---
description: 设置此对象的引用值。
title: IDebugObject：： SetReferenceValue |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugObject::SetReferenceValue
helpviewer_keywords:
- IDebugObject::SetReferenceValue method
ms.assetid: 08c78a4e-98eb-41cb-8b75-02a6a43d49f7
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 71f1b02a48d14c01c0a28433be3d0321c2fe3855e045af839e384808be9e52a9
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121451791"
---
# <a name="idebugobjectsetreferencevalue"></a>IDebugObject::SetReferenceValue
设置此对象的引用值。

## <a name="syntax"></a>语法

```cpp
HRESULT SetReferenceValue( 
   IDebugObject* pObject
);
```

```csharp
int SetReferenceValue(
   [In] IDebugObject pObject
);
```

## <a name="parameters"></a>参数
`pObject`\
中表示新引用值的 [IDebugObject](../../../extensibility/debugger/reference/idebugobject.md) 对象。

## <a name="return-value"></a>返回值
 如果成功，将返回 S_OK;否则，将返回错误代码。

## <a name="remarks"></a>备注
 此方法使此 [IDebugObject](../../../extensibility/debugger/reference/idebugobject.md) 对象引用参数中给定的对象的值 `pObject` ，同时丢弃任何以前的引用。 请注意，此 `IDebugObject` 对象必须已经是引用类型。

## <a name="see-also"></a>另请参阅
- [IDebugObject](../../../extensibility/debugger/reference/idebugobject.md)
- [GetValue](../../../extensibility/debugger/reference/idebugobject-getvalue.md)
