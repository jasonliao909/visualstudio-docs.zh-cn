---
title: 菜单和命令Visual Studio |Microsoft Docs
description: 了解为用户创建新功能时，命令栏如何在用户界面中实现灵活性Visual Studio。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
ms.assetid: 0a1ed675-2bd1-4603-ba3a-f40dfb5cfb69
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: 135744265dde5cf24225aee773180ebc2865bcfc
ms.sourcegitcommit: d38d1b083322019663fec7d1d85a4cda456aadca
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/22/2021
ms.locfileid: "135533950"
---
# <a name="menus-and-commands-for-visual-studio"></a>Visual Studio 的菜单和命令
## <a name="command-usage"></a>命令用法

### <a name="overview"></a>概述
 与 Microsoft Office（包含许多单独产品的套件）不同，Visual Studio包含许多产品，每个产品都向全局 IDE 提供其Visual Studio集。 IDE 通过根据上下文筛选可供用户使用的功能，管理数千个命令的复杂性。

 当用户的上下文发生更改（例如从设计窗口切换到代码编辑窗口）时，与新上下文无关的功能会消失。 同时，新功能与相关的动态信息（如"属性"和"工具箱"选项）一起显示。 用户不应注意到可用命令集的交换。 如果用户因命令出现或消失而分散注意力或感到困惑，则 UI 设计需要调整。 用户的当前上下文始终以一种或多种方式指示，例如 IDE 标题栏、属性窗口或"属性页"对话框。

 命令栏允许 UI 中的灵活性。 环境所固有的唯一Visual Studio结构是主菜单和主命令栏，它们既可自定义，也可以隐藏。 其他命令栏根据应用程序的状态显示和消失。 工具窗口和文档编辑器还可以在其窗口边缘内包含嵌入的工具栏。

#### <a name="basic-guidelines"></a>基本准则

##### <a name="use-existing-shared-commands-command-groups-and-menus-whenever-possible"></a>尽可能使用现有的共享命令、命令组和菜单。
 由于命令通常基于上下文显示，因此使用现有的共享菜单和命令组可确保命令结构在上下文中的更改之间保持相对稳定。 重新使用共享命令以及将新命令放置在相关共享命令附近还可以降低 IDE 复杂性，并创建更友好的用户体验。 如果需要定义新命令，请尝试将该命令放在现有的共享命令组中。 如果需要定义新组，请先将该组放在现有共享菜单中，靠近相关命令组，然后再创建新的顶级菜单。

##### <a name="do-not-create-icons-for-every-command"></a>不要为每个命令创建图标。
 创建命令图标之前，请仔细考虑。 应仅为以下命令创建图标：

- 显示在默认工具栏上。

- 用户可能会通过"自定义..."对话框添加到 **工具栏** 。

- 具有与另一 Microsoft 产品中的相同操作关联的图标。

##### <a name="limit-the-addition-of-keyboard-shortcuts"></a>限制添加键盘快捷方式
 绝大多数用户采用所有可用快捷方式中的一小部分。 如有疑问，请勿将功能绑定到键盘快捷方式。 在添加新快捷方式之前，请与用户体验团队合作。

##### <a name="give-commands-a-default-menu-placement"></a>为命令提供默认菜单位置。
 请注意，你的命令由其他人自定义，并相应地进行设计。 没有隐藏命令这样的操作。 所有Visual Studio命令都显示在"工具 **">"** 自定义"对话框、"命令窗口"、"自动完成"、"工具">"选项 **">"** 键盘"对话框以及"开发工具环境" (DTE) 。 请确保在 .进行文件中为命令提供名称和工具提示，以便用户可以轻松找到它们。

##### <a name="do-not-duplicate-shared-commands-on-an-embedded-toolbar"></a>不要复制嵌入工具栏上的共享命令。
 将命令放在靠近用户焦点区域的位置很有用。 为此，一种方式是在工具窗口或文档编辑器顶部创建嵌入工具栏。 工具栏上放置的命令应特定于窗口中的内容区域。 不要复制这些工具栏上的共享命令。 例如，切勿在嵌入式工具栏中放置"保存"图标。

### <a name="content-and-command-visibility"></a>内容和命令可见性
 命令存在于以下作用域中： **环境**、 **层次结构** 和 **文档**。 了解每个范围，以便对命令放置具有置信度。

 环境作用域 **中的命令** 建立主上下文，并在多个上下文之间共享。 它们更改文档和工具窗口的可见性或排列方式。 环境作用域中的命令包括"新建"Project、连接"服务器"、"附加进程"、"剪切"、"复制"、"粘贴 **"、"查找**"、"选项"、"**自定义**"、"**新建** 窗口"和"**查看帮助"。** 

 层次结构作用域 **中的命令** 管理层次结构中的 **Visual Studio包括** Project、**团队****和数据。** 它们与项目的子上下文相关 -例如，调试、**生成**、**测试**、**体系结构** 或 **分析**。 层次结构作用域中的命令包括"添加新项"、"新建查询"、Project 设置、"**添加新数据源**"、"**启动** 性能向导"和"**新建关系图"。** 

 文档范围 **中的** 命令对文档内容（如代码、设计或工作项查询） (WIQ) 。 它们还处理工具窗口的视图，或者特定于该工具窗口。 文档范围命令还处理本身特定于层次结构的文件对象，例如从 **Project。** 文档范围中的命令包括"重命名>、创建工作项 **副本**、全部展开、**全部** 折叠和 **创建用户任务**。 

### <a name="command-placement-decisions"></a>命令放置决策
 决定创建命令后，需要确定命令的适当位置以及是否创建键盘快捷方式。 按照此决策路径确定命令的放置位置：

 ![命令放置决策图表](../../extensibility/ux-guidelines/media/0501-a_commandplacement.png "0501-a_CommandPlacement")

 **命令在命令位置的决策Visual Studio**

### <a name="command-placement-in-menus"></a>命令在菜单中的位置

#### <a name="main-menu-bar"></a>主菜单栏
 主菜单栏应是参与 UI 的任何上下文特定菜单包的命令的标准位置。 主菜单栏与其他命令结构不同，因为环境使用它来控制哪些命令可见。 所有其他命令栏只是禁用上下文外的命令，无论这些命令放置在菜单上还是工具栏上。

 环境定义内置于主菜单栏中的一组命令，这些命令在整个 IDE 和多个任务域中很常见。 无论将哪些 VSPackage 加载到环境中，这些命令始终可见。 虽然 VSPackage 可以扩展这组命令，但每个产品的命令集及其命令的位置由每个团队负责。

 主菜单Visual Studio可细分为以下菜单类别：

##### <a name="core-menus"></a>核心菜单

- 文件

- 编辑

- 查看

- 工具

- 窗口

- 帮助

##### <a name="project-specific-menus"></a>Project菜单

- Project

- 构建

- 调试

##### <a name="context-specific-menus"></a>上下文特定的菜单

- 组

- 数据

- 测试

- 体系结构

- 分析

##### <a name="document-specific-menus"></a>文档特定的菜单

- 格式

- 表

##### <a name="when-designing-main-menus-adhere-to-these-rules"></a>设计主菜单时，请遵循以下规则：

- 给定上下文中不超过 25 个顶级项

- 菜单的高度不应超过 600 像素。

- 在多个上下文中评估主菜单，例如，在 Ultimate SKU 和 General Profile 中。

- 可接受弹出菜单。

- 弹出菜单应包含至少三个项，且不超过七个。

- 弹出菜单应只具有一个级别深度 - 某些Visual Studio菜单项具有级联子菜单，但不建议此模式。

- 使用不超过六个分隔符。 分组应遵循下图：

     ![主菜单分组指南](../../extensibility/ux-guidelines/media/0501-b_mainmenus.png "0501-b_MainMenus")

- 虽然不需要在图中设置每个分组，但添加其他分组会受到限制。

- 每个分组应包含两到七个菜单项。

#### <a name="main-menu-ordering"></a>主菜单排序
 添加新的顶级项之前，请考虑将命令置于现有的顶级菜单中。 添加新的顶级菜单时，请务必将菜单放在正确的位置。 确定菜单是特定于项目、上下文还是文档。 保持顶级菜单的名称简洁，并且只使用一个词。

 核心菜单应预订其余命令。 "文件"、"编辑"和"视图"应始终在左侧，"工具"、"窗口"和"帮助"应始终在右侧。

#### <a name="context-menus"></a>上下文菜单
 在上下文菜单中放置过多的功能会导致难以学习的界面。 所有主要功能都应通过主菜单栏提供。 命令的位置应该与现有命令协调，以避免重复的命令。 对于上下文菜单，shell 定义应包含的标准菜单组，具体取决于上下文菜单是适用于解决方案、项目节点还是项目项。

 设计上下文菜单时，遵循与主菜单相同的规则，此外，

- 不要超过 25 个顶级菜单项。

- 弹出菜单是可接受的，但不能超过一级深度 - 切勿使用级联弹出。

- 使用不超过六个分隔符。

### <a name="command-placement-in-toolbars"></a>工具栏中的命令放置

#### <a name="general-toolbars"></a>常规工具栏
 设计和排列工具栏时，请遵循以下标准：

- 每个按钮不要使用多个谓词。 一个按钮 = 一个操作。

- 仅在需要与标签一起增强时，才将文本与图标一起使用。

- 对将在一个会话中多次切换的属性专门使用组合框。 否则，在其他地方公开 属性。

- 组合框的宽度应等于框中最长项的宽度 + 30%。 例如，如果最长项为 200 像素，则组合框应宽 260 像素。

- 限制分隔符的使用。 在下拉列表旁边使用分隔符是一种反模式，因为下拉列表本身的形状充当可视分隔符。

- 图标组应包含三到六个图标。

- 如果限定符导致多个有用的命令，请使用存储最后一个设置的拆分按钮：

     ![Visual Studio 中的“拆分”按钮](../../extensibility/ux-guidelines/media/0501-c_splitbuttons.png "0501-c_SplitButtons")

     **拆分按钮的示例。左侧的六个命令可以改为适合单个按钮。**

#### <a name="product-specific-toolbars"></a>特定于产品的工具栏
 每个产品都可以提供包含常用和重要命令的默认工具栏，并且每个产品的默认工具栏应在安装产品Visual Studio首次启动时显示。

 产品还应利用 IDE 提供的共享命令组和菜单。 每个共享命令组都放置在共享菜单中，该菜单旨在以有意义的方式为用户组织相关命令。 必须利用此共享命令结构来降低复杂性。

#### <a name="global-toolbars"></a>全局工具栏
 全局工具栏需要容纳在一个开箱即用行上。 创建新的全局工具栏时，请遵循该工具栏类型的准则。

 **常规工具栏指南：**

- 每个工具栏在公共控件中具有 24 个像素， (器、溢出) 。

- 每个工具栏按钮的宽为 22 像素，包括填充。 使图标成为拆分按钮会再添加 11 像素的宽度。

- 允许跨工具栏重复命令。

  **当特定文件类型处于活动状态** 时，将显示特定于文档的工具栏，当其他文件类型变为活动时，这些工具栏将消失。

- 特定于文档的工具栏不能超过 12 个按钮。

- 工具栏的总宽度不能超过 300 像素。

- 每个文件类型可以有一个嵌入工具栏或一个文档特定的全局工具栏，但不能同时具有这两种工具栏。

  **设置特定上下文时** ，会出现上下文特定的工具栏，并且往往长时间保持活动状态。

- 所有特定于上下文的工具栏的按钮限制为 18。

- 如果上下文处于活动状态时，大多数用户不会一致地采用此工具栏的命令，请不要将此工具栏与上下文关联。

- 确保工具栏在退出上下文时消失。 启动时不应显示任何工具栏。

  **没有上下文的工具栏永远不会** 自动显示。 这些仅在用户激活它们时显示。 将最大宽度保持在 200 像素以下。

### <a name="general-organization-and-shell-defined-groups"></a>常规组织和 shell 定义的组
 使用现有的共享命令、命令组和菜单。 如果需要定义新命令，请尝试将该命令放在现有的共享命令组中。 如果需要定义新组，请在创建新的顶级菜单之前，尝试将该组放在靠近相关命令组的现有共享菜单中。 这降低了命令复杂性，同时确保在 IDE 中一致地放置命令。

 共享 **格式** 菜单（通常显示在设计器样式文档窗口的上下文中）如下图所示：

 ![具有标注的 Visual Studio 格式菜单](../../extensibility/ux-guidelines/media/0501-d_formatmenu.png "0501-d_FormatMenu")

 **菜单中的菜单Visual Studio**

### <a name="reducing-and-reusing-commands"></a>减少和重新使用命令
 命令通常基于上下文显示，以减少用户在任意给定时间看到的命令数。 但是，还应重用现有的共享菜单和命令组，以确保命令结构在上下文中的更改之间保持相对稳定。

 重新使用共享命令，将新命令放置在相关共享命令附近可降低 IDE 复杂性，并创建更友好的用户体验。

## <a name="naming-commands"></a>命名命令

### <a name="naming-conventions"></a>命名约定
 一致的命令命名至关重要，以便用户可以使用命令行或绑定到键盘快捷方式来查找和执行命令。 命令名称还有助于用户了解命令在工具栏或级联或上下文菜单中显示时的用途。

#### <a name="when-naming-commands"></a>命名命令时：

- 构造文本，以便易于本地化。 有关本地化文本的更多内容，请参阅 [本地化最佳做法](/dotnet/standard/globalization-localization/best-practices-for-developing-world-ready-apps#localization-best-practices)。

- 简洁。 命令不应超过三个单词。

- 使用标题大小写大写：每个单词的第一个字母都应大写。 有关文本格式设置Visual Studio，请参阅[文本样式](../../extensibility/ux-guidelines/fonts-and-formatting-for-visual-studio.md#BKMK_TextStyle)。

- 考虑命令的放置位置。 它是在顶级菜单还是弹出菜单中？ 例如，在 flyout 中对对齐命令进行分组时，顶级命令应为"Align"，而 flyout 命令应为"Left"、"Right"、"Center"、"Justify"等。 将 flyout 命令命名为"左对齐"或"右对齐"是多余的。

     ![Visual Studio 格式菜单](../../extensibility/ux-guidelines/media/0502-a_formatmenu.png "0502-a_FormatMenu")

### <a name="using-icons-with-commands"></a>将图标与命令一同使用
 请谨慎使用图标与命令配对。 尽管将唯一图像与命令关联会加快用户识别该命令的能力，但图像过度使用会导致视觉混乱和低效。 以下规则有助于确定是否创建命令图标。

#### <a name="use-an-icon-with-a-command-only-if"></a>仅在符合要求时，才使用包含命令的图标：

- 同一命令在另一个突出的 Microsoft 产品（例如其中一个应用程序）Microsoft Office与之关联。

- 命令将置于默认工具栏中。

- 命令是一个特殊命令，用户可能会使用"自定义 **..."** 对话框将其添加到工具栏。

## <a name="access-and-shortcut-keys"></a>访问键和快捷键

### <a name="overview"></a>概述
 有两种类型的键盘键分配：

- **访问 (** 也称为快捷键) 允许键盘通过菜单进行命令访问，并允许通过对话框 UI 中的每个标签访问。 访问键主要用于辅助功能，分配给所有菜单和大多数对话框控件，不应记住，仅影响当前窗口，并且已本地化。

- **快捷键主要** 使用 Ctrl (控件) Fn (函数) 键序列。 它们专为高级用户设计，有助于提高工作效率。 它们仅分配给最常用的命令，并允许在绕过主菜单时快速访问。 快捷键旨在记住，因此必须分配与配置文件方案一致的快捷键。 快捷键方案可能因配置文件而异。 用户可以通过"工具"和"选项"> **键盘 >快捷键**。

### <a name="assigning-access-keys"></a>分配访问密钥
 访问密钥由 Alt 和字母数字 (键) 。 向每个菜单项分配访问密钥，无异常。 遵循Windows密钥的常见约定。 例如，"新建> **的访问** 密钥应始终 **为 Alt、F、N**。

 请勿使用单像素宽度字母（例如大写或小写字母) 或小写字母"l"中的"i" (）并避免将字符与降序字母 (g、j、p、q 和 y) 一起使用，因为二者难以区分。

 尽可能避免使用重复键。 如果重复无法避免，菜单系统会通过循环访问使用该键的所有命令来处理冲突。 例如，对于复制"N"访问密钥的"文件"菜单下的假设"Number"命令 **，Alt、F、N** 将创建一个新文件 **，Alt、F、N、N** 将执行"Number"命令。

### <a name="assigning-shortcut-keys"></a>分配快捷键
 避免分配新的快捷键，因为并非每个命令都需要这些快捷键，并且对系统内存和用户 (和用户内存) 过度使用。 CEIP 客户体验改善计划 (数据) 表明Visual Studio用户仅使用集成快捷方式的一小部分。

 定义快捷方式时，请遵循以下规则：

- **使用 Ctrl (Ctrl) 和 Function (Fn) 键序列。**

- **保留常用的快捷方式。** 保留最常用的快捷方式。

- **使编辑器快捷方式易于键入。** 将易于键入的快捷方式绑定到开发人员在编写代码时最常用的命令。 例如 **，Edit.InvokeSmartTag** 需要具有快速快捷键（如 Ctrl+/ ），而不是 Alt+Shift+F10。

- **尽量使用一致的带提示的快捷方式。**

- **按照Windows确定要采用哪个修饰符键。** 对具有大规模效果的命令（例如应用于整个文档的命令）使用 Ctrl 组合键。 对扩展或补充标准快捷键操作的命令使用 Shift 组合键。 请勿使用 Ctrl+Alt 组合。

- **删除多余的快捷方式。** 如果具有旧版功能，请考虑从 CEIP 数据) 中删除使用极不频繁 (少于 10 次或从 CE) IP 数据 (中不经常使用 (次少于 100 次（如果访问密钥提供对同一命令的快速访问） 的快捷方式。 例如：Alt、H、C 将打开"帮助/内容"。

  没有一种简单的方式来检查快捷方式可用性。 如果要添加快捷方式，请执行以下步骤：

1. 检查[这些Visual Studio 2013列表](../../ide/default-keyboard-shortcuts-in-visual-studio.md)，以确定是否有类似的命令用于对命令进行分组。

2. 转到" **工具>选项>">键盘"** 并测试快捷方式。 检查"应用以下附加键盘映射方案"下列出的每个键盘映射方案。 检查常规、C#、VB和 C++ 配置文件，因为这些配置文件共享唯一的快捷方式。 如果快捷方式未映射到其中任何位置，则快捷方式可用。
