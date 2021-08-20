---
description: 枚举指定要检索有关断点请求的信息的有效值。
title: BPREQI_FIELDS90 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- BPREQI_FIELDS90 enumeration
ms.assetid: bf6f7efc-39f2-46a2-906d-c3647bf89995
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 859da0750f3522ae8a889612ae13db43816aa4d1
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122145739"
---
# <a name="bpreqi_fields90"></a>BPREQI_FIELDS90
枚举指定要检索有关断点请求的信息的有效值。 此枚举 [扩展BPREQI_FIELDS枚举](../../../extensibility/debugger/reference/bpreqi-fields.md) 。

## <a name="syntax"></a>语法

```cpp
enum enum_BPREQI_FIELDS90
{
    // VS 8.0 values
    BPREQI90_BPLOCATION                = 0x0001,
    BPREQI90_LANGUAGE                  = 0x0002,
    BPREQI90_PROGRAM                   = 0x0004,
    BPREQI90_PROGRAMNAME               = 0x0008,
    BPREQI90_THREAD                    = 0x0010,
    BPREQI90_THREADNAME                = 0x0020,
    BPREQI90_PASSCOUNT                 = 0x0040,
    BPREQI90_CONDITION                 = 0x0080,
    BPREQI90_FLAGS                     = 0x0100,
    BPREQI90_ALLOLDFIELDS              = 0x01ff,
    BPREQI90_VENDOR                    = 0x0200,
    BPREQI90_CONSTRAINT                = 0x0400,
    BPREQI90_TRACEPOINT                = 0x0800,

    // Values added in VS 9.0
    BPREQI90_MACROTRACEPOINT           = 0x1000,

    BPREQI90_ALLFIELDS                 = 0xffff
};
typedef DWORD BPREQI_FIELDS90;
```

```csharp
public enum enum_BPREQI_FIELDS90
{
    // VS 8.0 values
    BPREQI90_BPLOCATION                = 0x0001,
    BPREQI90_LANGUAGE                  = 0x0002,
    BPREQI90_PROGRAM                   = 0x0004,
    BPREQI90_PROGRAMNAME               = 0x0008,
    BPREQI90_THREAD                    = 0x0010,
    BPREQI90_THREADNAME                = 0x0020,
    BPREQI90_PASSCOUNT                 = 0x0040,
    BPREQI90_CONDITION                 = 0x0080,
    BPREQI90_FLAGS                     = 0x0100,
    BPREQI90_ALLOLDFIELDS              = 0x01ff,
    BPREQI90_VENDOR                    = 0x0200,
    BPREQI90_CONSTRAINT                = 0x0400,
    BPREQI90_TRACEPOINT                = 0x0800,

    // Values added in VS 9.0
    BPREQI90_MACROTRACEPOINT           = 0x1000,

    BPREQI90_ALLFIELDS                 = 0xffff
};
```

## <a name="fields"></a>字段
`BPREQI90_BPLOCATION`\
初始化或使用 (或) 结构 `bpLocation` BP_REQUEST_INFO BP_REQUEST_INFO2断点位置。 [](../../../extensibility/debugger/reference/bp-request-info.md) [](../../../extensibility/debugger/reference/bp-request-info2.md)

`BPREQI90_LANGUAGE`\
初始化或使用 或 `guidLanguage` 结构的 `BP_REQUEST_INFO` `BP_REQUEST_INFO2` 字段。

`BPREQI90_PROGRAM`\
初始化或使用 或 `pProgram` 结构的 `BP_REQUEST_INFO` `BP_REQUEST_INFO2` 字段。

`BPREQI90_PROGRAMNAME`\
初始化或使用 或 `bstrProgramName` 结构的 `BP_REQUEST_INFO` `BP_REQUEST_INFO2` 字段。

`BPREQI90_THREAD`\
初始化或使用 或 `pThread` 结构的 `BP_REQUEST_INFO` `BP_REQUEST_INFO2` 字段。

`BPREQI90_THREADNAME`\
初始化或使用 或 `bstrThreadName` 结构的 `BP_REQUEST_INFO` `BP_REQUEST_INFO2` 字段。

`BPREQI90_PASSCOUNT`\
初始化或使用 或 `bpPassCount` 结构的 `BP_REQUEST_INFO` `BP_REQUEST_INFO2` 字段。

`BPREQI90_CONDITION`\
初始化或使用 或 `bpCondition` (字段) 断 `BP_REQUEST_INFO` 点 `BP_REQUEST_INFO2` 条件。

`BPREQI90_FLAGS`\
初始化或使用 或 `dwFlags` 结构的 `BP_REQUEST_INFO` `BP_REQUEST_INFO2` 字段。

`BPREQI90_ALLOLDFIELDS`\
初始化或使用 结构 的所有 `BP_REQUEST_INFO` 字段。

`BPREQI90_VENDOR`\
初始化或使用 结构的 `guidVendor` `BP_REQUEST_INFO2` 字段。

`BPREQI90_CONSTRAINT`\
初始化或使用 结构的 `bstrConstraint` `BP_REQUEST_INFO2` 字段。

`BPREQI90_TRACEPOINT`\
初始化或使用 结构的 `bstrTracepoint` `BP_REQUEST_INFO2` 字段。

`BPREQI90_MACROTRACEPOINT`\
初始化或使用 结构的 `bstrMacroTracepoint` `BP_REQUEST_INFO2` 字段。 BPREQI_ALLFIELDS不包括此字段。

`BPREQI90_ALLFIELDS`\
指定结构的所有 `BP_REQUEST_INFO2` 字段。

## <a name="requirements"></a>要求
标头：Msdbg90.h

命名空间：Microsoft.VisualStudio.Debugger.Interop

程序集：Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>请参阅
- [枚举](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)
