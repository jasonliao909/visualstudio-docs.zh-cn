---
description: 此方法通知进程会话现在正在调试进程。
title: IDebugProcessEx2：：Attach |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProcessEx2::Attach
helpviewer_keywords:
- IDebugProcessEx2::Attach method
ms.assetid: f3334ed7-39bf-4d02-a338-36f567b9b287
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 5687031d1b4cd0be439ef1953f54a609e19f6366
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122071921"
---
# <a name="idebugprocessex2attach"></a>IDebugProcessEx2::Attach
此方法通知进程会话现在正在调试进程。

## <a name="syntax"></a>语法

```cpp
HRESULT Attach( 
   IDebugSession2* pSession
);
```

```csharp
int Attach(
   IDebugSession2 pSession
);
```

## <a name="parameters"></a>参数
`pSession`\
[in]一个 值，该值唯一标识附加到此进程的会话。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK` ;否则返回错误代码。

## <a name="remarks"></a>备注
 传入的接口只被视为 Cookie，该值唯一标识附加到该进程的会话调试管理器;所提供的接口上的方法均 `pSession` 不起作用。

## <a name="see-also"></a>请参阅
- [IDebugProcessEx2](../../../extensibility/debugger/reference/idebugprocessex2.md)
