---
description: 获取描述此事件位置的代码上下文。
title: IDebugCanStopEvent2：： GetCodeContext |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugCanStopEvent2::GetCodeContext
helpviewer_keywords:
- IDebugCanStopEvent2::GetCodeContext
ms.assetid: eecf08b6-f9b7-4358-941b-3a448a92ac62
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: b906241a189edf78f3917d7d80ba4e4e073d50c4
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/25/2021
ms.locfileid: "105088583"
---
# <a name="idebugcanstopevent2getcodecontext"></a>IDebugCanStopEvent2::GetCodeContext
获取描述此事件位置的代码上下文。

## <a name="syntax"></a>语法

```cpp
HRESULT GetCodeContext( 
   IDebugCodeContext2** ppCodeContext
);
```

```csharp
int GetCodeContext( 
   out IDebugCodeContext2 ppCodeContext
);
```

## <a name="parameters"></a>参数
`ppCodeContext`\
弄返回表示当前代码位置的 [IDebugCodeContext2](../../../extensibility/debugger/reference/idebugcodecontext2.md) 对象。

## <a name="return-value"></a>返回值
 如果成功， `S_OK` 则返回; 否则返回错误代码。

## <a name="remarks"></a>备注
 对于大多数运行时结构，可以将代码上下文视为程序的执行流中的一个地址，指向特定指令。

 若要获取文档上下文（面向源代码的行），请调用 [GetDocumentContext](../../../extensibility/debugger/reference/idebugcanstopevent2-getdocumentcontext.md) 方法。

## <a name="see-also"></a>另请参阅
- [IDebugCanStopEvent2](../../../extensibility/debugger/reference/idebugcanstopevent2.md)
- [IDebugCodeContext2](../../../extensibility/debugger/reference/idebugcodecontext2.md)
- [GetDocumentContext](../../../extensibility/debugger/reference/idebugcanstopevent2-getdocumentcontext.md)
