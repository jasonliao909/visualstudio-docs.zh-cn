---
description: 此方法通过 DE (调试引擎启动) 。
title: IDebugEngineLaunch2：：LaunchSuspended |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugEngineLaunch2::LaunchSuspended
helpviewer_keywords:
- IDebugEngineLaunch2::LaunchSuspended
ms.assetid: 5dd2643e-c20a-470e-9024-2a423eb39856
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 27d4ae71dfa2c5a1c0f1d7806e1fa83c511a1bfd7131667880dce3dc5b3db54a
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121390081"
---
# <a name="idebugenginelaunch2launchsuspended"></a>IDebugEngineLaunch2::LaunchSuspended
此方法通过 DE (调试引擎启动) 。

## <a name="syntax"></a>语法

```cpp
HRESULT LaunchSuspended ( 
   LPCOLESTR             pszMachine,
   IDebugPort2*          pPort,
   LPCOLESTR             pszExe,
   LPCOLESTR             pszArgs,
   LPCOLESTR             pszDir,
   BSTR                  bstrEnv,
   LPCOLESTR             pszOptions,
   LAUNCH_FLAGS          dwLaunchFlags,
   DWORD                 hStdInput,
   DWORD                 hStdOutput,
   DWORD                 hStdError,
   IDebugEventCallback2* pCallback,
   IDebugProcess2**      ppDebugProcess
);
```

```csharp
int LaunchSuspended(
   string               pszServer,
   IDebugPort2          pPort,
   string               pszExe,
   string               pszArgs,
   string               pszDir,
   string               bstrEnv,
   string               pszOptions,
   enum_LAUNCH_FLAGS    dwLaunchFlags,
   uint                 hStdInput,
   uint                 hStdOutput,
   uint                 hStdError,
   IDebugEventCallback2 pCallback,
   out IDebugProcess2   ppProcess
);
```

## <a name="parameters"></a>参数
`pszMachine`\
[in]要启动进程的计算机的名称。 使用 null 值指定本地计算机。

`pPort`\
[in] [IDebugPort2](../../../extensibility/debugger/reference/idebugport2.md) 接口，表示程序将在中运行的端口。

`pszExe`\
[in]要启动的可执行文件的名称。

`pszArgs`\
[in]要传递给可执行文件的参数。 如果没有参数，则可能是 null 值。

`pszDir`\
[in]可执行文件使用的工作目录的名称。 如果不需要工作目录，则可能是 null 值。

`bstrEnv`\
[in]以 NULL 终止的字符串的环境块，后跟一个额外的 NULL 终止符。

`pszOptions`\
[in]可执行文件的选项。

`dwLaunchFlags`\
[in]指定 [LAUNCH_FLAGS的](../../../extensibility/debugger/reference/launch-flags.md) 会话。

`hStdInput`\
[in]备用输入流的句柄。 如果不需要重定向，则可能为 0。

`hStdOutput`\
[in]备用输出流的句柄。 如果不需要重定向，则可能为 0。

`hStdError`\
[in]备用错误输出流的句柄。 如果不需要重定向，则可能为 0。

`pCallback`\
[in]接收 [调试器事件的 IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md) 对象。

`ppDebugProcess`\
[out]返回生成的 [IDebugProcess2](../../../extensibility/debugger/reference/idebugprocess2.md) 对象，该对象表示启动的进程。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK` ;否则返回错误代码。

## <a name="remarks"></a>备注
 通常， [!INCLUDE[vsprvs](../../../code-quality/includes/vsprvs_md.md)] 使用 [LaunchSuspended](../../../extensibility/debugger/reference/idebugportex2-launchsuspended.md) 方法启动程序，然后将调试器附加到挂起的程序。 但是，在某些情况下，调试引擎可能需要启动程序 (例如，如果调试引擎是解释器的一部分，并且正在调试的程序是解释语言) ，在这种情况下使用 方法 [!INCLUDE[vsprvs](../../../code-quality/includes/vsprvs_md.md)] `IDebugEngineLaunch2::LaunchSuspended` 。

 调用 [ResumeProcess](../../../extensibility/debugger/reference/idebugenginelaunch2-resumeprocess.md) 方法，在进程成功启动后以挂起状态启动进程。

## <a name="see-also"></a>请参阅
- [IDebugEngineLaunch2](../../../extensibility/debugger/reference/idebugenginelaunch2.md)
- [IDebugPort2](../../../extensibility/debugger/reference/idebugport2.md)
- [LAUNCH_FLAGS](../../../extensibility/debugger/reference/launch-flags.md)
- [IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md)
- [IDebugProcess2](../../../extensibility/debugger/reference/idebugprocess2.md)
- [LaunchSuspended](../../../extensibility/debugger/reference/idebugportex2-launchsuspended.md)
- [ResumeProcess](../../../extensibility/debugger/reference/idebugenginelaunch2-resumeprocess.md)
