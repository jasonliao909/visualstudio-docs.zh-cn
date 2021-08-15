---
title: Project持久性|Microsoft Docs
description: 了解项目设计的持久性，包括使用 IPersistFileFormat 来持久保存文件对象和非基于文件的项目对象。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- persistence, projects
- projects [Visual Studio SDK], persistance
ms.assetid: 42907bcf-4e27-46bd-a8cb-01c2ccd2bde5
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: 19c2da562a3f9a50c9dc4aa56cf095df9d6da285aa482b5268d3ba79a955ff98
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121359281"
---
# <a name="project-persistence"></a>项目持久性
持久性是项目的关键设计注意事项。 大多数项目使用表示文件的项目项; [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 还支持其数据不基于文件的项目。 项目拥有的文件和项目文件都必须持久保存。 IDE 指示项目保存自身或项目项。

 项目的模板将传递到项目工厂。 模板应支持根据特定项目类型的要求初始化所有项目项。 这些模板稍后可以保存为项目文件，并通过解决方案由 IDE 进行管理。 有关详细信息，请参阅使用[Project 工厂和解决方案创建Project](../../extensibility/internals/creating-project-instances-by-using-project-factories.md)[实例](../../extensibility/internals/solutions-overview.md)。

 Project项可以基于文件，也可以基于非基于文件：

- 基于文件的项可以是本地项，也可以是远程项。 例如，在 C# 的 Web 项目中，与远程系统上的文件的连接在本地保留，而文件本身则保留于远程系统。

- 非基于文件的项可以将项保存到数据库或存储库。

## <a name="commit-models"></a>提交模型
 确定项目项所在的位置后，必须选择适当的提交模型。 例如，在具有本地文件的基于文件的模型中，每个项目都可以自主保存。 在存储库模型中，可以将多个项保存在一个事务中。 有关详细信息，请参阅类型[Project决策](../../extensibility/internals/project-type-design-decisions.md)。

 为了确定文件扩展名，项目实现 接口，该接口提供使对象的客户端实现"另存为"对话框的信息，即填写"另存为类型"下拉列表并管理初始 <xref:Microsoft.VisualStudio.Shell.Interop.IPersistFileFormat> 文件扩展名。  

 IDE 调用 `IPersistFileFormat` 项目上的 接口，以指示项目应适当地保留其项目项。 因此， 对象拥有其文件和格式的所有方面。 这包括 对象的格式的名称。

 如果项不是文件，则 仍保留非基于 `IPersistFileFormat` 文件的项。 Project文件（如项目的 .vbp [!INCLUDE[vbprvb](../../code-quality/includes/vbprvb_md.md)] 文件或项目的 .vcproj 文件） [!INCLUDE[vcprvc](../../code-quality/includes/vcprvc_md.md)] 也必须持久保存。

 对于保存操作，IDE 在 RDT (检查正在运行的) ，层次结构将命令传递给 和 <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistHierarchyItem> <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistHierarchyItem2> 接口。 <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistHierarchyItem.IsItemDirty%2A>实现 方法以确定该项是否已修改。 如果该项具有 ， <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistHierarchyItem.SaveItem%2A> 则实现 方法以保存已修改的项。

 接口上的方法用于确定是否可以重新加载项，如果可以重载该项， `IVsPersistHierarchyItem2` 则用于重新加载该项。 此外， <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistHierarchyItem2.IgnoreItemFileChanges%2A> 还可以实现 方法，使更改的项被丢弃而不保存。

## <a name="see-also"></a>另请参阅
- [清单：创建新的项目类型](../../extensibility/internals/checklist-creating-new-project-types.md)
- [使用项目工厂创建项目实例](../../extensibility/internals/creating-project-instances-by-using-project-factories.md)
