---
title: Visual Studio 的辅助功能提示和技巧
description: 了解有关提示和技巧的详细信息，通过这些信息，每位用户（包括残疾人士）都可更加轻松地使用 Visual Studio 集成开发环境 (IDE)。
ms.date: 04/04/2022
ms.topic: conceptual
helpviewer_keywords:
- accessibility [Visual Studio]
ms.assetid: 6b491d88-f79e-4686-8841-857624bdcfda
author: TerryGLee
ms.author: tglee
manager: jmartens
ms.technology: vs-ide-general
ms.workload:
- multiple
ms.openlocfilehash: 1cc98718783482f5756db13ac1647db342433838
ms.sourcegitcommit: d9cab667735450e735622f8b93266f07b8046f3e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2022
ms.locfileid: "141402254"
---
# <a name="accessibility-tips-and-tricks-for-visual-studio"></a>Visual Studio 的辅助功能提示和技巧

Visual Studio 具有内置辅助功能，这些辅助功能与屏幕阅读器以及其他辅助技术兼容。 无论你是要使用键盘快捷方式来导航 IDE，还是要使用高对比度主题来改进可见性，都将在此页上找到相关操作方式的多个提示和技巧。

我们还介绍了如何使用注释显示有关代码的实用信息以及如何设置生成和断点事件的声音提示。

> [!NOTE]
> 本主题适用于 Visual Studio  Windows 版。 对于 Visual Studio for Mac，请参阅 [Visual Studio for Mac 辅助功能](/visualstudio/mac/accessibility)。

## <a name="save-your-ide-settings"></a>保存 IDE 设置

可以通过保存窗口布局、键盘映射方案和其他首选项来自定义 IDE 体验。 有关详细信息，请参阅[个性化设置 Visual Studio IDE](../../ide/personalizing-the-visual-studio-ide.md)。

## <a name="modify-your-ide-for-high-contrast-viewing"></a>修改 IDE 实现高对比度查看

对某些人来说，某些颜色更难看见。 如果在编码时想要更高的对比度，但不想使用典型的“高对比度”主题，我们现在提供了“蓝（额外对比度）”主题。

  ![比较蓝色主题和蓝色额外对比主题](media/blue-extra-contrast-theme.png "显示“蓝色”主题和“蓝色额外对比度”主题的比较的屏幕截图")

::: moniker range="vs-2022"

> [!TIP]
> 请参阅 [**2022 年 Visual Studio 2022 年博客文章中的"我们升级了 UI**](https://devblogs.microsoft.com/visualstudio/weve-upgraded-the-ui-in-visual-studio-2022/)"，详细了解细微的颜色对比度调整和我们添加的新 [Cascadia Code](../how-to-change-fonts-and-colors-in-visual-studio.md#use-the-cascadia-code-font) 字体，使Visual Studio更易于所有人访问。

::: moniker-end

## <a name="use-annotations-to-reveal-useful-information-about-your-code"></a>使用注释显示关于代码的实用信息

Visual Studio 编辑器包括很多文本“修饰”，比如螺丝刀和灯泡图标、错误和警告“波形曲线”、定位标记等，这些修饰有助于了解代码行中特定点的特征和功能。 可以使用“显示行注释”命令集帮助发现并浏览这些修饰。

  ![使用“显示行批注”命令集](media/show-line-annotations-command-set.png "“显示行注释”菜单项的屏幕截图")

## <a name="access-toolbars-by-using-keyboard-shortcuts"></a>使用键盘快捷方式访问工具栏

与许多工具窗口一样，Visual Studio IDE 也具有多个工具栏。 以下键盘快捷方式可帮助你对其进行访问。

|功能|说明|键盘快捷方式|
|-------------|-----------------| - |
|IDE 工具栏|选择“标准”工具栏上的第一个按钮。|Alt、Ctrl+Tab|
|工具窗口工具栏|将焦点移动到工具窗口中的工具栏。 <br> <br> 注意：此方法适用于大多数工具窗口，但仅限焦点位于工具窗口的情况。 此外，还必须在按 Alt 键前按 Shift 键。 在一些工具窗口（如团队资源管理器）中，必须先按住 Shift 键一会才能按 Alt 键。|Shift+Alt |
|工具栏|转到下一工具栏中的第一项（当焦点位于工具栏时）。|Ctrl + Tab|

### <a name="other-useful-keyboard-shortcuts"></a>其他有用的键盘快捷方式

其他一些有用的键盘快捷方式包括以下各项。

|功能|说明|键盘快捷方式|
|-------------|-----------------| - |
|IDE|打开或关闭高对比度。 <br> <br> 注意：标准 Windows 键盘快捷方式|左 Alt+左 Shift+PrtScn  |
|对话框|选中或清除对话框中的复选框选项。 <br> <br> 注意：标准 Windows 键盘快捷方式|**空格键**|
|上下文菜单|打开上下文菜单（右键单击）。 <br> <br> 注意：标准 Windows 键盘快捷方式|Shift + F10|
|菜单|通过使用快捷键快速访问菜单项。 在菜单中按 Alt 键 + 带下划线的字母可激活命令。 例如，若要查看 Visual Studio 中的“打开项目”对话框，则应按 Alt+F+O+P   。  <br><br> 注意：标准 Windows 键盘快捷方式|Alt + [字母] |
|搜索框|使用 Visual Studio 中的搜索功能。|Ctrl+Q|
|工具箱窗口|在工具箱选项卡之间移动。|Ctrl+上箭头 <br /><br /> 以及<br /><br /> Ctrl+下箭头 |
|工具箱窗口|将工具箱中的控件添加到窗体或设计器。|Enter|
|“选项”对话框：“环境”>“键盘”|删除在“按快捷键”选项中输入的组合键。|Backspace|
|“通知”工具窗口|逐个使用两个键盘快捷方式组合来打开“通知”工具窗口。 然后，使用箭头键选择它来查看通知。| Ctrl+&#92;、Ctrl+N   |

有关完整列表，请参阅[Visual Studio中的键盘快捷方式](../default-keyboard-shortcuts-in-visual-studio.md)。

> [!NOTE]
> 显示的对话框和菜单命令可能会与“帮助”中的描述不同，具体取决于你的当前设置或版本。

## <a name="access-notifications-by-using-keyboard-shortcuts"></a>使用键盘快捷方式访问通知

当 IDE 中显示通知时，下面介绍了如何使用键盘快捷方式访问“通知”窗口：

1. 从 IDE 中的任何位置，按顺序逐个按以下两个键盘快捷方式：Ctrl+&#92; 和 Ctrl+N。

   此时将打开“通知”窗口。

   ![Visual Studio IDE 中的“通知”工具窗口](media/toast-notification.png "Visual Studio IDE 中的“通知”工具窗口的屏幕截图")

1. 使用 Tab 键或箭头键选择通知。

## <a name="use-the-sound-dialog-box-to-set-build-and-breakpoint-cues"></a>使用"声音"对话框设置生成和断点提示

可以使用Windows中的"声音"对话框为Visual Studio程序事件分配声音。 具体而言，可以将声音分配给以下程序事件：

* 命中断点
* 生成已取消
* 生成失败
* 生成成功

下面介绍如何向Windows 11或Windows 10中的程序事件添加声音。

### <a name="windows-11"></a>Windows 11

1. 在运行Windows 11的计算机上选择"开始"按钮，然后在 **"搜索**"框中键入 **"更改系统声音**"。

    :::image type="content" source="media/change-system-sounds-windows-11.png" alt-text="Windows 11中的&quot;搜索&quot;框的屏幕截图。":::

1. 从搜索结果中，选择"**更改系统声音**"的控制面板选项。  (或者，选择搜索结果右侧面板中的 **"打开** "图标。) 

    :::image type="content" source="media/select-change-system-sounds-windows-11.png" alt-text="Windows 11中&quot;更改系统声音&quot;搜索结果的屏幕截图。":::

1. 在“声音”对话框中，单击“声音”选项卡。

1. 在“程序事件”中，滚动至“Microsoft Visual Studio”，然后选择想要应用到选中事件的声音。

    :::image type="content" source="media/system-sounds-dialog-windows-11.png" alt-text="Windows 11中&quot;声音&quot;对话框的&quot;声音&quot;选项卡的屏幕截图。":::

1. 单击 **“确定”** 。

### <a name="windows-10"></a>Windows 10

1. 在运行 Windows 10 的计算机上的搜索框中，键入“更改系统声音”。

   ![Windows 10 中的搜索框](media/type-here-to-search.png "Windows 10 中的“搜索”框的屏幕截图")

   （或者，如果已启用 Cortana，可以说“你好，小娜”，然后说“更改系统声音”。）

1. 双击“更改系统声音”。

   ![Windows 10 中的搜索结果](media/change-system-sounds.png "Windows 10 中的“更改系统声音”搜索结果的屏幕截图")

1. 在“声音”对话框中，单击“声音”选项卡。

1. 在“程序事件”中，滚动至“Microsoft Visual Studio”，然后选择想要应用到选中事件的声音。

   ![Windows 10中"声音"对话框的"声音"选项卡](media/sound-applet.png "Windows 10中&quot;声音&quot;对话框的&quot;声音&quot;选项卡")

1. 单击 **“确定”** 。

::: moniker range="vs-2017"

> [!TIP]
> 要详细了解辅助功能更新，请参阅博客文章 [Visual Studio 2017 版本 15.3 中的辅助功能改进](https://devblogs.microsoft.com/visualstudio/accessibility-improvements-in-visual-studio-2017-version-15-3/)。

::: moniker-end

## <a name="see-also"></a>另请参阅

* [设置辅助功能选项](../how-to-change-fonts-and-colors-in-visual-studio.md#set-accessibility-options)
* [自定义Visual Studio中的菜单和工具栏](../../ide/how-to-customize-menus-and-toolbars-in-visual-studio.md)
* [个性化设置 Visual Studio IDE](../../ide/personalizing-the-visual-studio-ide.md)
* [辅助功能 (Visual Studio for Mac)](/visualstudio/mac/accessibility)
* [Microsoft 辅助功能](https://www.microsoft.com/Accessibility)
