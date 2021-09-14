---
description: 用于确定程序在到达执行中的特定点后能否停止执行。
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
ms.openlocfilehash: 4a9b61c9c77c015071e3661865b93575cb8bbb98
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126602487"
---
# <a name="canstop_reason"></a>CANSTOP_REASON
用于确定程序在到达执行中的特定点后能否停止执行。

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
作为参数传递给 [GetReason](../../../extensibility/debugger/reference/idebugcanstopevent2-getreason.md) 方法，以使用会话调试管理器 (SDM) 确认在到达程序的入口点或单步执行函数或方法后是否可停止。

## <a name="requirements"></a>要求
标头：msdbg.h

命名空间：Microsoft.VisualStudio.Debugger.Interop

程序集：Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>请参阅
- [枚举](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)
- [GetReason](../../../extensibility/debugger/reference/idebugcanstopevent2-getreason.md)
