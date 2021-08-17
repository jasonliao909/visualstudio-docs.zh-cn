---
description: 确定是否可以将当前指令指针设置为给定的堆栈帧。
title: IDebugThread2：：CanSetNextStatement |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugThread2::CanSetNextStatement
helpviewer_keywords:
- IDebugThread2::CanSetNextStatement
ms.assetid: 7014af80-ff4f-4790-a34b-0528918d1fa3
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: d19d6b92b4b7eb3196d42c6c18d93ebfb091c364eaed4e3656e1c9706abc3cfd
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121448723"
---
# <a name="idebugthread2cansetnextstatement"></a>IDebugThread2::CanSetNextStatement
确定是否可以将当前指令指针设置为给定的堆栈帧。

## <a name="syntax"></a>语法

```cpp
HRESULT CanSetNextStatement ( 
   IDebugStackFrame2*  pStackFrame,
   IDebugCodeContext2* pCodeContext
);
```

```csharp
int CanSetNextStatement ( 
   IDebugStackFrame2  pStackFrame,
   IDebugCodeContext2 pCodeContext
);
```

## <a name="parameters"></a>参数
`pStackFrame`\
保留供将来使用;设置为 null 值。 如果这是一个 null 值，请使用当前堆栈帧。

`pCodeContext`\
[in]描述要执行的代码位置及其上下文的 [IDebugCodeContext2](../../../extensibility/debugger/reference/idebugcodecontext2.md) 对象。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK` ;否则返回错误代码。

## <a name="remarks"></a>备注
 如果此方法返回 `S_OK` ，则调用 [SetNextStatement](../../../extensibility/debugger/reference/idebugthread2-setnextstatement.md) 方法以实际设置下一个语句。

## <a name="see-also"></a>请参阅
- [IDebugThread2](../../../extensibility/debugger/reference/idebugthread2.md)
- [IDebugStackFrame2](../../../extensibility/debugger/reference/idebugstackframe2.md)
- [IDebugCodeContext2](../../../extensibility/debugger/reference/idebugcodecontext2.md)
- [SetNextStatement](../../../extensibility/debugger/reference/idebugthread2-setnextstatement.md)
