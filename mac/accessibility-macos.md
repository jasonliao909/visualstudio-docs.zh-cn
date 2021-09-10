---
title: 使用 macOS 辅助选项
description: 使用 macOS 辅助选项和功能，如高对比度、键盘导航和 VoiceOver
author: heiligerdankgesang
ms.author: dominicn
ms.date: 09/23/2019
ms.assetid: 598FC25A-6DA3-44BB-B128-AD979E9F86EA
ms.topic: how-to
ms.openlocfilehash: 6796ab12716d1d2f3ec2570c32b410c8360b8a81
ms.sourcegitcommit: 0841d3f610bd2af4af1cf07dd9d31d1e0629b193
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/09/2021
ms.locfileid: "123963851"
---
# <a name="accessibility-features-of-macos"></a>macOS 辅助功能

macOS 是一种可访问的操作系统，具有许多功能，可帮助用户获取各种功能。 这些功能包括高对比度模式、键盘导航和 VoiceOver（macOS 屏幕读取器）。

## <a name="enable-accessibility-features"></a>管理辅助功能

默认情况下，Visual Studio for Mac 对辅助技术的支持处于禁用状态。 启用辅助功能支持：

1. 依次转到Visual Studio(菜单)”   > “首选项”   > “其他”  ，然后选择“辅助功能”  。

1. 选择“启用辅助功能”  复选框。

   ![辅助功能首选项的屏幕截图，其中选择了“启用辅助功能”](media/accessibility-preferences.png)

1. 选择“重启 Visual Studio”  ，以启用对 Apple 辅助技术的支持。

也可以使用命令行启用辅助功能。 为此，请在终端中输入以下命令：

```bash
defaults write com.microsoft.visual-studio com.monodevelop.AccessibilityEnabled 1
```

通过命令行更改此设置后，需要重启 Visual Studio。

## <a name="increase-the-contrast-in-macos"></a>提高 macOS 中的对比度

Visual Studio for Mac 支持 macOS 中提高的对比度，可提高 UI 元素的对比度并使轮廓更明确。 启用此项：

1. 打开“系统首选项”。

1. 转到“辅助功能”，然后选择“显示”。

1. 选择“增加对比度”复选框。
