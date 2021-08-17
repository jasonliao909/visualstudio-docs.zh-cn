---
title: 如何：实现嵌套项目|Microsoft Docs
description: 了解如何通过从解决方案和父项目Visual Studio生成项目层次结构，在项目中实现嵌套项目。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- nested projects, implementing
- projects [Visual Studio SDK], nesting
ms.assetid: d20b8d6a-f0e0-4115-b3a3-edda893ae678
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: de258e2b1ca7f57573a1e79d33c6a80960325d3662c8af9ce9e8111a330b6f12
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121359307"
---
# <a name="how-to-implement-nested-projects"></a>如何：实现嵌套项目

创建嵌套项目类型时，必须实现其他几个步骤。 父项目承担解决方案对嵌套的子项目 (一) 责任。 父项目是类似于解决方案的项目的容器。 具体而言，解决方案和父项目必须引发多个事件，以生成嵌套项目的层次结构。 以下创建嵌套项目的过程介绍了这些事件。

## <a name="create-nested-projects"></a>创建嵌套项目

1. IDE (集成) 通过调用 接口加载父项目的项目文件和启动 <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectFactory> 信息。 将创建父项目并添加到解决方案中。

    > [!NOTE]
    > 此时，父项目创建嵌套项目的过程还太早，因为必须先创建父项目，然后才能创建子项目。 按照此顺序，父项目可以将设置应用于子项目，子项目可根据需要从父项目获取信息。 如果客户端（如源代码管理） (SCC) 和 解决方案资源管理器，则此 **序列为**。

     父项目必须等待 IDE 调用 方法，然后才能创建其嵌套 (子) <xref:Microsoft.VisualStudio.Shell.Interop.IVsParentProject.OpenChildren%2A> 项目。

2. IDE 对 `QueryInterface` 的父项目调用 <xref:Microsoft.VisualStudio.Shell.Interop.IVsParentProject> 。 如果此调用成功，IDE 将调用父项目的 方法，以打开父 <xref:Microsoft.VisualStudio.Shell.Interop.IVsParentProject.OpenChildren%2A> 项目的所有嵌套项目。

3. 父项目调用 <xref:Microsoft.VisualStudio.Shell.Interop.IVsFireSolutionEvents.FireOnBeforeOpeningChildren%2A> 方法以通知侦听器嵌套项目即将创建。 例如，SCC 正在侦听这些事件，了解解决方案和项目创建过程中的步骤是否按顺序排列。 如果步骤顺序不正确，则可能无法正确向源代码管理注册解决方案。

4. 父项目在其 <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolution.AddVirtualProject%2A> 每个子项目上 <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolution.AddVirtualProjectEx%2A> 调用 方法或 方法。

     将 传递给 方法以指示 (嵌套) 项目应添加到项目窗口中（从生成中排除）并添加到源代码管理， <xref:Microsoft.VisualStudio.Shell.Interop.__VSADDVPFLAGS> `AddVirtualProject` 等等。 `VSADDVPFLAGS` 允许你控制嵌套项目的可见性，并指示与之关联的功能。

     如果重新加载以前存在的子项目，该项目 GUID 存储在父项目的项目文件中，则父项目将调用 `AddVirtualProjectEx` 。 和 之间的唯一区别是 具有 参数，使父项目能够为每个实例指定 ，以便子项目启用 和 `AddVirtualProject` `AddVirtualProjectEX` `AddVirtualProjectEX` `guidProjectID` <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolution.GetProjectOfGuid%2A> <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolution.GetProjectOfProjref%2A> 以正常运行。

     如果没有可用的 GUID，例如添加新的嵌套项目时，解决方案在项目添加到父级时会为该项目创建一个。 父项目负责将该项目 GUID 保留在其项目文件中。 如果删除嵌套项目，也可以删除该项目的 GUID。

5. IDE 对 <xref:Microsoft.VisualStudio.Shell.Interop.IVsParentProject.OpenChildren> 父项目的每个子项目调用 方法。

     如果要嵌套项目 `IVsParentProject` ，父项目必须实现 。 但是，即使父项目下方有父项目，它 `QueryInterface` `IVsParentProject` 也永远不会调用 。 解决方案处理对 的调用，如果实现， `IVsParentProject` 则调用 `OpenChildren` 以创建嵌套项目。 `AddVirtualProjectEX` 始终从 调用 `OpenChildren` 。 父项目不应调用它，以保持层次结构创建事件的顺序。

6. IDE 对 <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionEvents3.OnAfterOpenProject%2A> 子项目调用 方法。

7. 父项目调用 <xref:Microsoft.VisualStudio.Shell.Interop.IVsFireSolutionEvents.FireOnAfterOpeningChildren%2A> 方法以通知侦听器已创建父级的子项目。

8. 打开所有子项目后，IDE 对父 <xref:Microsoft.VisualStudio.Shell.Interop.IVsFireSolutionEvents.FireOnAfterOpenProject%2A> 项目调用 方法。

     如果不存在，父项目会通过调用 为每个嵌套项目创建 `CoCreateGuid` GUID。

    > [!NOTE]
    > `CoCreateGuid` 是在创建 GUID 时调用的 COM API。 有关详细信息，请参阅 `CoCreateGuid` MSDN 库中的 和 GUID。

     父项目将此 GUID 存储在其项目文件中，以在下次在 IDE 中打开时检索它。 有关调用 以检索子项目的 的信息，请参阅步骤 `AddVirtualProjectEX` `guidProjectID` 4。

9. 然后，为父 ItemID 调用 方法，该父 ItemID 是按约定 <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy.GetProperty%2A> 委托给嵌套项目的。 在父节点上调用时，检索嵌套要委派的项目 <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy.GetProperty%2A> 的节点的属性。

     由于父项目和子项目以编程方式实例化，因此此时可以设置嵌套项目的属性。

    > [!NOTE]
    > 不仅从嵌套项目中接收上下文信息，还可通过检查项目属性来询问父项目 [是否具有该项__VSHPROPID。VSHPROPID_UserContext](<xref:Microsoft.VisualStudio.Shell.Interop.__VSHPROPID.VSHPROPID_UserContext>)。 这样，就可以添加特定于单个嵌套项目的额外动态帮助属性和菜单选项。

10. 生成层次结构后，通过调用 **解决方案资源管理器** 在层次结构中 <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy.GetNestedHierarchy%2A> 显示。

     将层次结构传递给环境，以 `GetNestedHierarchy` 生成层次结构以在 解决方案资源管理器。 这样，解决方案就知道项目存在，并且可以通过生成管理器进行管理进行生成，或者允许将项目中的文件置于源代码控制之下。

11. 创建 Project1 的所有嵌套项目后，控制权将传递回解决方案，并且对 Project2 重复此过程。

     对于具有子级的子项目，创建嵌套项目的过程是相同的。 在这种情况下，如果 BuildProject1（Project1 的子级）具有子项目，则它们在 BuildProject1 之后和 Project2 之前创建。 该过程是递归的，层次结构从上到下生成。

     当用户关闭解决方案或特定项目本身而关闭嵌套项目时，将调用 上 `IVsParentProject` <xref:Microsoft.VisualStudio.Shell.Interop.IVsParentProject.CloseChildren%2A> 的另一种方法。 父项目使用 和 方法包装对 方法的调用，以通知解决方案事件的侦听器嵌套项目 <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolution.RemoveVirtualProject%2A> <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionEvents3.OnBeforeClosingChildren%2A> <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionEvents3.OnAfterClosingChildren%2A> 正在关闭。

以下主题介绍实现嵌套项目时要考虑的其他几个概念：

- [卸载和重新加载嵌套项目的注意事项](../../extensibility/internals/considerations-for-unloading-and-reloading-nested-projects.md)
- [对嵌套项目的向导支持](../../extensibility/internals/wizard-support-for-nested-projects.md)
- [为嵌套项目实现命令处理](../../extensibility/internals/implementing-command-handling-for-nested-projects.md)
- [筛选嵌套项目的"AddItem"对话框](../../extensibility/internals/filtering-the-additem-dialog-box-for-nested-projects.md)

## <a name="see-also"></a>请参阅

- [将项添加到"添加新项"对话框](../../extensibility/internals/adding-items-to-the-add-new-item-dialog-boxes.md)
- [注册项目和项模板](../../extensibility/internals/registering-project-and-item-templates.md)
- [清单：创建新项目类型](../../extensibility/internals/checklist-creating-new-project-types.md)
- [上下文参数](../../extensibility/internals/context-parameters.md)
- [向导 (.vsz) 文件](../../extensibility/internals/wizard-dot-vsz-file.md)
