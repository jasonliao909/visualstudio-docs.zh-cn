---
title: 如何：打开标准编辑器|Microsoft Docs
description: 了解如何使用标准编辑器实现 OpenItem 方法。 IDE 确定指定文件类型的标准编辑器。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- editors [Visual Studio SDK], opening
- projects [Visual Studio SDK], opening standard editors
ms.assetid: d5ce10f9-047a-4b74-aa1d-295128898b89
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: dda137697f4645af166d846af9605358c7f0c489bc3ef86692f00688f50f0221
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121401721"
---
# <a name="how-to-open-standard-editors"></a>如何：打开标准编辑器
打开标准编辑器时，让 IDE 确定指定文件类型的标准编辑器，而不是为文件指定特定于项目的编辑器。

 完成以下过程来实现 <xref:Microsoft.VisualStudio.Shell.Interop.IVsProject3.OpenItem%2A> 方法。 这会在标准编辑器中打开项目文件。

## <a name="to-implement-the-openitem-method-with-a-standard-editor"></a>使用标准编辑器实现 OpenItem 方法

1. 调用 <xref:Microsoft.VisualStudio.Shell.Interop.IVsRunningDocumentTable> `RDT_EditLock` () ，以确定文档数据对象文件是否已打开。

2. 如果文件已打开，请通过调用 方法，为 参数指定值 来 <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShellOpenDocument.IsDocumentOpen%2A> `IDO_ActivateIfOpen` 重新显示 `grfIDO` 文件。

     如果文件已打开，并且文档属于与调用项目不同的项目，则项目会收到警告，指出正在打开的编辑器来自另一个项目。 然后显示文件窗口。

3. 如果文档未打开或不在正在运行的文档表中，请调用 方法 () 打开文件 <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShellOpenDocument.OpenStandardEditor%2A> `OSE_ChooseBestStdEditor` 的标准编辑器。

     调用 方法时，IDE 将执行以下任务：

    1. IDE 会扫描注册表中的 Editor/{guidEditorType}/Extensions 子项，以确定哪个编辑器可以打开文件，并且具有执行此操作的最高优先级。

    2. IDE 确定哪个编辑器可以打开文件后，IDE 将调用 <xref:Microsoft.VisualStudio.Shell.Interop.IVsEditorFactory.CreateEditorInstance%2A> 。 编辑器的此方法实现返回 IDE 调用和站点新打开的文档 <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell.CreateDocumentWindow%2A> 所需的信息。

    3. 最后，IDE 使用常用的持久性接口（如 ）加载文档 <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistDocData2> 。

    4. 如果 IDE 以前已确定层次结构或层次结构项可用，则 IDE 将调用项目上的 方法，获取项目级上下文指针，以使用 方法调用传递 <xref:Microsoft.VisualStudio.Shell.Interop.IVsProject3.GetItemContext%2A> <xref:Microsoft.VisualStudio.OLE.Interop.IServiceProvider> 回 <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell.CreateDocumentWindow%2A> 。

4. 如果希望编辑器从项目获取上下文，当 IDE 调用项目时，返回指向 <xref:Microsoft.VisualStudio.OLE.Interop.IServiceProvider> IDE <xref:Microsoft.VisualStudio.Shell.Interop.IVsProject3.GetItemContext%2A> 的指针。

     执行此步骤可让项目向编辑器提供其他服务。

     如果文档视图或文档视图对象已成功在窗口框架中进行站点化，则通过调用 来使用其数据初始化该对象 <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistDocData2.LoadDocData%2A> 。

## <a name="see-also"></a>请参阅
- <xref:Microsoft.VisualStudio.OLE.Interop.IServiceProvider>
- [打开并保存项目项](../extensibility/internals/opening-and-saving-project-items.md)
- [如何：打开特定于项目的编辑器](../extensibility/how-to-open-project-specific-editors.md)
- [如何：打开打开的文档的编辑器](../extensibility/how-to-open-editors-for-open-documents.md)
- [使用"打开文件"命令显示文件](../extensibility/internals/displaying-files-by-using-the-open-file-command.md)
