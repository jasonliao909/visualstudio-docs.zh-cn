---
description: 此结构提供有关计算机上运行的进程的信息。
title: PROVIDER_PROCESS_DATA |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- PROVIDER_PROCESS_DATA
helpviewer_keywords:
- PROVIDER_PROCESS_DATA structure
ms.assetid: ec2362ed-4a0c-4a09-9d66-8ff04e4f41ee
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: c9345080eddebe1a7bf596263de93e46464114cc17e27b06c05a1bbe28adef6c
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121338210"
---
# <a name="provider_process_data"></a>PROVIDER_PROCESS_DATA
此结构提供有关计算机上运行的进程的信息。

## <a name="syntax"></a>语法

```cpp
typedef struct tagPROVIDER_PROCESS_DATA {
   PROVIDER_FIELDS    Fields;
   PROGRAM_NODE_ARRAY ProgramNodes;
   BOOL               fIsDebuggerPresent;
} PROVIDER_PROCESS_DATA;
```

```csharp
public struct PROVIDER_PROCESS_DATA {
   public uint               Fields;
   public PROGRAM_NODE_ARRAY ProgramNodes;
   public int                fIsDebuggerPresent;
}
```

## <a name="members"></a>成员
 `Fields`\
 来自 PROVIDER_FIELDS [标志的组合](../../../extensibility/debugger/reference/provider-fields.md) ，指示填充了哪些字段。

 `ProgramNodes`\
 包含 [PROGRAM_NODE_ARRAY](../../../extensibility/debugger/reference/program-node-array.md) 节点数组的一个结构。

 `fIsDebuggerPresent`\
 如果调试 () ，则非零值 () `TRUE` [!INCLUDE[vsprvs](../../../code-quality/includes/vsprvs_md.md)] `FALSE` 为零。

## <a name="remarks"></a>备注
 此结构将传递给 [GetProviderProcessData](../../../extensibility/debugger/reference/idebugprogramprovider2-getproviderprocessdata.md) 方法，该方法用于填充它。

## <a name="requirements"></a>要求
 标头：msdbg.h

 命名空间：Microsoft.VisualStudio.Debugger.Interop

 程序集：Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>另请参阅
- [结构和联合](../../../extensibility/debugger/reference/structures-and-unions.md)
- [PROVIDER_FIELDS](../../../extensibility/debugger/reference/provider-fields.md)
- [PROGRAM_NODE_ARRAY](../../../extensibility/debugger/reference/program-node-array.md)
- [GetProviderProcessData](../../../extensibility/debugger/reference/idebugprogramprovider2-getproviderprocessdata.md)
