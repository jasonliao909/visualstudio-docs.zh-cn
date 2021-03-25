---
description: 将端口枚举重置为第一个元素。
title: IEnumDebugPorts2：： Reset |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IEnumDebugPorts2::Reset
helpviewer_keywords:
- IEnumDebugPorts2::Reset
ms.assetid: 67da406c-eadb-421e-ae12-e26e9866f262
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 68e5885d5a0eab7fdd3eeb33b81ff912a02d5324
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/25/2021
ms.locfileid: "105052861"
---
# <a name="ienumdebugports2reset"></a>IEnumDebugPorts2::Reset
将枚举重置为第一个元素。

## <a name="syntax"></a>语法

```cpp
HRESULT Reset(
   void
);
```

```csharp
int Reset();
```

## <a name="return-value"></a>返回值
 如果成功， `S_OK` 则返回; 否则返回错误代码。

## <a name="remarks"></a>备注
 调用此方法后， [下一次调用的方法将](../../../extensibility/debugger/reference/ienumdebugports2-next.md) 返回枚举的第一个元素。

## <a name="see-also"></a>另请参阅
- [IEnumDebugPorts2](../../../extensibility/debugger/reference/ienumdebugports2.md)
