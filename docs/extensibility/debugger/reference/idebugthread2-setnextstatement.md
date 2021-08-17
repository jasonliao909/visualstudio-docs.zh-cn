---
description: 将当前指令指针设置为给定的代码上下文。
title: IDebugThread2：： SetNextStatement |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugThread2::SetNextStatement
helpviewer_keywords:
- IDebugThread2::SetNextStatement
ms.assetid: 9e2834dd-4ecf-45af-8e6c-f9318ebdac06
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 19029364411df0fa086b6821f4a7107072845a4edafbf17a7904f08aef3c9871
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121402085"
---
# <a name="idebugthread2setnextstatement"></a>IDebugThread2::SetNextStatement
将当前指令指针设置为给定的代码上下文。

## <a name="syntax"></a>语法

```cpp
HRESULT SetNextStatement ( 
   IDebugStackFrame2*  pStackFrame,
   IDebugCodeContext2* pCodeContext
);
```

```csharp
int SetNextStatement ( 
   IDebugStackFrame2  pStackFrame,
   IDebugCodeContext2 pCodeContext
);
```

## <a name="parameters"></a>参数
`pStackFrame`\
保留以供将来使用;设置为 null 值。

`pCodeContext`\
中描述要执行的代码位置及其上下文的 [IDebugCodeContext2](../../../extensibility/debugger/reference/idebugcodecontext2.md) 对象。

## <a name="return-value"></a>返回值
 如果成功， `S_OK` 则返回; 否则返回错误代码。 下表显示了其他可能的值。

|值|说明|
|-----------|-----------------|
|E_CANNOT_SET_NEXT_STATEMENT_ON_NONLEAF_FRAME|下一条语句不能位于帧堆栈更深层的堆栈帧中。|
|E_CANNOT_SETIP_TO_DIFFERENT_FUNCTION|下一条语句与堆栈中的任何帧都不关联。|
|E_CANNOT_SET_NEXT_STATEMENT_ON_EXCEPTION|某些调试引擎无法在发生异常后设置下一个语句。|

## <a name="remarks"></a>备注
 指令指针指示要执行的下一条指令或语句。 此方法用于重试一行源代码或强制在其他函数中继续执行（例如）。

## <a name="see-also"></a>请参阅
- [IDebugThread2](../../../extensibility/debugger/reference/idebugthread2.md)
- [IDebugStackFrame2](../../../extensibility/debugger/reference/idebugstackframe2.md)
- [IDebugCodeContext2](../../../extensibility/debugger/reference/idebugcodecontext2.md)
