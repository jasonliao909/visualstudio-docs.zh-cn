---
title: 动画Visual Studio |Microsoft Docs
description: 了解可帮助确保整个 IDE 中一致且用户友好的动画Visual Studio规则。
ms.custom: SEO-VS-2020
ms.date: 04/26/2017
ms.topic: reference
ms.assetid: 446773a9-e6f7-4c0c-8dbc-9e303bf32eb1
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: 933856cffcf7a012be7d9774b3d703aa92e335fb5d7939d804ef49043875f1a7
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121388323"
---
# <a name="animations-for-visual-studio"></a>Visual Studio 的动画
## <a name="animation-fundamentals"></a>动画基础

### <a name="animation-best-practices-in-visual-studio"></a>动画中的最佳动画Visual Studio
遵循这些规则，确保整个 IDE 中的动画样式一致且Visual Studio样式。

- **有选择性。** 将动画限制为用于特定用途的动画。

- **计时和速度对于确保** 转换感觉快速自然非常重要：

  - 在 500 毫秒或 500 毫秒 (内完成动画) 。

  - 频繁发生的动画需要足够快，以便它们不会中断用户的工作流。 观察循环中的动画并调整计时，直到感觉正确。

  - 动画应该不会那么快或太难理解，但速度不会那么慢，而是让转换完成一次。

  - 使用变量计时强调重要性。 例如，在类图中浏览一系列项时，在项之间快速转换，然后减慢以专注于重要项的速度。

- **使用从一种状态到另一** 种状态逐渐的非线性缓动，从而提供一种感觉和自然移动。

- 如果可能， **在悬停时使用细微动画** 来指示鼠标下的交互元素。

- 如果主要依赖于功能中的动画，则提供一种在本地关闭它们 (所有功能) 作为"工具"">选项 **"对话框中** 的选项。

- **一次只能发生一个动画** ，只传达一条信息。 移动或尝试传达多个内容的多个对象可能会令人困惑。

- **细微性非常重要。** 在大多数情况下，动画不需要用户关注来达到其用途。 计时、排序和行为中的细微变化可能会显著影响感知，并可能在有效动画和无效动画之间产生差异。

- 使用动画吸引用户注意某些内容时，请确保它值得 **中断用户的思维** 训练。

- **通过动画显示进度或** 状态时：

  - 当基础进程未前进时，停止显示进度移动。

  - 将不确定的进程与确定的进程区别。

  - 确保动画具有可识别的完成和失败状态。

  - 通过提供实际使用的其他信息，尽量减少显示状态的效果动画的使用，并确保它们具有实际价值。 示例包括暂时性状态更改和故障

#### <a name="animation-donts"></a>动画不：

- 请勿在占用空间较小 (使用小型移动) 。 与移动对象不同，首选淡入淡出和更改。

- 请勿使用在大量屏幕空间上播放的动画。 无论大小如何，这种动画样式都会让用户分散注意力。

- 请勿使用与用户当前关注的对象无关或与之交互的动画。

- 请勿使用需要用户交互来重置状态（如强制用户响应闪烁通知，使其停止闪烁）的动画。 以任何方式与之交互应该足以消除它们。

有关这些最佳做法的应用程序详细信息，请参阅 [动画模式](../../extensibility/ux-guidelines/animations-for-visual-studio.md#BKMK_AnimationPatterns)。

### <a name="animation-metrics"></a>动画指标

- 系统应在不到 10 毫秒内明显响应用户手势。

- 动画转换不应超过 500 毫秒才能完成。

- 补偿需要更长时间的转换的一种方式是，将转换分为两个部分。 例如，动画的第一部分可能是空内容容器 (最多 500 毫秒) ，然后内容逐渐消失到容器中 (最多 500 毫秒) 。

- 对于可以计算的加载时间，首选 (进度指示器，) 进度指示器。

- 对于无法计算的加载时间，适合使用光标或嵌入旋转动画等繁忙 (加载或) 指示器。

### <a name="animation-as-communicator"></a>作为通信器播放的动画
在 Visual Studio UI 中，动画仅用作通信工具。  它用于传达各种信息，例如 UI 中的结构更改 (例如，菜单打开或关闭) 。 动画有助于可视化复杂系统的时间相关行为，例如安装进度可视化。 动画还可用于通过警报和通知吸引注意力。

 UI 动画通常以四种方式工作：可视化、吸引注意、模拟和响应时间/进度指示器。

#### <a name="visualize"></a>可视化
动画可以强调对象的三维性质，并使用户能够更轻松地可视化其空间结构。 若要实现此目的，动画可能需要在整个圆圈中旋转对象，缓慢地来回旋转该对象，或使对象更靠近并略微增大其大小，以强调滚动或焦点。

尽管三维对象可能通过用户控件移动，但设计器应提前以编程 (手动方式确定) 如何以最佳方式对移动进行动画处理，从而提供最佳的对象理解。 然后，用户可以通过将光标置于对象上来激活此编程动画，而用户控制的移动则要求用户了解如何操作对象。 一次将移动限制为单个轴或方向;缩放、旋转或转换，但不要同时执行多个操作。

"可视化"类别包括数据、关系、状态、结构、序列和时间的各个方面。

##### <a name="data"></a>数据
阐释复杂和可变信息：

- 移动信息可视化效果，如图表和图形

- 单步执行序列、引导式教程和分页

- 突出显示详细信息、指向和突出显示特定信息

- 覆盖焦点元素上的详细信息和其他信息

- 从一种结构或组织表示形式变为另一种结构或组织表示形式

- 使用时间滑块、旋转和旋转滚轮以及传输控件来表示一 (播放、停止和暂停) 

##### <a name="relationships"></a>关系

- 说明项彼此关联或哪些项与给定项相关

- 显示层次结构和父子关系或同级关系

- 一个元素生成另一个元素

- 一个元素最小化为另一个元素

- 一个元素与另一个元素不一致

##### <a name="state"></a>状态

- 内容更新

- 用户焦点和选择

- 进度

- 错误

##### <a name="structure"></a>结构

- 透视一个节点上的结构

- 重新定向

- 最小化和最大化，或展开和折叠

##### <a name="sequence"></a>序列

- 幻灯片放映序列

- 翻转图片

##### <a name="time"></a>时间

- 显示一段时间的变化、时间推移和屏幕广播

- 移动到回收站、撤消和重做

- 还原历史状态

#### <a name="attract-attention"></a>吸引注意力
如果目标是将用户注意力吸引到多个元素中的单个元素或提醒用户更新信息，则动画可能适用。 例如，应用程序起始页可能会使用一个入门按钮，该按钮在页面加载后就位。

一般来说，屏幕上的最后一个移动元素会吸引用户的注意。  在一系列动画元素中，用户将关注最后一个移动对象。

##### <a name="alert"></a>警报

- 提醒用户、引起注意、显示进度

- 显示已正确或不正确地执行某些操作，或显示进度或进度更改

- 在任务期间提示用户，例如联机查找详细信息或了解当前任务

##### <a name="notifications"></a>通知

- 向用户发出警报，了解错误条件

- 中断用户以查看他们是否想要参加其他内容

- 轻轻向用户通知进程已完成或已更改，如下载完成时。

#### <a name="simulate"></a>Simulate
此类别涵盖 physicality 和维数。

- 说明对象来源或对象的目标位置

- 展开和折叠或打开和关闭

- 平移、滚动和翻页

- 堆叠和 z 顺序

- 轮播和折叠

- 翻转和旋转 UI

#### <a name="response-and-progress-indicators"></a>响应和进度指示器
进度指示器具有几个显著的优点：

- 确定性和不确定的进度指示器再次向用户，系统尚未崩溃并正在处理问题。

- 确定性指示器使用户能够了解该操作的进展情况，并使感觉更接近完成。

## <a name="animation-patterns"></a><a name="BKMK_AnimationPatterns"></a> 动画模式

### <a name="overview"></a>概述
Visual Studio 中的动画旨在提供特定的功能，而不会影响用户工作效率。 通常，Visual Studio 中的动画应为：

- 小型和非引人注目

- 自然和现实

- 微妙和温柔

- 快速高效

- 宽松，不十万火急

下图显示了我们建议 Visual Studio 的动画样式。 使用淡入/淡出的动画或细微动画是最常用的。 移动动画的应用程序（如展开和收缩、X 和 Y 位置更改和旋转）会受到限制。

![Visual Studio 的建议动画样式](../../extensibility/ux-guidelines/media/1202-a_vsanimstyles.png "1202-a_VSAnimStyles")<br />Visual Studio 的建议动画样式

#### <a name="appear-and-disappear"></a>显示并消失
使用此模式时，元素可以在无需过渡动画的情况下从可见切换到无视图切换。

![显示并消失动画](../../extensibility/ux-guidelines/media/1202-b_appearanddisappear.png "1202-b_AppearAndDisappear")<br />显示并消失动画

##### <a name="correct-usage"></a>正确使用
需要立即显示或消失的全新 UI 元素，以便用户既不分散也不会受到阻碍。 此外，转换速度缓慢的动画可能会被视为性能拖动，这不会出现在外观上并消失的样式。

##### <a name="incorrect-usage"></a>用法不正确
UI 出现的情况突然出现，用户不知道发生了什么情况，添加动画会有助于上下文理解。

##### <a name="animation-properties"></a>动画属性
时间延迟通常为零秒。

##### <a name="examples"></a>示例
- 自动隐藏工具窗口

- 键盘激活的编辑器 UI，如 IntelliSense 和参数帮助

- 展开和折叠代码区域

#### <a name="fade-in-and-fade-out"></a>淡入和淡出
使用此模式时，UI 元素将从不可见 (0% opacity) 转换为可见 (100% 不透明) ，反之亦然。

![淡入和淡出动画](../../extensibility/ux-guidelines/media/1202-c_fadeinfadeout.png "1202-c_FadeInFadeOut")<br />淡入和淡出动画

##### <a name="correct-usage"></a>正确使用
这是最常推荐的 UI 动画。 这是一种微妙的影响，它增加了不中断流的兴趣。 在某些情况下，用户甚至可能不会意识到有动画，觉察平滑和流动的 UI 系统。

##### <a name="animation-properties"></a>动画属性

- 开始不透明度：0% （对于淡入，100%）

- 结束不透明度：100% 的淡入，0% 表示淡出

- 持续时间：作为组合动画序列的一部分使用时，200毫秒独立，100毫秒

- 缓动样式：正弦 InOut

##### <a name="examples"></a>示例

- 自动隐藏工具窗口

- 菜单打开并关闭

- 背景和前景选项卡转换

#### <a name="color-blend-from-a-to-b"></a>从 A 到 B 的颜色混合
使用此模式时，UI 元素从颜色 A 变为颜色 B。

![颜色混合动画](../../extensibility/ux-guidelines/media/1202-d_colorblend.png "1202-d_ColorBlend")<br />颜色混合动画

##### <a name="correct-usage"></a>正确使用
当 UI 元素将颜色从一个上下文或状态更改为另一个时，转换为动态转换。

##### <a name="animation-properties"></a>动画属性

- 开始颜色： UI 特定

- 结束颜色： UI 特定

- 持续时间：作为组合动画序列的一部分使用时，200毫秒独立，100毫秒

- 缓动样式：正弦 InOut

##### <a name="examples"></a>示例

- 文档窗口状态转换 (活动、上次活动和非活动状态) 

- 工具窗口状态转换 (重点和失去焦点) 

#### <a name="expand-and-contract"></a>展开和收缩
使用此模式时，UI 元素以 X、Y 或双向方向展开。

![展开和收缩动画](../../extensibility/ux-guidelines/media/1202-e_expandcontract.png "1202-e_ExpandContract")<br />展开和收缩动画

##### <a name="correct-usage"></a>正确使用
当 UI 元素将大小从一个上下文更改到另一个上下文时，为动态转换。

##### <a name="animation-properties"></a>动画属性

- X 刻度：% 或特定的维度 (以像素为单位) 

- Y 刻度：% 或特定的维度 (（以像素为单位）) 

- 定位点位置：对于从右到左书写的语言，通常为左上角 () 或右上 () 

- 持续时间：作为组合动画序列的一部分使用时，200毫秒独立，100毫秒

##### <a name="examples"></a>示例

- 体系结构资源管理器面板展开和折叠

- Visual Studio 2017 开始页面项展开和折叠

#### <a name="x-y-position-change"></a>X Y 位置更改
使用此模式时，UI 元素将更改其 X 或 Y 位置，或同时更改两者。

![X Y 位置更改动画](../../extensibility/ux-guidelines/media/1202-f_xypositionchange.png "1202-f_XYPositionChange")<br />X Y 位置更改动画

##### <a name="correct-usage"></a>正确使用
当 UI 元素将位置从一个上下文更改到另一个上下文时，为动态转换。

##### <a name="animation-properties"></a>动画属性

- 开始 X 和 Y 位置： UI 特定

- 结束 X 和 Y 位置： UI 特定

- 运动路径：无

- 持续时间：作为组合动画序列的一部分使用时，200毫秒独立，100毫秒

- 缓动样式：正弦 InOut

##### <a name="example"></a>示例
Tab 重新排序

#### <a name="rotate"></a>旋转
在此模式中，UI 元素将旋转。

![UI 元素旋转动画](../../extensibility/ux-guidelines/media/1202-g_rotate.png "1202-g_Rotate")<br />UI 元素旋转动画

##### <a name="correct-usage"></a>正确用法
仅适用于不确定的旋转进度指示器。

##### <a name="animation-properties"></a>动画属性

- 旋转度：360

- 旋转中心：对象的中间

- 持续时间：连续

##### <a name="example"></a>示例
不确定旋转进度 (进度) 

### <a name="common-shell-ui-actions-and-recommended-animations"></a>常见的 shell UI 操作和推荐的动画

#### <a name="tab-open"></a>选项卡打开
![Tab 打开动画](../../extensibility/ux-guidelines/media/1202-h_tabopen.png "1202-h_TabOpen")<br />Tab 打开动画

- 样式：显示

- 持续时间：零秒

#### <a name="tab-close"></a>Tab 关闭
![Tab 关闭动画](../../extensibility/ux-guidelines/media/1202-i_tabclose.png "1202-i_TabClose")<br />Tab 关闭动画

- 样式：X 位置更改

- 持续时间：200 毫秒

#### <a name="tab-reorder"></a>Tab 键重新排序
![Visual Studio 中的选项卡重新排序动画](../../extensibility/ux-guidelines/media/1202-j_tabreorder.png "1202-j_TabReorder")<br />Tab 键重新排序动画

- 样式：X 位置更改

- 持续时间：200 毫秒

#### <a name="close-floating-document"></a>关闭浮动文档
![关闭浮动文档动画](../../extensibility/ux-guidelines/media/1202-k_closefloatingdocument.png "1202-k_CloseFloatingDocument")<br />关闭浮动文档动画

- 样式：显示

- 持续时间：200 毫秒

#### <a name="window-state-transition"></a>窗口状态转换
![窗口状态转换动画](../../extensibility/ux-guidelines/media/1202-l_windowstatetransition.png "1202-l_WindowStateTransition")<br />窗口状态转换动画

- 样式：为了与其他窗口保持一致，让当前操作系统定义文档关闭动画。

- 持续时间：200 毫秒

#### <a name="menu-open"></a>菜单打开
![菜单打开动画](../../extensibility/ux-guidelines/media/1202-m_menuopen.png "1202-m_MenuOpen")<br />菜单打开动画

- 样式：淡入

- 持续时间：200 毫秒

#### <a name="menu-close"></a>菜单关闭
![菜单关闭动画](../../extensibility/ux-guidelines/media/1202-n_menuclose.png "1202-n_MenuClose")<br />菜单关闭动画

- 样式：淡出

- 持续时间：200 毫秒

#### <a name="auto-hide-tool-window-reveal"></a>自动隐藏工具窗口显示
![自动隐藏工具窗口显示动画](../../extensibility/ux-guidelines/media/1202-o_autohidetoolwindowreveal.png "1202-o_AutoHideToolWindowReveal")<br />自动隐藏工具窗口显示动画

- 样式：显示

- 持续时间：零秒
