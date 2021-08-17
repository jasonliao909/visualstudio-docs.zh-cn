---
description: 以单独的对象的形式返回当前绑定断点枚举的副本。
title: IEnumDebugBoundBreakpoints2：： Clone |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IEnumDebugBoundBreakpoints2::Clone
helpviewer_keywords:
- IEnumDebugBoundBreakpoints2::Clone
ms.assetid: c6ce01a2-7da3-46ec-9837-855042fa7244
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: f33ce74eb5fc71e518dd0d9e1f15b399f94db3b1
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122070628"
---
# <a name="ienumdebugboundbreakpoints2clone"></a>IEnumDebugBoundBreakpoints2::Clone
以单独的对象的形式返回当前枚举的副本。

## <a name="syntax"></a>语法

```cpp
HRESULT Clone(
   IEnumDebugBoundBreakpoints2** ppEnum
);
```

```csharp
int Clone(
   out IEnumDebugBoundBreakpoints2 ppEnum
);
```

## <a name="parameters"></a>参数
`ppEnum`\
弄以单独的对象的形式返回此枚举的副本。

## <a name="return-value"></a>返回值
 如果成功， `S_OK` 则返回; 否则返回错误代码。

## <a name="remarks"></a>备注
 调用此方法时，该枚举的副本具有与原始的相同的状态。 但是，副本的和原始状态是独立的，可以单独更改。

## <a name="see-also"></a>请参阅
- [IEnumDebugBoundBreakpoints2](../../../extensibility/debugger/reference/ienumdebugboundbreakpoints2.md)
