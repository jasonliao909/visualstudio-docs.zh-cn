---
description: 确定此对象是否为只读。
title: IDebugObject：： IsReadOnly |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugObject::IsReadOnly
helpviewer_keywords:
- IDebugObject::IsReadOnly method
ms.assetid: c460f772-d08a-4b36-81f3-dff6a51a93fd
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 56a7aed66b30798d04c8b71a8e5209b2395a6342754e3993f48800892be0d2fb
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121451804"
---
# <a name="idebugobjectisreadonly"></a>IDebugObject::IsReadOnly
确定此对象是否为只读。

## <a name="syntax"></a>语法

```cpp
HRESULT IsReadOnly( 
   BOOL* pfIsReadOnly
);
```

```csharp
int IsReadOnly(
   out int pfIsReadOnly
);
```

## <a name="parameters"></a>参数
`pfIsReadOnly`\
弄 `TRUE` 如果此对象是只读的，则返回非零 () ; 否则，将返回零 (`FALSE`) 。

## <a name="return-value"></a>返回值
 如果成功，将返回 S_OK;否则，将返回错误代码。

## <a name="remarks"></a>备注
 创建只读对象后，其值不能更改。

## <a name="see-also"></a>另请参阅
- [IDebugObject](../../../extensibility/debugger/reference/idebugobject.md)
