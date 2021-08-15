---
description: 获取此程序或此程序的一部分的反汇编流。
title: IDebugProgram2：：GetDisassemblyStream |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProgram2::GetDisassemblyStream
helpviewer_keywords:
- IDebugProgram2::GetDisassemblyStream
ms.assetid: beda0da5-267e-4bf3-96c4-b659d29e2254
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 24a210654c359995d4dbcde9ecc705638e74ee151c7b65ddec5b7a9a92de1baa
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121416048"
---
# <a name="idebugprogram2getdisassemblystream"></a>IDebugProgram2::GetDisassemblyStream
获取此程序或此程序的一部分的反汇编流。

## <a name="syntax"></a>语法

```cpp
HRESULT GetDisassemblyStream( 
   DISASSEMBLY_STREAM_SCOPE   dwScope,
   IDebugCodeContext2*        pCodeContext,
   IDebugDisassemblyStream2** ppDisassemblyStream
);
```

```csharp
int GetDisassemblyStream( 
   enum_DISASSEMBLY_STREAM_SCOPE  dwScope,
   IDebugCodeContext2             pCodeContext,
   out IDebugDisassemblyStream2   ppDisassemblyStream
);
```

## <a name="parameters"></a>参数
`dwScope`\
[in]从定义反汇编 [流DISASSEMBLY_STREAM_SCOPE](../../../extensibility/debugger/reference/disassembly-stream-scope.md) 枚举中指定一个值。

`pCodeContext`\
[in] [IDebugCodeContext2](../../../extensibility/debugger/reference/idebugcodecontext2.md) 对象，表示开始反汇编流的位置。

`ppDisassemblyStream`\
[out]返回表示 [反汇编流的 IDebugDisassemblyStream2](../../../extensibility/debugger/reference/idebugdisassemblystream2.md) 对象。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK` ;否则返回错误代码。 如果 `E_DISASM_NOTSUPPORTED` 此特定体系结构不支持反汇编，则返回 。

## <a name="remarks"></a>备注
 如果 参数具有 DISASSEMBLY_STREAM_SCOPE 集的标志，则反汇编应返回大量反汇编指令，例如，针对整个文件或 `dwScopes` `DSS_HUGE` 模块。 [](../../../extensibility/debugger/reference/disassembly-stream-scope.md) 如果未设置 标志，则反汇编应仅限于一个小区域， `DSS_HUGE` 通常是单个函数的区域。

## <a name="see-also"></a>另请参阅
- [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)
- [DISASSEMBLY_STREAM_SCOPE](../../../extensibility/debugger/reference/disassembly-stream-scope.md)
- [IDebugCodeContext2](../../../extensibility/debugger/reference/idebugcodecontext2.md)
- [IDebugDisassemblyStream2](../../../extensibility/debugger/reference/idebugdisassemblystream2.md)
