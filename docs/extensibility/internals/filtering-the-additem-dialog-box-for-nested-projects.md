---
title: 筛选嵌套项目的 AddItem 对话框 |Microsoft Docs
description: 了解如何通过实现父项目的 IVsFilterAddProjectItemDlg 接口，在 Visual Studio 中筛选嵌套项目的 AddItem 对话框。
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
ms.openlocfilehash: aa65af14d05b60e78643f03c1f74719fb1c25eadf246451287ed04d58723e4f4
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121338002"
---
# <a name="filter-the-additem-dialog-box-for-nested-projects"></a>筛选嵌套项目的 AddItem 对话框
当你为嵌套项目显示 **AddItem** 对话框时，父项目可以控制哪些项显示在对话框中。

 使用 <xref:Microsoft.VisualStudio.Shell.Interop.IVsFilterAddProjectItemDlg2> 接口可以筛选将在 **AddItem** 对话框中的节点。 当子项目显示 " **AddItem** " 对话框时，父级可以实现 `IVsFilterAddProjectItemDlg` 接口，并筛选将在子项的项目中显示的项。

 当项目按特定父项目中的函数分组后，可以在 `IVsFilterAddProjectItemDlg` 用户在嵌套项目的快捷菜单上选择 "**添加 Project 项**" 时实现。 `IvsFilterAddProjectItemDlg displays`仅实现特定于该组的项目项或文件。 将从对话框筛选出其他组 Project 项，即使这些项存储在同一目录中也是如此。

 当用户打开儿童的 **AddItem** 对话框时，将调用该接口的父项目的实现 `IVsFilterAddProjectItemDlg` 。

 `IVsFilterAddProjectItemDlg`接口还可以实现按类别筛选。 有关详细信息，请参阅向 ["添加新项" 对话框添加项](../../extensibility/internals/adding-items-to-the-add-new-item-dialog-boxes.md) 和 [注册项目和项模板](../../extensibility/internals/registering-project-and-item-templates.md)。

## <a name="see-also"></a>另请参阅
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsFilterAddProjectItemDlg2>
- [向 "添加新项" 对话框添加项](../../extensibility/internals/adding-items-to-the-add-new-item-dialog-boxes.md)
- [注册项目和项模板](../../extensibility/internals/registering-project-and-item-templates.md)
- [嵌套项目](../../extensibility/internals/nesting-projects.md)
