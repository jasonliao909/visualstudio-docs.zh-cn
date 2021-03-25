---
description: 获取系统线程标识符。
title: IDebugThread2：： GetThreadId |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugThread2::GetThreadId
helpviewer_keywords:
- IDebugThread2::GetThreadId
ms.assetid: db8b1c07-6b86-47f9-b292-bac19c276d36
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 39702dad7ad154e2922f217f36c13a47588cb06d
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/25/2021
ms.locfileid: "105053030"
---
# <a name="idebugthread2getthreadid"></a>IDebugThread2::GetThreadId
获取系统线程标识符。

## <a name="syntax"></a>语法

```cpp
HRESULT GetThreadId (
    DWORD* pdwThreadId
);
```

```csharp
int GetThreadId (
    out uint pdwThreadId
);
```

## <a name="parameters"></a>参数
`pdwThreadId`\
弄返回系统线程标识符。

## <a name="return-value"></a>返回值
如果成功， `S_OK` 则返回; 否则返回错误代码。

## <a name="remarks"></a>备注
线程 ID 用于标识进程中的所有其他线程中的线程。

## <a name="example"></a>示例
下面的示例演示如何对 `CProgram` 实现 [IDebugThread2](../../../extensibility/debugger/reference/idebugthread2.md) 接口的简单对象实现此方法。

```cpp
HRESULT CProgram::GetThreadId(DWORD* pdwThreadId) {
    *pdwThreadId = GetCurrentThreadId();
    return NOERROR;
}
```

## <a name="see-also"></a>另请参阅
- [IDebugThread2](../../../extensibility/debugger/reference/idebugthread2.md)
