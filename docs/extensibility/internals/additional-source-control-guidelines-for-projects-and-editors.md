---
title: 项目和编辑器的源代码管理准则
description: 了解项目和编辑器为了支持源代码管理而应遵循的准则。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- source control [Visual Studio SDK], guidelines for projects and editors
ms.assetid: 2483cce5-321c-4d3c-9c5c-ee8385263f74
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: 68934fb67ff1bd4f17507ac4af72c0aaf113816c6b6ff643c9f49bbb40698e81
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121414683"
---
# <a name="additional-source-control-guidelines-for-projects-and-editors"></a>项目和编辑器的其他源代码管理准则
项目和编辑器应遵循许多准则来支持源代码管理。

## <a name="guidelines"></a>指南
 项目或编辑器还应执行以下操作以支持源代码管理：

|区域|项目|编辑器|详细信息|
|----------|-------------|------------|-------------|
|文件的专用副本|X||环境支持文件的专用副本。 也就是说，在项目中登记的每个人都有自己的项目中文件的专用副本。|
|ANSI/Unicode 暂留|X|X|如果编写持久性代码，请以 ANSI 格式保存文件，因为大多数源代码管理程序当前不支持 Unicode。|
|枚举文件|X||项目必须包含其中所有文件的特定列表，并且必须能够使用 或 <xref:Microsoft.VisualStudio.Shell.Interop.IVsSccProject2> <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy.GetProperty%2A> (VSH_PROPID_First_Child/Next_Sibling) 。 项目还应通过其实现公开项名称，并支持名称查找 (包括通过其实现) <xref:Microsoft.VisualStudio.Shell.Interop.IVsProject.GetMkDocument%2A> 文件 <xref:Microsoft.VisualStudio.Shell.Interop.IVsProject.IsDocumentInProject%2A> 。|
|文本格式|X|X|如果可能，文件应采用文本格式，以支持不同版本的合并。 非文本格式的文件以后无法与文件的其他版本合并。 首选文本格式为 XML。|
|基于引用|X||源代码管理中随时支持基于引用的项目。 但是，只要项目可以按需生成其文件列表，无论这些文件是否存在于磁盘上，源代码管理也支持基于目录的项目。 从源代码管理打开项目时，项目文件首先在其任何文件之前关闭。|
|按可预测的顺序持久保存对象和属性|X|X|以可预测的顺序（如字母顺序）保留文件，以便于合并。|
|重新加载|X|X|当文件在磁盘上发生更改时，编辑器必须能够重新加载它。 参与源代码管理时，环境会通过调用 实现来重新加载 <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistDocData2.ReloadDocData%2A> 数据。 最难以重载的情况是在调用 IVsQueryEditQuerySave：： 且正在处理信息时 <xref:Microsoft.VisualStudio.Shell.Interop.IVsQueryEditQuerySave2.QueryEditFiles%2A> 发生签出。 但是，重载代码必须能够在这种情况下运行。<br /><br /> 环境会自动重新加载项目文件。 但是，如果项目具有嵌套层次结构，则项目必须实现 ，以支持 <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistHierarchyItem2> 重新加载嵌套项目文件。|

## <a name="see-also"></a>另请参阅
- [支持源代码管理](../../extensibility/internals/supporting-source-control.md)
