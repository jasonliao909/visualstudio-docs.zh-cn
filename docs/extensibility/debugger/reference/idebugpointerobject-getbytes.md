---
title: IDebugPointerObject：： GetBytes |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugPointerObject::GetBytes
helpviewer_keywords:
- IDebugPointerObject::GetBytes method
ms.assetid: e986c188-87fb-4b51-86e9-ee6a0035bdab
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 1961aaf45478f25ed8eb55d8eda91a5c4eafc4dd
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2021
ms.locfileid: "99852942"
---
# <a name="idebugpointerobjectgetbytes"></a>IDebugPointerObject::GetBytes
获取作为一系列连续字节指向的值。

## <a name="syntax"></a>语法

```cpp
HRESULT GetBytes( 
   DWORD  dwStart,
   DWORD  dwCount,
   BYTE*  pBytes,
   DWORD* pdwBytes
);
```

```csharp
int GetBytes(
   uint       dwStart,
   uint       dwCount,
   out byte[] pBytes,
   out uint   pdwBytes
);
```

## <a name="parameters"></a>parameters
`dwStart`\
中从指向的对象的开始处的偏移量（以字节为单位）。

`dwCount`\
中要检索的字节数。

`pBytes`\
[in，out]一个数组，其中填充了值作为一系列连续字节，从指向的对象开始给定的偏移量。

`pdwBytes`\
弄返回实际检索到的字节数。

## <a name="return-value"></a>返回值
 如果成功，将返回 S_OK;否则，将返回错误代码。

## <a name="remarks"></a>备注
 如果此 [IDebugPointerObject](../../../extensibility/debugger/reference/idebugpointerobject.md) 表示的指针指向基元类型或基元 (类型的简单数组，则使用此方法，这是一个可以由) 的简单字节序列表示的数组。

## <a name="see-also"></a>另请参阅
- [IDebugPointerObject](../../../extensibility/debugger/reference/idebugpointerobject.md)
- [SetBytes](../../../extensibility/debugger/reference/idebugpointerobject-setbytes.md)
