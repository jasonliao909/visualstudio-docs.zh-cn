---
description: 获取与此对象关联的别名（如果有）。
title: IDebugObject2：： GetAlias |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugObject2::GetAlias
helpviewer_keywords:
- IDebugObject2::GetAlias method
ms.assetid: aa6824d5-c932-42ba-8713-950e7d1fb42f
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 494f76bc57ad75a8a52a7b8ce02ed3cb26861be591553e0b406ffe977695f65a
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121416984"
---
# <a name="idebugobject2getalias"></a>IDebugObject2::GetAlias
获取与此对象关联的别名（如果有）。

## <a name="syntax"></a>语法

```cpp
HRESULT GetAlias(
   IDebugAlias** ppAlias
);
```

```csharp
int GetAlias(
   out IDebugAlias ppAlias
);
```

## <a name="parameters"></a>参数
`ppAlias`\
弄返回表示此对象的别名的 [IDebugAlias](../../../extensibility/debugger/reference/idebugalias.md) 对象;否则，返回 null 值。

## <a name="return-value"></a>返回值
 如果成功，将返回 S_OK;否则，将返回错误代码。

## <a name="remarks"></a>备注
 对象的别名是通过调用 [CreateAlias](../../../extensibility/debugger/reference/idebugobject2-createalias.md) 方法创建的。

## <a name="see-also"></a>另请参阅
- [IDebugObject2](../../../extensibility/debugger/reference/idebugobject2.md)
- [IDebugAlias](../../../extensibility/debugger/reference/idebugalias.md)
