---
description: 获取运行此程序的进程。
title: IDebugProgram2：：GetProcess |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProgram2::GetProcess
helpviewer_keywords:
- IDebugProgram2::GetProcess
ms.assetid: 1d602485-ebaf-451c-9165-f2e226f20a90
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 135d8e632b4cef71050db0ba326388170037e732
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122126539"
---
# <a name="idebugprogram2getprocess"></a>IDebugProgram2::GetProcess
获取运行此程序的进程。

## <a name="syntax"></a>语法

```cpp
HRESULT GetProcess(
   IDebugProcess2** ppProcess
);
```

```csharp
int GetProcess(
   out IDebugProcess2 ppProcess
);
```

## <a name="parameters"></a>参数
`ppProcess`\
[out]返回 [表示进程的 IDebugProcess2](../../../extensibility/debugger/reference/idebugprocess2.md) 接口。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK` ;否则返回错误代码。

## <a name="remarks"></a>备注
 除非调试引擎 (DE) 实现[IDebugEngineLaunch2](../../../extensibility/debugger/reference/idebugenginelaunch2.md)接口，否则 DE 的此方法实现应始终返回 ，因为 DE 无法确定它正在哪个进程中运行，因此无法满足此方法的实现。 `E_NOTIMPL`

 实现 接口意味着 DE 必须知道如何创建进程;因此，DE 对 `IDebugEngineLaunch2` [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md) 接口的实现能够知道它正在其中运行的进程。

## <a name="see-also"></a>请参阅
- [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)
- [IDebugProcess2](../../../extensibility/debugger/reference/idebugprocess2.md)
- [IDebugEngineLaunch2](../../../extensibility/debugger/reference/idebugenginelaunch2.md)
