---
title: 面向 Windows 用户的 Visual Studio for Mac
description: 面向熟悉在 Windows 操作系统上使用 Visual Studio 的开发人员的 Visual Studio for Mac 简介。
author: heiligerdankgesang
ms.author: dominicn
ms.date: 11/09/2021
ms.assetid: 61CB6883-08CE-470F-8599-6F7570DB756E
ms.openlocfilehash: c6a98e8314bfdb9c838db3dc36afbec004755d2b
ms.sourcegitcommit: 4efdab6a579b31927c42531bb3f7fdd92890e4ac
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/26/2021
ms.locfileid: "130350984"
---
# <a name="visual-studio-for-mac-for-windows-users"></a>面向 Windows 用户的 Visual Studio for Mac

从一个操作系统迁移到另一个操作系统可能会很困难。 从用户界面到菜单项分类，跨平台应用程序中通常存在细微差异。 在这里，你将了解 Visual Studio for Mac 和 Visual Studio for Windows 之间的最常见区别。 你还将了解 macOS 与 Windows 之间的几个不同约定。

## <a name="keyboard-shortcuts"></a>键盘快捷方式

作为开发人员，很多人都习惯使用键盘来执行任务和导航。 键盘上的某些键在 Mac 和 Windows PC 之间是通用的。 你可能会认为，复制和粘贴等键盘操作使用相同的组合键。 但不总是这样。 幸运的是，你可以更改 Visual Studio for Mac 中的键绑定，使其与 Windows 中的 Visual Studio 相匹配。

首次运行时 Visual Studio for Mac 时，会看到“键盘快捷方式选择”窗口：![键绑定窗口](media/ide-tour-2019-keyboard-shortcut.png)

如果以后要更改键绑定，可以在“首选项”中找到相关设置：![键绑定首选项](media/customizing-the-ide-image10a.png)

需要注意的是，macOS 对 Windows 使用了不同的系统范围快捷方式。 更改键绑定首选项后，将允许你在 Visual Studio for Mac 中使用熟悉的 Windows 快捷方式。 但是，在 macOS 的其他区域中，需要熟悉 macOS 快捷方式。

MacOS 命令（⌘）修改键通常可以替换 Windows 中的控件键。 下面是一些示例和其他常用的快捷方式：

|任务                   |Windows 快捷方式         |macOS 快捷方式      |
|-----------------------|-------------------------|--------------------|
|复制                   |`Ctrl + C`               |`⌘ + C`             |
|粘贴                  |`Ctrl + V`               |`⌘ + V`             |
|剪切                    |`Ctrl + X`               |`⌘ + X`             |
|撤消                   |`Ctrl + Z`               |`⌘ + Z`             |
|重做                   |`Ctrl + Shift + Z`       |`⌘ + Shift + Z`     |
|删除光标右侧 |`Delete`                 |`fn + Backspace`    |
|删除字词            |`Ctrl + Delete`          |`fn + ⌥ + Backspace`|

> [!TIP]
> 可以在 [Apple 支持网站](https://support.apple.com/en-us/HT201236)中找到 macOS 快捷方式的完整列表。

## <a name="menus"></a>菜单

MacOS 中菜单的组织方式不同于 Windows 中的菜单。 Visual Studio for Mac 也不例外。 可在此处找到一些最常见的菜单选项：

|任务                   |Visual Studio (Windows)                                              |Visual Studio for Mac                |
|-----------------------|---------------------------------------------------------------------|-------------------------------------|
|首选项（选项）  |工具 > 选项 >...                                                   |Visual Studio > 首选项...       |
|扩展             |扩展 > 管理扩展                                       |Visual Studio > 扩展...        |
|布局                |窗口 > 应用窗口布局 > [选择布局]                       |视图 > 布局 > [选择布局]               |
|更新                |帮助 > 检查更新                                             |Visual Studio > 检查更新... |
|NuGet 程序包管理器  |工具 > NuGet 包管理器 > 管理解决方案的 NuGet 包... |项目 > 管理 NuGet 包...   |
|查找工具             |编辑 > 查找和替换 > [选择工具]                              |搜索 > [选择工具]               |
|关于 Visual Studio    |帮助 > 关于 Microsoft Visual Studio                                 |Visual Studio > 关于 Visual Studio  

> [!NOTE]
> 可在 [IDE 教程](ide-tour.md)中找到 Visual Studio for Mac 中最常见功能的概述
