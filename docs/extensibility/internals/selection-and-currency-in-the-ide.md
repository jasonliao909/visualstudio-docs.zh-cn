---
title: IDE 中的选择和货币|Microsoft Docs
description: 了解 VSPackage 如何参与货币跟踪。 IDE Visual Studio使用选择上下文维护有关当前所选对象的信息。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- currency, Visual Studio IDE
- IDE, selection
- selection, Visual Studio IDE
- IDE, currency
ms.assetid: 2f6f18d1-acd8-454d-a856-9a4d81155052
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: f540618c6b125012d332a683ba534fbaa5082990
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122049540"
---
# <a name="selection-and-currency-in-the-ide"></a>IDE 中的选择和货币
IDE (集成) 通过使用选择上下文 来维护有关用户当前 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 所选对象 *的信息*。 借助选择上下文，VSPackage 可以通过两种方式参与货币跟踪：

- 将 VSPackage 的货币信息传播到 IDE。

- 通过监视用户当前在 IDE 中的活动选择。

## <a name="selection-context"></a>选择上下文
 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]IDE 在其自己的全局选择上下文对象中全局跟踪 IDE 货币。 下表显示了组成选择上下文的元素。

|元素|说明|
|-------------|-----------------|
|当前层次结构|通常为当前项目;NULL 当前层次结构指示整个解决方案是最新的。|
|当前 ItemID|当前层次结构中的选定项;当项目窗口中有多个选择时，可以有多个当前项。|
|当前 `SelectionContainer`|保存对象应显示其属性属性窗口一个或多个对象。|

 此外，环境维护两个全局列表：

- 活动 UI 命令标识符的列表

- 当前活动元素类型的列表。

### <a name="window-types-and-selection"></a>窗口类型和选择
 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]IDE 将窗口组织为两种常规类型：

- 层次结构类型窗口

- 框架窗口，例如工具和文档窗口

  IDE 以不同方式跟踪其中每种窗口类型的货币。

  最常见的项目类型窗口是 IDE 控制的解决方案资源管理器。 项目类型窗口跟踪全局选择上下文的全局层次结构和 ItemID，该窗口依赖于用户的选择来确定当前层次结构。 对于项目类型窗口，环境提供全局服务 <xref:Microsoft.VisualStudio.Shell.Interop.SVsShellMonitorSelection> ，VSPackage 可以通过该服务监视打开元素的当前值。 环境中的属性浏览由此全局服务驱动。

  另一方面，框架窗口使用框架窗口中的 DocObject 推送 hierarchy/ItemID/SelectionContainer t一 (SelectionContext 值) 。 . 框架窗口使用此 <xref:Microsoft.VisualStudio.Shell.Interop.SVsShellMonitorSelection> 服务。 DocObject 只能推送选择容器的值，使层次结构和 ItemID 的本地值保持不变，就像 MDI 子文档的典型一样。

### <a name="events-and-currency"></a>事件和货币
 可能会发生两种类型的事件，这些事件可能会影响环境的货币概念：

- 传播到全局级别并更改窗口框架选择上下文的事件。 此类事件的示例包括正在打开的 MDI 子窗口、正在打开的全局工具窗口或正在打开的项目类型工具窗口。

- 更改窗口框架选择上下文中跟踪的元素的事件。 示例包括更改 DocObject 中的选择或更改项目类型窗口中的选择。

## <a name="see-also"></a>请参阅
- [选择上下文对象](../../extensibility/internals/selection-context-objects.md)
- [为用户提供反馈](../../extensibility/internals/feedback-to-the-user.md)
