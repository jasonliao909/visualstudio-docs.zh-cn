---
title: 布局Visual Studio |Microsoft Docs
description: 了解所有Visual Studio的布局，包括未设置名称的对话和具有一个"已设计"外观的新对话。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
ms.assetid: c19e3022-047c-43b6-a046-a82717efed4f
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: e52b7b3fd620080b73e8d3de80672003ecb8fcf7
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2021
ms.locfileid: "112900521"
---
# <a name="layout-for-visual-studio"></a>Visual Studio 的布局
大多数Visual Studio是实用工具对话布局，这是遵循[](../../extensibility/ux-guidelines/layout-for-visual-studio.md#BKMK_UtilityDialogLayout)标准 Windows 桌面对话框布局原则[的未主题对话](/windows/desktop/uxguide/win-dialog-box)。 随着Visual Studio UI 的刷新，一些更突出的对话具有一种新的设计，可将其建立为产品定义体验。 这些 ["以"为"的对话框](../../extensibility/ux-guidelines/layout-for-visual-studio.md#BKMK_ThemedDialogLayout) 布局具有一个以""为"的"外观"。

## <a name="utility-dialog-layout"></a><a name="BKMK_UtilityDialogLayout"></a> 实用工具对话框布局

- 实用工具对话框中的所有控件都应从顶部/左侧开始，然后向下流动。

- 切勿在对话框上居中控件以填充较大区域。

- 将环境字体用于所有对话文本。 编写视觉规范时，请指定环境字体，而不是选择特定的字体和大小。 请参阅 [环境字体](../../extensibility/ux-guidelines/fonts-and-formatting-for-visual-studio.md#BKMK_TheEnvironmentFont)。

- 使用一致的控制间距和放置来支持提高企业质量的目标。

- 对话框可能会从大量控件和/或唯一的控件并置而变得更复杂。 对于这些复杂情况，在控件分组之间留出足够的空间，以便为用户提供要分析的逻辑流。

### <a name="utility-dialog-layout-examples"></a>实用工具对话框布局示例
 所有维度都表示为像素。

 ![控件上方标签的对话框间距](../../extensibility/ux-guidelines/media/0801-a_utilityspacingabove.png "0801-a_UtilitySpacingAbove")

 **图 08.01-a：控件上方有标签的实用工具对话框的间距准则**

 ![控件左侧标签的对话框间距](../../extensibility/ux-guidelines/media/0801-b_utilityspacingleft.png "0801-b_UtilitySpacingLeft")

 **图 08.01-b：控件左侧带标签的实用工具对话框的间距准则**

### <a name="layout-details"></a>布局详细信息

#### <a name="margins"></a>边距

- 所有对话框应围绕所有边缘具有 12 像素的边框。

- 组帧内的边距应距框架边缘 9 像素。

- 选项卡控件内的边距应距选项卡控件边缘 6 像素。

#### <a name="command-buttons"></a>命令按钮

- 命令按钮在对话帧上操作，而不是对内容进行操作。 它们应位于右下角，并且应具有足够的上方变量空间，以将按钮分开设置。

- 如果存在在对话框中运行的水平按钮，则备用命令按钮配置是右上角的垂直堆栈。 请参阅 [下面的"内部"命令](../../extensibility/ux-guidelines/layout-for-visual-studio.md#BKMK_InteriorCommandButtons) 按钮。

- 命令按钮左侧的空间 (对话框的左下角/中间) 被视为对话操作控件的"带区"的一部分。 该空间上唯一应该包含与整体任务或对话框相关的帮助链接。

- 命令按钮应为 75x23 像素。

- 命令按钮应分开 6 像素。

  ![基本按钮对齐方式](../../extensibility/ux-guidelines/media/0801-c_buttonalign.png "0801-c_ButtonAlign")

  **图 08.01-c：基本按钮对齐方式**

#### <a name="labels"></a>标签

- 左对齐所有标签。

- 对于位于控件上方的标签，它们应与控件下方的控件精确左对齐，标签底部应位于另一个控件的顶部上方 5 像素 (例如组合框) 。

- 对于位于控件左侧的标签，标签和输入控件之间的最小宽度为 10 像素。 应建立隐含的第二列来对齐文本框、组合框或其他控件。

- 标签是句子大小写，后跟冒号。 请参阅 [文本样式](../../extensibility/ux-guidelines/fonts-and-formatting-for-visual-studio.md#BKMK_TextStyle)。

#### <a name="distance-between-controls"></a>控件之间的距离
 堆栈控件合理。 堆叠控件之间的间距没有绝对准则。 控件之间的紧密性在对话之间可能略有不同。 对于垂直控件/标签对，建议的间距为 20 像素，水平控件/标签对的建议间距为 9 像素。 水平对的最小控制间距为 6 像素。

 ![控件之间的建议距离](../../extensibility/ux-guidelines/media/0801-d_controldistance.png "0801-d_ControlDistance")

 **图 08.01-d：控件之间的距离建议**

#### <a name="control-indentation"></a>控件缩进
 嵌套控件时，将内部控件与上述控件的左边缘（通常是标签）水平对齐。

 ![嵌套控件对齐方式](../../extensibility/ux-guidelines/media/0801-e_controlalign.png "0801-e_ControlAlign")

 **图 08.01-e：嵌套控件对齐方式**

#### <a name="control-width"></a>控件宽度
 文本框或其他类似控件的宽度不应超过字段的平均输入。 平均英语单词为五个字符。 例如，需要长路径名称的文本框应长于水平布局允许的长度，而平台名称的下拉列表应仅包含允许最长条目的长度。

#### <a name="helper-text"></a>帮助程序文本

- 对话框可以显示帮助程序文本，该文本提供有关对话用途的详细信息。 这通常位于顶部，可以是 1-2 个句子。

- 行长度应为用户分析和读取的舒适宽度。 中型对话应不超过 550 像素宽。

#### <a name="interior-command-buttons"></a><a name="BKMK_InteriorCommandButtons"></a> 内部命令按钮
 在更复杂的对话框中，内部控件可能有其自己的相关按钮，这可能会影响对话框的提交按钮所在的位置。

- 当"确定取消 (右下角) 时，使用垂直对齐方式) 内 / 侧按钮的列对齐方式。

- 当"确定取消 (右上角垂直方向时，) 内侧按钮的水平对齐 / 方式。 这种情况不太常见。

- 内部按钮大小应面向标准按钮大小 75x23 像素，尽可能匹配"确定取消 / "按钮的大小。 如果按钮标签使按钮超过标准按钮大小，则该集内的其他按钮应符合该较宽的大小。

  ![水平“确定”和“取消”按钮](../../extensibility/ux-guidelines/media/0801-f_horizokcan.png "0801-f_HorizOKCan")

  **图 08.01-f：水平"确定/取消"的垂直内部按钮**

  ![垂直“确定”和“取消”按钮](../../extensibility/ux-guidelines/media/0801-g_vertokcan.png "0801-g_VertOKCan")

  **图 08.01-g：具有垂直"确定/取消"的水平内部按钮**

#### <a name="browse-button"></a>[浏览...]按钮
 **[浏览...]** 文本框后跟的按钮应拼写出"浏览..."完整，包括省略号。 如果空间很紧或屏幕上有多个 **[Browse...]** 按钮，该按钮可以缩减为省略号。

## <a name="themed-dialog-layout"></a><a name="BKMK_ThemedDialogLayout"></a> "以"为"的对话框布局
 对话框中的"Visual Studio对话框的外观更浅，并提供更多空白。 版式提供了更多重点和兴趣，提供了更多的开放行距以及字号和粗细的变体。 在可能的情况下，已减少或删除了 chrome 和标题栏。 这些对话框的布局应遵循以下基本模式：

1. 对话框的背景为白色。

2. 中间值灰色有一个 1 像素的规则边框。

3. 对话标题不再位于标题栏中，而是在较大的点大小中提供视觉兴趣和重点。  (请参阅文本样式 .) [中的字](../../extensibility/ux-guidelines/fonts-and-formatting-for-visual-studio.md#BKMK_TextStyle)号部分

4. 与附加文本（如说明）耦合的标签应为 **"环境字体 + 粗体"。**

5. 内部列由浅灰色的 1 像素规则分隔。

6. 默认链接没有下划线。 悬停和按下状态具有颜色更改和下划线。

7. 提交按钮 **("确定** 取消) / 位于右下角。

### <a name="themed-dialog-layout-examples"></a>"以对话为示例"的对话框布局示例
 ![主题对话框布局](../../extensibility/ux-guidelines/media/0801-h_themeddialog.png "0801-h_ThemedDialog")

 **图 08.01-h："已用"对话框**

 ![主题对话框尺寸](../../extensibility/ux-guidelines/media/0801-i_themeddialogdimensions.png "0801-i_ThemedDialogDimensions")

 **图 08.01-i："已用"对话框 - 维度**

 ![主题对话框字体](../../extensibility/ux-guidelines/media/0801-j_themeddialogfonts.png "0801-j_ThemedDialogFonts")

 **图 08.01-j：主题对话框 - 字体**

 ![主题对话框颜色](../../extensibility/ux-guidelines/media/0801-k_themeddialogcolors.png "0801-k_ThemedDialogColors")

 **图 08.01-k：主题对话框 - 颜色**

## <a name="see-also"></a>另请参阅
- [Visual Studio 的应用程序模式](../../extensibility/ux-guidelines/application-patterns-for-visual-studio.md)
- [Windows (控件) ](/windows/desktop/uxguide/controls)
- [Windows (对话框) ](/windows/desktop/uxguide/win-dialog-box)
