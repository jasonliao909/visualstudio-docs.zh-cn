---
title: IDE-Defined命令、菜单和组|Microsoft Docs
description: 了解在集成开发环境中定义的菜单、命令和命令组Visual Studio IDE (环境) 。
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
ms.openlocfilehash: 9f25616c97ed4f3b1e8402432a36db86e72edb58
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122042382"
---
# <a name="ide-defined-commands-menus-and-groups"></a>IDE 定义的命令、菜单和组
许多菜单、命令和命令组已定义供 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] IDE 使用。 扩展 时，这些命令也可供使用 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 。

## <a name="finding-environment-defined-commands"></a>查找Environment-Defined命令
 环境命令在一组四个 .vsct 文件中定义：

- SharedCmdDef.vsct

- SharedCmdPlace.vsct

- ShellCmdDef.vsct

- ShellCmdPlace.vsct

  这些文件位于 *\<Visual Studio SDK installation path>* \VisualStudioIntegration\Common\Inc \\ 中。 这些文件提供可在 VSPackage 的命令表配置 (.vsct) 文件中用作自己的菜单、组和命令容器的菜单和组的定义和 GUID。

## <a name="in-this-section"></a>本节内容
- [Visual Studio 菜单中的 GUID 和 ID](../../extensibility/internals/guids-and-ids-of-visual-studio-menus.md)

 为菜单栏上的菜单及其包含的组Visual Studio GUID 和 ID 值。

- [Visual Studio 工具栏中的 GUID 和 ID](../../extensibility/internals/guids-and-ids-of-visual-studio-toolbars.md)

 为 IDE 中的工具栏及其包含的组Visual Studio GUID 和 ID 值。

- [Visual Studio 命令中的 GUID 和 ID](../../extensibility/internals/guids-and-ids-of-visual-studio-commands.md)

 为 IDE 定义的命令提供 GUID 和 ID Visual Studio值。

## <a name="see-also"></a>请参阅
- [Visual Studio 命令表格 (.Vsct) 文件](../../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)
- [用于扩展项目系统的 IDE 定义的命令](../../extensibility/internals/ide-defined-commands-for-extending-project-systems.md)
- [VSPackage 如何添加用户界面元素](../../extensibility/internals/how-vspackages-add-user-interface-elements.md)
