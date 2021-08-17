---
title: 命令放置指南|Microsoft Docs
description: 了解在 IDE Visual Studio 集成开发环境中定位 (指南和) 。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- commands, small command sets
- small command sets
- command sets
ms.assetid: 63b3478e-e08a-420b-a0ec-76767e0cb289
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: f0e78221b93d766b8dd0f018501f3fc808a98c16
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122029003"
---
# <a name="command-placement-guidelines"></a>命令放置指南
在集成开发环境中定位命令Visual Studio IDE (IDE) 取决于命令集的大小。 根据 *.vsct* 文件中的信息定义和定位命令。

## <a name="best-practices-for-all-command-sets"></a>所有命令集的最佳实践
 对于每组命令，请遵循以下准则：

- 提前准备命令结构的图表。 标识将在多个位置使用的命令、组合框、命令组和快捷菜单。

- 在同一组中显示的命令应相关。

- 仅包含一个命令的组是可接受的。

- 包不应将大量命令添加到现有Visual Studio菜单中。 相反，它们应创建菜单或子菜单来托管新命令。

- 将命令放在现有菜单上时，请命名该命令，以便其用途清晰明了，并且不会与现有命令混淆。

## <a name="best-practices-for-small-command-sets"></a>适用于小型命令集的最佳实践
 如果要开发只有几个命令的 VSPackage，也请遵循以下准则：

- 如果可能，请使用 [命令](../../extensibility/parent-element.md) 、组合框、组或子菜单的 Parent 元素，以将元素放入相应的组中。

- 将这些组分配到 VSPackage 显示的菜单。

- 子菜单或命令的父级必须是 [Group](../../extensibility/group-element.md) 元素。 将命令和子菜单分配给组，然后将组分配给父菜单。

- 可以通过在命令定义后添加 [CommandPlacements](../../extensibility/commandplacements-element.md) 元素节，然后为元素添加每个附加组的 `CommandPlacements` [CommandPlacement 元素，将命令放入](../../extensibility/commandplacement-element.md) 其他组。

## <a name="best-practices-for-large-command-sets"></a>大型命令集的最佳实践
 如果 VSPackage 将有多个命令将出现在多个上下文中，也请遵循以下准则：

- 使菜单、组和命令成为自父级。 也就是说，请勿在 `Parent` 项的定义中分配 元素。

- 使用 `CommandPlacement` 元素节中的元素 `CommandPlacements` 条目将菜单、组和命令放在其父菜单和组中。

- 在 `CommandPlacements` 元素部分中，填充给定菜单或组的条目应彼此相邻。 这有助于可读性，使 `Priority` 排名更易于确定。

## <a name="see-also"></a>请参阅
- [VSPackage 如何添加用户界面元素](../../extensibility/internals/how-vspackages-add-user-interface-elements.md)
- [Visual Studio命令表 (.vsct) 文件](../../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)
