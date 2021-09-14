---
title: VSPackages 如何用户界面元素|Microsoft Docs
description: 了解 VSPackages 如何将用户界面 (UI) 元素（如菜单、工具栏和工具窗口）添加到Visual Studio。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- user interfaces, adding elements
- UI element design [Visual Studio SDK], VSPackages
- VSPackages, contributing UI elements
ms.assetid: abc5d9d9-b267-48a1-92ad-75fbf2f4c1b9
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: 8234183455083a05095acef1d73ad87917100660
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126600730"
---
# <a name="how-vspackages-add-user-interface-elements"></a>VSPackage 如何添加用户界面元素
VSPackage 可以通过 *.vsct* 文件 (UI) 元素（例如菜单、工具栏和工具窗口）Visual Studio用户界面。

有关 UI 元素的设计准则，Visual Studio[用户体验指南 。](../../extensibility/ux-guidelines/visual-studio-user-experience-guidelines.md)

## <a name="the-visual-studio-command-table-architecture"></a>Visual Studio命令表体系结构
如前所述，命令表体系结构支持上述体系结构原则。 命令表体系结构的抽象、数据结构和工具背后的原则如下：

- 有三种基本类型的项：菜单、命令和组。 菜单可以在 UI 中作为菜单、子菜单、工具栏或工具窗口公开。 命令是用户可在 IDE 中执行的过程，可以公开为菜单项、按钮、列表框或其他控件。 组是菜单和命令的容器。

- 每个项由定义指定，该定义描述该项、其相对于其他项的优先级以及修改其行为的标志。

- 每个项都有一个描述项父级的位置。 一个项可以有多个父项，以便它可以出现在 UI 中的多个位置。

每个命令都必须有一个组作为其父级，即使它是该组中的唯一子级。 每个标准菜单还必须有一个父组。 工具栏和工具窗口充当其自己的父窗口。 组可以将主菜单栏Visual Studio菜单、工具栏或工具窗口作为其父级。

### <a name="how-items-are-defined"></a>如何定义项
*.vsct* 文件采用 XML 格式。 它定义包的 UI 元素，并确定这些元素在 IDE 中的显示位置。 包中的每个菜单、组或命令首先在 节中分配一个 GUID 和 `Symbols` ID。 在 *.vsct 文件* 的其余部分中，每个菜单、命令和组都由 GUID 和 ID 组合进行标识。 以下示例演示在模板中选择菜单命令时，Visual Studio包模板生成的 `Symbols` 典型节。 

```xml
<Symbols>
  <!-- This is the package guid. -->
  <GuidSymbol name="guidMenuTextPkg" value="{b1253bc6-d266-402b-89e7-5e3d3b22c746}" />

  <!-- This is the guid used to group the menu commands together -->
  <GuidSymbol name="guidMenuTextCmdSet" value="{a633d4e4-6c65-4436-a138-1abeba7c9a69}">
    <IDSymbol name="MyMenuGroup" value="0x1020" />
    <IDSymbol name="cmdidMyCommand" value="0x0100" />
  </GuidSymbol>

  <GuidSymbol name="guidImages" value="{53323d9a-972d-4671-bb5b-9e418480922f}">
    <IDSymbol name="bmpPic1" value="1" />
    <IDSymbol name="bmpPic2" value="2" />
    <IDSymbol name="bmpPicSearch" value="3" />
    <IDSymbol name="bmpPicX" value="4" />
    <IDSymbol name="bmpPicArrows" value="5" />
  </GuidSymbol>
</Symbols>
```

节的顶级元素 `Symbols` 是 [GuidSymbol 元素](../../extensibility/guidsymbol-element.md)。 `GuidSymbol` 元素将名称映射到 IDE 用于标识包及其组件部分的 GUID。

> [!NOTE]
> GUID 由包模板Visual Studio生成。 还可以单击"工具"菜单上的"创建 **GUID"，创建** 唯 **一的 GUID。**

第 `GuidSymbol` 一个元素 `guid<PackageName>Pkg` 是包本身的 GUID。 这是用户用来加载包Visual Studio GUID。 通常，它不包含子元素。

按照约定，菜单和命令分组到第二个元素 下 `GuidSymbol` ，位 `guid<PackageName>CmdSet` 图位于第三个元素 `GuidSymbol` 下 `guidImages` 。 不需要遵循此约定，但每个菜单、组、命令和位图都必须是元素的 `GuidSymbol` 子级。

在表示 `GuidSymbol` 包命令集的第二个元素中，是多个 `IDSymbol` 元素。 每个 [IDSymbol 元素将](../../extensibility/idsymbol-element.md) 名称映射到数值，并可能表示属于命令集的菜单、组或命令。 第 `IDSymbol` 三个元素中的 `GuidSymbol` 元素表示位图，这些位图可能用作命令的图标。 由于 GUID/ID 对在应用程序中必须是唯一的，因此同一元素的两个子元素 `GuidSymbol` 不能具有相同的值。

### <a name="menus-groups-and-commands"></a>菜单、组和命令
当菜单、组或命令具有 GUID 和 ID 时，可以添加到 IDE。 每个 UI 元素都必须具有以下各项：

- 一 `guid` 个 属性，该属性与定义 `GuidSymbol` UI 元素的元素的名称匹配。

- `id`与关联元素的名称匹配的 `IDSymbol` 属性。

和 属性 `guid` `id` 共同构成 UI *元素* 的签名。

- 一 `priority` 个 属性，该属性确定 UI 元素在其父菜单或组中的位置。

- 一 [个 Parent](../../extensibility/parent-element.md) 元素，该元素具有指定父菜单 `guid` `id` 或组的签名的 和 属性。

#### <a name="menus"></a>菜单
每个菜单都定义为 节中 [的 Menu](../../extensibility/menu-element.md) `Menus` 元素。 菜单必须具有 `guid` 、 `id` 和 `priority` 属性以及 元素， `Parent` 以及以下附加属性和子项：

- 一个 属性，该属性指定菜单应作为一种菜单或工具栏出现在 `type` IDE 中。

- [一个 Strings](../../extensibility/strings-element.md)元素，该元素包含[ButtonText](../../extensibility/buttontext-element.md)元素 （指定 IDE 中菜单的标题）和[CommandName](../../extensibility/commandname-element.md)元素 ，该元素指定在"命令"窗口中用于访问菜单的名称。

- 可选标志。 [CommandFlag 元素可能出现](../../extensibility/command-flag-element.md)在菜单定义中，以在 IDE 中更改其外观或行为。

每个元素都必须有一个组作为父级，除非它是一个可停靠 `Menu` 的元素，如工具栏。 可停靠菜单是其自己的父级。 有关属性的菜单和值 `type` 详细信息，请参阅 [Menu 元素](../../extensibility/menu-element.md) 文档。

以下示例显示了显示在"工具"菜单旁边的Visual Studio **栏上的菜单**。

```xml
<Menu guid="guidTopLevelMenuCmdSet" id="TopLevelMenu" priority="0x700" type="Menu">
  <Parent guid="guidSHLMainMenu" id="IDG_VS_MM_TOOLSADDINS" />
  <Strings>
    <ButtonText>TestMenu</ButtonText>
    <CommandName>TestMenu</CommandName>
  </Strings>
</Menu>
```

#### <a name="groups"></a>组
组是在 `Groups` *.vsct* 文件的 节中定义的项。 组只是容器。 它们不会出现在 IDE 中，只是作为菜单上的分隔线。 因此 [，Group 元素](../../extensibility/group-element.md) 仅按其签名、优先级和父级定义。

一个组可以有一个菜单、另一个组或本身作为父级。 但是，父级通常是菜单或工具栏。 前面示例中的菜单是组的子级，该组是菜单栏Visual Studio `IDG_VS_MM_TOOLSADDINS` 子级。 以下示例中的组是前面示例中菜单的子级。

```xml
<Group guid="guidTopLevelMenuCmdSet" id="MyMenuGroup" priority="0x0600">
  <Parent guid="guidTopLevelMenuCmdSet" id="TopLevelMenu"/>
</Group>
```

由于它是菜单的一部分，因此此组通常包含命令。 但是，它也可以包含其他菜单。 这是定义子项时，如以下示例所示。

```xml
<Menu guid="guidTopLevelMenuCmdSet" id="SubMenu" priority="0x0100" type="Menu">
  <Parent guid="guidTopLevelMenuCmdSet" id="MyMenuGroup"/>
  <Strings>
    <ButtonText>Sub Menu</ButtonText>
    <CommandName>Sub Menu</CommandName>
  </Strings>
</Menu>
```

#### <a name="commands"></a>命令
提供给 IDE 的命令定义为 [Button 元素](../../extensibility/button-element.md) 或 [组合元素](../../extensibility/combo-element.md)。 若要显示在菜单或工具栏上，该命令必须将组作为其父级。

##### <a name="buttons"></a>按钮
按钮在 节中 `Buttons` 定义。 用户单击以执行单个命令的任何菜单项、按钮或其他元素都被视为按钮。 某些按钮类型还可以包括列表功能。 按钮具有与菜单相同的必需和可选属性，并且还可以具有一个 [Icon](../../extensibility/icon-element.md) 元素，该元素指定表示 IDE 中按钮的位图的 GUID 和 ID。 有关按钮及其属性的信息，请参阅 [Buttons 元素](../../extensibility/buttons-element.md) 文档。

以下示例中的按钮是上一示例中组的子级，在 IDE 中显示为该组的父菜单上的菜单项。

```xml
<Button guid="guidTopLevelMenuCmdSet" id="cmdidTestCommand" priority="0x0100" type="Button">
  <Parent guid="guidTopLevelMenuCmdSet" id="MyMenuGroup" />
  <Icon guid="guidImages" id="bmpPic1" />
  <Strings>
    <CommandName>cmdidTestCommand</CommandName>
    <ButtonText>Test Command</ButtonText>
  </Strings>
</Button>
```

##### <a name="combos"></a>组合
组合在 节中 `Combos` 定义。 每个 `Combo` 元素都表示 IDE 中的下拉列表框。 列表框可能或不可由用户写入，具体取决于组合 `type` 的 属性的值。 组合具有与按钮相同的元素和行为，还可以具有以下附加属性：

- 一 `defaultWidth` 个指定像素宽度的属性。

- 一 `idCommandList` 个 属性，该属性指定一个列表，该列表包含列表框中显示的项。 命令列表必须在包含组合的 `GuidSymbol` 同一节点中声明。

下面的示例定义组合元素。

```xml
<Combos>
  <Combo guid="guidFirstToolWinCmdSet"
         id="cmdidWindowsMediaFilename"
         priority="0x0100" type="DynamicCombo"
         idCommandList="cmdidWindowsMediaFilenameGetList"
         defaultWidth="130">
    <Parent guid="guidFirstToolWinCmdSet"
            id="ToolbarGroupID" />
    <CommandFlag>IconAndText</CommandFlag>
    <CommandFlag>CommandWellOnly</CommandFlag>
    <CommandFlag>StretchHorizontally</CommandFlag>
    <Strings>
      <CommandName>Filename</CommandName>
      <ButtonText>Enter a Filename</ButtonText>
    </Strings>
  </Combo>
</Combos>
```

##### <a name="bitmaps"></a>位图
与图标一起显示的命令必须包含一个元素，该元素使用其 GUID 和 ID 来引用位 `Icon` 图。 每个位图在 节中定义为 [位](../../extensibility/bitmap-element.md) `Bitmaps` 图元素。 定义的唯一必需 `Bitmap` 属性是 和 `guid` `href` ，它们指向源文件。 如果源文件是资源条，则还需要 **usedList** 属性，以列出条带中的可用图像。 有关详细信息，请参阅 [Bitmap 元素](../../extensibility/bitmap-element.md) 文档。

### <a name="parenting"></a>育儿
以下规则控制项如何调用另一个项作为其父级。

|元素|在命令表的此部分中定义|可以包含 (父项，也可以按节的位置包含，也可以同时包含两) `CommandPlacements`|可以包含 (父对象) |
|-------------| - | - | - |
|Group|[Groups 元素](../../extensibility/groups-element.md)、IDE、其他 vspackage|菜单、组、项本身|菜单、组和命令|
|菜单|[菜单元素](../../extensibility/menus-element.md)、IDE、其他 vspackage|1到 *n* 组|0到 *n* 组|
|工具栏|[菜单元素](../../extensibility/menus-element.md)、IDE、其他 vspackage|项本身|0到 *n* 组|
|菜单项|[按钮元素](../../extensibility/buttons-element.md)、IDE、其他 vspackage|1到 *n* 组，项本身|-0 到 *n* 组|
|Button|[按钮元素](../../extensibility/buttons-element.md)、IDE、其他 vspackage|1到 *n* 组，项本身||
|组合图|[Combos 元素](../../extensibility/combos-element.md)，IDE，其他 vspackage|1到 *n* 组，项本身||

### <a name="menu-command-and-group-placement"></a>菜单、命令和组放置
菜单、组或命令可以出现在 IDE 的多个位置中。 要使项出现在多个位置，必须将其 `CommandPlacements` 作为 [CommandPlacement 元素](../../extensibility/commandplacement-element.md)添加到节中。 任何菜单、组或命令均可作为命令位置添加。 但是，不能以这种方式定位工具栏，因为它们不能出现在多个区分上下文的位置。

命令放置具有 `guid` 、 `id` 和 `priority` 属性。 GUID 和 ID 必须与定位的项的 GUID 和 ID 匹配。 `priority`特性控制项相对于其他项的位置。 当 IDE 合并具有相同优先级的两个或多个项时，它们的位置是不确定的，因为 IDE 不保证每次生成包时按相同顺序读取包资源。

如果菜单或组出现在多个位置，则该菜单或组的所有子级都将显示在每个实例中。

## <a name="command-visibility-and-context"></a>命令可见性和上下文
安装多个 Vspackage 时，菜单、菜单项和工具栏的如此可能会打乱 IDE 的混乱程度。 若要避免此问题，可以使用 *可见性约束* 和命令标志来控制各个 UI 元素的可见性。

### <a name="visibility-constraints"></a>可见性约束
可见性约束设置为部分中的 [VisibilityItem 元素](../../extensibility/visibilityitem-element.md) `VisibilityConstraints` 。 可见性约束定义了可在其中查看目标项的特定 UI 上下文。 仅当其中一个定义的上下文处于活动状态时，才会显示此部分中包含的菜单或命令。 如果未在此部分中引用菜单或命令，默认情况下它始终可见。 本部分不适用于组。

`VisibilityItem` 元素必须具有三个属性，如下所示 `guid` ： `id` 目标 UI 元素和的和 `context` 。 `context`特性指定目标项何时可见，并将任何有效的 UI 上下文作为其值。 Visual Studio 的 UI 上下文常量是类的成员 <xref:Microsoft.VisualStudio.VSConstants> 。 每个 `VisibilityItem` 元素只能采用一个上下文值。 若要应用第二个上下文，请创建一个指向同一项的第二个 `VisibilityItem` 元素，如下面的示例中所示。

```xml
<VisibilityConstraints>
  <VisibilityItem guid="guidSolutionToolbarCmdSet"
        id="cmdidTestCmd"
        context="UICONTEXT_SolutionHasSingleProject" />
  <VisibilityItem guid="guidSolutionToolbarCmdSet"
        id="cmdidTestCmd"
        context="UICONTEXT_SolutionHasMultipleProjects" />
</VisibilityConstraints>
```

### <a name="command-flags"></a>命令标志
以下命令标志可能会影响应用于的菜单和命令的可见性。

`AlwaysCreate` 即使没有组或按钮，也会创建菜单。

适用于： `Menu`

`CommandWellOnly` 如果命令未显示在顶级菜单上，并且您要使其可用于其他外壳自定义（例如，将其绑定到密钥），请应用此标志。 安装 VSPackage 后，用户可以通过打开 " **选项** " 对话框，然后编辑 " **键盘环境** " 类别下的命令位置来自定义这些命令。 不影响快捷菜单、工具栏、菜单控制器或子菜单上的位置。

适用于： `Button` 、 `Combo`

`DefaultDisabled` 默认情况下，如果未加载实现该命令的 VSPackage 或未调用 QueryStatus 方法，则该命令处于禁用状态。

适用于： `Button` 、 `Combo`

`DefaultInvisible` 默认情况下，如果未加载实现命令的 VSPackage 或未调用 QueryStatus 方法，则该命令将不可见。

应与 `DynamicVisibility` 标志结合。

适用于： `Button` 、 `Combo` 、 `Menu`

`DynamicVisibility` 可以通过使用该 `QueryStatus` 部分中包含的方法或上下文 GUID 来更改该命令的可见性 `VisibilityConstraints` 。

适用于菜单上显示的命令，而不是工具栏上的命令。 当 `OLECMDF_INVISIBLE` 从方法返回标志时，可以禁用顶级工具栏项，但不能隐藏 `QueryStatus` 。

在菜单上，此标志还指示在隐藏其成员时应自动隐藏它。 此标志通常分配给子菜单，因为顶级菜单已经有了此行为。

应与 `DefaultInvisible` 标志结合。

适用于： `Button` 、 `Combo` 、 `Menu`

`NoShowOnMenuController` 如果将具有此标志的命令定位在菜单控制器上，则该命令不会出现在下拉列表中。

适用于： `Button`

有关命令标志的详细信息，请参阅 [CommandFlag 元素](../../extensibility/command-flag-element.md) 文档。

#### <a name="general-requirements"></a>一般要求
你的命令必须传递以下系列的测试，然后才能显示和启用：

- 命令位置正确。

- `DefaultInvisible`未设置标志。

- 父菜单或工具栏可见。

- 由于 [VisibilityConstraints 元素](../../extensibility/visibilityconstraints-element.md) 部分中的上下文条目，命令不可见。

- 用于实现接口的 VSPackage 代码会 <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget> 显示并启用你的命令。 没有接口代码截获并对其进行操作。

- 当用户单击你的命令时，它将受到 [路由算法](../../extensibility/internals/command-routing-algorithm.md)中所述的过程的制约。

## <a name="call-pre-defined-commands"></a>调用预定义的命令
[UsedCommands 元素](../../extensibility/usedcommands-element.md)使 vspackage 可以访问由其他 VSPACKAGE 或 IDE 提供的命令。 为此，请创建一个 [UsedCommand 元素](../../extensibility/usedcommand-element.md) ，该元素具有要使用的命令的 GUID 和 ID。 这可以确保 Visual Studio 加载命令，即使它不是当前 Visual Studio 配置的一部分也是如此。 有关详细信息，请参阅 [UsedCommand 元素](../../extensibility/usedcommand-element.md)。

## <a name="interface-element-appearance"></a>接口元素外观
选择和定位命令元素的注意事项如下：

- [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 提供了许多不同的位置显示的 UI 元素。

- 使用标志定义的 UI 元素 `DefaultInvisible` 将不会显示在 IDE 中，除非它是通过其 VSPackage 实现显示的 <xref:EnvDTE.IDTCommandTarget.QueryStatus%2A> ，或与部分中的特定 UI 上下文相关联 `VisibilityConstraints` 。

- 甚至可能不会显示成功定位的命令。 这是因为 IDE 会自动隐藏或显示某些命令，具体取决于 VSPackage 已 (或未) 实现的接口。 例如，VSPackage 的某些生成接口的实现将导致自动显示生成相关菜单项。

- `CommandWellOnly`在 UI 元素的定义中应用标志意味着只能通过自定义添加该命令。

- 命令仅在某些 UI 上下文中可用，例如，当 IDE 在设计视图中时显示对话框。

- 若要使某些 UI 元素在 IDE 中显示，您必须实现一个或多个接口或编写一些代码。

## <a name="see-also"></a>另请参阅
- [扩展菜单和命令](../../extensibility/extending-menus-and-commands.md)
