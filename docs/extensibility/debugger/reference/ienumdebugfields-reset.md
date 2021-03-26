---
description: 此方法将字段枚举重置为第一个元素。
title: IEnumDebugFields：： Reset |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IEnumDebugFields::Reset
helpviewer_keywords:
- IEnumDebugFields::Reset method
ms.assetid: 38ff61e4-0120-42e8-971a-16be6050b425
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 2edf4751151779297d6ff8ed9ffa930cc7bf3868
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/25/2021
ms.locfileid: "105086535"
---
# <a name="ienumdebugfieldsreset"></a>IEnumDebugFields::Reset
此方法将枚举重置为第一个元素。

## <a name="syntax"></a>语法

```cpp
HRESULT Reset(void);
```

```csharp
int Reset();
```

#### <a name="parameters"></a>参数
 无

## <a name="return-value"></a>返回值
 如果成功， `S_OK` 则返回; 否则返回错误代码。

## <a name="remarks"></a>备注
 调用此方法后，下 [一次调用将返回枚举](../../../extensibility/debugger/reference/ienumdebugfields-next.md) 的第一个元素。

## <a name="see-also"></a>另请参阅
- [IEnumDebugFields](../../../extensibility/debugger/reference/ienumdebugfields.md)
- [下一页](../../../extensibility/debugger/reference/ienumdebugfields-next.md)
