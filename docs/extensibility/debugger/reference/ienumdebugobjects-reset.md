---
title: IEnumDebugObjects：： Reset |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IEnumDebugObjects::Reset
helpviewer_keywords:
- IEnumDebugObjects::Reset method
ms.assetid: 4a245e47-cc39-4177-b83d-083ea0e3190f
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 39f2949a0c3b0c7009b17c8ceee09eee210c61cf
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2021
ms.locfileid: "99957096"
---
# <a name="ienumdebugobjectsreset"></a>IEnumDebugObjects::Reset
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
 调用此方法后，下 [一次调用将返回枚举](../../../extensibility/debugger/reference/ienumdebugobjects-next.md) 的第一个元素。

## <a name="see-also"></a>另请参阅
- [IEnumDebugObjects](../../../extensibility/debugger/reference/ienumdebugobjects.md)
- [下一页](../../../extensibility/debugger/reference/ienumdebugobjects-next.md)
