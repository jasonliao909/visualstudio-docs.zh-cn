---
title: 添加Project和Project项模板|Microsoft Docs
description: 了解如何将项目和项目项模板添加到 IDE Visual Studio集成开发 (对话框中) 。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- projects [Visual Studio SDK], adding
- project items [Visual Studio], adding
ms.assetid: 8c59217f-56e5-4540-a73b-cd10de189373
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: 703c8db7dcc8245719ca9c8abba98653254260ba
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122029133"
---
# <a name="add-project-and-project-item-templates"></a>添加项目和项目项模板
创建自己的项目类型时，必须使用 IDE 对话框中的标准集成开发环境 ([!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 添加新项目和) 项。 以下主题讨论用于添加项目和项目项的不同技术。

## <a name="in-this-section"></a>本节内容
- [Project上下文](../../extensibility/internals/project-context.md)

 说明项目为环境中转译内容提供了大部分上下文信息。

- [Project优先级](../../extensibility/internals/project-priority.md)

 说明项目项通常是一个项目的成员，以帮助避免有关使用哪个项目打开该项的歧义。

- [杂项文件项目](../../extensibility/internals/miscellaneous-files-project.md)

 提供有关可用于打开项目中文件的两种类型的编辑器的信息，以及项目在确定打开项目项时要使用哪个编辑器时所扮演的角色。

- [注册项目和项模板](../../extensibility/internals/registering-project-and-item-templates.md)

 说明创建项目 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 时发生的情况。

- [将项添加到"添加新项"对话框](../../extensibility/internals/adding-items-to-the-add-new-item-dialog-boxes.md)

 说明向"添加新项"对话框 **添加项** 的过程。

- [将目录添加到"新建Project对话框](../../extensibility/internals/adding-directories-to-the-new-project-dialog-box.md)

 提供注册包含 VSPackage 提供的自定义模板的新目录的示例。

- [将目录添加到"添加新项"对话框](../../extensibility/internals/adding-directories-to-the-add-new-item-dialog-box.md)

 提供为"添加新项"对话框注册一组 **新目录的示例** 。

- [用于扩展项目系统的 IDE 定义命令](../../extensibility/internals/ide-defined-commands-for-extending-project-systems.md)

 列出用于扩展项目系统的不同类型的命令项。

- [通常用于扩展项目的 对象的 CATID](../../extensibility/internals/catids-for-objects-that-are-typically-used-to-extend-projects.md)

 列出用于扩展 、 和 项目系统的 对象的 [!INCLUDE[vcprvc](../../code-quality/includes/vcprvc_md.md)] [!INCLUDE[csprcs](../../data-tools/includes/csprcs_md.md)] [!INCLUDE[vbprvb](../../code-quality/includes/vbprvb_md.md)] CATID。

## <a name="related-sections"></a>相关章节
- [如何：打开特定于项目的编辑器](../../extensibility/how-to-open-project-specific-editors.md)

 提供分步说明，用于打开本质上绑定到项目的特定编辑器的项。

- [如何：打开标准编辑器](../../extensibility/how-to-open-standard-editors.md)

 提供有关打开标准编辑器的分步说明。

- [Project子类型](../../extensibility/internals/project-subtypes.md)

 提供指向项目子类型概念主题的链接。 Project子类型扩展现有 [!INCLUDE[csprcs](../../data-tools/includes/csprcs_md.md)] 和 [!INCLUDE[vbprvb](../../code-quality/includes/vbprvb_md.md)] 项目。

- [项目类型](../../extensibility/internals/project-types.md)

 提供指向其他主题的链接，这些主题提供有关如何设计新项目类型的信息。
