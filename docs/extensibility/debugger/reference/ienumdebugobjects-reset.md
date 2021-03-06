---
description: 此方法将枚举重置为第一个 IDebugObject 元素。
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
ms.openlocfilehash: cacc9071004ddb68993bb3d3315eb1bda3b90cbb
ms.sourcegitcommit: f33ca1fc99f5d9372166431cefd0e0e639d20719
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2021
ms.locfileid: "102224650"
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

## <a name="parameters"></a>参数
 无

## <a name="return-value"></a>返回值
 如果成功， `S_OK` 则返回; 否则返回错误代码。

## <a name="remarks"></a>备注
 调用此方法后，下 [一次调用将返回枚举](../../../extensibility/debugger/reference/ienumdebugobjects-next.md) 的第一个元素。

## <a name="see-also"></a>请参阅
- [IEnumDebugObjects](../../../extensibility/debugger/reference/ienumdebugobjects.md)
- [下一页](../../../extensibility/debugger/reference/ienumdebugobjects-next.md)
