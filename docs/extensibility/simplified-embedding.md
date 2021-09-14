---
title: 简化的嵌入|Microsoft Docs
description: 了解简化的嵌入，当其文档视图对象是文档视图对象的子级时，可以在编辑器中启用Visual Studio。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- editors [Visual Studio SDK], custom - simple view embedding
ms.assetid: f1292478-a57d-48ec-8c9e-88a23f04ffe5
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: 02f30713513715df87dff72418328b46e795ec16
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126600842"
---
# <a name="simplified-embedding"></a>简化的嵌入
当编辑器的文档视图对象被父级 (，即，成为) 的子级时，编辑器中将启用简化的嵌入，并且实现 接口以处理 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] <xref:Microsoft.VisualStudio.Shell.Interop.IVsWindowPane> 其窗口命令。 简化的嵌入编辑器无法承载活动控件。 下图显示了用于创建具有简化嵌入的编辑器的对象。

 ![简化的嵌入编辑器图形](../extensibility/media/vssimplifiedembeddingeditor.gif "vsSimplifiedEmbeddingEditor") 具有简化嵌入的编辑器

> [!NOTE]
> 在此图中的对象中，创建基于文件的标准编辑器 `CYourEditorFactory` 只需要 对象。 如果要创建自定义编辑器，则无需实现 ，因为编辑器可能会具有 <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistDocData2> 其自己的专用持久性机制。 但是，对于非自定义编辑器，必须这样做。

 为创建具有简化嵌入的编辑器而实现的所有接口都包含在 `CYourEditorDocument` 对象中。 但是，若要支持文档数据的多个视图，将接口拆分为单独的数据并查看对象，如下表所示。

|接口|接口的位置|使用|
|---------------|---------------------------|---------|
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsWindowPane>|查看|提供与父窗口的连接。|
|<xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget>|查看|处理命令。|
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsStatusbarUser>|查看|启用状态栏更新。|
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsToolboxUser>|查看|启用 **工具箱** 项。|
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsFileChangeEvents>|数据|在文件更改时发送通知。|
|<xref:Microsoft.VisualStudio.Shell.Interop.IPersistFileFormat>|数据|为文件类型启用"另存为"功能。|
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistDocData2>|数据|实现文档持久性。|
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsDocDataFileChangeControl>|数据|允许抑制文件更改事件，例如重载触发。|
