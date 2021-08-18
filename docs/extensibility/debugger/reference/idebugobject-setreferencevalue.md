---
description: 设置此 对象的引用值。
title: IDebugObject：：SetReferenceValue |Microsoft Docs
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
ms.openlocfilehash: b18af9741c4108b2638be0d55cec78d9a4fc683f
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122034885"
---
# <a name="idebugobjectsetreferencevalue"></a>IDebugObject::SetReferenceValue
设置此 对象的引用值。

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
[in]表示 [新引用值的 IDebugObject](../../../extensibility/debugger/reference/idebugobject.md) 对象。

## <a name="return-value"></a>返回值
 如果成功，则返回S_OK;否则，返回错误代码。

## <a name="remarks"></a>备注
 此方法使此 [IDebugObject](../../../extensibility/debugger/reference/idebugobject.md) 对象成为对 参数中给定对象的值的引用，并丢弃 `pObject` 以前的任何引用。 请注意， `IDebugObject` 此对象必须已经是引用类型。

## <a name="see-also"></a>请参阅
- [IDebugObject](../../../extensibility/debugger/reference/idebugobject.md)
- [GetValue](../../../extensibility/debugger/reference/idebugobject-getvalue.md)
