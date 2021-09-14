---
title: 杂项文件 Project |Microsoft Docs
description: 了解两种类型的编辑器，它们可用于打开 Visual Studio 项目中的文件，以及用于确定要使用的编辑器的项目角色。
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
ms.openlocfilehash: ff3643d3a1f2d48b0fac071f57738d73055529e7
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126602585"
---
# <a name="miscellaneous-files-project"></a>杂项文件项目
当用户打开项目项时，IDE 会将所有不属于解决方案中项目的成员的项分配给杂项文件项目。

 项目在确定用户打开项目项时所使用的编辑器方面扮演着重要的角色。 项目可设计为使用特定于项目的编辑器或标准编辑器打开某些文件。

 特定于项目的编辑器通常要求用户具有特定的知识或使用项目中的特殊接口。 有关详细信息，请参阅 [如何：打开 Project-Specific 编辑器](../../extensibility/how-to-open-project-specific-editors.md)。

 标准编辑器可在任何项目中打开特定扩展的任何文件。 用户可以为项目自定义一些标准编辑器（如 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 文本编辑器），但仍保留其公共字符。 标准编辑器是使用方法创建的 <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShellOpenDocument.OpenStandardEditor%2A> 。

 如果解决方案中没有项目响应它可以打开项目项，则 IDE 将提供一个名为 "杂项文件" 项目的特殊项目，该项目将打开任何文件。

 此特殊项目用于打开项目上下文之外的文件。 在方法的处理过程中 <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShellOpenDocument.OpenDocumentViaProject%2A> ，杂项文件项目始终以非常低的优先级进行响应。 因此，杂项文件项目始终会生成任何可打开文件的更高优先级的项目。

 "杂项文件" 项目不要求用户用 "**新建 Project** " 对话框显式创建它。 此外，杂项文件项目不会永久管理项目成员的列表。 它使用可选功能来记录每个用户最近使用过的文件的列表。

## <a name="see-also"></a>另请参阅
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsProject3>
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShellOpenDocument>
- <xref:Microsoft.VisualStudio.Shell.Interop.VSDOCUMENTPRIORITY>
- [如何：打开项目特定的编辑器](../../extensibility/how-to-open-project-specific-editors.md)
- [如何：打开标准编辑器](../../extensibility/how-to-open-standard-editors.md)
- [添加项目和项目项模板](../../extensibility/internals/adding-project-and-project-item-templates.md)
- [添加项目和项目项模板](../../extensibility/internals/adding-project-and-project-item-templates.md)
