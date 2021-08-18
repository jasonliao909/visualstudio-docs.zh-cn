---
description: 返回特定代码上下文的代码位置标识符。
title: IDebugDisassemblyStream2：：GetCodeLocationId |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugDisassemblyStream2::GetCodeLocationId
helpviewer_keywords:
- IDebugDisassemblyStream2::GetCodeLocationId
ms.assetid: 567adfb8-2f54-499a-a027-e4ecb82277ef
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: fce5176c8461f9e04859641bf33da9b60bbeb5ad
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122096565"
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
[in]要 [转换为标识符的 IDebugCodeContext2](../../../extensibility/debugger/reference/idebugcodecontext2.md) 对象。

`puCodeLocationId` [out]返回代码位置标识符。 请参阅“备注”。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK` ;否则返回错误代码。 如果 `E_CODE_CONTEXT_OUT_OF_SCOPE` 代码上下文有效但超出范围，则返回 。

## <a name="remarks"></a>备注
 代码位置标识符特定于支持反汇编 (DE) 引擎。 DE 在内部使用此位置标识符来跟踪代码中的位置，通常是某种地址或偏移量。 唯一的要求是，如果一个位置的代码上下文小于另一个位置的代码上下文，则第一个代码上下文的相应代码位置标识符也必须小于第二个代码上下文的代码位置标识符。

 若要检索代码位置标识符的代码上下文，请调用 [GetCodeContext](../../../extensibility/debugger/reference/idebugdisassemblystream2-getcodecontext.md) 方法。

## <a name="see-also"></a>请参阅
- [IDebugDocumentContext2](../../../extensibility/debugger/reference/idebugdocumentcontext2.md)
- [IDebugCodeContext2](../../../extensibility/debugger/reference/idebugcodecontext2.md)
- [GetCodeContext](../../../extensibility/debugger/reference/idebugdisassemblystream2-getcodecontext.md)
