---
title: 文档Windows |Microsoft Docs
description: 了解文档中的文档Visual Studio，包括如何实现它们，以及运行文档表 (RDT) 跟踪其状态。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- Visual Studio SDK, document windows
ms.assetid: 50081d48-987f-43db-8bf9-51b7cf76e9c0
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: 1a1659bc97e1626e198b2a3867223005c84cf9e7
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126664393"
---
# <a name="document-windows"></a>文档窗口
在Visual Studio中，*文档窗口* 是一个框架子窗口，与 MDI 窗口 (多文档) 窗口。 文档窗口通常用于显示和修改源代码或文本，但它们还可以承载其他功能类型。 文档窗口：

- 可以在父 MDI 中的单独水平或垂直选项卡组中进行组织，以便可以同时查看多个文件。

- 可以按父 MDI 中的任意顺序停靠。

- 可以自由浮动。

- 按 Tab 键顺序链接到其他 MDI 窗口。

  可以在文档窗口选项卡的快捷菜单上找到用于分组、停靠和浮动的命令。

  有关中窗口行为Visual Studio，请参阅[自定义窗口布局](../../ide/customizing-window-layouts-in-visual-studio.md)。

## <a name="document-window-implementation"></a>文档窗口实现
 文档窗口通过实现编辑器创建。 <xref:Microsoft.VisualStudio.Shell.Interop.IVsEditorFactory>接口在实例化编辑器时创建文档窗口。 有关详细信息，请参阅编辑器 [中的旧版接口](/previous-versions/visualstudio/visual-studio-2015/extensibility/legacy-interfaces-in-the-editor?preserve-view=true&view=vs-2015)。

> [!NOTE]
> 若要在窗口中提供向后和向前导航点，请实现 <xref:Microsoft.VisualStudio.Shell.Interop.IVsBackForwardNavigation> 接口。 文本编辑器使用文本标记来标识文档中的导航点。

## <a name="the-running-document-table"></a>"正在运行"文档表
 IDE 使用 RDT (运行) 表来跟踪每个文档窗口的状态。 RDT 是一种机制，通过该机制，文档窗口会收到事件通知，例如解决方案关闭或文件已编辑时。 有关详细信息，请参阅运行 [文档表](../../extensibility/internals/running-document-table.md)。

## <a name="see-also"></a>另请参阅
- [延迟文档加载](../../extensibility/internals/delayed-document-loading.md)
