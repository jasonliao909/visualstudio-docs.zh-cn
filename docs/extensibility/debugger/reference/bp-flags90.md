---
description: 枚举可选标志的有效值。
title: BP_FLAGS90 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- BP_FLAGS90 enumeration
ms.assetid: 3e5a06c5-fb30-4b8a-b2d5-4a0570fc80bd
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 24e6b8bcefd47ddded83c28fc7d5df71327ced86
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122080099"
---
# <a name="bp_flags90"></a>BP_FLAGS90
枚举可选标志的有效值。 设置断点时，可选标志可用于指定其他信息。 此枚举 [扩展BP_FLAGS枚举](../../../extensibility/debugger/reference/bp-flags.md) 。

## <a name="syntax"></a>语法

```cpp
enum enum_BP_FLAGS90
{
    // VS 8.0 values
    BP90_FLAG_NONE               = 0x0000,
    BP90_FLAG_MAP_DOCPOSITION    = 0x0001,
    BP90_FLAG_DONT_STOP          = 0x0002,

    // Values added in VS 9.0
    BP90_FLAG_TRACEPOINT_CONTINUE = 0x0004,
};
typedef DWORD BP_FLAGS90;
```

```csharp
public enum enum_BP_FLAGS90
{
    // VS 8.0 values
    BP90_FLAG_NONE                = 0x0000,
    BP90_FLAG_MAP_DOCPOSITION     = 0x0001,
    BP90_FLAG_DONT_STOP           = 0x0002,

    // Values added in VS 9.0
    BP90_FLAG_TRACEPOINT_CONTINUE = 0x0004,
};
```

## <a name="fields"></a>字段
`BP90_FLAG_NONE`\
不指定断点标志。

`BP90_FLAG_MAP_DOCPOSITION`\
指定调试引擎 (DE) 应该使用文档位置映射断点。 这仅适用于面向脚本的源文件中设置的断点，例如 Active Server Pages (ASP) 。

`BP90_FLAG_DONT_STOP`\
指定调试引擎应处理断点，但调试引擎最终不应停止该断点;也就是说， [不应发送 IDebugBreakpointEvent2](../../../extensibility/debugger/reference/idebugbreakpointevent2.md) 事件对象。 此标志主要用于跟踪点。

`BP90_FLAG_TRACEPOINT_CONTINUE`\
由本机调试引擎用来确定是否应清除单步执行状态。 它不同于BP90_FLAG_DONT_STOP，BP90_FLAG_DONT_STOP如果跟踪点执行宏，则不设置值。

## <a name="requirements"></a>要求
标头：Msdbg90.h

命名空间：Microsoft.VisualStudio.Debugger.Interop

程序集：Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>请参阅
- [枚举](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)
