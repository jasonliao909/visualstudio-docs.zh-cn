---
description: 描述或指定进程的属性。
title: PROCESS_INFO_FLAGS |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- PROCESS_INFO_FLAGS
helpviewer_keywords:
- PROCESS_INFO_FLAGS enumeration
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: c2708f2cdf4d2bb9150eaf1b5f235ddecc4164e3
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122050528"
---
# <a name="process_info_flags"></a>PROCESS_INFO_FLAGS

描述或指定进程的属性。

## <a name="syntax"></a>语法

```cpp
enum enum_PROCESS_INFO_FLAGS { 
   PIFLAG_SYSTEM_PROCESS    = 0x00000001,
   PIFLAG_DEBUGGER_ATTACHED = 0x00000002,
   PIFLAG_PROCESS_STOPPED   = 0x00000004,
   PIFLAG_PROCESS_RUNNING   = 0x00000008,
};
typedef DWORD PROCESS_INFO_FLAGS;
```

```csharp
enum enum_PROCESS_INFO_FLAGS { 
   PIFLAG_SYSTEM_PROCESS    = 0x00000001,
   PIFLAG_DEBUGGER_ATTACHED = 0x00000002,
   PIFLAG_PROCESS_STOPPED   = 0x00000004,
   PIFLAG_PROCESS_RUNNING   = 0x00000008,
};
```

## <a name="fields"></a>字段

`PIFLAG_SYSTEM_PROCESS`\
指示该进程是一个系统进程。

`PIFLAG_DEBUGGER_ATTACHED`\
指示进程正在由调试器调试。 它可以是调试器，也可能是一些其他调试器， [!INCLUDE[vsprvs](../../../code-quality/includes/vsprvs_md.md)] 例如 WinDbg。

`PIFLAG_PROCESS_STOPPED`\
指示进程已停止。 仅在还指定了 `PIFLAG_DEBUGGER_ATTACHED` 时有效。 在 Visual Studio 2005 及更高版本中可用。

`PIFLAG_PROCESS_RUNNING`\
指示进程正在运行。 仅在还指定了 `PIFLAG_DEBUGGER_ATTACHED` 时有效。 在 Visual Studio 2005 及更高版本中可用。

## <a name="remarks"></a>备注

用于 `Flags` 结构PROCESS_INFO成员。 [](../../../extensibility/debugger/reference/process-info.md)

这些标志可以与位 合并 `OR` 。

## <a name="requirements"></a>要求

标头：msdbg.h

命名空间：Microsoft.VisualStudio.Debugger.Interop

程序集：Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>请参阅

- [枚举](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)
- [PROCESS_INFO](../../../extensibility/debugger/reference/process-info.md)
