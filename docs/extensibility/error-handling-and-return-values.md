---
title: 错误处理和返回值|Microsoft Docs
description: 了解 Visual Studio SDK 如何提供互操作程序集，以在接收错误通知时记录丰富的错误信息。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- errors [Visual Studio SDK], handling
- error handling
- return values
ms.assetid: b2d9079d-39a6-438a-8010-290056694b5c
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: 187b2896026b7550d4e67df7cbf85d69dae99ac99184be5f456b19d7a862b16d
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121376880"
---
# <a name="error-handling-and-return-values"></a>错误处理和返回值
VSPackage 和 COM 对错误使用相同的体系结构。 和 函数是 Win32 应用程序编程接口的 `SetErrorInfo` `GetErrorInfo` 一部分， (API) 。 集成开发环境中的任何 VSPackage (IDE) 可以调用这些全局 Win32 API，以在接收错误通知时记录丰富的错误信息。 [!INCLUDE[vsipsdk](../extensibility/includes/vsipsdk_md.md)]提供互操作程序集来管理错误信息。

## <a name="interop-methods"></a>互操作方法
 为方便起见，IDE 提供了一个方法 ，以 <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell.SetErrorInfo%2A> 使用 ，而不是调用 Win32 API。 在托管代码中，使用 <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell.SetErrorInfo%2A> 。 当错误到达应显示错误消息的级别时 (通常是实现命令处理程序) 的对象，IDE 使用另一种方法 来显示相应的 `HRESULT` <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget> <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell.ReportErrorInfo%2A> 消息框。 在托管代码中使用 <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell.ReportErrorInfo%2A> 方法。

 作为 VSPackage 实现者，COM 对象通常实现 `ISupportErrorInfo` 。 `ISupportErrorInfo`接口可确保丰富的错误信息可以在调用链上垂直移动。 可能跨进程或跨线程使用的对象必须支持 ，以确保将丰富的错误信息正确封 `ISupportErrorInfo` 送回调用方。

 与 VSPackage 相关且涉及扩展 IDE 的所有对象（包括编辑器工厂、编辑器、层次结构和提供的服务）都应支持丰富的错误信息。 虽然 IDE 不需要这些 VSPackage 对象来实现 `ISupportErrorInfo` ，但始终建议这样做。

 每当 传播到 IDE 时，IDE 负责报告错误信息，并向 的用户 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] `HRESULT` 显示此信息。 IDE 也是创建对象 `ErrorInfo` 的机制。

## <a name="general-guidelines"></a>一般指南
 也可使用 <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell.SetErrorInfo%2A> 和 <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell.ReportErrorInfo%2A> 方法设置并报告 VSPackage 实现内部的错误。 但是，作为一般规则，请遵循以下准则来处理 VSPackage 中的错误消息：

- 在 `ISupportErrorInfo` VSPackage COM 对象中实现 。

- 创建一个错误报告机制，该机制 <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell.SetErrorInfo%2A> 在实现 的对象中调用 方法 <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget> 。

- 让 IDE 通过 方法向用户显示 <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell.ReportErrorInfo%2A> 错误。

## <a name="error-information-in-the-ide"></a>IDE 中的错误信息
 以下规则指示如何处理 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] IDE 中的错误信息：

- 作为保证不会向用户报告过时错误信息的防御策略，调用 方法的函数 <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell.ReportErrorInfo%2A> 应首先调用 <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell.SetErrorInfo%2A> 方法。 在调用 `null` 任何可能设置新错误信息的内容之前，请传递 以清除缓存的错误消息。

- 只有在不直接报告错误消息的函数返回错误 时 <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell.SetErrorInfo%2A> ，才允许调用 方法 `HRESULT` 。 在函数的条目上或在返回 时， `ErrorInfo` 可以清除 <xref:Microsoft.VisualStudio.VSConstants.S_OK> 。 此规则的唯一例外是当调用返回错误时，接收方可以从中 `HRESULT` 显式恢复或安全地忽略该错误。

- 显式忽略错误的任何一 `HRESULT` 方都必须使用 <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell.SetErrorInfo%2A> 调用 方法 <xref:Microsoft.VisualStudio.VSConstants.S_OK> 。 否则，当另一方在未提供自己的 的情况下生成错误时， `ErrorInfo` 可能会意外使用 `ErrorInfo` 该对象。

- 建议所有源自错误 `HRESULT` 的方法调用 方法来 <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell.SetErrorInfo%2A> 提供丰富的错误信息。 如果返回 `HRESULT` 的 是特殊 `FACILITY_ITF` 错误，则方法需要提供正确的 `ErrorInfo` 对象。 如果返回的错误是标准系统错误 (例如 、 等) 则无需显式调用 方法即可返回错误 <xref:Microsoft.VisualStudio.VSConstants.E_OUTOFMEMORY> <xref:Microsoft.VisualStudio.VSConstants.E_ABORT> <xref:Microsoft.VisualStudio.VSConstants.E_INVALIDARG> <xref:Microsoft.VisualStudio.VSConstants.E_UNEXPECTED> <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell.SetErrorInfo%2A> 代码。 作为防御性编码策略，在 (错误（包括) 错误）时，请始终调用 方法，同时更详细地描述故障 `HRESULT` <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell.SetErrorInfo%2A> `ErrorInfo` ，或 `null` 。

- 返回由另一个调用产生的错误的所有函数都必须传递从 中的失败调用接收的信息， `HRESULT` 而无需修改 `ErrorInfo` 对象。

## <a name="see-also"></a>请参阅
- <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget>
- [SetErrorInfo (Component Automation) ](/previous-versions/windows/desktop/api/oleauto/nf-oleauto-seterrorinfo)
- [GetErrorInfo](/previous-versions/windows/desktop/api/oleauto/nf-oleauto-geterrorinfo)
- [ISupportErrorInfo 接口](/previous-versions/windows/desktop/api/oaidl/nn-oaidl-isupporterrorinfo)
