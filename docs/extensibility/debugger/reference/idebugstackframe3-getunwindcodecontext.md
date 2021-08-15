---
description: 返回代码上下文，该上下文表示发生堆栈展开操作时的位置。
title: IDebugStackFrame3：：GetUnwindCodeContext |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugStackFrame3::GetUnwindCodeContext
helpviewer_keywords:
- IDebugStackFrame3::GetUnwindCodeContext method
ms.assetid: b25f7e7d-2b24-48e4-93b3-829e61d73ebf
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 8a3b88da3473ca6557f2aae36b87f13f2b3fc0be3dc7bfcea6d9ce2645959535
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121389496"
---
# <a name="idebugstackframe3getunwindcodecontext"></a>IDebugStackFrame3::GetUnwindCodeContext
返回代码上下文，该上下文表示发生堆栈展开操作时的位置。

## <a name="syntax"></a>语法

```cpp
HRESULT GetUnwindCodeContext(
   IDebugCodeContext2 **ppCodeContext
);
```

```csharp
int GetUnwindCodeContext(
   out IDebugCodeContext2 ppCodeContext
);
```

## <a name="parameters"></a>参数
`ppCodeContext`\
[out]返回一个 [IDebugCodeContext2](../../../extensibility/debugger/reference/idebugcodecontext2.md) 对象，该对象表示发生堆栈展开时的代码上下文位置。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK` ;否则返回错误代码。

## <a name="remarks"></a>备注
 即使此方法可能在堆栈展开后返回位置的代码上下文，但不一定意味着堆栈展开实际上可以在当前堆栈帧中发生。

## <a name="see-also"></a>另请参阅
- [IDebugStackFrame3](../../../extensibility/debugger/reference/idebugstackframe3.md)
- [IDebugCodeContext2](../../../extensibility/debugger/reference/idebugcodecontext2.md)
