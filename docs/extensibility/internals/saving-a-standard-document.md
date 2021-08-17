---
title: 保存标准文档|Microsoft Docs
description: 了解添加到 IDE 中项目类型的标准文档Visual Studio过程。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- editors [Visual Studio SDK], saving standard documents
- projects [Visual Studio SDK], saving standard documents
- persistence, saving standard documents
ms.assetid: d692fedf-b46e-4d60-84bd-578635042235
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: 71e4aaa99a17e8643af104a30e12caf3300e0570a00cc1715d80016333aff64f
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121375647"
---
# <a name="saving-a-standard-document"></a>保存标准文档
环境处理"保存"、"另存为"和"全部保存"命令。 当用户从"文件"菜单中选择 **"** 保存"、另存为或"全部保存"或关闭解决方案时，导致"全部 **保存**"时，将发生以下过程。

 ![标准编辑器](../../extensibility/internals/media/public.gif "公共") 标准编辑器的"另存为"和"全部保存"命令处理

 以下步骤详细介绍了此过程：

1. 选择 **"保存** 并 **另** 存为"命令后，环境将使用服务来确定活动文档窗口 <xref:Microsoft.VisualStudio.Shell.Interop.SVsShellMonitorSelection> ，从而确定应保存哪些项。 活动文档窗口已知后，环境将查找层次结构指针和项标识符 (为正在运行的文档表中的) 指定 itemID。 有关详细信息，请参阅 [运行文档表](../../extensibility/internals/running-document-table.md)。

    选择 **"全部** 保存"命令后，环境将使用正在运行的文档表中的信息来编译要保存的所有项的列表。

2. 解决方案收到调用时，会 (所选项集，即服务公开的多个 <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget.QueryStatus%2A> <xref:Microsoft.VisualStudio.Shell.Interop.SVsShellMonitorSelection>) 。

3. 在选择的每个项上，解决方案使用层次结构指针调用 方法来 <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistHierarchyItem2.IsItemDirty%2A> 确定是否应启用 **"保存** "菜单命令。 如果一个或多个项是脏项，则 **启用"保存** "命令。 如果层次结构使用标准编辑器，则层次结构通过调用 方法将查询脏状态委托给 <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistDocData2.IsDocDataDirty%2A> 编辑器。

4. 在每个选定的脏项上，解决方案使用层次结构指针在 <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistHierarchyItem2.SaveItem%2A> 相应的层次结构上调用 方法。

    层次结构通常使用标准编辑器来编辑文档。 在这种情况下，该编辑器的文档数据对象应支持 <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistDocData2> 接口。 收到方法调用后，项目应通知编辑器正在通过调用文档数据对象上的 方法 <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistHierarchyItem2.SaveItem%2A> <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistDocData2.SaveDocData%2A> 保存文档。 编辑器可以通过调用 接口，允许环境处理"另存 `Query Service` 为" <xref:Microsoft.VisualStudio.Shell.Interop.SVsUIShell> 对话框。 这会返回指向 接口的 <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell> 指针。 然后，编辑器必须调用 <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell.SaveDocDataToFile%2A> 方法，并通过 参数将指针 <xref:Microsoft.VisualStudio.Shell.Interop.IPersistFileFormat> 传递给编辑器的 `pPersistFile` 实现。 然后，环境执行"保存"操作，并提供 **编辑器的** "另存为"对话框。 然后，环境使用 调用回编辑器 <xref:Microsoft.VisualStudio.Shell.Interop.IPersistFileFormat> 。

5. 如果用户尝试保存未标题的文档 (，即以前未保存的文档) ，则实际执行另存为命令。

6. 对于"另存为"命令，环境显示"另存为"对话框，提示用户输入文件名。

    如果文件的名称已更改，则层次结构负责通过调用 (VSFPROPID_MkDocument) 来 <xref:Microsoft.VisualStudio.Shell.Interop.IVsWindowFrame.SetProperty%2A> 更新文档框架的缓存 (VSFPROPID_MkDocument) 。

   如果 **"另** 存为"命令移动文档的位置，并且层次结构对文档位置敏感，则层次结构负责将打开的文档窗口的所有权转移给其他层次结构。 例如，如果项目跟踪文件是内部文件还是外部文件， (文件) 与项目相关的其他文件。 使用以下过程将文件的所有权更改为杂项文件项目。

## <a name="changing-file-ownership"></a>更改文件所有权

#### <a name="to-change-file-ownership-to-the-miscellaneous-files-project"></a>将文件所有权更改为杂项文件项目

1. 接口的查询 <xref:Microsoft.VisualStudio.Shell.Interop.SVsExternalFilesManager> 服务。

     返回指向 <xref:Microsoft.VisualStudio.Shell.Interop.IVsExternalFilesManager2> 的指针。

2. 调用 <xref:Microsoft.VisualStudio.Shell.Interop.IVsExternalFilesManager2.TransferDocument%2A> (`pszMkDocumentNew` `punkWindowFrame` ，) 方法将文档转移到新层次结构。 执行"另存为"命令的层次结构调用此方法。

## <a name="see-also"></a>请参阅
- <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget>
- [打开和保存项目项](../../extensibility/internals/opening-and-saving-project-items.md)
