---
description: 包含一个 对象数组，这些对象描述感兴趣的程序。
title: PROGRAM_NODE_ARRAY |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- PROGRAM_NODE_ARRAY
helpviewer_keywords:
- PROGRAM_NODE_ARRAY structure
ms.assetid: 8eeea600-eda5-4b7c-868a-0b86d177b0a5
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 9b2860214acc534b43c4c47ea837e74c18eb6fbe
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122103047"
---
# <a name="program_node_array"></a>PROGRAM_NODE_ARRAY
包含一个 对象数组，这些对象描述感兴趣的程序。

## <a name="syntax"></a>语法

```cpp
typedef struct tagPROGRAM_NODE_ARRAY {
   DWORD                dwCount;
   IDebugProgramNode2** Members;
} PROGRAM_NODE_ARRAY;
```

```csharp
public struct tagPROGRAM_NODE_ARRAY {
   public uint                 dwCount;
   public IDebugProgramNode2[] Members;
}
```

## <a name="members"></a>成员
 `dwCount`\
 数组中的对象 `Members` 数。

 `Members`\
 描述所请求 [的程序的 IDebugProgramNode2](../../../extensibility/debugger/reference/idebugprogramnode2.md) 对象的数组。

## <a name="remarks"></a>备注
 此结构是 PROVIDER_PROCESS_DATA结构的[](../../../extensibility/debugger/reference/provider-process-data.md)一部分，而该结构又通过调用[GetProviderProcessData](../../../extensibility/debugger/reference/idebugprogramprovider2-getproviderprocessdata.md)方法进行填充。

## <a name="requirements"></a>要求
 标头：msdbg.h

 命名空间：Microsoft.VisualStudio.Debugger.Interop

 程序集：Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>请参阅
- [结构和联合](../../../extensibility/debugger/reference/structures-and-unions.md)
- [PROVIDER_PROCESS_DATA](../../../extensibility/debugger/reference/provider-process-data.md)
- [IDebugProgramNode2](../../../extensibility/debugger/reference/idebugprogramnode2.md)
- [GetProviderProcessData](../../../extensibility/debugger/reference/idebugprogramprovider2-getproviderprocessdata.md)
