---
description: 设置或更改与此绑定断点关联的传递计数。
title: IDebugBoundBreakpoint2：： SetPassCount |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugBoundBreakpoint2::SetPassCount
helpviewer_keywords:
- SetPassCount method
- IDebugBoundBreakpoint2::SetPassCount method
ms.assetid: b32c12f9-b34d-43bd-a1b9-61af6cf8e51b
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: fd7851bf7bdd37fe2d3dc86296d15f54a6c08970
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122111575"
---
# <a name="idebugboundbreakpoint2setpasscount"></a>IDebugBoundBreakpoint2::SetPassCount
设置或更改与此绑定断点关联的传递计数。

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
中 [BP_PASSCOUNT](../../../extensibility/debugger/reference/bp-passcount.md) 结构，它指定传递计数。

## <a name="return-value"></a>返回值
 如果成功， `S_OK` 则返回; 否则返回错误代码。 `E_BP_DELETED`如果绑定断点对象的状态设置为 `BPS_DELETED` [BP_STATE](../../../extensibility/debugger/reference/bp-state.md)枚举)  (部分，则返回。

## <a name="remarks"></a>备注
 传递计数确定何时激发断点。 可以通过调用 [GetHitCount](../../../extensibility/debugger/reference/idebugboundbreakpoint2-gethitcount.md) 方法获取当前通过或命中次数。

 以前与此断点关联的任何传递计数都将丢失。

## <a name="see-also"></a>请参阅
- [IDebugBoundBreakpoint2](../../../extensibility/debugger/reference/idebugboundbreakpoint2.md)
- [GetHitCount](../../../extensibility/debugger/reference/idebugboundbreakpoint2-gethitcount.md)
- [BP_PASSCOUNT](../../../extensibility/debugger/reference/bp-passcount.md)
- [BP_STATE](../../../extensibility/debugger/reference/bp-state.md)
