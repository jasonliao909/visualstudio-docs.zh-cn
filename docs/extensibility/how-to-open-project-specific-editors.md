---
title: 如何：打开Project-Specific编辑器|Microsoft Docs
description: 了解如何使用特定于项目的编辑器实现 OpenItem 方法，以便项目可以打开绑定到该项目的编辑器的文件。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- project types, opening a project-specific editor
- editors [Visual Studio SDK], opening project-specific editors
- projects [Visual Studio SDK], opening folders
ms.assetid: 83e56d39-c97b-4c6b-86d6-3ffbec97e8d1
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: 7f28ce796b38c0d0ce51c67b7c5a36a573dae771
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122050307"
---
# <a name="how-to-open-project-specific-editors"></a>如何：打开特定于项目的编辑器
如果项目打开的项文件本质上绑定到该项目的特定编辑器，则项目必须使用特定于项目的编辑器打开该文件。 文件不能委派给 IDE 的用于选择编辑器的机制。 例如，可以使用此项目特定的编辑器选项来指定识别项目中唯一的信息的特定位图编辑器，而不是使用标准位图编辑器。

 当 IDE 确定特定项目应打开文件时，它将 <xref:Microsoft.VisualStudio.Shell.Interop.IVsProject3.OpenItem%2A> 调用 方法。 有关详细信息，请参阅使用 ["打开文件"命令 显示文件](../extensibility/internals/displaying-files-by-using-the-open-file-command.md)。 使用以下指南实现 方法，使项目使用特定于项目的 `OpenItem` 编辑器打开文件。

## <a name="to-implement-the-openitem-method-with-a-project-specific-editor"></a>使用特定于项目的编辑器实现 OpenItem 方法

1. 调用 <xref:Microsoft.VisualStudio.Shell.Interop.IVsRunningDocumentTable.FindAndLockDocument%2A> 方法 `RDT_EditLock` () ，以确定文件 (数据对象) 是否已打开。

    > [!NOTE]
    > 有关文档数据和文档视图对象的信息，请参阅自定义 [编辑器中的文档数据和文档视图](../extensibility/document-data-and-document-view-in-custom-editors.md)。

2. 如果文件已打开，请通过调用 方法并指定 参数的 IDO_ActivateIfOpen 来 <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShellOpenDocument.IsDocumentOpen%2A> 重新显示 `grfIDO` 文件。

     如果文件已打开，并且文档由调用项目外的项目拥有，则向用户显示警告，指出正在打开的编辑器来自另一个项目。 然后显示文件窗口。

3. 如果文本缓冲区 (文档数据) 对象已打开，并且你想要附加另一个视图，则你负责挂接该视图。 从项目中实例化文档 (对象) 的建议方法如下：

    1. 在 `QueryService` 服务 <xref:Microsoft.VisualStudio.Shell.Interop.SLocalRegistry> 上调用 ，获取指向 接口的 <xref:Microsoft.VisualStudio.Shell.Interop.ILocalRegistry2> 指针。

    2. 调用 <xref:Microsoft.VisualStudio.Shell.Interop.ILocalRegistry2.CreateInstance%2A> 方法以创建文档视图类的实例。

4. 调用 <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell.CreateDocumentWindow%2A> 方法，指定文档视图对象。

     此方法将文档视图对象站点在文档窗口中。

5. 对 或 方法 <xref:Microsoft.VisualStudio.Shell.Interop.IPersistFileFormat.InitNew%2A> 执行适当的 <xref:Microsoft.VisualStudio.Shell.Interop.IPersistFileFormat.Load%2A> 调用。

     此时，视图应完全初始化并准备好打开。

6. 调用 <xref:Microsoft.VisualStudio.Shell.Interop.IVsWindowFrame.Show%2A> 方法来显示并打开视图。

## <a name="see-also"></a>请参阅
- [打开并保存项目项](../extensibility/internals/opening-and-saving-project-items.md)
- [如何：打开标准编辑器](../extensibility/how-to-open-standard-editors.md)
- [如何：打开打开的文档的编辑器](../extensibility/how-to-open-editors-for-open-documents.md)
