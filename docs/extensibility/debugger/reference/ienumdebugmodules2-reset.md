---
description: 将模块枚举重置为第一个元素。
title: IEnumDebugModules2：： Reset |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IEnumDebugModules2::Reset
helpviewer_keywords:
- IEnumDebugModules2::Reset
ms.assetid: f6ff364c-2644-4919-b950-3cb82eb6f601
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 5de8ef3fa6b5b35d27c37802ee8cdcd6e4845e46
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/25/2021
ms.locfileid: "105080028"
---
# <a name="ienumdebugmodules2reset"></a>IEnumDebugModules2::Reset
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
 调用此方法后， [下一次调用的方法将](../../../extensibility/debugger/reference/ienumdebugmodules2-next.md) 返回枚举的第一个元素。

## <a name="see-also"></a>另请参阅
- [IEnumDebugModules2](../../../extensibility/debugger/reference/ienumdebugmodules2.md)
