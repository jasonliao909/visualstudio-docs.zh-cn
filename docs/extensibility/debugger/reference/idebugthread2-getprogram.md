---
description: 获取线程正在其中运行的程序。
title: IDebugThread2：： GetProgram |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugThread2::GetProgram
helpviewer_keywords:
- IDebugThread2::GetProgram
ms.assetid: 8c9c5ea1-2031-472e-bc8f-30e22e754566
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: cd58ffb9cbcfd073d20643c4702194759f6267a0
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2021
ms.locfileid: "102164586"
---
# <a name="idebugthread2getprogram"></a>IDebugThread2::GetProgram
获取线程正在其中运行的程序。

## <a name="syntax"></a>语法

```cpp
HRESULT GetProgram ( 
   IDebugProgram2** ppProgram
);
```

```csharp
int GetProgram ( 
   out IDebugProgram2 ppProgram
);
```

## <a name="parameters"></a>参数
`ppProgram`\
弄返回一个 [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md) 对象，该对象表示此线程正在其中运行的程序。

## <a name="return-value"></a>返回值
 如果成功， `S_OK` 则返回; 否则返回错误代码。

## <a name="see-also"></a>另请参阅
- [IDebugThread2](../../../extensibility/debugger/reference/idebugthread2.md)
- [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)
