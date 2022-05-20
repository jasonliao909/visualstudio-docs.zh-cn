---
title: Visual Studio for Mac - 集成终端
description: 使用 Visual Studio for Mac 中的集成终端。
author: jmatthiesen
ms.author: jomatthi
manager: dominicn
ms.date: 05/16/2022
ms.topic: how-to
ms.assetid: EFD53CE9-8174-4FE4-8863-2984D22FD921
ms.openlocfilehash: 69594a4037a5b773b64301afeef4b227af3eb309
ms.sourcegitcommit: 4264e57e45dede8bf55ddf0f7e81738a42580081
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/20/2022
ms.locfileid: "145183458"
---
# <a name="integrated-terminal"></a>集成终端

 [!INCLUDE [Visual Studio for Mac](~/includes/applies-to-version/vs-mac-only.md)]

> [!NOTE] 
> 集成终端目前在简体中文或繁体中文区域设置中不可用。 我们修复了与中文字符输入相关的 bug，此功能即将推出。 

可以在Visual Studio for Mac中打开集成终端窗口，从解决方案的根目录开始。 终端适用于不同类型的情况，包括运行前端任务（例如：npm、ng 或 vue）、管理容器、运行高级 git 命令、执行实体框架命令、查看 dotnet CLI 输出、添加 NuGet 包等。 

打开 **终端**：
- 使用带有反杆字符的 **Ctrl + 键盘** 快捷方式显示或隐藏终端窗口。
- 使用 **ViewTerminal**  >  菜单命令。
- 使用 **搜索** 栏中的 **终端** 命令。

::: moniker range="vsmac-2019"

![Visual Studio for Mac 集成终端在启动后立即运行。](media/integrated-terminal-intro.png)

::: moniker-end

::: moniker range="vsmac-2022"

:::image type="content" source="media/vsmac-2022/integrated-terminal-intro.png" alt-text="显示启动后立即Visual Studio for Mac集成终端的屏幕截图。":::

::: moniker-end

默认情况下，当终端启动时，它将：
- 将工作目录设置为当前解决方案的路径。
- 加载默认的系统 shell。

## <a name="search"></a>搜索
可以使用 **“搜索”>“查找...”** 菜单搜索终端窗口的内容。

![Visual Studio for Mac 集成终端中的搜索体验](media/integrated-terminal-search.png)

## <a name="terminal-keyboard-shortcuts"></a>终端键盘快捷方式
|命令|键盘快捷键|
|-|-|
|显示/隐藏终端窗口|**Ctrl+`**|
|创建新的终端实例|**Ctrl+'**|
|向上滚动页面|PgUp|
|向下滚动页面|PgDn|
|浏览之前使用的命令|**↑**、**↓**|
|增大字号|**⌘+**|
|减小字号|**⌘-**|

## <a name="multiple-instances"></a>多个实例
终端的多个实例随时可能正在运行。 你可以使用 Ctrl+' 键盘快捷方式创建新的实例。 可以切换实例，操作方法是：单击每个实例的选项卡，或者使用 Ctrl+tab 快捷方式打开窗口选取器对话框。

![Visual Studio for Mac 中的多个终端实例](media/integrated-terminal-multiple-instances.png) 

## <a name="customizing-the-terminal-window"></a>自定义终端窗口

### <a name="configuring-the-terminal-font"></a>配置终端字体

可以从 **“首选项**”中更改用于 **终端窗口内容的** 字体 **系列**、**字号** 和 **大小**... > **环境** > **字体**。 默认情况下，字体将与使用 Menlo Regular 11 的 **输出窗口内容** 相同。 你可以将其设置为任何字体，独立于 **文本编辑器** 字体。

::: moniker range="vsmac-2019"

![自定义集成终端的字体设置](media/integrated-terminal-change-font.png)

::: moniker-end

::: moniker range="vsmac-2022"

:::image type="content" source="media/vsmac-2022/integrated-terminal-customize-font.png" alt-text="显示自定义集成终端的字体设置的屏幕截图。":::

::: moniker-end

### <a name="reusing-system-terminal-customizations"></a>重复使用系统终端自定义项

集成终端使用与 macOS 系统终端相同的默认值和配置。 这意味着，你的终端自定义项（zsh、oh-my-zsh 等）也可在集成终端使用。
