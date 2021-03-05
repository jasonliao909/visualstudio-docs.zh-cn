---
description: 获取数组中元素的类型。
title: IDebugArrayField：： GetElementType |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugArrayField::GetElementType
helpviewer_keywords:
- IDebugArrayField::GetElementType method
ms.assetid: c46bf625-0a48-4cbb-8f1f-286356f2c065
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 9624a04ae70c8d29abd9b8af5b597b583efb7834
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2021
ms.locfileid: "102143839"
---
# <a name="idebugarrayfieldgetelementtype"></a>IDebugArrayField::GetElementType
获取数组中元素的类型。

## <a name="syntax"></a>语法

```cpp
HRESULT GetElementType( 
   IDebugField** ppType
);
```

```csharp
int GetElementType(
   out IDebugField ppType
);
```

## <a name="parameters"></a>参数
`ppType`\
弄返回一个 [IDebugField](../../../extensibility/debugger/reference/idebugfield.md) 对象，该对象描述元素的类型。

## <a name="return-value"></a>返回值
 如果成功，将返回 S_OK;否则，将返回错误代码。

## <a name="remarks"></a>备注
 [IDebugArrayField](../../../extensibility/debugger/reference/idebugarrayfield.md)对象假定数组的所有元素都是相同的类型。

## <a name="see-also"></a>另请参阅
- [IDebugArrayField](../../../extensibility/debugger/reference/idebugarrayfield.md)
- [IDebugField](../../../extensibility/debugger/reference/idebugfield.md)
