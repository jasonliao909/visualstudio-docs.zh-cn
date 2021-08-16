---
title: 保存自定义文档|Microsoft Docs
description: 了解添加到 IDE 中的项目类型的自定义文档Visual Studio过程。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- persistence, saving custom documents
- projects [Visual Studio SDK], saving custom documents
- editors [Visual Studio SDK], saving custom documents
ms.assetid: 040b36d6-1f0a-4579-971c-40fbb46ade1d
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: ae3e4fd732b4a0a296701b137fa158eb5926162b11f1cdaf8988c2f4ed3a10bb
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121401229"
---
# <a name="saving-a-custom-document"></a>保存自定义文档
环境处理"保存 **"、"****另存为**"和"**全部保存"** 命令。 当用户单击"文件 **"菜单上的"保存**"、"另存为"或"全部保存"或关闭解决方案时，导致"全部保存"时，将发生以下过程。  

 ![客户编辑器保存](../../extensibility/internals/media/private.gif "专用") 自定义编辑器的"保存"、"另存为"和"全部保存"命令处理

 以下步骤详细介绍了此过程：

1. 对于 **"另** 存 **为** "命令，环境使用 服务来确定 <xref:Microsoft.VisualStudio.Shell.Interop.SVsShellMonitorSelection> 活动文档窗口，从而确定应保存哪些项。 活动文档窗口已知后，环境将查找层次结构指针和项标识符 (为正在运行的文档表中的) 指定 itemID。 有关详细信息，请参阅 [运行文档表](../../extensibility/internals/running-document-table.md)。

     对于"全部保存"命令，环境使用正在运行的文档表中的信息来编译要保存的所有项的列表。

2. 当解决方案收到调用时，它会在一组所选项中 (，即服务公开的多个 <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget.QueryStatus%2A> <xref:Microsoft.VisualStudio.Shell.Interop.SVsShellMonitorSelection>) 。

3. 在选择的每个项上，解决方案使用层次结构指针调用 方法来 <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistHierarchyItem2.IsItemDirty%2A> 确定是否应启用"保存"菜单命令。 如果一个或多个项是脏项，则启用"保存"命令。 如果层次结构使用标准编辑器，则层次结构通过调用 方法将查询脏状态委托给 <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistDocData2.IsDocDataDirty%2A> 编辑器。

4. 在每个选定的脏项上，解决方案使用层次结构指针在 <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistHierarchyItem2.SaveItem%2A> 相应的层次结构上调用 方法。

     对于自定义编辑器，文档数据对象与项目之间的通信是私有的。 因此，这两个对象之间会处理任何特殊的持久性问题。

    > [!NOTE]
    > 如果实现自己的持久性，请务必调用 <xref:Microsoft.VisualStudio.Shell.Interop.IVsQueryEditQuerySave2.QuerySaveFiles%2A> 方法来节省时间。 此方法进行检查以确保将文件保存为 (，例如，文件不是只读) 。

## <a name="see-also"></a>另请参阅
- <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget>
- [打开和保存项目项](../../extensibility/internals/opening-and-saving-project-items.md)
