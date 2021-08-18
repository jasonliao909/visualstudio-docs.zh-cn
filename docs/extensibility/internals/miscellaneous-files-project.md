---
title: 杂项文件Project |Microsoft Docs
description: 了解两种类型的编辑器，这些编辑器可用于打开 Visual Studio 项目中的文件，以及项目在确定使用哪个编辑器时的角色。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- files, adding existing files to solutions
- Miscellaneous Files project
- Solution Items folder
- files, opening with Miscellaneous Files project
ms.assetid: 93a278a8-d4f4-400b-8945-4f1b0a2b5bac
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: 2a3c372e80b9c0843d63c1ed6e674cf9cc5c1bb6d1d68bec4f6fa1e06b4476dc
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121337885"
---
# <a name="miscellaneous-files-project"></a>杂项文件项目
当用户打开项目项时，IDE 会向杂项文件项目分配不是解决方案中任何项目的成员的任何项。

 在用户打开项目项时，项目在确定使用哪个编辑器方面扮演重要角色。 项目可以通过使用特定于项目的编辑器或标准编辑器来打开某些文件。

 特定于项目的编辑器通常要求用户具有特殊知识或使用项目中的特殊接口。 有关详细信息，请参阅 [如何：打开Project-Specific编辑器](../../extensibility/how-to-open-project-specific-editors.md)。

 标准编辑器可以在任何项目中打开特定扩展名的任何文件。 用户可以为项目自定义一些标准编辑器（如文本编辑器） [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 但仍保留其公共字符。 标准编辑器是使用 方法 <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShellOpenDocument.OpenStandardEditor%2A> 创建的。

 如果解决方案中没有任何项目响应它可以打开项目项，则 IDE 会提供一个称为"杂项文件"项目的特殊项目，用于打开任何文件。

 此特殊项目提供在项目上下文之外打开文件。 在处理 方法期间 <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShellOpenDocument.OpenDocumentViaProject%2A> ，杂项文件项目始终以非常低的优先级进行响应。 因此，杂项文件项目始终生成任何可以打开文件的更高优先级项目。

 杂项文件项目不要求用户使用"新建文件"对话框 **Project创建它**。 此外，杂项文件项目不会永久管理项目成员列表。 它使用可选功能来记录每个用户最近使用的文件列表。

## <a name="see-also"></a>请参阅
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsProject3>
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShellOpenDocument>
- <xref:Microsoft.VisualStudio.Shell.Interop.VSDOCUMENTPRIORITY>
- [如何：打开项目特定的编辑器](../../extensibility/how-to-open-project-specific-editors.md)
- [如何：打开标准编辑器](../../extensibility/how-to-open-standard-editors.md)
- [添加项目和项目项模板](../../extensibility/internals/adding-project-and-project-item-templates.md)
- [添加项目和项目项模板](../../extensibility/internals/adding-project-and-project-item-templates.md)
