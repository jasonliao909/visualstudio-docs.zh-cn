---
title: IDE-Defined 命令、菜单和组 |Microsoft Docs
description: 了解 Visual Studio 集成开发环境 (IDE) 中定义的菜单、命令和命令组。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- commands, environment-defined
- .vsct files, environment-defined constants
- command groups, environment-defined
ms.assetid: 86b3af13-7163-48c6-986b-7beeedbc26cc
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: febe1d37ecd79b46771f006691dae1a3006a8709fc91599dd9562474990a6ad9
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121448021"
---
# <a name="ide-defined-commands-menus-and-groups"></a>IDE 定义的命令、菜单和组
许多菜单、命令和命令组已定义为供 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] IDE 使用。 扩展时，还可以使用这些命令 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 。

## <a name="finding-environment-defined-commands"></a>查找 Environment-Defined 命令
 环境命令在一组 .vsct 文件中定义：

- SharedCmdDef. .vsct

- SharedCmdPlace. .vsct

- ShellCmdDef. .vsct

- ShellCmdPlace. .vsct

  这些文件位于 \VisualStudioIntegration\Common\Inc 中 *\<Visual Studio SDK installation path>* \\ 。 这些文件提供菜单和组的定义和 Guid，可在命令表配置 (. .vsct) 文件中使用，作为你自己的菜单、组和命令的容器。

## <a name="in-this-section"></a>本节内容
- [Visual Studio 菜单中的 GUID 和 ID](../../extensibility/internals/guids-and-ids-of-visual-studio-menus.md)

 提供 Visual Studio 菜单栏上的菜单的 GUID 和 ID 值以及它们所包含的组的 ID 值。

- [Visual Studio 工具栏中的 GUID 和 ID](../../extensibility/internals/guids-and-ids-of-visual-studio-toolbars.md)

 提供 Visual Studio IDE 中工具栏的 GUID 和 ID 值以及它们包含的组的 ID 值。

- [Visual Studio 命令中的 GUID 和 ID](../../extensibility/internals/guids-and-ids-of-visual-studio-commands.md)

 提供 Visual Studio IDE 定义的命令的 GUID 和 ID 值。

## <a name="see-also"></a>另请参阅
- [Visual Studio 命令表格 (.Vsct) 文件](../../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)
- [用于扩展项目系统的 IDE 定义的命令](../../extensibility/internals/ide-defined-commands-for-extending-project-systems.md)
- [VSPackage 如何添加用户界面元素](../../extensibility/internals/how-vspackages-add-user-interface-elements.md)
