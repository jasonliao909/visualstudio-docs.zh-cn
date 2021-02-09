---
title: IDebugPointerField：： GetDereferencedField |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugPointerField::GetDereferencedField
helpviewer_keywords:
- IDebugPointerField::GetDereferencedField method
ms.assetid: 8de988ab-cd79-4287-be72-3c900f2fe407
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 9b502b83ec793733ef642585b6ded260f72aa1be
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2021
ms.locfileid: "99869656"
---
# <a name="idebugpointerfieldgetdereferencedfield"></a>IDebugPointerField::GetDereferencedField
此方法返回此指针对象指向的对象的类型。

## <a name="syntax"></a>语法

```cpp
HRESULT GetDereferencedField(
   IDebugField** ppField
);
```

```csharp
int GetDereferencedField(
   out IDebugField ppField
);
```

## <a name="parameters"></a>parameters
`ppField`\
弄返回描述目标对象类型的 [IDebugField](../../../extensibility/debugger/reference/idebugfield.md) 。

## <a name="return-value"></a>返回值
 如果成功， `S_OK` 则返回; 否则返回错误代码。

## <a name="remarks"></a>备注
 例如，如果 [IDebugPointerField](../../../extensibility/debugger/reference/idebugpointerfield.md) 对象指向一个整数，则此方法返回的 [IDebugField](../../../extensibility/debugger/reference/idebugfield.md) 类型将描述该整数类型。

## <a name="see-also"></a>另请参阅
- [IDebugPointerField](../../../extensibility/debugger/reference/idebugpointerfield.md)
- [IDebugField](../../../extensibility/debugger/reference/idebugfield.md)
