---
description: 请求正在此进程中运行代码的下一个程序停止并发送 IDebugBreakEvent2 事件对象。
title: IDebugProcess2：：CauseBreak |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProcess2::CauseBreak
helpviewer_keywords:
- IDebugProcess2::CauseBreak
ms.assetid: efda8865-2319-4d53-90bf-6d9d74cd5195
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: c8431c4b283a7ec235483eeb4637f5f6bef60697
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122087998"
---
# <a name="idebugprocess2causebreak"></a>IDebugProcess2::CauseBreak
请求正在此进程中运行代码的下一个程序停止并发送 [IDebugBreakEvent2](../../../extensibility/debugger/reference/idebugbreakevent2.md) 事件对象。

## <a name="syntax"></a>语法

```cpp
HRESULT CauseBreak( 
   void
);
```

```csharp
int CauseBreak();
```

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK` ;否则返回错误代码。

## <a name="see-also"></a>请参阅
- [IDebugProcess2](../../../extensibility/debugger/reference/idebugprocess2.md)
