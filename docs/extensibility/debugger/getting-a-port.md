---
title: 获取端口|Microsoft Docs
description: 了解如何Visual Studio向调试引擎提供一个端口，以向该端口注册程序节点并满足对进程信息的请求。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- ports, getting
- debugging [Debugging SDK], ports
ms.assetid: 745c2337-cfff-4d02-b49c-3ca7c4945c5e
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
ms.openlocfilehash: 1fda47e5ea15b1c09a4f08ff050ac15389e129f9408bef90506c64c275d126aa
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121342721"
---
# <a name="get-a-port"></a>获取端口
端口表示与正在运行进程计算机的连接。 该计算机可以是本地计算机或远程计算机 (运行非基于 Windows的操作系统;有关详细信息[，](../../extensibility/debugger/ports.md)请参阅端口) 。

端口由 [IDebugPort2 接口](../../extensibility/debugger/reference/idebugport2.md) 表示。 它用于获取有关端口连接到的计算机上运行的进程的信息。

调试引擎需要访问端口才能向端口注册程序节点，并满足对进程信息的请求。 例如，如果调试引擎实现 [IDebugProgramProvider2](../../extensibility/debugger/reference/idebugprogramprovider2.md) 接口， [则 GetProviderProcessData](../../extensibility/debugger/reference/idebugprogramprovider2-getproviderprocessdata.md) 方法的实现可能会请求端口返回必要的进程信息。

Visual Studio向调试引擎提供所需的端口，然后从端口供应商获取此端口。 如果程序从调试器内部附加到 (或由于引发异常（触发实时 [JIT] 对话框) ），则用户可以选择传输 (端口供应商) 使用另一个名称。 否则，如果用户从调试器中启动程序，则项目系统将指定使用的端口供应商。 在任一Visual Studio，实例化由[IDebugPortSupplier2](../../extensibility/debugger/reference/idebugportsupplier2.md)接口表示的端口供应商，并通过使用[IDebugPortRequest2](../../extensibility/debugger/reference/idebugportrequest2.md)接口调用[AddPort](../../extensibility/debugger/reference/idebugportsupplier2-addport.md)来请求新端口。 然后，此端口以一种或另一种形式传递给调试引擎。

## <a name="example"></a>示例
此代码片段演示如何使用提供给 [LaunchSuspended](../../extensibility/debugger/reference/idebugenginelaunch2-launchsuspended.md) 的端口在 ResumeProcess 中注册 [程序节点](../../extensibility/debugger/reference/idebugenginelaunch2-resumeprocess.md)。 为清楚起见，省略了与此概念不直接相关的参数。

> [!NOTE]
> 此示例使用 端口启动和恢复进程，并假定 [IDebugPortEx2](../../extensibility/debugger/reference/idebugportex2.md) 接口在端口上实现。 这并不是执行这些任务的唯一方法，并且除了向端口提供程序的 [IDebugProgramNode2](../../extensibility/debugger/reference/idebugprogramnode2.md) 外，甚至可能不会涉及该端口。

```cpp
// This is an IDebugEngineLaunch2 method.
HRESULT CDebugEngine::LaunchSuspended(/* omitted parameters */,
                                      IDebugPort2 *pPort,
                                      /* omitted parameters */,
                                      IDebugProcess2**ppDebugProcess)
{
    // do stuff here to set up for a launch (such as handling the other parameters)
    ...

    // Now get the IPortNotify2 interface so we can register a program node
    // in CDebugEngine::ResumeProcess.
    CComPtr<IDebugDefaultPort2> spDefaultPort;
    HRESULT hr = pPort->QueryInterface(&spDefaultPort);
    if (SUCCEEDED(hr))
    {
        CComPtr<IDebugPortNotify2> spPortNotify;
        hr = spDefaultPort->GetPortNotify(&spPortNotify);
        if (SUCCEEDED(hr))
        {
            // Remember the port notify so we can use it in ResumeProcess.
            m_spPortNotify = spPortNotify;

            // Now launch the process in a suspended state and return the
            // IDebugProcess2 interface
            CComPtr<IDebugPortEx2> spPortEx;
            hr = pPort->QueryInterface(&spPortEx);
            if (SUCCEEDED(hr))
            {
                // pass on the parameters we were given (omitted here)
                hr = spPortEx->LaunchSuspended(/* omitted parameters */,ppDebugProcess)
            }
        }
    }
    return(hr);
}

HRESULT CDebugEngine::ResumeProcess(IDebugProcess2 *pDebugProcess)
{
    // Make a program node for this process
    HRESULT hr;
    CComPtr<IDebugProgramNode2> spProgramNode;
    hr = this->GetProgramNodeForProcess(pProcess, &spProgramNode);
    if (SUCCEEDED(hr))
    {
        hr = m_spPortNotify->AddProgramNode(spProgramNode);
        if (SUCCEEDED(hr))
        {
            // resume execution of the process using the port given to us earlier.
            // (Querying for the IDebugPortEx2 interface is valid here since
            // that's how we got the IDebugPortNotify2 interface in the first place.)
            CComPtr<IDebugPortEx2> spPortEx;
            hr = m_spPortNotify->QueryInterface(&spPortEx);
            if (SUCCEEDED(hr))
            {
                hr = spPortEx->ResumeProcess(pDebugProcess);
            }
        }
    }
    return(hr);
}
```

## <a name="see-also"></a>另请参阅
- [注册程序](../../extensibility/debugger/registering-the-program.md)
- [启用要调试的程序](../../extensibility/debugger/enabling-a-program-to-be-debugged.md)
- [端口供应商](../../extensibility/debugger/port-suppliers.md)
- [端口](../../extensibility/debugger/ports.md)
