---
description: 调试引擎不实现此方法。
title: IDebugThread2：：GetLogicalThread |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugThread2::GetLogicalThread
helpviewer_keywords:
- IDebugThread2::GetLogicalThread
ms.assetid: bce6230e-41d4-49b7-a050-2dde5efb6805
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: de33532e0d81287b44e9e623df683c9a76de1a7c
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122029551"
---
# <a name="idebugthread2getlogicalthread"></a>IDebugThread2::GetLogicalThread
调试引擎不实现此方法。

## <a name="syntax"></a>语法

```cpp
HRESULT GetLogicalThread( 
   IDebugStackFrame2*     pStackFrame,
   IDebugLogicalThread2** ppLogicalThread
);
```

```csharp
int GetLogicalThread( 
   IDebugStackFrame2        pStackFrame,
   out IDebugLogicalThread2 ppLogicalThread
);
```

## <a name="parameters"></a>参数
`pStackFrame`\
[in]表示 [堆栈帧的 IDebugStackFrame2](../../../extensibility/debugger/reference/idebugstackframe2.md) 对象。

`ppLogicalThread`\
[out]返回 `IDebugLogicalThread2` 表示关联逻辑线程的接口。 调试引擎实现应设置为 null 值。

## <a name="return-value"></a>返回值
 调试引擎实现始终返回 `E_NOTIMPL` 。

## <a name="see-also"></a>请参阅
- [IDebugThread2](../../../extensibility/debugger/reference/idebugthread2.md)
