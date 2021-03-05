---
description: 返回特定代码上下文的代码位置标识符。
title: IDebugDisassemblyStream2：： GetCodeLocationId |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugDisassemblyStream2::GetCodeLocationId
helpviewer_keywords:
- IDebugDisassemblyStream2::GetCodeLocationId
ms.assetid: 567adfb8-2f54-499a-a027-e4ecb82277ef
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 8c1c3a6f7a9f2e2a0617f1322d17073a9dcc7c32
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2021
ms.locfileid: "102162922"
---
# <a name="idebugdisassemblystream2getcodelocationid"></a>IDebugDisassemblyStream2::GetCodeLocationId
返回特定代码上下文的代码位置标识符。

## <a name="syntax"></a>语法

```cpp
HRESULT GetCodeLocationId( 
   IDebugCodeContext2* pCodeContext,
   UINT64*             puCodeLocationId
);
```

```csharp
int GetCodeLocationId( 
   IDebugCodeContext2 pCodeContext,
   out ulong          puCodeLocationId
);
```

## <a name="parameters"></a>参数
`pCodeContext`\
中要转换为标识符的 [IDebugCodeContext2](../../../extensibility/debugger/reference/idebugcodecontext2.md) 对象。

`puCodeLocationId` 弄返回代码位置标识符。 请参阅“备注”。

## <a name="return-value"></a>返回值
 如果成功， `S_OK` 则返回; 否则返回错误代码。 `E_CODE_CONTEXT_OUT_OF_SCOPE`如果代码上下文有效但在范围外，则返回。

## <a name="remarks"></a>备注
 代码位置标识符特定于调试引擎 (DE) 支持反汇编。 此位置标识符由 DE 在内部使用，用于跟踪代码中的位置，通常为某个地址或某种类型的偏移量。 唯一的要求是，如果一个位置的代码上下文小于另一个位置的代码上下文，则第一个代码上下文的相应代码位置标识符也必须小于第二个代码上下文的代码位置标识符。

 若要检索代码位置标识符的代码上下文，请调用 [GetCodeContext](../../../extensibility/debugger/reference/idebugdisassemblystream2-getcodecontext.md) 方法。

## <a name="see-also"></a>另请参阅
- [IDebugDocumentContext2](../../../extensibility/debugger/reference/idebugdocumentcontext2.md)
- [IDebugCodeContext2](../../../extensibility/debugger/reference/idebugcodecontext2.md)
- [GetCodeContext](../../../extensibility/debugger/reference/idebugdisassemblystream2-getcodecontext.md)
