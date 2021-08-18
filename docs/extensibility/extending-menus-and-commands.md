---
title: 扩展菜单和命令 |Microsoft Docs
description: 了解用于将操作和进程添加到 Visual Studio 的命令。 VSPackage 项目模板演示如何实现一个非常基本的命令。
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
ms.openlocfilehash: 208166391ddff405f30f9ed2d5f4fdc7c16cc4c0
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122087192"
---
# <a name="extend-menus-and-commands"></a>扩展菜单和命令
命令是向 Visual Studio 添加操作和过程的方式。 在大多数情况下，会在菜单或工具栏上显示命令。 VSPackage 项目模板演示如何实现一个非常基本的命令。 对于稍长但仍是基本实现的，请参阅 [使用菜单命令创建扩展](../extensibility/creating-an-extension-with-a-menu-command.md)。

 有关 Visual Studio 命令、菜单和工具栏的详细信息，请参阅[命令、菜单和工具栏](../extensibility/internals/commands-menus-and-toolbars.md)。

 命令、菜单和工具栏是在 VSPackage 项目中的 *.vsct* 文件中定义的。 可以在 [vspackage 添加用户界面元素的方式](../extensibility/internals/how-vspackages-add-user-interface-elements.md)中查找有关 Visual Studio IDE 和 *.vsct* 文件的信息。

 以下主题介绍如何添加不同种类的命令、菜单和工具栏。

## <a name="in-this-section"></a>本节内容
- [向 Visual Studio 菜单栏添加菜单](../extensibility/adding-a-menu-to-the-visual-studio-menu-bar.md)说明如何向顶部 Visual Studio 菜单栏添加菜单。

- [将键盘快捷方式绑定到菜单项](../extensibility/binding-keyboard-shortcuts-to-menu-items.md) 说明如何将键盘快捷方式 (如 CTRL + 3) 添加到菜单项。

- [向菜单中添加子](../extensibility/adding-a-submenu-to-a-menu.md) 菜单说明如何将子菜单添加到顶部菜单。

- [向子菜单添加最近使用](../extensibility/adding-a-most-recently-used-list-to-a-submenu.md) 过的列表说明如何添加最近使用的列表。

- [创建可重用的按钮组](../extensibility/creating-reusable-groups-of-buttons.md) 介绍如何对命令项进行分组，以便可以将它们包含在多个菜单上。

- [向菜单命令添加图标](../extensibility/adding-icons-to-menu-commands.md) 介绍如何将图标添加到工具栏和菜单上的命令。

- [更改菜单命令的文本](../extensibility/changing-the-text-of-a-menu-command.md) 描述如何使用 `TextChanges` 标志来使菜单项动态更改。

- [更改命令的外观](../extensibility/changing-the-appearance-of-a-command.md) 描述如何动态地启用或禁用命令。

- [更新用户界面](../extensibility/updating-the-user-interface.md) 描述如何强制用户界面的更新反映最近的更改。

- "[本地化" 菜单命令](../extensibility/localizing-menu-commands.md)说明如何本地化菜单命令。
