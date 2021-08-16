---
description: 指定要检索的进程的信息类型。
title: PROCESS_INFO_FIELDS |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- PROCESS_INFO_FIELDS
helpviewer_keywords:
- PROCESS_INFO_FIELDS enumeration
ms.assetid: 0d9cc345-3d3a-44d8-ae15-a67acb97a828
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 622213e1eb0f43af3f3e034b76af11d941559724605a6758dd31f9ed3b4081af
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121433068"
---
# <a name="process_info_fields"></a>PROCESS_INFO_FIELDS
指定要检索的进程的信息类型。

## <a name="syntax"></a>语法

```cpp
enum enum_PROCESS_INFO_FIELDS { 
   PIF_FILE_NAME             = 0x00000001,
   PIF_BASE_NAME             = 0x00000002,
   PIF_TITLE                 = 0x00000004,
   PIF_PROCESS_ID            = 0x00000008,
   PIF_SESSION_ID            = 0x00000010,
   PIF_ATTACHED_SESSION_NAME = 0x00000020,
   PIF_CREATION_TIME         = 0x00000040,
   PIF_FLAGS                 = 0x00000080,
   PIF_ALL                   = 0x000000ff
};
typedef DWORD PROCESS_INFO_FIELDS;
```

```csharp
public enum enum_PROCESS_INFO_FIELDS { 
   PIF_FILE_NAME             = 0x00000001,
   PIF_BASE_NAME             = 0x00000002,
   PIF_TITLE                 = 0x00000004,
   PIF_PROCESS_ID            = 0x00000008,
   PIF_SESSION_ID            = 0x00000010,
   PIF_ATTACHED_SESSION_NAME = 0x00000020,
   PIF_CREATION_TIME         = 0x00000040,
   PIF_FLAGS                 = 0x00000080,
   PIF_ALL                   = 0x000000ff
};
```

## <a name="fields"></a>字段
 `PIF_FILE_NAME`\
 初始化/使用 `bstrFileName` 结构PROCESS_INFO字段。 [](../../../extensibility/debugger/reference/process-info.md)

 `PIF_BASE_NAME`\
 初始化/使用 `bstrBaseName` 结构的 `PROCESS_INFO` 字段。

 `PIF_TITLE`\
 初始化/使用 `bstrTitle` 结构的 `PROCESS_INFO` 字段。

 `PIF_PROCESS_ID`\
 初始化/使用 `ProcessId` 结构的 `PROCESS_INFO` 字段。

 `PIF_SESSION_ID`\
 初始化/使用 `dwSessionId` 结构的 `PROCESS_INFO` 字段。

 `PIF_ATTACHED_SESSION_NAME`\
 初始化/使用 `bstrAttachedSessionName` 结构的 `PROCESS_INFO` 字段。

 `PIF_CREATION_TIME`\
 初始化/使用 `CreationTime` 结构的 `PROCESS_INFO` 字段。

 `PIF_FLAGS`\
 初始化/使用 `Flags` 结构的 `PROCESS_INFO` 字段。

 `PIF_ALL`\
 填写所有字段。

## <a name="remarks"></a>备注
 传递给[GetInfo](../../../extensibility/debugger/reference/idebugprocess2-getinfo.md)方法以指示要初始化PROCESS_INFO的[](../../../extensibility/debugger/reference/process-info.md)字段。

 还用于 `Fields` 结构的 `PROCESS_INFO` 字段，以指示使用哪些字段且有效。

 这些标志可以与位 合并 `OR` 。

## <a name="requirements"></a>要求
 标头：msdbg.h

 命名空间：Microsoft.VisualStudio.Debugger.Interop

 程序集：Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>请参阅
- [枚举](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)
- [PROCESS_INFO](../../../extensibility/debugger/reference/process-info.md)
