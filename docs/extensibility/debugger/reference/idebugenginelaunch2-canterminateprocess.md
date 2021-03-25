---
description: 确定进程是否可以终止。
title: IDebugEngineLaunch2：： CanTerminateProcess |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugEngineLaunch2::CanTerminateProcess
helpviewer_keywords:
- IDebugEngineLaunch2::CanTerminateProcess
ms.assetid: 7973454d-c957-4123-a0ee-80ebcdbbd2d1
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 20df2c6d44e9bb0afd6610d6ded01ed637035b4b
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/25/2021
ms.locfileid: "105077442"
---
# <a name="idebugenginelaunch2canterminateprocess"></a>IDebugEngineLaunch2::CanTerminateProcess
确定进程是否可以终止。

## <a name="syntax"></a>语法

```cpp
HRESULT CanTerminateProcess ( 
   IDebugProcess2* pProcess
);
```

```csharp
int CanTerminateProcess ( 
   IDebugProcess2 pProcess
);
```

## <a name="parameters"></a>参数
`pProcess`\
中表示要终止的进程的 [IDebugProcess2](../../../extensibility/debugger/reference/idebugprocess2.md) 对象。

## <a name="return-value"></a>返回值
 如果成功， `S_OK` 则返回; 否则返回错误代码。 `S_FALSE`如果引擎无法终止进程（例如，拒绝访问），则返回。

## <a name="remarks"></a>备注
 如果此方法返回 `S_OK` ，则可以调用 [TerminateProcess](../../../extensibility/debugger/reference/idebugenginelaunch2-terminateprocess.md) 方法来实际终止进程。

## <a name="see-also"></a>另请参阅
- [IDebugEngineLaunch2](../../../extensibility/debugger/reference/idebugenginelaunch2.md)
- [IDebugProcess2](../../../extensibility/debugger/reference/idebugprocess2.md)
- [TerminateProcess](../../../extensibility/debugger/reference/idebugenginelaunch2-terminateprocess.md)
