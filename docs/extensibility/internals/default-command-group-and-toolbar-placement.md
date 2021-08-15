---
title: 默认命令、组和工具栏|Microsoft Docs
description: 了解 IDE 命令、产品命令和编辑器命令，Visual Studio用户界面默认显示这些命令。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- commands [Visual Studio], default groups
- toolbars [Visual Studio], default
- commands [Visual Studio], default editor
- command groups
- commands [Visual Studio], default IDE
- commands [Visual Studio], default product
ms.assetid: 35342110-d639-4577-8367-00b21dcc6f07
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: 86b58d33f07eaae8ef93ddb82a77516a6eb182c467d77cc5857336bab6756844
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121359606"
---
# <a name="default-command-group-and-toolbar-placement"></a>默认命令、组和工具栏位置
为了产品一致性和稳定性，UI 默认显示某些命令组，并提供 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 命令和命令组的定义。 VSPackages 还可使用标准命令和命令组。

 默认命令组分为三类：IDE 命令、产品命令和编辑器命令。

## <a name="default-ide-commands"></a>默认 IDE 命令
 默认 IDE 工具栏包括 由 中包含的所有产品共享的命令 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 。 其中包括与泛型项目操作相关的命令，例如 **Save** 命令和 **Add Item** 命令。 VSPackage 不应在此工具栏中添加或减去，但一个例外：如果产品或 VSPackage 添加新的工具窗口，则窗口应添加到"视图"菜单上的可用工具 **窗口列表中** 。 新产品或 VSPackage 可以添加自己的工具栏。

## <a name="default-product-commands"></a>默认产品命令
 每个产品都可以为 IDE 提供其自己的默认工具栏，其中包含重要且常用的命令。 但是，最好尽可能使用现有菜单和工具栏，并根据需要使用其他特定于任务的工具栏来补充它们。

 工具栏的优先级字段确定其行位置。 零优先级将工具栏放在第 3 行 (第 3 行) 菜单栏下 (第 1 行) "标准"工具栏 (第2 行) 。 因此，其他工具栏显示在行中 (优先级 + 3) 。 后续工具栏将放置在同一行（如果有空间）;否则，它们会自动移动到下一行。

## <a name="default-editor-commands"></a>默认编辑器命令
 提供自定义编辑器的 VSPackage 应提供一个默认工具栏，其中包含该编辑器中最重要且最常用的命令。 编辑器工具栏应在编辑器处于活动状态时显示，在编辑器不处于活动状态时应隐藏。 此可见性在 `VisibilityConstraints` *.vsct* 文件的 元素中控制。

 编辑器工具栏应放置在 IDE 和产品工具栏下方。

## <a name="see-also"></a>另请参阅
- [IDE 定义的命令、菜单和组](../../extensibility/internals/ide-defined-commands-menus-and-groups.md)
- [VSPackage 如何添加用户界面元素](../../extensibility/internals/how-vspackages-add-user-interface-elements.md)
