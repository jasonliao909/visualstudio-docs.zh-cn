---
title: 源代码管理包模型|Microsoft Docs
description: 此模型表示源代码管理实现。 本文显示了类的名称，以便更轻松地查看如何执行源代码管理。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- source control [Visual Studio SDK], model
ms.assetid: 6164b2d3-a622-4de8-bef3-a6de985e9ebd
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: a43d1feb2dde67d6eae291490476db4b98850870
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122117860"
---
# <a name="model-for-source-control-packages"></a>源代码管理包的模型
下面的模型表示源代码管理实现的示例。 在模型中，可以看到必须实现的接口以及必须调用的环境服务。 像所有服务一样，实际上调用通过服务获取的特定接口的方法。 标识类的名称，以便更轻松地查看如何执行源代码管理。

 ![SCC&#95;TUP 示例](../../extensibility/internals/media/scc_tup.gif "SCC_TUP")源代码管理示例Project

## <a name="interfaces"></a>界面
 可以使用下表中所示的接口列表Visual Studio中的新项目类型实现源代码管理。

|接口|用途|
|---------------|---------|
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsQueryEditQuerySave2>|由项目和编辑器在保存或更改脏文件之前 () 调用。 此接口是使用 服务 <xref:Microsoft.VisualStudio.Shell.Interop.SVsQueryEditQuerySave> 访问的。|
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsTrackProjectDocuments2>|由项目调用，以请求添加、删除或重命名文件或目录的权限。 当批准的添加、删除或重命名操作完成时，项目也会调用此接口来通知环境。 它使用 服务 <xref:Microsoft.VisualStudio.Shell.Interop.SVsTrackProjectDocuments> 访问。|
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsTrackProjectDocumentsEvents2>|由注册以在项目添加、重命名或删除文件或目录时收到通知的任何实体实现。 若要注册事件通知，请调用 <xref:Microsoft.VisualStudio.Shell.Interop.IVsTrackProjectDocuments2.AdviseTrackProjectDocumentsEvents%2A> 。|
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsSccManager2>|由项目调用，以向源代码管理包注册并获取有关源代码管理状态的信息。 此接口是使用 服务 <xref:Microsoft.VisualStudio.Shell.Interop.SVsSccManager> 访问的。|
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsSccProject2>|由项目实现，用于响应有关文件的信息的源代码管理请求，以及获取项目文件所需的源代码管理设置。|

## <a name="see-also"></a>请参阅
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsQueryEditQuerySave2>
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsSccManager2>
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsSccProject2>
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsTrackProjectDocuments2>
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsTrackProjectDocuments2.AdviseTrackProjectDocumentsEvents%2A>
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsTrackProjectDocumentsEvents2>
- [支持源代码管理](../../extensibility/internals/supporting-source-control.md)
