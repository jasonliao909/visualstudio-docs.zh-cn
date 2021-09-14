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
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126665376"
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
指示进程是系统进程。

`PIFLAG_DEBUGGER_ATTACHED`\
指示调试器正在调试该进程。 它可能是一个 [!INCLUDE[vsprvs](../../../code-quality/includes/vsprvs_md.md)] 调试器，也可能是其他一些调试器，例如 WinDbg。

`PIFLAG_PROCESS_STOPPED`\
指示进程已停止。 仅当 `PIFLAG_DEBUGGER_ATTACHED` 还指定了时才有效。 在 Visual Studio 2005 及更高版本中可用。

`PIFLAG_PROCESS_RUNNING`\
指示进程正在运行。 仅当 `PIFLAG_DEBUGGER_ATTACHED` 还指定了时才有效。 在 Visual Studio 2005 及更高版本中可用。

## <a name="remarks"></a>备注

用于 `Flags` [PROCESS_INFO](../../../extensibility/debugger/reference/process-info.md) 结构的成员。

这些标志可以与按位组合 `OR` 。

## <a name="requirements"></a>要求

标头： msdbg

命名空间： VisualStudio

程序集： Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>请参阅

- [枚举](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)
- [PROCESS_INFO](../../../extensibility/debugger/reference/process-info.md)
