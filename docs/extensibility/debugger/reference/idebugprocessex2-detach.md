---
description: 此方法通知进程，会话不再调试该进程。
title: IDebugProcessEx2：:D etach |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProcessEx2::Detach
helpviewer_keywords:
- IDebugProcessEx2::Detach method
ms.assetid: 66d54c2c-9302-47c8-9975-f30ed988ab29
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: c5ad25fe6461f1df89ada83623ab4e28194ca207
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/25/2021
ms.locfileid: "105076324"
---
# <a name="idebugprocessex2detach"></a>IDebugProcessEx2::Detach
此方法通知进程，会话不再调试该进程。

## <a name="syntax"></a>语法

```cpp
HRESULT Detach( 
   IDebugSession2* pSession
);
```

```csharp
int Detach(
   IDebugSession2 pSession
);
```

## <a name="parameters"></a>参数
`pSession`\
中一个值，该值唯一标识要从其分离此进程的会话。

## <a name="return-value"></a>返回值
 如果成功， `S_OK` 则返回; 否则返回错误代码。

## <a name="remarks"></a>备注
 传入的接口 `pSession` 仅被视为 cookie，这是唯一标识最初附加到此进程的会话调试管理器的值; 提供的接口上的任何方法都不起作用。

## <a name="see-also"></a>另请参阅
- [IDebugProcessEx2](../../../extensibility/debugger/reference/idebugprocessex2.md)
