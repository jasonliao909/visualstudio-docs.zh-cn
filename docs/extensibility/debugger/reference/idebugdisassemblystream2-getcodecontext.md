---
description: 返回对应于指定代码位置标识符的代码上下文对象。
title: IDebugDisassemblyStream2：： GetCodeContext |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugDisassemblyStream2::GetCodeContext
helpviewer_keywords:
- IDebugDisassemblyStream2::GetCodeContext
ms.assetid: a6d0ae82-7617-4915-9713-369abe3e2e53
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: bf54a3a89b98b29af2a1109b6ba2830bc09d7aaae62960039d30bd432c8b5640
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121417361"
---
# <a name="idebugdisassemblystream2getcodecontext"></a>IDebugDisassemblyStream2::GetCodeContext
返回对应于指定代码位置标识符的代码上下文对象。

## <a name="syntax"></a>语法

```cpp
HRESULT GetCodeContext( 
   UINT64               uCodeLocationId,
   IDebugCodeContext2** ppCodeContext
);
```

```csharp
int GetCodeContext( 
   ulong                  uCodeLocationId,
   out IDebugCodeContext2 ppCodeContext
);
```

## <a name="parameters"></a>参数
`uCodeLocationId`\
中指定代码位置标识符。 有关代码位置标识符的说明，请参阅 [GetCodeLocationId](../../../extensibility/debugger/reference/idebugdisassemblystream2-getcodelocationid.md) 方法的 "备注" 部分。

`ppCodeContext`\
弄返回一个 [IDebugCodeContext2](../../../extensibility/debugger/reference/idebugcodecontext2.md) 对象，该对象表示关联的代码上下文。

## <a name="return-value"></a>返回值
 如果成功， `S_OK` 则返回; 否则返回错误代码。

## <a name="remarks"></a>备注
 可以通过调用 [GetCurrentLocation](../../../extensibility/debugger/reference/idebugdisassemblystream2-getcurrentlocation.md) 方法返回代码位置标识符，并且该标识符可以出现在 [DisassemblyData](../../../extensibility/debugger/reference/disassemblydata.md) 结构中。

 若要将代码上下文转换为代码位置标识符，请调用 [GetCodeLocationId](../../../extensibility/debugger/reference/idebugdisassemblystream2-getcodelocationid.md) 方法。

## <a name="see-also"></a>另请参阅
- [IDebugDisassemblyStream2](../../../extensibility/debugger/reference/idebugdisassemblystream2.md)
- [IDebugCodeContext2](../../../extensibility/debugger/reference/idebugcodecontext2.md)
- [GetCodeLocationId](../../../extensibility/debugger/reference/idebugdisassemblystream2-getcodelocationid.md)
- [GetCurrentLocation](../../../extensibility/debugger/reference/idebugdisassemblystream2-getcurrentlocation.md)
- [DisassemblyData](../../../extensibility/debugger/reference/disassemblydata.md)
