---
title: 公共控件的常见Visual Studio |Microsoft Docs
description: 了解常见Visual Studio如何遵循桌面Windows指南，以及增强这些指南的特殊情况。
ms.custom: SEO-VS-2020
ms.date: 04/26/2017
ms.topic: reference
ms.assetid: 3e893949-6398-42f1-9eab-a8d8c2b7f02d
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: 6c5e57859aa1efc561e4462d741e33589b4cc853ed7828d8a0cfc00eb3b36e56
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121337001"
---
# <a name="common-control-patterns-for-visual-studio"></a>Visual Studio 的公共控件模式
## <a name="common-controls"></a><a name="BKMK_CommonControls"></a> 常见控件

### <a name="overview"></a>概述
常见控件是应用程序的大部分用户界面Visual Studio。 在桌面界面中使用的Visual Studio控件应遵循桌面Windows[指南](/windows/desktop/uxguide/controls)。 本主题特定于特定Visual Studio，涵盖可增强这些操作指南的Windows或详细信息。

#### <a name="common-controls-in-this-topic"></a>本主题中的常见控件

- [滚动条](../../extensibility/ux-guidelines/common-control-patterns-for-visual-studio.md#BKMK_Scrollbars)

- [输入字段](../../extensibility/ux-guidelines/common-control-patterns-for-visual-studio.md#BKMK_InputFields)

- [组合框和下拉列表](../../extensibility/ux-guidelines/common-control-patterns-for-visual-studio.md#BKMK_ComboBoxesAndDropDowns)

- [复选框](../../extensibility/ux-guidelines/common-control-patterns-for-visual-studio.md#BKMK_CheckBoxes)

- [单选按钮](../../extensibility/ux-guidelines/common-control-patterns-for-visual-studio.md#BKMK_RadioButtons)

- [组帧](../../extensibility/ux-guidelines/common-control-patterns-for-visual-studio.md#BKMK_GroupFrames)

- [文本控件](../../extensibility/ux-guidelines/common-control-patterns-for-visual-studio.md#BKMK_TextControls)

- [按钮和超链接](../../extensibility/ux-guidelines/common-control-patterns-for-visual-studio.md#BKMK_ButtonsAndHyperlinks)

- [树视图](../../extensibility/ux-guidelines/common-control-patterns-for-visual-studio.md#BKMK_TreeViews)

#### <a name="visual-style"></a>视觉样式
设置控件样式时要考虑的第一件事是控件是否将在带样式的 UI 中使用。 标准 UI 中的控件是非主题 UI，并且必须遵循Windows桌面样式[，](/windows/desktop/uxguide/controls)这意味着它们不会重新模板化，应出现在其默认控件外观中。

- **标准 (实用工具) 对话框：非** "带"。 不要重新模板。 使用基本控件样式默认值。

- **工具窗口、文档编辑器、设计图面和主图对话框：** 使用颜色服务使用专用化的彩色外观。

### <a name="scroll-bars"></a><a name="BKMK_Scrollbars"></a> 滚动条
 滚动条应遵循[滚动条的常见](/windows/desktop/Controls/about-scroll-bars)Windows模式，除非它们增加了内容信息，如在代码编辑器中一样。

### <a name="input-fields"></a><a name="BKMK_InputFields"></a> 输入字段
 对于典型的交互行为，请Windows[文本框 的桌面指南](/windows/desktop/uxguide/ctrl-text-boxes)。

#### <a name="visual-style"></a>视觉样式

- 不应在实用工具对话框中设置输入字段的样式。 使用控件内部的基本样式。

- 只应在"带"的对话框和工具窗口中使用"带"的输入字段。

#### <a name="specialized-interactions"></a>专用交互

- 只读字段将在后台禁用 (灰色) ，但默认 (处于) 状态。

- 必填字段应 **\<Required>** 包含作为水印。 除非在极少数情况下，否则不应更改背景的颜色。

- 错误验证：请参阅[通知和进度Visual Studio](../../extensibility/ux-guidelines/notifications-and-progress-for-visual-studio.md)

- 输入字段的大小应调整为适合内容，不能适应显示输入字段的窗口宽度，也不能任意匹配长字段的长度（如路径）。 长度可能指示用户对字段中允许的字符数存在限制。

     ![输入字段长度不正确：名称不太可能长。](../../extensibility/ux-guidelines/media/0707-01_incorrectinputfieldcontrol.png "0707-01_IncorrectInputFieldControl")<br />输入字段长度不正确：名称不太可能长。

     ![正确的输入字段长度：输入字段是预期内容的合理宽度。](../../extensibility/ux-guidelines/media/0707-02_correctinputfieldcontrol.png "0707-02_CorrectInputFieldControl")<br />正确的输入字段长度：输入字段是预期内容的合理宽度。

### <a name="combo-boxes-and-drop-down-lists"></a><a name="BKMK_ComboBoxesAndDropDowns"></a> 组合框和下拉列表
对于典型的交互行为，请Windows[下拉列表和组合](/windows/desktop/uxguide/ctrl-drop)框 的桌面指南。

#### <a name="visual-style"></a>视觉样式

- 在实用工具对话框中，不要重新设置控件的模板。 使用控件内部的基本样式。

- 在带标记的 UI 中，组合框和下拉列表遵循控件的标准标记。

#### <a name="layout"></a>Layout
组合框和下拉列表的大小应调整为适合内容，不能适应显示它们的窗口宽度，也不能任意匹配长字段的长度（如路径）。

![不正确：下拉宽度对于要显示的内容来说太长。](../../extensibility/ux-guidelines/media/0707-03_incorrectdropdownlayout.png "0707-03_IncorrectDropDownLayout")<br />不正确：下拉宽度对于要显示的内容来说太长。

![正确：下拉列表的大小调整为允许翻译增长，但不一定长。](../../extensibility/ux-guidelines/media/0707-04_correctdropdownlayout.png "0707-04_CorrectDropDownLayout")<br />正确：下拉列表的大小调整为允许翻译增长，但不一定长。

### <a name="check-boxes"></a><a name="BKMK_CheckBoxes"></a> 复选框
对于典型的交互行为，请Windows[复选框 的桌面指南](/windows/desktop/uxguide/ctrl-check-boxes)。

#### <a name="visual-style"></a>视觉样式

- 在实用工具对话框中，不要重新设置控件的模板。 使用控件内部的基本样式。

- 在带标记的 UI 中，复选框遵循控件的标准标记。

#### <a name="specialized-interactions"></a>专用交互

- 与复选框交互不得弹出对话框或导航到另一区域。

- 将复选框与第一行文本的基线对齐。

     ![不正确：复选框以文本为中心。](../../extensibility/ux-guidelines/media/0707-05_incorrectcheckboxalign.png "0707-05_IncorrectCheckBoxAlign")<br />不正确：复选框以文本为中心。

     ![正确：复选框与文本的第一行对齐。](../../extensibility/ux-guidelines/media/0707-06_correctcheckboxalign.png "0707-06_CorrectCheckBoxAlign")<br />正确：复选框与文本的第一行对齐。

### <a name="radio-buttons"></a><a name="BKMK_RadioButtons"></a> 单选按钮
对于典型的交互行为，请Windows[单选按钮 的桌面指南](/windows/desktop/uxguide/ctrl-radio-buttons)。

#### <a name="visual-style"></a>视觉样式
在实用工具对话框中，不要设置单选按钮的样式。 使用控件内部的基本样式。

#### <a name="specialized-interactions"></a>专用交互
无需使用分组框来封闭单选按钮选项，除非需要在严格的布局中保持组区别。

### <a name="group-frames"></a><a name="BKMK_GroupFrames"></a> 组帧
对于典型的交互行为，请遵循[Windows框架 的桌面指南](/windows/desktop/uxguide/ctrl-group-boxes)。

#### <a name="visual-style"></a>视觉样式
在实用工具对话框中，请勿设置组帧的样式。 使用控件内部的基本样式。

#### <a name="layout"></a>Layout

- 无需使用分组框来封闭单选按钮选项，除非需要在严格的布局中保持组区别。

- 切勿将组帧用于单个控件。

- 有时，可以使用水平规则而不是组帧容器。

## <a name="text-controls"></a><a name="BKMK_TextControls"></a> 文本控件

### <a name="static-text-fields"></a>静态文本字段

静态文本字段显示只读信息，用户无法选择该字段。 避免将其用于用户可能想要复制到剪贴板的任何文本。 但是，只读静态文本可能会更改以反映状态更改。 在下面的示例中，"信息"组下的"输出名称"静态文本将发生更改，以反映对上方的"根命名空间"文本框进行的任何更改。

有两种方法可以显示静态文本信息。

如果没有分组冲突，静态文本可以在对话框中自行显示，而不会包含任何内容。 确定框的额外行是否确实是必需的。 例如，在组行创建的节下显示目录路径，如下所示：

![文本控件中的静态文本信息](../../extensibility/ux-guidelines/media/DisplayingStaticText.png "DisplayingStaticText.png")<br />文本控件中的静态文本信息

在存在其他分组区域并包含信息的对话框中，当可以隐藏或显示 (（如 **属性窗口** 说明窗格) 或想要与类似 UI 一致）时，将静态文本放在框中。 此分组框应为单个规则，并且使用 进行着色 `ButtonShadow` ：

![静态文本属性窗口](../../extensibility/ux-guidelines/media/PropertiesWindow.png "PropertiesWindow.png")<br />静态文本属性窗口

### <a name="read-only-text-box"></a>只读文本框

这允许用户选择字段中的文本，但不能对其进行编辑。 这些文本框由常用的三维边框边框，并填充 `ButtonShadow` 。

当用户更改关联的控件时 (文本框) ，例如选中/取消选中复选框或选择/取消选择单选按钮时，文本框可能会变为活动状态。 例如，在如下所示的"**工具 &gt; 选项**"页中，取消选中"使用默认值"复选框时，"主页"文本框将变为活动状态。

![只读文本框，显示非活动状态和活动状态](../../extensibility/ux-guidelines/media/ReadOnlyTextBox.png "ReadOnlyTextBox.png")<br />只读文本框，显示非活动状态和活动状态

### <a name="using-text-in-dialogs"></a>在对话框中使用文本

对话框中文本的关键准则：

- 无名称对话框中文本框、列表框和框架的标签以谓词开头，仅第一个词具有初始大写，以冒号结尾。

    > 主题对话框中的文本控件遵循Windows [UX](/windows/desktop/uxguide/top-violations)指南，不采用结束标点，"帮助"链接中的问号除外。

- 复选框和选项按钮的标签以谓词开始，仅第一个单词的初始大写，没有结束标点。

- 按钮、菜单、菜单项和选项卡的标签在每个单词上都有初始大写 (标题) 。

- 标签术语应与其他对话框中的类似标签一致。

- 如果可能，请让编写器/编辑器编写或批准文本，然后再将文本转到开发人员进行实现。

- 所有控件都应具有标签，除非在特殊情况下使用 Tab 键已足够。
在适当的时候使用帮助程序文本。

### <a name="helper-text"></a>帮助程序文本

包含在对话框中，以帮助用户了解对话的用途或指示要采取哪些操作。 帮助程序文本应仅在需要时使用，以避免混乱的简单对话。 帮助程序文本的两种变体是对话框和水印。

遵循帮助程序文本的常见位置，并有选择地引入新区域。 帮助程序文本的常见方案包括：

- 对话框中的帮助器文本，用于提供与复杂对话交互的其他方向。

- 空工具窗口或对话框中的水印文本，用于说明为何没有内容可见。

- 描述窗格，如底部 **属性窗口。**

- 空编辑器中的水印文本，用于说明用户应执行哪些操作才能开始使用。

### <a name="dialog-helper-text"></a>对话框帮助程序文本

用户体验设计器可帮助确定何时适合帮助程序文本。 设计器可以定义帮助程序文本的显示位置及其常规内容。 用户帮助可以编写/编辑实际文本。

### <a name="watermarks"></a>水印

对话受益于略有不同水印准则。 由于对话框可能有很多 UI 元素 (标签、提示文本、按钮和其他带有文本) 的容器控件，尤其是当这些控件以黑色显示时，水印在深灰色 (VSColor：) 中更突出。 `ButtonShadow` 通常，水印显示在控件中，如 VSColor 上背景为白色 (的列表框 `Window`) 。

- 文本以深灰色显示， (VSColor： `ButtonShadow`) 。 但是，如果水印显示在中等灰色或其他彩色的 (VSColor：) 背景上，并且担心其可读性，则使用黑色文本 (`ButtonFace` VSColor： `WindowText`) 。

- 水印可以居中或向左刷新。 在做出对齐决策时应用标准设计规则。 无法在后台选择水印。

![水印文本示例](../../extensibility/ux-guidelines/media/WatermarkTextExample.gif)<br />水印文本示例

### <a name="context-specific-dynamic-text"></a>特定于上下文 (动态) 文本

动态文本可用于对话框或无模式 UI 中的两种方式之一：作为动态标签或动态内容。

- 动态标签：动态文本的常见用途是在描述性面板中为所选项提供详细信息，例如，在包含右侧网格中显示的元素和属性列表的对话框中。 属性网格的标签可能是动态的，因此在左侧选择某个项时，右侧网格会显示该特定项的信息。

- 动态文本：在需要以此方式显示特定信息而不是常规信息的实例中非常有用，但应注意不要过度使用。

如果希望用户能够复制信息，动态文本应包含只读文本字段。

## <a name="buttons-and-hyperlinks"></a><a name="BKMK_ButtonsAndHyperlinks"></a> 按钮和超链接

### <a name="overview"></a>概述
按钮和链接控件 (超链接) 应该遵循有关Windows、文字、大小调整和[](/windows/desktop/uxguide/ctrl-links)间距的超链接的基本桌面指南。

### <a name="choosing-between-buttons-and-links"></a>在按钮和链接之间选择
传统上，按钮用于操作，超链接保留用于导航。 可以在所有情况下使用按钮，但链接的角色已在 Visual Studio以便按钮和链接在某些情况下更可互换。

何时使用命令按钮：

- 主命令

- 显示用于收集输入或做出选择的窗口，即使它们是辅助命令

- 破坏性操作或不可逆操作

- 向导和页面流中的承诺按钮

如果标签需要两个以上单词，请避免使用工具窗口中的命令按钮。 链接可以具有较长的标签。

 何时使用链接：

- 导航到其他窗口、文档或网页

- 需要较长的标签或短句来描述操作意图的情况

- 如果操作不是破坏性的或不可逆的，按钮会给 UI 造成压力的紧凑空间

- 在有许多命令的情况下，取消强调辅助命令

#### <a name="examples"></a>示例
![状态消息后在 InfoBar 中使用的命令链接](../../extensibility/ux-guidelines/media/070703-01_commandlinkinfobar.png "070703-01_CommandLinkInfobar")<br />状态消息后在 InfoBar 中使用的命令链接

![CodeLens 弹出中使用的链接](../../extensibility/ux-guidelines/media/070703-02_linksincodelens.png "070703-02_LinksInCodeLens")<br />CodeLens 弹出中使用的链接

![用于辅助命令的链接，其中按钮会吸引过多的注意](../../extensibility/ux-guidelines/media/070703-03_linksassecondarycommands.png "070703-03_LinksAsSecondaryCommands")<br />用于辅助命令的链接，其中按钮会吸引过多的注意

### <a name="common-buttons"></a>常用按钮

#### <a name="text"></a>文本
遵循 UI 文本 [和术语 中的编写准则](../../extensibility/ux-guidelines/ui-text-and-help-for-visual-studio.md#BKMK_UITextAndTerminology)。

#### <a name="visual-style"></a>视觉样式

##### <a name="standard-unthemed"></a>标准 (无) 
大多数按钮Visual Studio显示在实用工具对话框中，不应进行样式设置。 它们应反映操作系统所指示的按钮的标准外观。

##### <a name="themed"></a>主题
在某些情况下，按钮可以在样式 UI 内使用，必须适当地设置这些按钮的样式。 有关 [有针对](../../extensibility/ux-guidelines/application-patterns-for-visual-studio.md#BKMK_Dialogs) 的控件的信息，请参阅对话框。

### <a name="special-buttons"></a>特殊按钮

#### <a name="browse-buttons"></a>浏览。。。按钮
**[浏览...]** 按钮用于网格、对话框、工具窗口和其他无模式 UI 元素。 它们显示一个选取器，可帮助用户将值填充到 控件中。 此按钮有两种变体：长按钮和短按钮。

![长 [浏览...] 按钮](../../extensibility/ux-guidelines/media/070703-04_browselong.gif "070703-04_BrowseLong")<br />长 [浏览...] 按钮

![省略号 -"仅短 ""[...] "按钮](../../extensibility/ux-guidelines/media/070703-05_browseshort.gif "070703-05_BrowseShort")<br />省略号 -"仅短 ""[...] "按钮

何时使用仅省略号短按钮：

- 如果对话框中存在多个长 **[浏览...]** 按钮，如多个字段允许浏览时。 使用每个的 **short [...]** 按钮，以避免这种情况创建的混淆访问密钥 (&**浏览** 和 **B**&行在同一对话框中) 。

- 在紧凑对话中，或者当没有合理位置放置长按钮时。

- 如果按钮将显示在网格控件中。

使用按钮的准则：

- 请勿使用访问密钥。 若要使用键盘进行访问，用户必须从相邻的控件中进行 tab 键。 确保 tab 键顺序为 "任何浏览" 按钮紧接在它将填充的字段之后。 在第一个句点下面不要使用下划线。

- 将 "Microsoft Active Accessibility (MSAA) **名称** " 属性设置为 " **浏览 ...** (包括省略号) ，以便屏幕阅读器将其读取为" 浏览 "而不是" 句点-句点 "或" 句点-句点 "。 对于托管控件，这意味着设置 **AccessibleName** 属性。

- 请勿将省略号 **[...]** 按钮用于除浏览操作之外的任何内容。 例如，如果需要 **[New ...]** 按钮，但没有足够的空间用于文本，则需要重新设计对话框。

##### <a name="sizing-and-spacing"></a>大小调整和间距
![调整大小 [浏览 ...] 按钮：标准版本为75x23 像素，短版本为26x23 像素](../../extensibility/ux-guidelines/media/070703-06_browsesizing.png "070703-06_BrowseSizing")<br />调整[浏览...]按钮大小

![间距 [浏览 ...] 按钮：相关控件和标准浏览按钮之间的间距7像素，相关控件和简短浏览按钮之间的间距5像素](../../extensibility/ux-guidelines/media/070703-07_browsespacing.png "070703-07_BrowseSpacing")<br />设置[浏览...]按钮间距

#### <a name="graphical-buttons"></a>图形按钮
某些按钮应始终使用图形图像而不包含文本来节省空间，避免本地化问题。 它们通常用于字段选取器和其他可排序列表。

> [!NOTE]
> 用户必须按 tab 键进入这些按钮 (没有) 的访问密钥，因此应将其设置为明智的顺序。 将 `name` 按钮的属性映射到它所采取的操作，以便屏幕阅读器正确解释按钮操作。

| 函数 | Button |
| --- | --- |
| 添加 | ![图形“添加”按钮](../../extensibility/ux-guidelines/media/070703-08_buttonadd.png "070703-08_ButtonAdd") |
| 删除 | ![图形“删除”按钮](../../extensibility/ux-guidelines/media/070703-09_buttonremove.png "070703-09_ButtonRemove") |
| 全部添加 | ![图形“全部添加”按钮](../../extensibility/ux-guidelines/media/070703-10_buttonaddall.png "070703-10_ButtonAddAll") |
| 全部删除 | ![图形“全部删除”按钮](../../extensibility/ux-guidelines/media/070703-11_buttonremoveall.png "070703-11_ButtonRemoveAll") |
| “上移” | ![图形“上移”按钮](../../extensibility/ux-guidelines/media/070703-12_buttonmoveup.png "070703-12_ButtonMoveUp") |
| “下移” | ![图形“下移”按钮](../../extensibility/ux-guidelines/media/070703-13_buttonmovedown.png "070703-13_ButtonMoveDown") |
| 删除 | ![图形“删除”按钮](../../extensibility/ux-guidelines/media/070703-14_buttondelete.png "070703-14_ButtonDelete") |

##### <a name="sizing-and-spacing"></a>大小调整和间距
调整图形按钮的大小与 " **浏览 ...** " 按钮的简短版本相同 (26x23 像素) ：

![按钮上图形图像的外观，显示和不显示透明颜色](../../extensibility/ux-guidelines/media/070703-15_graphicalbuttonspacing.png "070703-15_GraphicalButtonSpacing")<br />按钮上图形图像的外观，显示和不显示透明颜色

### <a name="hyperlinks"></a>超链接
超链接非常适合用于基于导航的操作，如打开帮助主题、模式对话框或向导。 如果某个命令使用超链接，则它应始终显示对 UI 的可见且明显的更改。 通常，使用按钮可以更好地使用提交到操作 (如保存、取消和删除) 的操作。

#### <a name="writing-style"></a>写入样式
按照[Windows 桌面指南来获取用户界面文本](/windows/desktop/uxguide/text-ui)。 不要使用 "了解详细信息"、"告诉我详细信息" 或 "通过此短语获取帮助"。 短语会根据帮助内容所回答的主要问题来帮助链接文本。 例如，"**如何实现将服务器添加到服务器资源管理器？**"

#### <a name="visual-style"></a>视觉样式

- 超链接应始终使用 [VSColor 服务](../../extensibility/ux-guidelines/colors-and-styling-for-visual-studio.md#BKMK_TheVSColorService)。 如果超链接的样式不正确，则它会在活动时闪烁红色，或在访问后显示不同的颜色。

- 不要在控件的 "静止" 状态下包含下划线，除非该链接是整个句子中的句子片段（如水印）。

- 悬停时不应出现下划线。 相反，向用户发送的链接处于活动状态时，会有轻微的颜色更改和相应的链接光标。

## <a name="tree-views"></a><a name="BKMK_TreeViews"></a> 树视图

树视图提供了一种将复杂列表组织到父-子组中的方法。 用户可以展开或折叠父组以显示或隐藏基础项。 可以选择树视图中的每个项以提供进一步的操作。

### <a name="tree-view-visual-style"></a><a name="BKMK_TreeViewVisualStyle"></a> 树视图视觉样式

#### <a name="expanders"></a>扩展器
树视图控件应符合 Windows 和 Visual Studio 使用的扩展器设计。 每个节点都使用扩展器控件来显示或隐藏基础项。 使用扩展器控件为可能在 Windows 和 Visual Studio 中遇到不同树视图的用户提供一致性。

![正确：使用扩展器控件正确的树视图节点样式](../../extensibility/ux-guidelines/media/070705-1_treeviewcorrect.png "070705-1_TreeViewCorrect")<br />正确：使用扩展器控件正确的树视图节点样式

![错误：树视图节点的样式不正确](../../extensibility/ux-guidelines/media/070705-2_treeviewincorrect1.png "070705-2_TreeViewIncorrect1")<br />错误：树视图节点的样式不正确

#### <a name="selection"></a>选择
如果在树视图中选择了节点，则突出显示应扩展到树视图控件的整个宽度。 这有助于用户清楚地识别他们所选的项。 选择颜色应反映当前 Visual Studio 主题。

![正确：所选节点的突出显示适合整个树视图控件的宽度。](../../extensibility/ux-guidelines/media/070705-1_treeviewcorrect.png "070705-1_TreeViewCorrect")<br />正确：所选节点的突出显示适合整个树视图控件的宽度。

![错误：所选节点的突出显示不符合树视图控件的整个宽度。](../../extensibility/ux-guidelines/media/070705-3_treeviewincorrect2.png "070705-3_TreeViewIncorrect2")<br />错误：所选节点的突出显示不符合树视图控件的整个宽度。

#### <a name="icons"></a>图标
如果在树视图控件中有助于直观地标识项之间的差异，则应仅在树视图控件中使用图标。 通常，仅应在其图标携带信息以区分元素类型的异类列表中使用图标。 使用图标的同类列表中经常会出现干扰，应避免这样做。 在这种情况下，组图标 (父) 可以传达其中的项的类型。 此规则的例外情况是：图标是动态的，并用于指示状态。

#### <a name="scroll-bars"></a>滚动栏
如果内容适合树视图控件，则应始终隐藏滚动条。 滚动条处于隐藏状态，或在可滚动窗口中处于半透明状态，并且在包含树视图的窗口具有焦点或悬停于树视图本身时出现。

![将显示垂直滚动条和水平滚动条，因为内容超出了树视图控件的限制。](../../extensibility/ux-guidelines/media/070705-4_scrollbars.png "070705-4_Scrollbars")<br />将显示垂直滚动条和水平滚动条，因为内容超出了树视图控件的限制。

### <a name="tree-view-interactions"></a><a name="BKMK_TreeViewInteractions"></a> 树视图交互

#### <a name="context-menus"></a>上下文菜单
树视图节点可以显示上下文菜单中的子菜单选项。 通常，当用户右键单击某项或按选定的项在 Windows 键盘上按下菜单键时，会发生这种情况。 此节点必须获得焦点并处于选中状态，这一点很重要。 这可以帮助用户标识子菜单所属的项。

![生成上下文菜单的项获得焦点，以通知用户已选择了哪个项。](../../extensibility/ux-guidelines/media/070705-5_contextmenu.png "070705-5_ContextMenu")<br />生成上下文菜单的项获得焦点，以通知用户已选择了哪个项。

#### <a name="keyboard"></a>Keyboard
树视图应提供选择项和使用键盘展开/折叠节点的功能。 这可以确保导航满足我们的辅助功能要求。

##### <a name="tree-view-control"></a>树视图控件
Visual Studio 树控件应遵循常见的键盘导航：

- **向上键：** 通过向上移动树选择项

- **下箭头：** 通过向下移动树来选择项

- **向右箭头：** 展开树中的节点

- **左箭头：** 折叠树中的节点

- **输入密钥：** 启动、加载、执行选定项

##### <a name="trid-tree-view-and-grid-view"></a>Trid (树视图和网格视图) 
Trid 控件是包含网格中的树视图的复杂控件。 展开、折叠和导航树应遵循与树视图相同的键盘命令，同时添加以下内容：

- **向右箭头：** 展开节点。 节点展开后，应继续导航到右侧最近的列。 导航应在行尾停止。

- **选项卡：** 导航到右侧最近的单元格。  在行的末尾，导航将继续到下一行。

- **Shift + Tab：** 导航到左侧最近的单元格。  在行的开头，导航将继续到上一行中最右边的单元格。

![Visual Studio 中的 trid 控件](../../extensibility/ux-guidelines/media/070705-6_trid.png "070705-6_Trid")<br />Visual Studio 中的 trid 控件
