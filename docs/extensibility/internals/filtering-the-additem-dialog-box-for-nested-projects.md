---
title: 筛选嵌套项目的"AddItem"对话框|Microsoft Docs
description: 了解如何通过实现父项目的 IVsFilterAddProjectItemDlg 接口来筛选 Visual Studio 中的嵌套项目的 AddItem 对话框。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- filtering, nested projects
- nested projects, AddItem dialog box filtering
ms.assetid: 5b3e352e-7f18-4f66-be16-b0ad55637ce5
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: 5bb4a9a76cc4ca074051ccb7ad48ae70b0e29e92
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122069929"
---
# <a name="filter-the-additem-dialog-box-for-nested-projects"></a>筛选嵌套项目的"AddItem"对话框
为嵌套项目 **显示 AddItem** 对话框时，父项目可以控制对话框中显示哪些项。

 <xref:Microsoft.VisualStudio.Shell.Interop.IVsFilterAddProjectItemDlg2>使用 接口可以筛选将会出现在 **AddItem** 对话框中的节点。 当子项目显示 **"AddItem"** 对话框时，父项目可以实现接口并筛选将在子项目中 `IVsFilterAddProjectItemDlg` 显示的项目。

 当项目按特定父项目下的函数分组时，当用户在嵌套项目的快捷菜单上选择"添加Project项"时，即可 `IVsFilterAddProjectItemDlg` 实现 。  仅 `IvsFilterAddProjectItemDlg displays` 实现特定于该组的项目项或文件。 Project组的所有项都从对话框中筛选出来，即使它们存储在同一目录中。

 当用户打开子项的 **AddItem** 对话框时，将调用父项目的 `IVsFilterAddProjectItemDlg` 接口实现。

 `IVsFilterAddProjectItemDlg`接口还可以按类别实现筛选。 有关详细信息，请参阅 [将项添加到"添加新项"对话框](../../extensibility/internals/adding-items-to-the-add-new-item-dialog-boxes.md) 和 [注册项目和项模板](../../extensibility/internals/registering-project-and-item-templates.md)。

## <a name="see-also"></a>请参阅
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsFilterAddProjectItemDlg2>
- [将项添加到"添加新项"对话框](../../extensibility/internals/adding-items-to-the-add-new-item-dialog-boxes.md)
- [注册项目和项模板](../../extensibility/internals/registering-project-and-item-templates.md)
- [嵌套项目](../../extensibility/internals/nesting-projects.md)
