---
description: 提供可选标志，这些标志可用于在设置断点时指定其他信息。
title: BP_FLAGS |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- BP_FLAGS
helpviewer_keywords:
- BP_FLAGS enumeration
ms.assetid: c45dfc74-5e7f-4f1e-a147-ab2a55dccbd0
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 5f0d79bd6e3c1495f85ed6f8436a781445173810
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122104646"
---
# <a name="bp_flags"></a>BP_FLAGS
提供可选标志，这些标志可用于在设置断点时指定其他信息。

## <a name="syntax"></a>语法

```cpp
enum enum_BP_FLAGS {
    BP_FLAG_NONE            = 0x0000,
    BP_FLAG_MAP_DOCPOSITION = 0x0001,
    BP_FLAG_DONT_STOP       = 0x0002
};
typedef DWORD BP_FLAGS;
```

```csharp
public enum enum_BP_FLAGS {
    BP_FLAG_NONE            = 0x0000,
    BP_FLAG_MAP_DOCPOSITION = 0x0001,
    BP_FLAG_DONT_STOP       = 0x0002
};
```

## <a name="fields"></a>字段
`BP_FLAG_NONE`\
不指定断点标志。

`BP_FLAG_MAP_DOCPOSITION`\
指定调试引擎 (DE) 应该使用文档位置映射断点。 这仅适用于在面向脚本的源文件中设置的断点，例如 ACTIVE Server Pages (ASP) 。

`BP_FLAG_DONT_STOP`\
指定调试引擎应处理断点，但调试引擎最终不应停止 (也就是说，不应将 [IDebugBreakpointEvent2](../../../extensibility/debugger/reference/idebugbreakpointevent2.md) 事件对象) 。 此标志主要用于跟踪点。

## <a name="remarks"></a>备注
用于 `dwFlags` 成员和BP_REQUEST_INFO BP_REQUEST_INFO2[](../../../extensibility/debugger/reference/bp-request-info.md)成员。 [](../../../extensibility/debugger/reference/bp-request-info2.md)

这些值可以与位 合并 `OR` 。

## <a name="requirements"></a>要求
标头：msdbg.h

命名空间：Microsoft.VisualStudio.Debugger.Interop

程序集：Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>请参阅
- [枚举](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)
- [BP_REQUEST_INFO](../../../extensibility/debugger/reference/bp-request-info.md)
- [BP_REQUEST_INFO2](../../../extensibility/debugger/reference/bp-request-info2.md)
- [IDebugBreakpointEvent2](../../../extensibility/debugger/reference/idebugbreakpointevent2.md)
