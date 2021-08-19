---
description: 指定异常状态。
title: EXCEPTION_STATE |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- EXCEPTION_STATE
helpviewer_keywords:
- EXCEPTION_STATE enumeration
ms.assetid: 597f4f4c-9b70-485c-b5dc-3c2e3aecc664
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 26729a2b7be80f60c0eb3720bf1853247558314f
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122072988"
---
# <a name="exception_state"></a>EXCEPTION_STATE
指定异常状态。

## <a name="syntax"></a>语法

```cpp
enum enum_EXCEPTION_STATE {
    EXCEPTION_NONE                          = 0x0000,
    EXCEPTION_STOP_FIRST_CHANCE             = 0x0001,
    EXCEPTION_STOP_SECOND_CHANCE            = 0x0002,
    EXCEPTION_STOP_USER_FIRST_CHANCE        = 0x0010,
    EXCEPTION_STOP_USER_UNCAUGHT            = 0x0020,
    EXCEPTION_STOP_ALL                      = 0x00FF,
    EXCEPTION_CANNOT_BE_CONTINUED           = 0x0100,

    // These are for exception types only
    EXCEPTION_CODE_SUPPORTED                = 0x1000,
    EXCEPTION_CODE_DISPLAY_IN_HEX           = 0x2000,
    EXCEPTION_JUST_MY_CODE_SUPPORTED        = 0x4000,
    EXCEPTION_MANAGED_DEBUG_ASSISTANT       = 0x8000,

    // These are no longer used
    EXCEPTION_STOP_FIRST_CHANCE_USE_PARENT      = 0x0004,
    EXCEPTION_STOP_SECOND_CHANCE_USE_PARENT     = 0x0008,
    EXCEPTION_STOP_USER_FIRST_CHANCE_USE_PARENT = 0x0040,
    EXCEPTION_STOP_USER_UNCAUGHT_USE_PARENT     = 0x0080,
};
typedef DWORD EXCEPTION_STATE;
```

```csharp
public enum enum_EXCEPTION_STATE {
    EXCEPTION_NONE                          = 0x0000,
    EXCEPTION_STOP_FIRST_CHANCE             = 0x0001,
    EXCEPTION_STOP_SECOND_CHANCE            = 0x0002,
    EXCEPTION_STOP_USER_FIRST_CHANCE        = 0x0010,
    EXCEPTION_STOP_USER_UNCAUGHT            = 0x0020,
    EXCEPTION_STOP_ALL                      = 0x00FF,
    EXCEPTION_CANNOT_BE_CONTINUED           = 0x0100,

    // These are for exception types only
    EXCEPTION_CODE_SUPPORTED                = 0x1000,
    EXCEPTION_CODE_DISPLAY_IN_HEX           = 0x2000,
    EXCEPTION_JUST_MY_CODE_SUPPORTED        = 0x4000,
    EXCEPTION_MANAGED_DEBUG_ASSISTANT       = 0x8000,

    // These are no longer used
    EXCEPTION_STOP_FIRST_CHANCE_USE_PARENT      = 0x0004,
    EXCEPTION_STOP_SECOND_CHANCE_USE_PARENT     = 0x0008,
    EXCEPTION_STOP_USER_FIRST_CHANCE_USE_PARENT = 0x0040,
    EXCEPTION_STOP_USER_UNCAUGHT_USE_PARENT     = 0x0080,
};
```

## <a name="fields"></a>字段
`EXCEPTION_NONE`\
异常时请勿停止。

`EXCEPTION_STOP_FIRST_CHANCE`\
发生异常时停止。 描述异常事件时，此标志指示异常事件是第一次异常事件。

`EXCEPTION_STOP_SECOND_CHANCE`\
在第二次引发异常时停止。 描述异常事件时，指示异常事件是第二次异常事件。

`EXCEPTION_STOP_USER_FIRST_CHANCE`\
第一次触发用户模式异常时停止。 描述异常事件时，指示异常事件是第一次用户异常事件。

`EXCEPTION_STOP_USER_UNCAUGHT`\
在未捕获到用户模式异常时停止。 描述异常事件时，指示异常事件是未捕获的用户模式异常事件。

`EXCEPTION_STOP_ALL`\
出现任何异常时停止。 描述异常事件时不使用。

`EXCEPTION_CANNOT_BE_CONTINUED`\
描述异常事件时，指示异常无法继续。

`EXCEPTION_CODE_SUPPORTED`\
指示异常具有支持它的代码。 用于显示异常

`EXCEPTION_CODE_DISPLAY_IN_HEX`\
指示异常代码应以十六进制显示。 用于显示异常。

`EXCEPTION_JUST_MY_CODE_SUPPORTED`\
指示异常代码支持 JustMyCode。 用于显示异常。

`EXCEPTION_MANAGED_DEBUG_ASSISTANT`\
指示托管代码调试器应处理异常。 如果未设置，则默认调试器会处理异常。 这会传递到 [SetAllExceptions](../../../extensibility/debugger/reference/idebugengine3-setallexceptions.md) 方法，而不会在 [EXCEPTION_INFO](../../../extensibility/debugger/reference/exception-info.md) 结构中使用。

`EXCEPTION_STOP_FIRST_CHANCE_USE_PARENT`\
过时，不使用。

`EXCEPTION_STOP_SECOND_CHANCE_USE_PARENT`\
过时，不使用。

`EXCEPTION_STOP_USER_FIRST_CHANCE_USE_PARENT`\
过时，不使用。

`EXCEPTION_STOP_USER_SECOND_CHANCE_USE_PARENT`\
过时，不使用。

## <a name="remarks"></a>备注
用作 `dwState` [EXCEPTION_INFO](../../../extensibility/debugger/reference/exception-info.md) 结构的成员，以指示异常的状态以及可对其执行的操作。

还会将这些值传递给 [SetAllExceptions](../../../extensibility/debugger/reference/idebugengine3-setallexceptions.md) 方法，以设置所有异常的状态。

这些标志可以与按位 "或" 组合在一起。

## <a name="requirements"></a>要求
标头： msdbg

命名空间： VisualStudio

程序集： Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>请参阅
- [枚举](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)
- [EXCEPTION_INFO](../../../extensibility/debugger/reference/exception-info.md)
- [SetAllExceptions](../../../extensibility/debugger/reference/idebugengine3-setallexceptions.md)
