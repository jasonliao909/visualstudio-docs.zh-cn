---
title: 选择上下文对象|Microsoft Docs
description: 了解 IDE 如何使用全局Visual Studio上下文对象来确定应在 IDE 中显示的内容的内部机制。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- selection, tracking
- selection, context objects
ms.assetid: 7308ea8f-a42c-47e5-954e-7dee933dce7a
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: 6e6df11b81a48a95d9c401ff801be548923c6f52
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122132270"
---
# <a name="selection-context-objects"></a>选择上下文对象
IDE (集成) 使用全局选择上下文对象来确定 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 应在 IDE 中显示的内容。 IDE 中的每个窗口都可以将其自己的选择上下文对象推送到全局选择上下文。 当窗口具有焦点时，IDE 使用窗口中的值更新全局选择上下文。 有关详细信息，请参阅 [向用户反馈](../../extensibility/internals/feedback-to-the-user.md)。

 IDE 中的每个窗口框架或站点都有一个称为 的服务 <xref:Microsoft.VisualStudio.Shell.Interop.STrackSelection> 。 由位于窗口框架中的 VSPackage 创建的对象必须调用 方法来 `QueryService` 获取指向 接口的 <xref:Microsoft.VisualStudio.Shell.Interop.ITrackSelection> 指针。

 框架窗口可以阻止部分选择上下文信息在启动时传播到全局选择上下文。 此功能对于可能需要从空选择开始的工具窗口非常有用。

 修改全局选择上下文会触发 VSPackage 可以监视的事件。 VSPackage 可以通过实现 和 接口来执行以下 `IVsTrackSelectionEx` <xref:Microsoft.VisualStudio.Shell.Interop.IVsMonitorSelection> 任务：

- 更新层次结构中的当前活动文件。

- 监视对某些类型的元素的更改。 例如，如果 VSPackage 使用特殊的"属性"窗口，可以在活动"属性"窗口中监视更改，并按需要重启。

  以下序列显示选择跟踪的典型过程。

1. IDE 从新打开的窗口检索选择上下文，并将它置于全局选择上下文中。 如果选择上下文使用HIERARCHY_DONTPROPAGATE或SELCONTAINER_DONTPROPAGATE，则该信息不会传播到全局上下文。 有关详细信息，请参阅 [向用户反馈](../../extensibility/internals/feedback-to-the-user.md)。

2. 通知事件将广播到请求通知事件的任何 VSPackage。

3. VSPackage 通过执行更新层次结构、重新激活工具或其他类似任务等活动来处理它接收的事件。

## <a name="see-also"></a>请参阅
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsTrackSelectionEx>
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsMonitorSelection>
- [Visual Studio 中的层次结构](../../extensibility/internals/hierarchies-in-visual-studio.md)
- [IDE 中的选择和货币](../../extensibility/internals/selection-and-currency-in-the-ide.md)
- [项目类型](../../extensibility/internals/project-types.md)
