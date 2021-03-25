---
description: 获取作为连续字节序列的对象的值。
title: IDebugObject：： GetValue |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugObject::GetValue
helpviewer_keywords:
- IDebugObject::GetValue method
ms.assetid: eec6051e-8ecb-49fa-bdd4-dd786f211692
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: d957743a725ad462a9ed95fca6ebdffbecb6de16
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/25/2021
ms.locfileid: "105054122"
---
# <a name="idebugobjectgetvalue"></a>IDebugObject::GetValue
获取作为连续字节序列的对象的值。

## <a name="syntax"></a>语法

```cpp
HRESULT GetValue( 
   BYTE* pValue,
   UINT  nSize
);
```

```csharp
int GetValue(
   ref byte[] pValue,
   uint nSize
);
```

## <a name="parameters"></a>参数
`pValue`\
[in，out]用一系列连续的字节填充的数组，表示对象的值。

`nSize`\
中要提取的最大字节数。

## <a name="return-value"></a>返回值
 如果成功，将返回 S_OK;否则，将返回错误代码。

## <a name="remarks"></a>备注
 获取可通过调用 [GetSize](../../../extensibility/debugger/reference/idebugobject-getsize.md) 方法提取的值字节的总数。

## <a name="see-also"></a>另请参阅
- [IDebugObject](../../../extensibility/debugger/reference/idebugobject.md)
