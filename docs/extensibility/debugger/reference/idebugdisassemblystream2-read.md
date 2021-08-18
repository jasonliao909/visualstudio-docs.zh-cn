---
description: 读取从反汇编流中的当前位置开始的说明。
title: IDebugDisassemblyStream2：：Read |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugDisassemblyStream2::Read
helpviewer_keywords:
- IDebugDisassemblyStream2::Read
ms.assetid: 7db5f6bb-73ee-45bc-b187-c1b6aa2dfdd5
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 7d39c8db44d4f59d9eeb7ef93877bcb64e029e23
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122064456"
---
# <a name="idebugdisassemblystream2read"></a>IDebugDisassemblyStream2::Read
读取从反汇编流中的当前位置开始的说明。

## <a name="syntax"></a>语法

```cpp
HRESULT Read( 
   DWORD                     dwInstructions,
   DISASSEMBLY_STREAM_FIELDS dwFields,
   DWORD*                    pdwInstructionsRead,
   DisassemblyData*          prgDisassembly
);
```

```csharp
int Read( 
   uint                           dwInstructions,
   enum_DISASSEMBLY_STREAM_FIELDS dwFields,
   out uint                       pdwInstructionsRead,
   DisassemblyData[]              prgDisassembly
);
```

## <a name="parameters"></a>参数
`dwInstructions`\
[in]要反汇编的说明数。 此值也是数组的最大 `prgDisassembly` 长度。

`dwFields`\
[in]来自 DISASSEMBLY_STREAM_FIELDS [标志的组合](../../../extensibility/debugger/reference/disassembly-stream-fields.md) ，用于指示 `prgDisassembly` 要填充 的哪些字段。

`pdwInstructionsRead`\
[out]返回实际反汇编的指令数。

`prgDisassembly`\
[out]使用反 [汇编代码](../../../extensibility/debugger/reference/disassemblydata.md) 填充的反汇编数据结构数组，每个反汇编指令一个结构。 此数组的长度由 参数 `dwInstructions` 决定。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK` ;否则返回错误代码。

## <a name="remarks"></a>备注
 可以通过调用 [GetSize](../../../extensibility/debugger/reference/idebugdisassemblystream2-getsize.md) 方法获取当前作用域中可用的最大指令数。

 可以通过调用 [Seek](../../../extensibility/debugger/reference/idebugdisassemblystream2-seek.md) 方法更改下一个指令的读取位置。

 可以将 标志添加到 参数中的 标志，以指示在反汇编指令时 `DSF_OPERANDS_SYMBOLS` `DSF_OPERANDS` `dwFields` 应该使用符号名称。

## <a name="see-also"></a>请参阅
- [IDebugDisassemblyStream2](../../../extensibility/debugger/reference/idebugdisassemblystream2.md)
- [DISASSEMBLY_STREAM_FIELDS](../../../extensibility/debugger/reference/disassembly-stream-fields.md)
- [DisassemblyData](../../../extensibility/debugger/reference/disassemblydata.md)
- [GetSize](../../../extensibility/debugger/reference/idebugdisassemblystream2-getsize.md)
- [Seek](../../../extensibility/debugger/reference/idebugdisassemblystream2-seek.md)
