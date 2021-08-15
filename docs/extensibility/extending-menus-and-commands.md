---
title: 扩展菜单和命令|Microsoft Docs
description: 了解命令，这些命令将操作和进程添加到Visual Studio。 VSPackage 项目模板演示如何实现非常基本的命令。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- menus, common tasks
- VSPackages, menu tasks
- .vsct files, common menu tasks
ms.assetid: 7b2be4b9-e3fe-4412-874f-ae72ebc84c4b
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: a9b7070b491b56c0a99e3fc6a06e4d64b0f7d4c20834fdd1a069c9b54a267deb
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121448372"
---
# <a name="extend-menus-and-commands"></a>扩展菜单和命令
命令是向用户添加操作和Visual Studio。 在大多数情况下，命令显示在菜单或工具栏上。 VSPackage 项目模板演示如何实现非常基本的命令。 有关稍长但仍为基本实现，请参阅 [使用菜单命令 创建扩展](../extensibility/creating-an-extension-with-a-menu-command.md)。

 有关命令、Visual Studio和工具栏的信息，请参阅命令[、菜单和工具栏](../extensibility/internals/commands-menus-and-toolbars.md)。

 命令、菜单和工具栏在 VSPackage 项目的 *.vsct* 文件中定义。 可以在 [VSPackages](../extensibility/internals/how-vspackages-add-user-interface-elements.md)如何添加用户界面元素 中Visual Studio IDE 和 *.vsct* 文件的信息。

 以下主题介绍如何添加不同类型的命令、菜单和工具栏。

## <a name="in-this-section"></a>本节内容
- [将菜单添加到菜单Visual Studio栏](../extensibility/adding-a-menu-to-the-visual-studio-menu-bar.md)说明如何将菜单添加到菜单栏的顶部Visual Studio菜单。

- [将键盘快捷方式绑定到菜单项](../extensibility/binding-keyboard-shortcuts-to-menu-items.md) 说明如何向菜单项添加键盘快捷方式 (如 CTRL + 3) 键。

- [向菜单添加子菜单](../extensibility/adding-a-submenu-to-a-menu.md) 说明如何将子菜单添加到顶部菜单。

- [将最近使用的列表添加到子项](../extensibility/adding-a-most-recently-used-list-to-a-submenu.md) 说明如何添加"最近使用"列表。

- [创建可重用的按钮组](../extensibility/creating-reusable-groups-of-buttons.md) 介绍如何对命令项进行分组，以便它们可以包含在多个菜单上。

- [向菜单命令添加图标](../extensibility/adding-icons-to-menu-commands.md) 介绍如何向工具栏和菜单上的命令添加图标。

- [更改菜单命令的文本](../extensibility/changing-the-text-of-a-menu-command.md) 描述如何使用 `TextChanges` 标志来启用要动态更改的菜单项。

- [更改命令的外观](../extensibility/changing-the-appearance-of-a-command.md) 介绍如何动态启用或禁用命令。

- [更新用户界面](../extensibility/updating-the-user-interface.md) 描述如何强制更新用户界面以反映最近的更改。

- [本地化菜单命令](../extensibility/localizing-menu-commands.md) 说明如何本地化菜单命令。
