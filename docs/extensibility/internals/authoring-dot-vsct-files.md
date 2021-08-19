---
title: 创作。Vsct 文件|Microsoft Docs
description: 了解如何创作 .vsct 文件，这些文件将菜单项、工具栏和其他 UI 元素添加到 IDE Visual Studio集成 (环境) 。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- VSCT files, manual authoring
ms.assetid: e9f715dc-12b7-439b-bdf3-f3dc75e62f1c
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: 0f28286276bf2616ed84b68caf84949398b3f20e
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122159290"
---
# <a name="author-vsct-files"></a>创作 .vsct 文件
本文档演示如何创作 *.vsct* 文件，以将菜单项、工具栏和其他用户界面 (UI) 元素添加到 Visual Studio 集成开发环境 (IDE) 。 将 UI 元素添加到没有 *.vsct* Visual Studio (VSPackage) 的 VSPackage 包时，请使用以下步骤。

 对于新项目，建议使用 Visual Studio 包模板，因为它会生成一个 *.vsct* 文件，该文件已具有菜单命令、工具窗口或自定义编辑器所需的元素，具体取决于你的选择。 可以修改此 *.vsct* 文件以满足 VSPackage 的要求。 若要详细了解如何修改 *.vsct* 文件，请参阅扩展菜单和命令 [中的示例](../../extensibility/extending-menus-and-commands.md)。

## <a name="author-the-file"></a>创作文件
 在这些阶段 *创作 .vsct* 文件：创建文件和资源的结构、声明 UI 元素、将 UI 元素放入 IDE，以及添加任何专用行为。

### <a name="file-structure"></a>文件结构
 *.vsct* 文件的基本结构是包含 Commands 元素和 [Symbols](../../extensibility/symbols-element.md) [](../../extensibility/commands-element.md)元素的 [CommandTable](../../extensibility/commandtable-element.md)根元素。

#### <a name="to-create-the-file-structure"></a>创建文件结构

1. 按照 *如何：创建 .vsct* 文件 中的步骤将 [.vsct 文件添加到项目](../../extensibility/internals/how-to-create-a-dot-vsct-file.md)。

2. 将所需的命名空间添加到 `CommandTable` 元素，如以下示例所示：

    ```xml
    <CommandTable xmlns="http://schemas.microsoft.com/VisualStudio/2005-10-18/CommandTable"
        xmlns:xs="http://www.w3.org/2001/XMLSchema">

    ```

3. 在 `CommandTable` 元素中，添加 `Commands` 一个 元素来托管所有自定义菜单、工具栏、命令组和命令。 为了可以加载自定义 UI 元素，元素的 属性必须 `Commands` `Package` 设置为包的名称。

     在 `Commands` 元素之后，添加 元素以定义包的 `Symbols` GUID，以及 UI 元素的名称和命令 ID。

### <a name="include-visual-studio-resources"></a>包括Visual Studio资源
 使用[Extern](../../extensibility/extern-element.md)元素访问定义 Visual Studio命令的文件，以及将 UI 元素放入 IDE 所需的菜单。 如果使用在包外部定义的命令，请使用[UsedCommands](../../extensibility/usedcommands-element.md)元素来通知Visual Studio。

#### <a name="to-include-visual-studio-resources"></a>包含Visual Studio资源

1. 在 元素的顶部，为要引用的每个外部文件添加一个元素，将 属性设置为 `CommandTable` `Extern` `href` 文件的名称。 可以引用以下头文件来访问Visual Studio资源：

   - *Stdidcmd.h：* 定义由 Visual Studio 公开的所有命令的 ID。

   - *Vsshlids.h：* 包含用于菜单Visual Studio ID。

2. 如果包调用由 Visual Studio或其他包定义的任何命令，请添加 `UsedCommands` 元素之后 `Commands` 的元素。 对于不是包的一部分调用的每个命令，使用 [UsedCommand](../../extensibility/usedcommand-element.md) 元素填充此元素。 将 `guid` 元素 `id` 的 和 属性设置为要调用的命令的 GUID 和 `UsedCommand` ID 值。

   若要详细了解如何查找命令的 GUID 和 VISUAL STUDIO，请参阅命令 的[GUID Visual Studio。](../../extensibility/internals/guids-and-ids-of-visual-studio-commands.md) 若要从其他包调用命令，请使用这些包的 *.vsct* 文件中定义的 GUID 和命令 ID。

### <a name="declare-ui-elements"></a>声明 UI 元素
 声明 `Symbols` *.vsct* 文件的 节中的所有新 UI 元素。

#### <a name="to-declare-ui-elements"></a>声明 UI 元素

1. 在 `Symbols` 元素中，添加三 [个 GuidSymbol](../../extensibility/guidsymbol-element.md) 元素。 每个 `GuidSymbol` 元素都有 `name` 一个 属性和一个 `value` 特性。 设置 `name` 属性，以便它反映元素的用途。 `value`属性采用 GUID。  (生成 GUID，请在"工具"菜单上选择"创建 **GUID"，** 然后选择"注册表格式 **.)**

     第 `GuidSymbol` 一个元素表示包，通常没有子元素。 第 `GuidSymbol` 二个元素表示命令集，将包含定义菜单、组和命令的所有符号。 第 `GuidSymbol` 三个元素表示图像存储，并包含命令的所有图标的符号。 如果没有使用图标的命令，可以省略第三 `GuidSymbol` 个元素。

2. 在 `GuidSymbol` 表示命令集的 元素中，添加一个或多个 [IDSymbol](../../extensibility/idsymbol-element.md) 元素。 其中每个都表示要添加到 UI 的菜单、工具栏、组或命令。

     对于每个元素，将 属性设置为用于引用相应菜单、组或命令的名称，然后将元素设置为表示其命令 ID 的十六进制数字 `IDSymbol` `name` `value` 。 父级 `IDSymbol` 相同的两个元素不能具有相同的值。

3. 如果任何 UI 元素都需要图标，则向表示图像存储的元素添加每个图标 `IDSymbol` `GuidSymbol` 的元素。

### <a name="put-ui-elements-in-the-ide"></a>在 IDE 中放入 UI 元素
 "[菜单](../../extensibility/menus-element.md)["、"](../../extensibility/groups-element.md)组"和"[按钮](../../extensibility/buttons-element.md)"元素包含包中定义的所有菜单、组和命令的定义。 通过使用父元素（UI 元素定义的一部分）或通过使用其他地方定义的[](../../extensibility/parent-element.md)[CommandPlacement](../../extensibility/commandplacement-element.md)元素，将这些菜单、组和命令放入 IDE 中。

 每个 `Menu` `Group` 、 `Button` 和 元素都有 `guid` 一个 属性和一个 `id` 属性。 始终将 属性设置为与表示命令集的元素的名称匹配，将 属性设置为表示 节中的菜单、组或 `guid` `GuidSymbol` `id` `IDSymbol` 命令的元素 `Symbols` 的名称。

#### <a name="to-define-ui-elements"></a>定义 UI 元素

1. 如果要定义任何新菜单、子菜单、快捷菜单或工具栏，请向 `Menus` 元素添加 `Commands` 元素。 然后，对于要创建的每个菜单，将 [Menu](../../extensibility/menu-element.md) 元素添加到 `Menus` 元素。

    设置 `guid` `id` 元素的 和 `Menu` 属性，然后将 `type` 属性设置为你需要的菜单类型。 还可以设置 `priority` 属性，以建立菜单在父组中的相对位置。

   > [!NOTE]
   > `priority`属性不适用于工具栏和上下文菜单。

2. IDE 中Visual Studio必须由命令组承载，这些命令组是菜单和工具栏的直接子项。 如果要向 IDE 添加新菜单或工具栏，这些菜单或工具栏必须包含新的命令组。 还可以将命令组添加到现有菜单和工具栏，以便直观地对命令进行分组。

    添加新命令组时，必须先创建元素，然后为每个命令组添加 `Groups` [Group](../../extensibility/group-element.md) 元素。

    设置每个元素的 和 属性，然后设置 属性以建立组在父菜单 `guid` `id` `Group` `priority` 上的相对位置。 有关详细信息，请参阅 [创建可重用的按钮组](../../extensibility/creating-reusable-groups-of-buttons.md)。

3. 如果要向 IDE 添加新命令，请向 `Buttons` 元素添加 `Commands` 元素。 然后，对于每个命令，向 [元素添加 Button](../../extensibility/button-element.md) `Buttons` 元素。

   1. 设置 `guid` `id` 每个元素的 和 属性，然后将 `Button` `type` 属性设置为你需要的按钮类型。 还可以设置 `priority` 属性，以建立命令在父组中的相对位置。

       > [!NOTE]
       > 用于 `type="button"` 工具栏上的标准菜单命令和按钮。

   2. 在 `Button` 元素中，添加 [包含](../../extensibility/strings-element.md) [ButtonText](../../extensibility/buttontext-element.md) 元素和 [CommandName](../../extensibility/commandname-element.md) 元素的 Strings 元素。 `ButtonText`元素提供菜单项的文本标签，或工具栏按钮的工具提示。 `CommandName`元素提供命令井中要使用的命令的名称。

   3. 如果命令将具有图标，请创建 元素中的 [Icon](../../extensibility/icon-element.md) 元素，并设置其 和 属性到 `Button` 该图标 `guid` `id` `Bitmap` 的元素。

       > [!NOTE]
       > 工具栏按钮必须具有图标。

   有关详细信息，请参阅 [MenuCommands 与 OleMenuCommands](/previous-versions/visualstudio/visual-studio-2015/misc/menucommands-vs-olemenucommands?preserve-view=true&view=vs-2015)。

4. 如果任何命令需要图标，请向 元素 [添加 Bitmaps](../../extensibility/bitmaps-element.md) `Commands` 元素。 然后，对于每个图标，向 元素 [添加一个 Bitmap](../../extensibility/bitmap-element.md) `Bitmaps` 元素。 这是指定位图资源的位置的位置。 有关详细信息，请参阅将 [图标添加到菜单命令](../../extensibility/adding-icons-to-menu-commands.md)。

   可以依赖父级结构来正确放置大多数菜单、组和命令。 对于非常大的命令集，或者当菜单、组或命令必须出现在多个位置时，建议指定命令位置。

#### <a name="to-rely-on-parenting-to-place-ui-elements-in-the-ide"></a>依赖父级将 UI 元素放在 IDE 中

1. 对于典型的父级设置，在包中定义的每个 、 和 `Parent` `Menu` `Group` `Command` 元素中创建一个元素。

    元素的目标是包含菜单、组或命令的菜单 `Parent` 或组。

   1. 将 `guid` 属性设置为定义 `GuidSymbol` 命令集的元素的名称。 如果目标元素不是包的一部分，请使用相应 *.vsct* 文件中定义的该命令集的 guid。

   2. 设置 `id` 属性以匹配 `id` 目标菜单或组的属性。 有关由 Visual Studio 公开的菜单和组列表，请参阅 Visual Studio 菜单的[GUID](../../extensibility/internals/guids-and-ids-of-visual-studio-menus.md)或 VISUAL STUDIO 工具栏的 GUID 和[VISUAL STUDIO。](../../extensibility/internals/guids-and-ids-of-visual-studio-toolbars.md)

   如果要在 IDE 中放置大量 UI 元素，或者如果元素应出现在多个位置，请定义这些元素在 [CommandPlacements](../../extensibility/commandplacements-element.md) 元素中的放置，如以下步骤所示。

#### <a name="to-use-command-placement-to-place-ui-elements-in-the-ide"></a>使用命令放置将 UI 元素放在 IDE 中

1. 在 `Commands` 元素后面添加 `CommandPlacements` 元素。

2. 在 `CommandPlacements` 元素中，为 `CommandPlacement` 要放置的每个菜单、组或命令添加元素。

    每个 `CommandPlacement` 元素或 `Parent` 元素将一个菜单、组或命令位于一个 IDE 位置。 UI 元素只能有一个父级，但它可以有多个命令位置。 若要将 UI 元素放在多个位置，请 `CommandPlacement` 添加每个位置的 元素。

3. 将 `guid` 每个 `id` 元素的 和 属性 `CommandPlacement` 设置为宿主菜单或组，就像对元素进行 `Parent` 设置一样。 还可以设置 `priority` 属性以建立 UI 元素的相对位置。

   可以通过父级设置和命令放置来混合放置。 但是，对于非常大的命令集，我们建议你仅使用命令放置。

### <a name="add-specialized-behaviors"></a>添加专用行为
 例如，可以使用 [CommandFlag](../../extensibility/command-flag-element.md) 元素修改菜单和命令的行为，以更改其外观和可见性。 您还可以使用 [VisibilityConstraints](../../extensibility/visibilityconstraints-element.md) 元素来影响命令何时可见，或者使用 [KeyBindings](../../extensibility/keybindings-element.md) 元素添加键盘快捷方式。 某些类型的菜单和命令已内置了专用行为。

#### <a name="to-add-specialized-behaviors"></a>添加专用行为

1. 若要使 UI 元素仅在某些 UI 上下文中可见，例如，加载解决方案时，请使用可见性约束。

   1. 在 `Commands` 元素后面添加 `VisibilityConstraints` 元素。

   2. 对于要约束的每个 UI 项，请添加 [VisibilityItem](../../extensibility/visibilityitem-element.md) 元素。

   3. 对于每个元素，将 和 属性设置为菜单、组或命令，然后将 属性设置为需要 UI 上下文，如 `VisibilityItem` `guid` `id` `context` <xref:Microsoft.VisualStudio.Shell.Interop.UIContextGuids80> 类中定义。

2. 若要在代码中设置 UI 项的可见性或可用性，请使用以下一个或多个命令标志：

   - `DefaultDisabled`

   - `DefaultInvisible`

   - `DynamicItemStart`

   - `DynamicVisibility`

   - `NoShowOnMenuController`

   - `NotInTBList`

   有关详细信息，请参阅 [CommandFlag](../../extensibility/command-flag-element.md) 元素。

3. 若要更改元素的显示方式或动态更改其外观，请使用以下一个或多个命令标志：

   - `AlwaysCreate`

   - `CommandWellOnly`

   - `DefaultDocked`

   - `DontCache`

   - `DynamicItemStart`

   - `FixMenuController`

   - `IconAndText`

   - `Pict`

   - `StretchHorizontally`

   - `TextMenuUseButton`

   - `TextChanges`

   - `TextOnly`

   有关详细信息，请参阅 [CommandFlag](../../extensibility/command-flag-element.md) 元素。

4. 若要更改元素在接收命令时的反应方式，请使用以下一个或多个命令标志：

   - `AllowParams`

   - `CaseSensitive`

   - `CommandWellOnly`

   - `FilterKeys`

   - `NoAutoComplete`

   - `NoButtonCustomize`

   - `NoKeyCustomize`

   - `NoToolbarClose`

   - `PostExec`

   - `RouteToDocs`

   - `TextIsAnchorCommand`

   有关详细信息，请参阅 [CommandFlag](../../extensibility/command-flag-element.md) 元素。

5. 若要将依赖于菜单的键盘快捷方式附加到菜单或菜单上的项，请为菜单或菜单项 (&) 元素中添加一个和 `ButtonText` 字符。 当父菜单打开时，与 号后的字符是活动键盘快捷方式。

6. 若要将与菜单无关的键盘快捷方式附加到命令，请使用 [KeyBindings](../../extensibility/keybindings-element.md) 元素。 有关详细信息，请参阅 [KeyBinding](../../extensibility/keybinding-element.md) 元素。

7. 若要本地化菜单文本，请使用 `LocCanonicalName` 元素。 有关详细信息，请参阅 [Strings](../../extensibility/strings-element.md) 元素。

   某些菜单和按钮类型包括专用行为。 以下列表介绍了一些专用菜单和按钮类型。 有关其他类型，请参阅菜单 `types` 、按钮和组合[](../../extensibility/menu-element.md)元素[中的属性](../../extensibility/combo-element.md)说明。 [](../../extensibility/button-element.md)

   - 组合框：组合框是可在工具栏中使用的下拉列表。 若要向 UI 添加组合框，请 [创建 元素中的 Combos](../../extensibility/combos-element.md) `Commands` 元素。 然后，向 `Combos` 元素添加 `Combo` 要添加的每个组合框的元素。 `Combo` 元素具有与 元素相同的属性和子 `Button` 元素，还具有 `DefaultWidth` `idCommandList` 和 特性。 `DefaultWidth`属性设置宽度（以像素为单位）并且属性指向用于填充组合 `idCommandList` 框的命令 ID。

   - 菜单控制器：菜单控制器是旁边有箭头的按钮。 单击箭头将打开列表。 若要将菜单控制器添加到 UI，请创建 元素，将其 属性设置为 `Menu` `type` 或 `MenuController` `MenuControllerLatched` ，具体取决于你的行为。 若要填充菜单控制器，请设置它作为元素的 `Group` 父级。 菜单控制器将在其下拉列表中显示该组的所有子级。

## <a name="see-also"></a>请参阅
- [扩展菜单和命令](../../extensibility/extending-menus-and-commands.md)
- [Visual Studio命令表 (.vsct) 文件](../../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)
- [VSCT XML 架构参考](../../extensibility/vsct-xml-schema-reference.md)