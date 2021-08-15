---
description: 确定会话调试管理器 (SDM) 是否可以分离进程。
title: IDebugProcess2：： CanDetach |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProcess2::CanDetach
helpviewer_keywords:
- IDebugProcess2::CanDetach
ms.assetid: 2830f7c3-69fb-474a-97b8-5b869e38d546
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: f89e96ca584ea6bcbe2f3f5e24e919c352cb450de2ffc915c1e9f4bd81a203cf
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121339042"
---
# <a name="idebugprocess2candetach"></a>IDebugProcess2::CanDetach
确定会话调试管理器 (SDM) 是否可以分离进程。

## <a name="syntax"></a>语法

```cpp
HRESULT CanDetach(
   void
);
```

```csharp
int CanDetach();
```

## <a name="return-value"></a>返回值
 如果成功，则返回， `S_OK.` `S_FALSE` 如果调试器无法与进程分离，则返回。 否则，返回错误代码。

## <a name="see-also"></a>另请参阅
- [CanDetach](../../../extensibility/debugger/reference/idebugprogram2-candetach.md)
- [IDebugProcess2](../../../extensibility/debugger/reference/idebugprocess2.md)
