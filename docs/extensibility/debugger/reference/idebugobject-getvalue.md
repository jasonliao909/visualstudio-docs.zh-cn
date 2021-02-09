---
title: IDebugObject：： GetValue |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugObject::GetValue
helpviewer_keywords:
- IDebugObject::GetValue method
ms.assetid: eec6051e-8ecb-49fa-bdd4-dd786f211692
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: f7534a05879bdae0a885ae0cbe23d072c30132d0
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2021
ms.locfileid: "99846798"
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

## <a name="parameters"></a>parameters
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
