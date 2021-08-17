---
description: 用于确定程序是否可以在到达执行中的特定点后停止执行。
title: CANSTOP_REASON |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- CANSTOP_REASON
helpviewer_keywords:
- CANSTOP_REASON enumeration
ms.assetid: 6da944eb-36cd-4a8c-8d71-544c775cfcc1
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 995b197cd74612f324344c8fe9b74f9f96fc89449abfd83ba656f4102c9b52cf
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121378063"
---
# <a name="canstop_reason"></a>CANSTOP_REASON
用于确定程序是否可以在到达执行中的特定点后停止执行。

## <a name="syntax"></a>语法

```cpp
enum enum_CANSTOP_REASON {
    CANSTOP_ENTRYPOINT = 0x0000,
    CANSTOP_STEPIN     = 0x0001
};
typedef DWORD CANSTOP_REASON;
```

```csharp
public enum enum_CANSTOP_REASON {
    CANSTOP_ENTRYPOINT = 0x0000,
    CANSTOP_STEPIN     = 0x0001
};
```

## <a name="fields"></a>字段
`CANSTOP_ENTRYPOINT`\
指定给定程序的入口点。

`CANSTOP_STEPIN`\
指定单步执行函数。

## <a name="remarks"></a>备注
作为参数传递给 [GetReason](../../../extensibility/debugger/reference/idebugcanstopevent2-getreason.md) 方法，以便在到达程序的入口点或单步执行函数或方法之后停止后，使用会话调试管理器 (SDM) 来确认。

## <a name="requirements"></a>要求
标头： msdbg

命名空间： VisualStudio

程序集： Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>请参阅
- [枚举](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)
- [GetReason](../../../extensibility/debugger/reference/idebugcanstopevent2-getreason.md)
