---
title: 文档锁持有者管理|Microsoft Docs
description: 了解如何在运行的文档表中对文档放置编辑锁，而用户不会在文档窗口中看到打开的文档。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- editors [Visual Studio SDK], custom - document locking
ms.assetid: fa1ce513-eb7d-42bc-b6e8-cb2433d051d5
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: c62658c14754a317554fd7e06960cd2f87ff3f2a43bc98811a7479b98700bd3c
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121414969"
---
# <a name="document-lock-holder-management"></a>文档锁持有者管理

RDT (运行) 维护打开的文档计数及其拥有的任何编辑锁。 当文档在后台以编程方式编辑时，可以在 RDT 中对文档放置编辑锁，而用户不会在文档窗口中看到打开的文档。 通过图形用户界面修改多个文件的设计器通常使用此功能。

## <a name="document-lock-holder-scenarios"></a>文档锁持有者方案

### <a name="file-a-has-a-dependence-on-file-b"></a>文件"a"依赖于文件"b"

请考虑为文件类型"a"实现标准编辑器"A"的情况，并且"a"类型的每个文件都有对 (的引用或依赖于) "b"类型的文件。 "b"类型的文件存在标准编辑器"B"。 当编辑器"A"打开文件"a"时，它会检索对相应文件"b"的引用。 不显示文件"b"，但编辑器"A"可以修改它。 编辑器"A"从 方法获取对文件"b"的文档数据的引用，并维护对文件 <xref:Microsoft.VisualStudio.Shell.Interop.IVsRunningDocumentTable.FindAndLockDocument%2A> "b"的编辑锁。 编辑器"A"修改完文件"b"后，可以通过调用 方法来缩小文件"b"上的编辑锁 <xref:Microsoft.VisualStudio.Shell.Interop.IVsRunningDocumentTable.UnlockDocument%2A> 计数。 如果调用方法时参数设置为 <xref:Microsoft.VisualStudio.Shell.Interop.IVsRunningDocumentTable.FindAndLockDocument%2A> `dwRDTLockType` [_VSRDTFLAGS。RDT_NoLock](<xref:Microsoft.VisualStudio.Shell.Interop._VSRDTFLAGS.RDT_NoLock>)。

### <a name="file-b-is-opened-by-a-different-editor"></a>文件"b"由其他编辑器打开

如果编辑器"A"尝试打开文件"b"时，编辑器"B"已打开文件"b"，则有两个单独的方案需要处理：

- 如果文件"b"在兼容的编辑器中打开，则必须使用 方法使编辑器"A"在文件"b"上注册文档编辑 <xref:Microsoft.VisualStudio.Shell.Interop.IVsRunningDocumentTable.RegisterDocumentLockHolder%2A> 锁。 编辑器"A"修改完文件"b"后，使用 方法取消注册文档编辑 <xref:Microsoft.VisualStudio.Shell.Interop.IVsRunningDocumentTable.UnregisterDocumentLockHolder%2A> 锁。

- 如果文件"b"以不兼容的方式打开，可以让编辑器"A"尝试打开文件"b"失败，也可以让与编辑器"A"关联的视图部分打开并显示相应的错误消息。 错误消息应指示用户在不兼容的编辑器中关闭文件"b"，然后使用编辑器"A"重新打开文件"a"。 还可以实现 方法，以提示用户关闭在不兼容编辑器中打开的文件 [!INCLUDE[vsipsdk](../extensibility/includes/vsipsdk_md.md)] <xref:Microsoft.VisualStudio.Shell.Interop.IVsRunningDocumentTable2.QueryCloseRunningDocument%2A> "b"。 如果用户关闭文件"b"，编辑器"A"中的文件"a"的打开将正常继续。

## <a name="additional-document-edit-lock-considerations"></a>其他文档编辑锁定注意事项

如果编辑器"A"是唯一对文件"b"具有文档编辑锁的编辑器，与编辑器"B"也持有文件"b"上的文档编辑锁时的行为不同。 在 中类设计器是可视化设计器的一个示例，该设计器不持有关联代码 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 文件的编辑锁。  也就是说，如果用户具有在设计视图中打开的类图，并且关联的代码文件同时打开，并且用户修改代码文件但不保存更改，则更改也会丢失到类图 (.cd) 文件中。 如果 **类设计器** 对代码文件具有唯一的文档编辑锁，则关闭代码文件时不会要求用户保存更改。 IDE 要求用户仅在用户关闭更改后保存 **类设计器。** 保存的更改将反映在这两个文件中。 如果 **类设计器和** 代码文件编辑器对代码文件都持有文档编辑锁，则关闭代码文件或窗体时，系统会提示用户保存。 此时，保存的更改会同时反映在窗体和代码文件中。 有关类图详细信息，请参阅使用类[图 (类设计器) 。 ](../ide/class-designer/designing-and-viewing-classes-and-types.md)

请注意，如果需要对非编辑器的文档设置编辑锁，则必须实现 <xref:Microsoft.VisualStudio.Shell.Interop.IVsDocumentLockHolder> 接口。

许多时候，以编程方式修改代码文件的 UI 设计器会更改多个文件。 在这种情况下， 方法通过"是否要保存对以下项的更改？"对话框来处理一 <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell2.SaveItemsViaDlg%2A> **个或多个文档的** 保存。

## <a name="see-also"></a>请参阅

- [运行文档表](../extensibility/internals/running-document-table.md)
- [持久性和正在运行的文档表](../extensibility/internals/persistence-and-the-running-document-table.md)
