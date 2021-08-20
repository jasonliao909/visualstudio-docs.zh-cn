---
description: 包含有关进程的信息。
title: PROCESS_INFO |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- PROCESS_INFO
helpviewer_keywords:
- PROCESS_INFO structure
ms.assetid: 260c33cc-a05e-4645-84b6-536d0b3b0537
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: e2fc29833c8d3f6b64e5bbc683ad6f5fc82231ef
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122118094"
---
# <a name="process_info"></a>PROCESS_INFO
包含有关进程的信息。

## <a name="syntax"></a>语法

```cpp
typedef struct tagPROCESS_INFO { 
   PROCESS_INFO_FIELDS Fields;
   BSTR                bstrFileName;
   BSTR                bstrBaseName;
   BSTR                bstrTitle;
   AD_PROCESS_ID       ProcessId;
   DWORD               dwSessionId;
   BSTR                bstrAttachedSessionName;
   FILETIME            CreationTime;
   PROCESS_INFO_FLAGS  Flags;
} PROCESS_INFO;
```

```csharp
public struct PROCESS_INFO { 
   public uint          Fields;
   public string        bstrFileName;
   public string        bstrBaseName;
   public string        bstrTitle;
   public AD_PROCESS_ID ProcessId;
   public uint          dwSessionId;
   public string        bstrAttachedSessionName;
   public FILETIME      CreationTime;
   public uint          Flags;
};
```

## <a name="members"></a>成员
 `Fields`\
 指定填充哪些字段 [PROCESS_INFO_FIELDS](../../../extensibility/debugger/reference/process-info-fields.md) 枚举中的标志组合。

 `bstrFileName`\
 进程的完整路径名称。 等效于使用 [参数 调用 GetName](../../../extensibility/debugger/reference/idebugprocess2-getname.md) 方法 `GN_FILENAME` 。

 `bstrBaseName`\
 进程的文件名和扩展名。 等效于使用 `IDebugProcess2::Getname` 参数 调用 方法 `GN_BASENAME` 。

 `bstrTitle`\
 进程的标题（如果存在）。 等效于使用 `IDebugProcess2::Getname` 参数 调用 方法 `GN_TITLE` 。

 `ProcessId`\
 标识 [AD_PROCESS_ID](../../../extensibility/debugger/reference/ad-process-id.md) 的一个结构。 等效于调用 [GetPhysicalProcessId](../../../extensibility/debugger/reference/idebugprocess2-getphysicalprocessid.md) 方法。

 `dwSessionId`\
 运行此过程的调试会话的标识符。

 `bstrAttachedSessionName`\
 附加的会话名称。 等效于调用 [GetAttachedSessionName](../../../extensibility/debugger/reference/idebugprocess2-getattachedsessionname.md) 方法。

 `CreationTime`\
 创建进程的时间。

 `Flags`\
 指定进程属性PROCESS_INFO_FLAGS集合中[](../../../extensibility/debugger/reference/process-info-flags.md)标志的组合。

## <a name="remarks"></a>备注
 此结构将传递到 [GetInfo](../../../extensibility/debugger/reference/idebugprocess2-getinfo.md) 方法中填充它。

## <a name="requirements"></a>要求
 标头：msdbg.h

 命名空间：Microsoft.VisualStudio.Debugger.Interop

 程序集：Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>请参阅
- [结构和联合](../../../extensibility/debugger/reference/structures-and-unions.md)
- [PROCESS_INFO_FIELDS](../../../extensibility/debugger/reference/process-info-fields.md)
- [PROCESS_INFO_FLAGS](../../../extensibility/debugger/reference/process-info-flags.md)
- [GetInfo](../../../extensibility/debugger/reference/idebugprocess2-getinfo.md)
- [GetName](../../../extensibility/debugger/reference/idebugprocess2-getname.md)
- [GetPhysicalProcessId](../../../extensibility/debugger/reference/idebugprocess2-getphysicalprocessid.md)
- [GetAttachedSessionName](../../../extensibility/debugger/reference/idebugprocess2-getattachedsessionname.md)
