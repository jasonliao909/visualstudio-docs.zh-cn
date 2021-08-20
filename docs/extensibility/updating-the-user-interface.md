---
title: 更新用户界面 |Microsoft Docs
description: 了解如何在 VSPackage 中实现新命令后添加代码以更新用户界面。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- user interfaces, updating
- commands, updating UI
ms.assetid: 376e2f56-e7bf-4e62-89f5-3dada84a404b
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: ef946f99589ba0bd0a2d334866e247b9a99aae2a
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122144374"
---
# <a name="updating-the-user-interface"></a>更新用户接口
实现命令后，可以添加代码以使用新命令的状态更新用户界面。

 在典型的 Win32 应用程序中，可以持续轮询命令集，并可以在用户查看各个命令时调整其状态。 但是，由于 shell 可以托管无限数量的 VSPackage，因此广泛的轮询可能会降低响应能力，尤其是跨托管代码和 COM 之间的互操作程序集 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 进行轮询。

### <a name="to-update-the-ui"></a>更新 UI

1. 执行以下步骤之一：

    - 调用 <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell.UpdateCommandUI%2A> 方法。

         <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell>接口可以从服务获取 <xref:Microsoft.VisualStudio.Shell.Interop.SVsUIShell> ，如下所示。

        ```csharp
        void UpdateUI(Microsoft.VisualStudio.Shell.ServiceProvider sp)
        {
            IVsUIShell vsShell = (IVsUIShell)sp.GetService(typeof(IVsUIShell));
            if (vsShell != null)
            {
                int hr = vsShell.UpdateCommandUI(0);
                Microsoft.VisualStudio.ErrorHandler.ThrowOnFailure(hr);
            }
        }

        ```

         如果 的参数不 <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell.UpdateCommandUI%2A> 为零 `TRUE` () ，则立即同步执行更新。 建议为此参数传递零 `FALSE` () ，以帮助保持良好的性能。 若要避免缓存，在 .vsct 文件中创建命令时 `DontCache` 应用 标志。 不过，请谨慎使用 标志，否则性能可能会降低。 有关命令标志的信息，请参阅 [命令标志元素](../extensibility/command-flag-element.md) 文档。

    - 在通过窗口中的就ActiveX托管控件的 VSPackage 中，使用 方法可能更方便 <xref:Microsoft.VisualStudio.Shell.Interop.IOleInPlaceComponentUIManager.UpdateUI%2A> 。 <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell.UpdateCommandUI%2A>接口中的 <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell> 方法和 接口中的 方法在功能 <xref:Microsoft.VisualStudio.Shell.Interop.IOleInPlaceComponentUIManager.UpdateUI%2A> <xref:Microsoft.VisualStudio.Shell.Interop.IOleInPlaceComponentUIManager> 上是等效的。 这两种操作都会导致环境重新查询所有命令的状态。 通常，不会立即执行更新。 相反，更新将延迟到空闲时间。 shell 缓存命令状态以帮助保持良好性能。 若要避免缓存，在 .vsct 文件中创建命令时 `DontCache` 应用 标志。 不过，请谨慎使用 标志，因为性能可能会降低。

         请注意，可以通过对 对象调用 方法或从服务获取 接口 <xref:Microsoft.VisualStudio.Shell.Interop.IOleInPlaceComponentUIManager> `QueryInterface` 来获取 <xref:Microsoft.VisualStudio.Shell.Interop.IOleComponentUIManager> <xref:Microsoft.VisualStudio.Shell.Interop.SOleComponentUIManager> 接口。

## <a name="see-also"></a>请参阅
- [VSPackage 如何添加用户界面元素](../extensibility/internals/how-vspackages-add-user-interface-elements.md)
- [实现](../extensibility/internals/command-implementation.md)
