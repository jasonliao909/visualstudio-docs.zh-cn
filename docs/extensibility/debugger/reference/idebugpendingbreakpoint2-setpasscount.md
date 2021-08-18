---
description: 设置或更改与挂起断点关联的传递计数。
title: IDebugPendingBreakpoint2：：SetPassCount |Microsoft Docs
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
ms.technology: vs-ide-debug
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 0d1d72cc83d66bc0bd553db9ef392bb62d22c3af
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122050853"
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
[in]包含 [BP_PASSCOUNT](../../../extensibility/debugger/reference/bp-passcount.md) 计数的一个对象结构。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK` ;否则返回错误代码。 如果 `E_BP_DELETED` 断点已删除，则返回 。

## <a name="remarks"></a>备注
 以前与挂起断点关联的任何传递计数将丢失。 将调用从此挂起断点绑定的所有断点，以将传递计数设置为 `bpPassCount` 参数。

## <a name="see-also"></a>请参阅
- [IDebugPendingBreakpoint2](../../../extensibility/debugger/reference/idebugpendingbreakpoint2.md)
- [BP_PASSCOUNT](../../../extensibility/debugger/reference/bp-passcount.md)
