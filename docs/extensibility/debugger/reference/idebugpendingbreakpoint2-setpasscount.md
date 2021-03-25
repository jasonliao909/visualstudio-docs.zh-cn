---
description: 设置或更改与挂起断点关联的传递计数。
title: IDebugPendingBreakpoint2：： SetPassCount |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugPendingBreakpoint2::SetPassCount
helpviewer_keywords:
- SetPassCount method
- IDebugPendingBreakpoint2::SetPassCount method
ms.assetid: 08ddd328-57eb-42e0-baa9-8424dcd1bf04
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: d83249667bd9489b052f35a4d3d3b7ca826d540f
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/25/2021
ms.locfileid: "105058347"
---
# <a name="idebugpendingbreakpoint2setpasscount"></a>IDebugPendingBreakpoint2::SetPassCount
设置或更改与挂起断点关联的传递计数。

## <a name="syntax"></a>语法

```cpp
HRESULT SetPassCount( 
   BP_PASSCOUNT bpPassCount
);
```

```csharp
int SetPassCount( 
   BP_PASSCOUNT bpPassCount
);
```

## <a name="parameters"></a>参数
`bpPassCount`\
中包含传递计数的 [BP_PASSCOUNT](../../../extensibility/debugger/reference/bp-passcount.md) 结构。

## <a name="return-value"></a>返回值
 如果成功， `S_OK` 则返回; 否则返回错误代码。 `E_BP_DELETED`如果已删除断点，则返回。

## <a name="remarks"></a>备注
 以前与挂起断点关联的任何传递计数都将丢失。 将调用从此挂起断点绑定的所有断点，以将其传递计数设置为 `bpPassCount` 参数。

## <a name="see-also"></a>另请参阅
- [IDebugPendingBreakpoint2](../../../extensibility/debugger/reference/idebugpendingbreakpoint2.md)
- [BP_PASSCOUNT](../../../extensibility/debugger/reference/bp-passcount.md)
