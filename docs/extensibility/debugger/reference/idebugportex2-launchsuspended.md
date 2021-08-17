---
description: 启动可执行文件。
title: IDebugPortEx2：： LaunchSuspended |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugPortEx2::LaunchSuspended
helpviewer_keywords:
- IDebugPortEx2::LaunchSuspended
ms.assetid: 34b2cf99-2e52-4757-8969-1d12ac517ec0
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 0c6db6cc7f67cc8cb4106215d33eb791c551a66b
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122030277"
---
# <a name="idebugportex2launchsuspended"></a>IDebugPortEx2::LaunchSuspended
启动可执行文件。

## <a name="syntax"></a>语法

```cpp
HRESULT LaunchSuspended( 
   LPCOLESTR        pszExe,
   LPCOLESTR        pszArgs,
   LPCOLESTR        pszDir,
   BSTR             bstrEnv,
   DWORD            hStdInput,
   DWORD            hStdOutput,
   DWORD            hStdError,
   IDebugProcess2** ppPortProcess
);
```

```csharp
int LaunchSuspended( 
   string             pszExe,
   string             pszArgs,
   string             pszDir,
   string             bstrEnv,
   uint               hStdInput,
   uint               hStdOutput,
   uint               hStdError,
   out IDebugProcess2 ppPortProcess
);
```

## <a name="parameters"></a>参数
`pszExe`\
中要启动的可执行文件的名称。 此路径可以是完整路径，也可以是在参数中指定的工作目录 `pszDir` 。

`pszArgs`\
中要传递给可执行文件的参数。 如果没有参数，则可以为 null 值。

`pszDir`\
中可执行文件使用的工作目录的名称。 如果不需要任何工作目录，则可以为 null 值。

`bstrEnv`\
中以 null 结尾的字符串的环境块，后跟一个其他 NULL 终止符。

`hStdInput`\
中替代输入流的句柄。 如果不需要重定向，则可以为0。

`hStdOutput`\
中备用输出流的句柄。 如果不需要重定向，则可以为0。

`hStdError`\
中备用错误输出流的句柄。 如果不需要重定向，则可以为0。

`ppPortProcess`\
弄返回一个 [IDebugPendingBreakpoint2](../../../extensibility/debugger/reference/idebugpendingbreakpoint2.md) 对象，该对象表示已启动的进程。

## <a name="return-value"></a>返回值
 如果成功， `S_OK` 则返回; 否则返回错误代码。

## <a name="remarks"></a>备注
 此方法应启动进程，使其挂起并且不运行任何代码。 调用 [ResumeProcess](../../../extensibility/debugger/reference/idebugportex2-resumeprocess.md) 方法以恢复进程。

 还可以从调试引擎启动程序。 有关详细信息，请参阅 [启动程序](../../../extensibility/debugger/launching-a-program.md)。

## <a name="see-also"></a>请参阅
- [IDebugPortEx2](../../../extensibility/debugger/reference/idebugportex2.md)
- [IDebugPendingBreakpoint2](../../../extensibility/debugger/reference/idebugpendingbreakpoint2.md)
- [ResumeProcess](../../../extensibility/debugger/reference/idebugportex2-resumeprocess.md)
- [启动程序](../../../extensibility/debugger/launching-a-program.md)
