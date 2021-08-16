---
title: RDT_ReadLock使用情况|Microsoft Docs
description: 了解_VSRDTFLAGS。RDT_ReadLock标志，该标志提供用于锁定运行文档表中的文档的逻辑。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- RDT_ReadLock
- visible
- RDT_EditLock
- invisible
ms.assetid: b935fc82-9d6b-4a8d-9b70-e9a5c5ad4a55
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: 957e67e852baac541cfe62955fa7220ac2e170cdff75c60c82cc58a357396c00
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121414436"
---
# <a name="rdt_readlock-usage"></a>RDT_ReadLock 用法

[_VSRDTFLAGS。RDT_ReadLock](<xref:Microsoft.VisualStudio.Shell.Interop._VSRDTFLAGS.RDT_ReadLock>)是一个标志，该标志提供逻辑用于锁定运行文档表 (RDT) 中的文档，这是当前在 Visual Studio IDE 中打开的所有文档的列表。 此标志确定文档何时打开，以及文档在用户界面中是可见的，还是以不可见状态在内存中。

通常，使用 [_VSRDTFLAGS。RDT_ReadLock](<xref:Microsoft.VisualStudio.Shell.Interop._VSRDTFLAGS.RDT_ReadLock>) 其中一个为 true 时，将执行以下操作：

- 你想要以不公开和只读方式打开文档，但尚未确定应该 <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy> 拥有它。

- 希望系统提示用户保存在用户向 UI 中显示文档之前未完全打开的文档，然后尝试将其关闭。

## <a name="how-to-manage-visible-and-invisible-documents"></a>如何管理可见文档和不可见文档

当用户在 UI 中打开文档时，必须建立文档的所有者，并创建 <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy> [_VSRDTFLAGS。RDT_EditLock](<xref:Microsoft.VisualStudio.Shell.Interop._VSRDTFLAGS.RDT_EditLock>) 标志。 如果无法建立所有者，则当用户单击"全部保存"或关闭 <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy> IDE时，将不会保存文档。 这意味着，如果文档在内存中被修改的不公开位置打开，并且系统提示用户在关闭时保存文档，或者如果选择"全部保存"，则不能使用 。  `RDT_ReadLock` 相反，必须使用 ， `RDT_EditLock` 在注册时 <xref:Microsoft.VisualStudio.Shell.Interop.IVsDocumentLockHolder> 注册 [__VSREGDOCLOCKHOLDER。RDLH_WeakLockHolder](<xref:Microsoft.VisualStudio.Shell.Interop.__VSREGDOCLOCKHOLDER.RDLH_WeakLockHolder>) 标志。

## <a name="rdt_editlock-and-document-modification"></a>RDT_EditLock文档修改

前面提到的标志指示当用户将文档打开到可见的 DocumentWindow 中时，不可见的文档打开将 `RDT_EditLock` **生成它**。 发生这种情况时，当可见的 **DocumentWindow** 关闭时，用户会出现"保存"提示。 `Microsoft.VisualStudio.Package.Automation.OAProject.CodeModel` 使用服务的 实现最初仅在只 (（即，在以不公开状态打开文档以分析文档时 <xref:Microsoft.VisualStudio.Shell.Interop.IVsInvisibleEditorManager> `RDT_ReadLock` ）) 。 稍后，如果必须修改文档，则锁将升级到弱 **RDT_EditLock。** 如果用户随后在可见的 **DocumentWindow** 中打开文档， `CodeModel` 将释放 的 `RDT_EditLock` 弱 。

如果用户随后关闭 **DocumentWindow，** 然后在系统提示保存打开的文档时选择"否"，则实现将释放文档中的所有信息，然后在下次需要文档更多信息时以不公开状态从磁盘重新打开文档。 `CodeModel` 此行为的细微之处是用户打开不可见打开的文档的 **DocumentWindow，** 对其进行修改，将其关闭，然后在系统提示保存文档时选择"否"。  在这种情况下，如果文档具有 ，则文档实际上不会关闭，并且修改后的文档在内存中保持打开状态，即使用户选择不保存文档。 `RDT_ReadLock`

如果文档的不可见打开使用弱 ，则当用户以可视状态打开文档并且未持有其他锁时，它将 `RDT_EditLock` 生成其锁。 当用户关闭 **DocumentWindow** 并选择"否"时，当系统提示保存文档时，必须从内存中关闭该文档。 这意味着不可见的客户端必须侦听 RDT 事件以跟踪这种情况。 下次需要文档时，必须重新打开该文档。
