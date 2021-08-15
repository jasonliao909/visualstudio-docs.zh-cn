---
title: UX Essentials for Visual Studio |Microsoft Docs
description: 查看这些用户体验最佳做法，了解你为屏幕Visual Studio新功能，包括了解屏幕分辨率。
ms.custom: SEO-VS-2020
ms.date: 04/26/2017
ms.topic: reference
ms.assetid: a793cf7a-f230-43ce-88d0-fa5d6f1aa9c7
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: 569ab6c839c9944550b351152abe86c0f7a6722dab3bd3b743adbaf87139d695
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121259846"
---
# <a name="ux-essentials-for-visual-studio"></a>Visual Studio 用户体验基础知识

## <a name="best-practices"></a>最佳做法

### <a name="1-be-consistent-within-the-visual-studio-environment"></a>1.在安全环境中Visual Studio一致。

- 遵循 [shell 中的](interaction-patterns-for-visual-studio.md) 现有交互模式。

- 设计功能，以与 shell 的视觉语言和 [视觉要求保持一致](evaluation-tools-for-visual-studio.md)。

- 当共享命令和控件存在时，请使用它们。

- 了解Visual Studio层次结构及其如何建立上下文和驱动 UI。

### <a name="2-use-the-environment-service-for-fonts-and-colors"></a>2.将环境服务用于字体和颜色。

- UI 应遵守当前 [环境字体](fonts-and-formatting-for-visual-studio.md) 设置，除非它在"选项"对话框的"字体和颜色"页中公开用于自定义。

- UI 元素必须使用 [VSColor 服务](colors-and-styling-for-visual-studio.md)，使用共享环境令牌或功能特定的令牌。

### <a name="3-make-all-imagery-consistent-with-the-new-vs-style"></a>3.使所有图像与新的 VS 样式一致。

- 遵循Visual Studio图标、标志符号和其他图形的设计原则。

- 不要将文本放在图形元素中。

### <a name="4-design-from-a-user-centric-perspective"></a>4.从以用户为中心的角度进行设计。

- 在任务流中各个功能之前创建任务流。

- 熟悉用户，在规范中明确掌握这些知识。

- 查看 UI 时，请评估完整的体验以及详细信息。

- 设计 UI，以便无论区域设置或语言如何，它都能保持功能和吸引力。

## <a name="screen-resolution"></a>屏幕分辨率

### <a name="minimum-resolution"></a>最小分辨率

- 2015 年Visual Studio分辨率为 **1280x720。** 这意味着可以在此 *解决方法* Visual Studio，尽管它可能不是最佳用户体验。 无法保证所有方面在低于 1280x720 的分辨率下都可用。

- 目标分辨率为 **1366x768 Visual Studio 1366x768。** 这是我们承诺提供良好用户体验的最低解决方法。 

- 初始对话高度 **应小于 700 像素**，因此它适合 IDE 帧的最小分辨率（96 dpi）。

### <a name="high-density-displays"></a>高密度显示器
 Visual Studio UI 必须能够很好地处理所有支持Windows DPI 缩放因素：150%、200% 和 250%。

## <a name="anti-patterns"></a>若干反模式
 Visual Studio许多 UI 示例，这些示例遵循我们的指南和最佳做法。 为了保持一致，开发人员通常从产品 UI 设计模式借用，这些模式类似于他们正在构建的模式。 尽管这是一种很好的方法，可帮助我们提高用户交互和视觉设计的一致性，但我们有时会提供一些细节，但由于计划约束或缺陷优先级的原因，这些细节不符合我们的准则。 在这些情况下，我们不希望团队复制这些"反模式"之一，因为它们在环境环境中Visual Studio不一致。

### <a name="required-fieldssettings-shown-in-error-state-by-default"></a>默认以错误状态显示的必填字段/设置

#### <a name="feature-team-goals"></a>功能团队目标

- 警告用户已添加必须配置的元素。

- 将用户注意力吸引到需要输入的区域。

#### <a name="anti-pattern-solution"></a>反模式解决方案
 用户启动操作后，在完成任务之前，立即将关键停止图标放在需要配置的区域旁边。

#### <a name="example-manifest-designer-declarations"></a>示例：清单设计器声明
 将声明添加到列表会立即将声明添加到错误状态，该状态将一直保留到用户设置所需属性。

 在这种情况下，还有一个额外的问题，因为用于警报的图标包含""图标，因此不能旁边使用常见的删除 &times; 图标。 因此，UI 使用"删除"按钮，这是一种更不可靠的控件。

 ![默认情况下，将 UI 置于错误状态是一种Visual Studio模式。](../../extensibility/ux-guidelines/media/manifestdesignererrordeclarationsanti-pattern.png "ManifestDesignererrordeclarationsanti-模式")<br />默认情况下，将 UI 置于错误状态是一种Visual Studio模式。

#### <a name="alternatives"></a>备选方法

此问题的更好解决方案是：

- 允许用户在不发出警告的情况下添加声明，然后立即移动以设置项的属性。

- 将警告图标 (在) 项移动时添加警告图标，例如向列表添加另一个声明或尝试更改设计器中的选项卡。

- 如果用户尝试在任何声明上设置属性之前更改选项卡，则弹出一个对话框，说明应用程序不会生成 (或在解决警告之前) 任何影响。 如果用户关闭对话框并更改选项卡，则图标 (严重或警告，) 添加到"声明"选项卡。

### <a name="multiple-clicks-to-dismiss-ui"></a>多次单击以关闭 UI

#### <a name="feature-team-goals"></a>功能团队目标
 不允许用户在未看到解释文本的情况下关闭 UI。

#### <a name="anti-pattern"></a>反模式
 将视频链接插入 VS UI 中各个位置的团队决定针对 UX 指定的"关闭按钮和工具提示说明"这一常见模式，而是实现了下拉列表和" &times; 不再显示"链接。

#### <a name="example-video-links-in-team-explorer"></a>示例：视频链接团队资源管理器
强制用户在关闭 UI 之前阅读解释性文本是一种反模式Visual Studio。 正确设计后，视频链接应显示包含悬停附加信息的工具提示，单击""应关闭消息，而无需 &times; 进一步交互。

 ![说明性文本反&#45;模式&#45;不正确](../../extensibility/ux-guidelines/media/incorrectuseofmultipleclicks.png "Incorrectuseofmultipleclicks")<br />不正确的视频链接模式

用户只能单击一 (关闭按钮) ，而是使用两次单击来直接关闭视频链接出现每个位置的 UI。

针对这种情况的正确设计是遵循 Internet Explorer、Office 和 Visual Studio：悬停时，用户可以看到工具提示说明，一键隐藏 UI。

 ![说明性文本反&#45;模式&#45;正确](../../extensibility/ux-guidelines/media/explanatorytextanti-pattern-correct.png "Explanatorytextanti-模式-正确")<br />正确的视频链接模式

### <a name="using-command-bars-for-settings"></a>使用命令栏进行设置

**图 A** 表示此反模式：将设置置于命令按钮下面，该按钮不仅适用于 命令。 在此草图中，除了"开始调试"之外，还有一些命令（例如"在浏览器中查看"、"开始执行而不调试"和"逐步执行"）将遵守所选设置。

![图 A：命令栏反模式](../../extensibility/ux-guidelines/media/commandbaranti-pattern-figurea.png "Commandbaranti-FigureA")<br />图 A：命令栏反模式

稍微好一些，但仍不需要在工具栏中放置此类型的设置，如图 **B 所示**。虽然拆分按钮占用的空间较少，因此比下拉列表要改进，但两种设计仍使用工具栏来提升不是命令的项。

![图 B：更好，但仍为命令栏反模式](../../extensibility/ux-guidelines/media/commandbaranti-pattern-figureb.png "Commandbaranti-FigureB")<br />图 B：更好，但仍为命令栏反模式

在图 C 所示的正确方法 **中**，设置绑定到一系列命令。 未设置全局设置，我们只需在四个命令之间切换。 这是工具栏中可接受命令的唯一情况。

![图 C：正确使用Visual Studio栏模式](../../extensibility/ux-guidelines/media/commandbaranti-pattern-figurec.png "Commandbaranti-FigureC")<br />图 C：正确使用Visual Studio栏模式

### <a name="control-anti-patterns"></a>控制反模式
 某些反模式只是控件或一组控件的用法或表示方式不正确。

#### <a name="underlining-used-as-a-group-label-not-a-hyperlink"></a>用作组标签的下划线，而不是超链接
 带下划线的文本应仅用于超链接。

 **坏：**\
 ![不是超链接的带下划线的文本是Visual Studio模式。](../../extensibility/ux-guidelines/media/0102-g_grouplabelincorrect.png "0102-g_GroupLabelIncorrect")<br />不是超链接的带下划线的文本是Visual Studio模式。

 **好：**\
 ![正确设置样式后，非超链接文本在环境字体中未显示。](../../extensibility/ux-guidelines/media/0102-h_grouplabelcorrect.png "0102-h_GroupLabelCorrect")<br />正确设置样式后，非超链接文本在环境字体中未显示。

#### <a name="clicking-on-a-check-box-results-in-a-pop-up-dialog"></a>单击复选框会导致弹出对话框
 单击"发布"向导中的"启用所有角色的远程桌面"复选框Windows Azure 应用程序弹出一个弹出对话框，Visual Studio反模式。 此外，复选框字段在选中后不会填充复选框，这是另一种交互反模式。

 ![单击复选框后启动对话框是一种Visual Studio模式。](../../extensibility/ux-guidelines/media/0102-i_checkboxpopup.png "0102-i_CheckboxPopup")<br />单击复选框后启动对话框是一种Visual Studio模式。

### <a name="hyperlink-anti-patterns"></a>超链接反模式
 以下示例包含两种反模式：

1. 悬停时的前景色为红色表示字体服务中未使用正确的共享颜色。

2. "了解更多"不是指向概念性主题的链接的适当文本。 用户的目标不是了解更多，它是了解他们选择的影响。

   ![忽略颜色服务并使用 "了解更多" 超链接 Visual Studio 反模式。](../../extensibility/ux-guidelines/media/0102-j_hyperlinkincorrect.png "0102-j_HyperlinkIncorrect")<br />忽略颜色服务并使用 "了解更多" 超链接 Visual Studio 反模式。

**更好的解决方案：** 单击链接，提出用户要询问的问题。 例如：

- Windows Azure 服务的工作原理是什么？

- 何时需要 Windows Azure 移动服务项目？

#### <a name="using-click-here-for-links"></a>为链接使用 "单击此处"
 超链接应是自描述性的。 这是一种可使用 "单击此处" 或任何类似变体的反模式。

 **错误：** 单击此处了解有关如何创建新项目的说明。

 **不错：** "如何实现创建新项目？"
