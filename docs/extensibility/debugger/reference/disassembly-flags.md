---
description: 指定反汇编的标志。
title: DISASSEMBLY_FLAGS |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- DISASSEMBLY_FLAGS
helpviewer_keywords:
- DISASSEMBLY_FLAGS enumeration
ms.assetid: c1ec5a4d-5d42-4660-932c-7348550140cb
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: d4640ee39a936318b5e200fc46135e1fc271c46b
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122119992"
---
# <a name="disassembly_flags"></a>DISASSEMBLY_FLAGS
指定反汇编的标志。

## <a name="syntax"></a>语法

```cpp
enum enum_DISASSEMBLY_FLAGS {
    DF_DOCUMENTCHANGE     = 0x00000001,
    DF_DISABLED           = 0x00000002,
    DF_INSTRUCTION_ACTIVE = 0x00000004,
    DF_DATA               = 0x00000008,
    DF_HASSOURCE          = 0x00000010,
    DF_DOCUMENT_CHECKSUM  = 0x00000020
};
typedef DWORD DISASSEMBLY_FLAGS;
```

```csharp
public enum enum_DISASSEMBLY_FLAGS {
    DF_DOCUMENTCHANGE     = 0x00000001,
    DF_DISABLED           = 0x00000002,
    DF_INSTRUCTION_ACTIVE = 0x00000004,
    DF_DATA               = 0x00000008,
    DF_HASSOURCE          = 0x00000010,
    DF_DOCUMENT_CHECKSUM  = 0x00000020
};
```

## <a name="fields"></a>字段
`DF_DOCUMENTCHANGE`\
指示此指令与上一个指令位于不同的文档中。

`DF_DISABLED`\
指示将不执行此指令。

`DF_INSTRUCTION_ACTIVE`\
指示此指令是要执行的下一个指令 (可能有多个) 。

`DF_DATA`\
指示此指令实际上是 (不是代码) 的数据。

`DF_HASSOURCE`\
指示此指令具有源。 某些说明（例如，事件探查或垃圾收集代码）没有相应的源。

`DF_DOCUMENT_CHECKSUM`\
指示 `bstrDocumentUrl` 字段包含文档 URL 后面的校验和数据。 有关校验和数据的存储方式，请参阅 [DisassemblyData](../../../extensibility/debugger/reference/disassemblydata.md) 结构的 "备注" 部分。

## <a name="remarks"></a>备注
用作 `dwFlags` [DisassemblyData](../../../extensibility/debugger/reference/disassemblydata.md) 结构的成员。

这些标志可以与按位组合 `OR` 。

## <a name="requirements"></a>要求
标头： msdbg

命名空间： VisualStudio

程序集： Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>请参阅
- [枚举](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)
- [DisassemblyData](../../../extensibility/debugger/reference/disassemblydata.md)
