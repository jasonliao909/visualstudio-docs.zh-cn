---
title: 互操作程序集中的命令协定 |Microsoft Docs
description: 了解有关通过 VisualStudio 接口处理命令的基本协定，请参阅。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- command handling with interop assemblies, command contracts
- interop assemblies, command contracts
ms.assetid: 57245708-f539-42dc-8963-2754a48f0189
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: f3e0921c37786c3be755f42a477c20465edfe1c2
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122050203"
---
# <a name="command-contracts-in-interop-assemblies"></a>互操作程序集中的命令约定
通过接口处理命令的基本协定 <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget> 是，环境调用 <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget.QueryStatus%2A> 方法来确定命令是否受支持，如果受支持，则确定其状态和文本。 然后，环境调用 <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget.Exec%2A> 方法来执行命令。

 <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget.QueryStatus%2A>对于所有命令，此方法的处理方式相同。 如果需要，还需要进行进一步的通信 (例如，使用下拉列表) ，可通过 <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget.Exec%2A> 使用适当的参数调用方法来进行管理。 这些参数的解释取决于指定的命令。

 如果命令目标返回 output 参数中的值，则调用方始终负责释放已分配的所有资源。 由于此参数是一个变量，因此清除变量将释放资源。

 如果命令必须在层次结构窗口中运行，则 <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIHierarchy> 必须使用接口。 <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIHierarchy>接口具有具有类似方法的类似协定： <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIHierarchy.QueryStatusCommand%2A> 和 <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIHierarchy.ExecCommand%2A> 。

## <a name="see-also"></a>请参阅
- [Vspackage 如何添加用户界面元素](../../extensibility/internals/how-vspackages-add-user-interface-elements.md)
- [Vspackage 中的命令传送](../../extensibility/internals/command-routing-in-vspackages.md)
- [命令实现](../../extensibility/internals/command-implementation.md)
