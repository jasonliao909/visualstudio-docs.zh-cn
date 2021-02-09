---
title: IEnumDebugAddresses：： Reset |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IEnumDebugAddresses::Reset
helpviewer_keywords:
- IEnumDebugAddresses::Reset method
ms.assetid: 3a9d7f20-5bc6-4e13-8e91-5af4092e092f
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: a29620fe97079c865aa18d354a88cc6bd12e6893
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2021
ms.locfileid: "99897097"
---
# <a name="ienumdebugaddressesreset"></a>IEnumDebugAddresses::Reset
此方法将枚举重置为第一个元素。

## <a name="syntax"></a>语法

```cpp
HRESULT Reset(void);
```

```csharp
int Reset();
```

## <a name="parameters"></a>parameters
 无

## <a name="return-value"></a>返回值
 如果成功， `S_OK` 则返回; 否则返回错误代码。

## <a name="remarks"></a>备注
 调用此方法后，下 [一次调用将返回枚举](../../../extensibility/debugger/reference/ienumdebugaddresses-next.md) 的第一个元素。

## <a name="see-also"></a>另请参阅
- [IEnumDebugAddresses](../../../extensibility/debugger/reference/ienumdebugaddresses.md)
- [下一页](../../../extensibility/debugger/reference/ienumdebugaddresses-next.md)
