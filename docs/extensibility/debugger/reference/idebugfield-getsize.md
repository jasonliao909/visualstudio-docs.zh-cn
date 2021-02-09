---
title: IDebugField：： GetSize |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugField::GetSize
helpviewer_keywords:
- IDebugField::GetSize method
ms.assetid: 73329924-3751-4f44-af54-5986b7943374
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 6330179f1bbfffcb1f590dfc09ae0c06385f12e9
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2021
ms.locfileid: "99869851"
---
# <a name="idebugfieldgetsize"></a>IDebugField::GetSize
此方法获取字段的大小（以字节为单位）。

## <a name="syntax"></a>语法

```cpp
HRESULT GetSize( 
   DWORD* pdwSize
);
```

```csharp
int GetSize(
   out uint pdwSize
);
```

## <a name="parameters"></a>parameters
`pdwSize`\
弄返回大小。

## <a name="return-value"></a>返回值
 如果成功， `S_OK` 则返回; 否则返回错误代码。

## <a name="remarks"></a>备注
 所有字段都具有类型并且所有类型都具有大小。 例如，类型为 byte 的字段的大小为1字节。

## <a name="see-also"></a>另请参阅
- [IDebugField](../../../extensibility/debugger/reference/idebugfield.md)
