---
title: 支持源代码管理|Microsoft Docs
description: 了解如何Visual Studio项目或编辑器的文件签出、签入和其他源代码管理操作。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- source control [Visual Studio SDK], supporting
ms.assetid: 567acde3-354e-4f39-8d99-0ef86c103396
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: 4601c7e10d3f3092ad274e0570148bb348a7f41a
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122086477"
---
# <a name="supporting-source-control"></a>支持源代码管理
[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 支持项目或编辑器的文件签出、签入和其他源代码管理操作。 作为源代码管理客户端， 旨在与源代码管理包（如 ）交互，该包为动态定义的一组文件提供存档、版本控制和 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] [!INCLUDE[vsvss](../../extensibility/includes/vsvss_md.md)] 控制功能。

## <a name="in-this-section"></a>本节内容
- [源代码管理包的模型](../../extensibility/internals/model-for-source-control-packages.md)

 描述项目类型必须实现以支持源代码管理接口。

- [设计决策](../../extensibility/internals/source-control-design-decisions.md)

 提供其答案会更改项目类型实现方案的问题。

- [配置详细信息](../../extensibility/internals/source-control-configuration-details.md)

 描述支持源代码管理如何更改项目类型的实现。

- [项目和编辑器的其他指南](../../extensibility/internals/additional-source-control-guidelines-for-projects-and-editors.md)

 讨论项目类型和编辑器的最佳实践。

- [运行时详细信息](../../extensibility/internals/source-control-runtime-details.md)

 描述当用户将项目添加到源代码管理系统时如何注册项目。

## <a name="reference"></a>参考
 <xref:Microsoft.VisualStudio.Shell.Interop.IVsQueryEditQuerySave2> 向环境或源代码管理包指示文件即将在内存中更改或保存。

 <xref:Microsoft.VisualStudio.Shell.Interop.IVsSccManager2> 允许项目和层次结构向源代码管理注册自身，并获取有关源代码管理状态的信息。

 <xref:Microsoft.VisualStudio.Shell.Interop.IVsSccProject2> 在项目系统中实现，为项目文件和项目项提供源代码管理。

 <xref:Microsoft.VisualStudio.Shell.Interop.IVsTrackProjectDocuments2> 由项目用来查询环境以在解决方案中添加、删除或重命名文件或目录的权限。

 <xref:Microsoft.VisualStudio.Shell.Interop.IVsTrackProjectDocumentsEvents2> 向客户端通知对项目文件或目录所做的更改。

## <a name="related-sections"></a>相关章节
- [项目类型](../../extensibility/internals/project-types.md)

 概述作为 IDE 集成开发环境的基本构建基块 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 的项目 (IDE) 。 提供了其他主题的链接，这些主题介绍了项目如何控制代码的生成和编译。
