---
title: 查询编辑查询 保存 (源代码管理 VSPackage) |Microsoft Docs
description: 了解事件Query-Edit Query-Save以及源代码管理 VSPackage 如何处理这些事件。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- QEQS events
- Query Edit Query Save events
- source control packages, Query Edit Query Save events
ms.assetid: c360d2ad-fe42-4d65-899d-d1588cc8a322
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: 3ce9aef41af1cb0b11e5098ce2c6767716510eec8632fdf419d1b1f143afa72d
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121337859"
---
# <a name="query-edit-query-save-source-control-vspackage"></a>查询编辑查询保存（源代码管理 VSPackage）
[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 编辑器可以广播查询编辑查询保存 (QEQS) 事件。 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 源代码管理存根实现 QEQS 服务，以便它是 QEQS 事件的接收者。 然后，这些事件将委托给当前处于活动状态的源代码管理 VSPackage。 活动源代码管理 VSPackage 实现 <xref:Microsoft.VisualStudio.Shell.Interop.IVsQueryEditQuerySave2> 及其方法。 接口的方法通常在首次编辑文档之前和保存文档之前 `IVsQueryEditQuerySave2` 立即调用。

## <a name="queryeditquerysave-events"></a>QueryEditQuerySave 事件
 源代码管理 VSPackage 必须通过实现 接口和必要的方法来处理 QEQS `IVsQueryEditQuerySave2` 事件。 下面是 VSPackage 至少必须实现两种方法的简要说明。 实际实现必须与源代码管理模型的逻辑一样。

### <a name="queryeditfiles-method"></a>QueryEditFiles 方法
 <xref:Microsoft.VisualStudio.Shell.Interop.IVsQueryEditQuerySave2.QueryEditFiles%2A>当任何项目或编辑器想要修改文件时，将调用 。 理想情况下，在修改 *文件和* 保存文件时调用此方法。 调用时， 方法检查给定的文件是否受源代码管理，是否需要签出这些文件， `IVsQueryEditQuerySave2::QueryEditFiles` 以及是否可以重新加载这些文件。 如果情况阻止文件可编辑，则 方法 `IVsQueryEditQuerySave2::QueryEditFiles` 会告知调用程序取消编辑。 调用方还可以指定调用模式。 在"无提示"模式下，此方法仅在不会导致任何 UI 出现时采取措施。 如果 UI 无法避免，则必须返回标志以指示问题。

 方法以事务方式运行;也就是说，如果取消对单个文件的编辑，则取消所有文件的编辑。 相反，如果允许编辑，则允许所有文件进行编辑。 如果此方法允许对一组给定文件进行一次编辑，则它必须始终允许对同一组文件的后续调用进行编辑。 allow-edit 循环将继续，直到文件关闭、保存和重新加载;直到其属性 (属性) 更改;或 ，直到源代码管理包更改。 实现 方法时要考虑的情况 `IVsQueryEditQuerySave2::QueryEditFiles` 包括多个文件、特殊文件、取消用户和内存中编辑。

### <a name="querysavefiles-method"></a>QuerySaveFiles 方法
 <xref:Microsoft.VisualStudio.Shell.Interop.IVsQueryEditQuerySave2.QuerySaveFiles%2A>当任何项目或编辑器需要保存一组文件时，将调用 。 调用时， `IVsQueryEditQuerySave2::QuerySaveFiles` 方法检查给定的文件是否是只读的，以及它们是否受源代码管理。 如果需要签出文件，则调用将委托给源代码管理包。 如果情况阻止保存文件，则 方法 `IVsQueryEditQuerySave2::QuerySaveFiles` 必须告知编辑器取消保存。 与 方法 `IVsQueryEditQuerySave2::QueryEditFiles` 一样，调用方可以指定调用模式。 在"无提示"模式下，此方法仅在不会导致任何 UI 出现时采取措施。 如果 UI 无法避免，则必须返回标志以指示问题。

 此方法必须以事务方式运行;也就是说，如果对单个文件取消了保存，则取消所有文件的保存。 相反，如果允许保存，则必须允许所有文件保存。 与 方法一样，实现 方法时要考虑的事例包括多个文件、特殊文件、取消用户和 `IVsQueryEditQuerySave2::QueryEditFiles` `IVsQueryEditQuerySave2::QuerySaveFiles` 内存中编辑。

## <a name="see-also"></a>请参阅
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsQueryEditQuerySave2>
